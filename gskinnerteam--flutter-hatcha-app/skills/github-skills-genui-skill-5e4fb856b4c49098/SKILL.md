---
name: genui
description: Core GenUI framework for dynamic AI-driven UIs. Use when: working with Conversation, SurfaceController, Transport, Surface, SurfaceHost, Catalog, CatalogItem, CatalogItemContext, DataModel, DataContext, DataPath, A2uiSchemas, ClientFunction, PromptBuilder, A2UiClientCapabilities, data binding, A2UI message protocol, ChatMessage, UiEvent, or SurfaceDefinition. Use when this capability is needed.
metadata:
  author: gskinnerTeam
---

# GenUI Package — API Reference

The `genui` package (v0.9.0) is the core framework for building Flutter applications with dynamically generated user interfaces powered by AI. The UI is not predefined — it is constructed in real-time through a conversation cycle between the app, an AI model, and the user. Implements the [A2UI protocol](https://a2ui.org) v0.9.

## When to Use

- Working with `Conversation` lifecycle (send requests, listen for surfaces/text/errors)
- Rendering dynamic UI with `Surface` widget
- Implementing a custom `Transport`
- Subscribing to or updating `DataModel` / `DataContext` paths
- Working with `A2uiSchemas` reference types
- Using `CatalogItemContext` properties (data, dataContext, buildChild, dispatchEvent)
- Processing `A2uiMessage` protocol messages (CreateSurface, UpdateComponents, UpdateDataModel, DeleteSurface)
- Working with `ChatMessage` or `MessagePart` types
- Defining custom `ClientFunction` implementations
- Building prompts with `PromptBuilder`
- Generating `A2UiClientCapabilities` from catalogs

> **Project conventions** for creating catalogue item _files_ (5-step convention, naming, example data rules, three-tier pattern) live in the `catalogue-items` skill. This skill covers the _package API_.

---

## Core Architecture

```
┌─────────────────────────────────────┐
│   Application (Flutter Widgets)     │
├─────────────────────────────────────┤
│   Facade Layer                      │
│   - Conversation                    │
│   - PromptBuilder                   │
│   - Surface (Widget)                │
├─────────────────────────────────────┤
│   Engine Layer                      │
│   - SurfaceController               │
│   - SurfaceRegistry                 │
│   - DataModelStore                  │
├─────────────────────────────────────┤
│   Model Layer                       │
│   - Catalog, CatalogItem            │
│   - DataModel, DataContext          │
│   - A2uiMessage types              │
│   - ChatMessage types               │
│   - A2UiClientCapabilities          │
├─────────────────────────────────────┤
│   Transport Layer                   │
│   - Transport (interface)           │
│   - A2uiTransportAdapter            │
│   - A2uiParserTransformer           │
├─────────────────────────────────────┤
│   Interfaces                        │
│   - SurfaceHost                     │
│   - SurfaceContext                  │
│   - A2uiMessageSink                │
└─────────────────────────────────────┘
```

### Interaction Flow

```
User
 │  (1) sendRequest(ChatMessage)
 ▼
Conversation ──► Transport (A2A / Direct AI)
 │                    │
 │  (2) incomingMessages (Stream<A2uiMessage>)
 │      incomingText (Stream<String>)
 ▼                    │
SurfaceController ◄───┘
 │  (3) surfaceUpdates (Stream<SurfaceUpdate>)
 ▼
Surface (Flutter Widget)
 │  (4) Catalog widget builders render
 │      Flutter widgets from Components
 ▼
User interactions → UiEvent → back to Transport
```

---

## Quick Reference — Top-Level Classes

### `Conversation`

High-level facade for managing a GenUI conversation. Orchestrates the `SurfaceController` and `Transport`.

```dart
Conversation({
  required SurfaceController controller,
  required Transport transport,
})
```

| Property / Method      | Type                                         | Purpose                                        |
| ---------------------- | -------------------------------------------- | ---------------------------------------------- |
| `controller`           | `SurfaceController`                          | Manages surfaces                               |
| `transport`            | `Transport`                                  | AI communication                               |
| `events`               | `Stream<ConversationEvent>`                  | Event stream (surfaces, text, errors)          |
| `state`                | `ValueListenable<ConversationState>`         | Current conversation state                     |
| `sendRequest(message)` | `Future<void>`                               | Send user message to AI                        |
| `dispose()`            | `void`                                       | Clean up resources                             |

### ConversationEvent (Sealed)

| Event                          | Key Fields               | Purpose                |
| ------------------------------ | ------------------------ | ---------------------- |
| `ConversationSurfaceAdded`     | `surfaceId`, `definition`| New surface created    |
| `ConversationComponentsUpdated`| `surfaceId`, `definition`| Components updated     |
| `ConversationSurfaceRemoved`   | `surfaceId`              | Surface deleted        |
| `ConversationContentReceived`  | `text`                   | Text response from AI  |
| `ConversationWaiting`          | —                        | Waiting for response   |
| `ConversationError`            | `error`, `stackTrace?`   | Error occurred         |

### ConversationState

```dart
class ConversationState {
  final List<String> surfaces;   // Active surface IDs
  final String latestText;       // Latest text received
  final bool isWaiting;          // Waiting for response
}
```

---

### `Surface`

Flutter widget that dynamically renders a UI from a `SurfaceDefinition`.

```dart
Surface({
  required SurfaceHost host,
  required String surfaceId,
  WidgetBuilder? defaultBuilder,
})
```

- Listens to `host` for updates to `surfaceId`
- Recursively builds Flutter widgets from `Component` definitions via the `Catalog`
- Dispatches user interactions back to the host

---

### `Transport` (Interface)

Abstract interface for AI communication. Implement this to connect to a custom backend.

```dart
abstract interface class Transport {
  Stream<String> get incomingText;
  Stream<A2uiMessage> get incomingMessages;
  Future<void> sendRequest(ChatMessage message);
  void dispose();
}
```

---

### `A2uiTransportAdapter`

Push-based transport for imperative integration. Wraps `A2uiParserTransformer` to parse streaming text into A2UI messages.

```dart
A2uiTransportAdapter({ManualSendCallback? onSend})
```

| Method / Property  | Type                    | Purpose                                |
| ------------------ | ----------------------- | -------------------------------------- |
| `addChunk(text)`   | `void`                  | Feed text from LLM                     |
| `addMessage(msg)`  | `void`                  | Inject raw A2uiMessage                 |
| `incomingText`     | `Stream<String>`        | Sanitized text for chat UI             |
| `incomingMessages` | `Stream<A2uiMessage>`   | Parsed A2UI messages                   |
| `sendRequest(msg)` | `Future<void>`          | Delegates to `onSend` callback         |

---

### `SurfaceController`

Runtime controller for the GenUI system. Manages surfaces, data models, and message routing.

```dart
SurfaceController({
  required Iterable<Catalog> catalogs,
  Duration pendingUpdateTimeout = const Duration(minutes: 1),
})
```

| Property / Method         | Type                              | Purpose                                    |
| ------------------------- | --------------------------------- | ------------------------------------------ |
| `catalogs`                | `Iterable<Catalog>`               | Available component catalogs               |
| `surfaceUpdates`          | `Stream<SurfaceUpdate>`           | Surface lifecycle events                   |
| `onSubmit`                | `Stream<ChatMessage>`             | Messages to submit to AI                   |
| `activeSurfaceIds`        | `Iterable<String>`                | Currently active surfaces                  |
| `clientCapabilities`      | `A2UiClientCapabilities`          | Auto-generated from catalogs               |
| `handleMessage(msg)`      | `void`                            | Process an A2uiMessage                     |
| `contextFor(surfaceId)`   | `SurfaceContext`                  | Get context for a surface                  |
| `dispose()`               | `void`                            | Clean up                                   |

Implements both `SurfaceHost` and `A2uiMessageSink`.

---

### `PromptBuilder`

Builds system prompts from catalogs and fragments for AI communication.

```dart
// Chat-style: creates new surfaces per response, no deletions
PromptBuilder.chat({
  required Catalog catalog,
  Iterable<String> systemPromptFragments = const [],
  String importancePrefix = 'IMPORTANT: ',
  JsonMap? clientDataModel,
})

// Custom operations control
PromptBuilder.custom({
  required Catalog catalog,
  required SurfaceOperations allowedOperations,
  Iterable<String> systemPromptFragments = const [],
  ...
})
```

### `PromptFragments`

Static utility methods for common prompt fragments:

| Method | Purpose |
|---|---|
| `PromptFragments.acknowledgeUser()` | Require AI to acknowledge user message |
| `PromptFragments.requireAtLeastOneSubmitElement()` | Require submit elements |
| `PromptFragments.currentDate()` | Inject current date |
| `PromptFragments.uiGenerationRestriction()` | Restrict to JSON text blocks |

---

### `A2UiClientCapabilities`

Describes the client's UI rendering capabilities to the server.

```dart
A2UiClientCapabilities({
  required List<String> supportedCatalogIds,
  List<JsonMap>? inlineCatalogs,
})

// From catalogs:
factory A2UiClientCapabilities.fromCatalogs(
  Iterable<Catalog> catalogs, {
  InlineCatalogHandling inlineHandling = InlineCatalogHandling.missingIds,
})
```

| `InlineCatalogHandling` | Behavior |
|---|---|
| `none` | Never inline; throw if catalog has no ID |
| `missingIds` | Inline only catalogs without a `catalogId` |
| `all` | Inline all catalogs |

---

### `SurfaceUpdate` (Sealed)

Events broadcast when surfaces change.

```dart
sealed class SurfaceUpdate {
  final String surfaceId;
}

final class SurfaceAdded extends SurfaceUpdate {
  final SurfaceDefinition definition;
}

final class ComponentsUpdated extends SurfaceUpdate {
  final SurfaceDefinition definition;
}

final class SurfaceRemoved extends SurfaceUpdate {}
```

---

## Reference Docs

| Topic                         | File                                            | Key Classes                                                                        |
| ----------------------------- | ----------------------------------------------- | ---------------------------------------------------------------------------------- |
| Data binding & A2uiSchemas    | [data-binding.md](./references/data-binding.md) | `DataModel`, `DataContext`, `DataPath`, `A2uiSchemas`, `DataContextExtensions`     |
| Catalog & widget building     | [catalog-api.md](./references/catalog-api.md)   | `Catalog`, `CatalogItem`, `CatalogItemContext`, `BasicCatalog`                     |
| A2UI protocol & chat messages | [messages.md](./references/messages.md)         | `A2uiMessage`, `ChatMessage`, `MessagePart`                                        |
| UI models, events & tools     | [ui-models.md](./references/ui-models.md)       | `SurfaceDefinition`, `Component`, `SurfaceUpdate`, `UiEvent`, `SurfaceController`  |

---
> Source: [gskinnerTeam/flutter-hatcha-app](https://github.com/gskinnerTeam/flutter-hatcha-app) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-24 -->
