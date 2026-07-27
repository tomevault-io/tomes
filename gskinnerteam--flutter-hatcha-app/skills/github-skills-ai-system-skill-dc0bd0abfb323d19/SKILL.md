---
name: ai-system
description: AI communication architecture for the Flutter A2UI + Python hatcha_agent system. Use when: adding a new ControllerConfig or GeminiConversationConfig, creating a Python agent, working with system prompts, modifying routing, or understanding the Two-Layer AI pattern. Covers both Flutter and Python sides. Use when this capability is needed.
metadata:
  author: gskinnerTeam
---

# AI System — Developer Guide

This skill covers the full AI communication architecture: Flutter conversation configs, Python agent routing, prompt files, and the protocols connecting them.

> **Working on the background image builder?** Use the [image-builder skill](../image-builder/SKILL.md) instead — it is the focused guide for editing the refiner prompt, the pixel system instruction, and running the local iteration loop.

## When to Use

- Adding a new `ControllerConfig` (GenUI widget-rendering)
- Adding a new `GeminiConversationConfig` (text-only AI)
- Creating or modifying a Python agent in `agents/hatcha_agent/`
- Working with system prompts in `agents/hatcha_agent/prompts/`
- Debugging AI routing or session issues
- Understanding the TextProxyAgent pattern

---

## 1. Two-Layer AI Architecture

Every AI request routes through the Python `hatcha_agent` A2A server. No direct Gemini API calls in Flutter.

```
Flutter App
├── GenUI (ControllerConfig)
│     └── A2A request → RoutingExecutor → {feature}Agent → widget JSON
│
└── GeminiService (GeminiConversationConfig)
      └── A2A request ("System Instruction: {prompt}\n\n{msg}")
                      → TextProxyAgent → Gemini → text response
```

| Pattern   | Dart class                 | Backend            | Output                             |
| --------- | -------------------------- | ------------------ | ---------------------------------- |
| **GenUI** | `ControllerConfig`         | Named Python agent | JSON widget tree (`surfaceUpdate`) |
| **Text**  | `GeminiConversationConfig` | `TextProxyAgent`   | Plain text / JSON string           |

---

## 2. GeminiService (Text Conversations)

**File**: `lib/core/genui/gemini_service.dart`

Each `GeminiConversationConfig` creates its own `GeminiService` instance via `GeminiServiceLogic`.

### How messages reach Python

```dart
$gemini.getById(conversationId).sendMessage(message);
// Sends: "System Instruction: {systemPrompt}\n\n{message}"
// Python TextProxyAgent extracts systemPrompt, calls Gemini, returns text
```

### Key methods

| Method                | Purpose                                              |
| --------------------- | ---------------------------------------------------- |
| `sendMessage(String)` | Queue or send immediately                            |
| `clearHistory()`      | Reset conversation without dispose (use on back-nav) |
| `dispose()`           | Deferred if request in-flight                        |

### Batching

When `enableBatching: true` (default), messages within a 1-second window are concatenated. Batch-handling instructions are auto-injected into the system prompt.

---

## 3. GeminiConversationConfig

Base class for text-only AI conversations. Subclasses live in `lib/features/*/generative/`.

```dart
abstract class GeminiConversationConfig {
  String get groupId;         // Groups related conversations
  String get conversationId;  // Unique per instance
  String get systemPrompt;    // Sent as "System Instruction: {prompt}"
  GeminiConfig get config;    // Model params
}
```

### All conversation configs

| Config class                           | Feature         | Purpose                                                  |
| -------------------------------------- | --------------- | -------------------------------------------------------- |
| `GenerateEventDetailsConversation`     | configure_event | Extract title/date/location from summary                 |
| `GenerateInviteAndModulesConversation` | configure_event | Extract `InviteModule[]` + `DashboardModule[]`           |
| `EventAssistantConversationConfig`     | host_dashboard  | Natural-language event modification                      |
| `ModuleInterviewSummaryConversation`   | host_dashboard  | Interview summary → structured module update             |
| `OrchestratorConversationConfig`       | interview       | Multi-turn orchestrator (questions, confidence, summary) |
| `SummaryConversationConfig`            | interview       | Markdown summary from answers                            |
| `DigestConversationConfig`             | core/services   | Event digest generation/update                           |

---

## 4. GenUI Controllers (ControllerConfig)

Base class for widget-rendering. Subclasses live in `lib/features/*/genui/`.

```dart
abstract class ControllerConfig {
  String get groupId;
  String get contextSuffix;       // Combined → contextId (session key)
  Catalog get catalog;            // Widget catalogue for this context
  Transport get transport;        // Points at A2A server (was ContentGenerator)
  // Optional: maxInstances, enableAutoRetry, maxRetryAttempts, retryDelay
}
```

`contextId = "{groupId}_{contextSuffix}"` — used for sticky session routing in Python.

### All controllers

| Controller class                   | Feature            | Python agent             | Status    |
| ---------------------------------- | ------------------ | ------------------------ | --------- |
| `GuestInviteController`            | guest_invite       | `GuestAnswerAgent`       | ✅ Active |
| `GuestModuleController`            | guest_invite       | `GuestModuleAgent`       | ✅ Active |
| `HostModuleController`             | host_dashboard     | `HostModuleAgent`        | ✅ Active |
| `GuestResponsesController`         | host_dashboard     | `GuestResponsesAgent`    | ✅ Active |
| `ModuleSuggestionsController`      | host_dashboard     | `ModuleSuggestionsAgent` | ✅ Active |
| `InterviewGenuiControllerConfig`   | interview (inline) | `InterviewQuestionAgent` | ✅ Active |
| `InterviewSummaryControllerConfig` | interview          | `InterviewSummaryAgent`  | ✅ Active |

---

## 5. Context ID Patterns

Context IDs are session keys for sticky routing:

| Feature                   | Pattern                                     | Example                               |
| ------------------------- | ------------------------------------------- | ------------------------------------- |
| Guest invite per-question | `guest_invite_{eventId}_{moduleId}`         | `guest_invite_abc123_dietary`         |
| Host module card          | `host_module_{eventId}_{moduleId}`          | `host_module_abc123_catering`         |
| Guest responses chart     | `guest_responses_{eventId}_{moduleId}`      | `guest_responses_abc123_dietary`      |
| Module suggestions        | `module_suggestions_{eventId}`              | `module_suggestions_abc123`           |
| Interview orchestrator    | `interview_orchestrator_{groupId}`          | `interview_orchestrator_event_abc123` |
| Interview per-question    | `interview_question_{groupId}_{questionId}` | `interview_question_event_abc123_q1`  |

---

## 6. Python Agent Architecture

All code in `agents/hatcha_agent/`.

### Key files

| File                | Purpose                                              |
| ------------------- | ---------------------------------------------------- |
| `agent.py`          | Agent registry — all agents registered here          |
| `agent_executor.py` | `RoutingExecutor` — session-sticky message routing   |
| `a2ui_protocol.py`  | A2UI extension handler — parses GenUI JSON responses |
| `base_agent.py`     | `BaseAgent` — shared Gemini call logic               |
| `prompts/`          | All system prompt strings (one file per agent)       |

### Agent types

- **GenUI agents** (`use_ui=True`): Respond with text + `---a2ui_JSON---` block containing `surfaceUpdate` objects
- **Text agents** (`use_ui=False`): Return plain text. `TextProxyAgent` is the only text agent

### Routing (RoutingExecutor)

1. First message to a `contextId`: agent detected from message prefix pattern
2. Agent stored in `_session_routes[context_id]`
3. All subsequent messages with same `contextId` → same agent (sticky)

### Agent routing table

| Python Agent             | Trigger pattern                 | GenUI? |
| ------------------------ | ------------------------------- | ------ |
| `TextProxyAgent`         | `system instruction:` substring | No     |
| `InterviewQuestionAgent` | `question:` prefix              | Yes    |
| `GuestAnswerAgent`       | `answer_question:`              | Yes    |
| `HostModuleAgent`        | `module_data:`                  | Yes    |
| `GuestResponsesAgent`    | `visualize_module:`             | Yes    |
| `ModuleSuggestionsAgent` | `# event context`               | Yes    |
| `ConfigureEventAgent`    | Configure event context         | Yes    |
| `GuestInviteAgent`       | Guest invite context            | Yes    |
| `HostDashboardAgent`     | Host dashboard context          | Yes    |
| `GuestModuleAgent`       | Guest module context            | Yes    |
| `InterviewSummaryAgent`  | Interview summary context       | Yes    |
| `SuggestionChipsAgent`   | Suggestion chips context        | Yes    |
| `InterviewAgent`         | Default fallback                | Yes    |

### Prompt files

All in `agents/hatcha_agent/prompts/`:

| File                                   | Agent / Purpose                                                                                       |
| -------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| `interview_orchestrator.py`            | `InterviewOrchestratorAgent`                                                                          |
| `interview_question.py`                | `InterviewQuestionAgent`                                                                              |
| `interview_summary.py`                 | `InterviewSummaryAgent`                                                                               |
| `interview_assistant_toolable.py`      | Toolable interview assistant                                                                          |
| `configure_event.py`                   | `ConfigureEventAgent`                                                                                 |
| `guest_answer.py`                      | `GuestAnswerAgent`                                                                                    |
| `guest_invite.py`                      | `GuestInviteAgent`                                                                                    |
| `guest_module.py`                      | `GuestModuleAgent`                                                                                    |
| `guest_responses.py`                   | `GuestResponsesAgent`                                                                                 |
| `host_module.py`                       | `HostModuleAgent`                                                                                     |
| `host_dashboard.py`                    | `HostDashboardAgent`                                                                                  |
| `module_suggestions.py`                | `ModuleSuggestionsAgent`                                                                              |
| `suggestion_chips.py`                  | `SuggestionChipsAgent`                                                                                |
| `event_hub_assistant.py`               | Event hub assistant                                                                                   |
| `event_assistant_toolable.py`          | Toolable event assistant                                                                              |
| `event_details_toolable.py`            | Toolable event details                                                                                |
| `event_palette_toolable.py`            | Toolable event palette                                                                                |
| `invite_and_modules_toolable.py`       | Toolable invite and modules                                                                           |
| `module_interview_summary_toolable.py` | Toolable module interview summary                                                                     |
| `background_image.py`                  | `BackgroundImageAgent` (image builder refiner — see [image-builder skill](../image-builder/SKILL.md)) |
| `image_adjustments_ui.py`              | `ImageAdjustmentsUIAgent` (sliders for image tweaks)                                                  |
| `image_rules.py`                       | Shared composition + safety rules used by both the refiner and the pixel call site                    |
| `shared.py`                            | Common constants, UI schema docs                                                                      |

---

## 7. Key Message Prefixes (Flutter → Python)

| Prefix                                                  | Python agent             |
| ------------------------------------------------------- | ------------------------ |
| `answer_question: {description}`                        | `GuestAnswerAgent`       |
| `question: {prefix}\n{dataType}...`                     | `InterviewQuestionAgent` |
| `module_data: {json}`                                   | `HostModuleAgent`        |
| `visualize_module: {label}\n{description}\n{responses}` | `GuestResponsesAgent`    |
| `# EVENT CONTEXT\n...`                                  | `ModuleSuggestionsAgent` |
| `System Instruction: {prompt}\n\n{message}`             | `TextProxyAgent`         |

---

## 8. Interview System

Three AI layers in combination:

### Orchestrator (GeminiService)

`OrchestratorConversationConfig` — stateful multi-turn. Issues question batches, tracks confidence (0-100), generates CTA headlines and markdown summaries.

**Message protocol**:

| Flutter → Orchestrator             | Response                                 |
| ---------------------------------- | ---------------------------------------- |
| Initial context text               | `{questions, cta, confidence, summary?}` |
| `question_rendered: label`         | `{confidence}`                           |
| `question_answered: label \| data` | `{confidence, summary?}`                 |
| `more_questions`                   | `{questions, cta}`                       |

**Data type → widget mapping**:

| `data_type`  | Widget            |
| ------------ | ----------------- |
| `set`        | `MultiSelect`     |
| `choice`     | `RadioSelect`     |
| `range`      | `SteppedSlider`   |
| `date`       | `DateTimePicker`  |
| `text`       | `TextInput`       |
| `dual_range` | Dual range widget |
| `bubble_set` | Bubble set widget |

### Per-Question GenUI

One `InterviewGenuiControllerConfig` per question → `InterviewQuestionAgent` → renders widget.

### Summary

The orchestrator handles summary generation as part of its multi-turn conversation flow.

---

## 9. Module Interview Parser

`ModuleInterviewSummaryService` orchestrates three operations:

| Operation | Input                               | Output                                          |
| --------- | ----------------------------------- | ----------------------------------------------- |
| `add`     | Interview summary + event context   | New `DashboardModule` + optional `InviteModule` |
| `modify`  | Interview summary + existing module | Updated label + description                     |
| `resolve` | Interview summary + guest response  | `ResolveAction` + updated description           |

Prepends `CONTEXT_DATA` block with live event/module state before calling the parser.

---

## 10. EventDigestService

Globally accessible as `$digestService`. Maintains `event.eventDetailsDigest`.

```dart
$digestService.generateDigest(eventId, interviewSummary)  // Initial
$digestService.updateDigest(eventId, updateContent)        // Incremental (batched)
```

**Integration points**: event creation, invite prompt changes, guest RSVP submission, module create/update/delete.

---

## 11. Adding a New AI Conversation

### New GenUI agent (widget-rendering)

1. Create prompt: `agents/hatcha_agent/prompts/<name>.py`
2. Create agent class in `agent.py` inheriting `BaseAgent`
3. Add prefix detection to `RoutingExecutor._detect_feature()` in `agent_executor.py`
4. Register agent in `agent.py` root agent list
5. Create `ControllerConfig` subclass in `lib/features/<feature>/genui/`

### New text conversation

1. Create `GeminiConversationConfig` subclass in `lib/features/<feature>/generative/`
2. Set `systemPrompt` — it will be extracted by `TextProxyAgent` automatically
3. No Python-side changes needed (TextProxyAgent handles all text conversations)

---

## 12. Response Parsing

### Orchestrator responses

Sealed class hierarchy: `OrchestratorFullResponse`, `OrchestratorQuestionsResponse`, `OrchestratorUpdateResponse`, `OrchestratorConfidenceResponse`.

### Configure event responses

```dart
EventDetailsParserResponse? parseEventDetailsResponse(String json)
InviteAndModulesResponse? parseInviteAndModulesResponse(String json)
```

### Module parser results

```dart
ModuleInterviewSummaryResult { label, description, guestQuestion? }
ResolveAction { update, dismiss, createQuestion, ... }
```

---
> Source: [gskinnerTeam/flutter-hatcha-app](https://github.com/gskinnerTeam/flutter-hatcha-app) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-24 -->
