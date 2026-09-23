---
name: dualforge-workflow
description: Build Claude + Codex dual AI collaboration framework for new projects. Start from PRD co-creation, generate complete division of labor system (plan design, implementation verification, review process). Suitable for projects with clear requirements and long-term iteration needs. Use when this capability is needed.
metadata:
  author: zc8163623
---

# DualForge Workflow - Dual AI Collaboration Framework Builder

## Core Concept

Establish a clear AI collaboration system:
- **Claude (Designer)**: Requirements analysis, technical solution design, architecture decisions, code review
- **Codex (Implementer)**: Coding according to established plans, writing tests, running verification scripts
- **Human (Decision Maker)**: Final judgment, requirement confirmation, direction control

**Workflow:** Human → Claude (Plan) → Codex (Implement) → Claude (Review) → Human (Decision)

## Your Responsibilities

As Claude, you are responsible for guiding users through the entire framework setup:
1. Co-create PRD document with users
2. Configure collaboration mechanisms based on project characteristics
3. Generate complete documentation system
4. Output follow-up work guidance

## Workflow

### Stage 0: Project Information Collection

First, ask the user:

```
I will help you set up the Claude + Codex dual AI collaboration framework. First, I need to understand basic project information:

1. What is the project name?
2. Describe the project in one sentence (core value/problem to solve)
3. Project scale estimate:
   □ Small (personal project/quick MVP, core features < 10)
   □ Medium (team project/standard product, core features 10-30)
   □ Large (complex system/platform-level product, core features > 30)
```

### Stage 1: PRD Co-creation

Adopt different depths based on project scale:

**Small Projects (Lightweight PRD)**
- Core feature list (5-10 items)
- Target user personas (1-2)
- Key technical constraints (3-5 items)
- Estimated 5-10 rounds of conversation

**Medium Projects (Standard PRD)**
- Functional requirements with numbering (FR-1.1, FR-1.2...)
- Acceptance criteria for each requirement
- User personas and use cases
- Technical architecture requirements
- Estimated 10-15 rounds of conversation

**Large Projects (In-depth PRD)**
- Complete requirement numbering system
- Detailed acceptance criteria (main text + appendix)
- Multiple user personas with priorities
- Design principles (3-5 items)
- Technical prerequisites and architectural constraints
- Not-to-do list (MVP scope definition)
- Estimated 20+ rounds of conversation

**Guidance Principles:**
- Use conversational approach, not form-based (don't ask 20 questions at once)
- Focus on one theme each time (users → features → constraints → principles)
- Adjust questioning intensity based on user response depth
- Summarize and confirm understanding promptly

**PRD Required Sections:**
1. Project Overview (background, goals, users)
2. Functional Requirements (numbered FR list)
3. Acceptance Criteria (testable standards for each FR)
4. Technical Requirements (architecture, tech stack, performance requirements)
5. Design Principles (if any, 3-5 items for conflict resolution)
6. Not-to-do List (clearly define what MVP does not include)

Output file: `PRD.md`

### Stage 2: Collaboration Mechanism Configuration

Based on PRD content, ask the user:

```
PRD is complete! Now configure the collaboration mechanism:

1. Do you need task plan file mechanism?
   Detected this is a [{scale}] project, recommendation: [{recommendation}]
   
   □ Yes - Each task has Claude write technical plan file first, then Codex implements
           Suitable for: complex requirements, multi-iteration, team collaboration projects
   
   □ No - Claude gives plans directly in conversation, Codex implements from conversation
          Suitable for: simple requirements, rapid prototypes, personal projects

2. What is the tech stack? (e.g., TypeScript + React + Node.js)
   
3. Any special architectural layering requirements?
   Example: certain layer must be pure functions, no external service dependencies
   (Can skip, can supplement in AGENTS.md later)

4. Test coverage requirements?
   □ Standard (overall ≥60%, core modules ≥80%)
   □ Strict (overall ≥80%)
   □ Relaxed (overall ≥40%, rapid iteration priority)
```

**Recommendation Rules:**
- Small projects: No task files needed (unless user specifically requires strict process)
- Medium projects: Recommend using task files
- Large projects: Strongly recommend using task files

### Stage 3: Generate Collaboration Framework

Based on information from previous two stages, generate the following files:

#### Required Files (All Projects)

**1. `CLAUDE.md` - Claude Behavior Specification**

Generate based on template, core content:
- Role division explanation
- Requirements analysis method (start from PRD, locate FR)
- Technical solution design requirements
- Project planning principles
- Code review checklist
- Decision recording specifications
- **Handoff instruction requirement**:
  ```markdown
  ## 2. Technical Solution Design
  
  [Original content...]
  
  ### Handoff After Plan Output
  
  After plan file is output, must output a concise handoff instruction, including:
  - Plan file path
  - Corresponding FR and acceptance criteria highlights
  - Constraints requiring special attention
  
  Example format:
  ```
  Plan ready: .ai/tasks/1.2-feature-name.md
  
  📋 Handoff to Codex:
  Please implement FR-x.x [Feature Name]. Key points:
  - Point 1
  - Point 2
  - Test coverage requirement ≥ X%
  
  See plan file "Acceptance Criteria" section for verification standards, check each one carefully.
  ```
  ```

Insert project-specific information:
- PRD file path
- Design principles (if any)
- Key technical constraints

**2. `AGENTS.md` - Codex Behavior Specification**

Generate based on template, core content:
- Pre-work checklist (plan file → brief.md → PRD)
- Iron rules (non-violable constraints)
- Architectural boundaries (dependency direction, layering requirements)
- Coding standards (language, style, naming)
- Testing requirements (coverage, required test cases)
- check.sh verification process
- Commit standards
- Delivery checklist (self-check → update status → append implementation record → request Review)
- Situations requiring stop and ask

Insert project-specific information:
- Tech stack (TypeScript / Python / Go, etc.)
- Test coverage requirements
- Architectural layering constraints (if any)
- First task: "Improve the three scripts under scripts/ (check.sh, build.sh, test.sh)"

**3. `scripts/check.sh` - Verification Script Framework**

Generate framework script with detailed comments, including stages:
1. Project structure check
2. Architectural boundary check (if layering requirements exist)
3. Code format check
4. Lint check
5. Type check
6. Unit tests
7. Integration tests (optional)

Each stage explained with comments:
```bash
# ========== Stage 5: Type Check ==========
# Implement corresponding type check command based on your tech stack:
# Examples:
#   TypeScript: tsc --noEmit
#   Python: mypy src/
#   Go: go vet ./...
#   Rust: cargo check

echo "⚠️  Type check not yet implemented, please have Codex improve this stage based on tech stack"
# TODO: Implement type check command
```

**4. `scripts/build.sh` - Build Script Framework**

Generate build script template:
```bash
#!/bin/bash
# Build script - improve based on project tech stack

set -e  # Exit immediately on error

echo "🔨 Starting build..."

# TODO: Implement build command based on tech stack
# Examples:
#   TypeScript: npm run build or tsc
#   Python: python setup.py build
#   Go: go build ./...
#   Rust: cargo build --release

echo "⚠️  Build command not yet implemented, please have Codex improve based on tech stack"
exit 1
```

**5. `scripts/test.sh` - Test Script Framework**

Generate test script template:
```bash
#!/bin/bash
# Test script - improve based on project tech stack

set -e  # Exit immediately on error

echo "🧪 Running tests..."

# TODO: Implement test command based on tech stack
# Examples:
#   TypeScript: npm test or vitest
#   Python: pytest
#   Go: go test ./...
#   Rust: cargo test

echo "⚠️  Test command not yet implemented, please have Codex improve based on tech stack"
exit 1
```

**6. `src/` - Source Code Root Directory**

Create empty source directory as root for subsequent code development.

**7. `.ai/brief.md` - Entry Context + Collaboration Contract**

Include:
- Project one-line definition (from Stage 0)
- Project background and goals (from PRD)
- Core feature overview
- Design principles (if any)
- Technical requirements summary
- **Collaboration contract** (fixed content):
  - Task flow sequence diagram
  - Four responsibility assignments table
  - Stop-and-ask trigger conditions
  - Plan file naming rules
- Related documentation index
- **Quick-switch phrases**:
  ```markdown
  ## Quick Switch Commands (Copy-Paste)
  
  ### Handoff to Codex for Implementation
  > Please implement according to plan file `.ai/tasks/<number>-<identifier>.md`, request Review after completion.
  
  ### Handoff to Claude for Review
  > Task X.X completed, check.sh all green, please Review. Implementation record appended to plan file.
  ```

**8. `.ai/plan.md` - Project Plan**

Generate initial task outline based on PRD functional modules:

```markdown
# Project Plan - {Project Name}

## Stage 0: Infrastructure (Estimated X days)

### 0.1 Script Improvement ○
- Improve check commands in scripts/check.sh
- Corresponding FR: None (engineering foundation)

### 0.2 Project Structure Setup ○
- Create directory structure
- Configure build tools
- Corresponding FR: None (engineering foundation)

## Stage 1: [Core Module Name] (Estimated X days)

### 1.1 [Feature 1] ○
- Corresponding FR-x.x
- Dependencies: 0.1, 0.2

### 1.2 [Feature 2] ○
- Corresponding FR-x.x
- Dependencies: 1.1

[Auto-generate more stages based on PRD...]

---

## Status Markers

- ○ To start
- ◍ In progress
- ✓ Completed

Updated by Codex upon completion.
```

**9. `.ai/review.md` - Review Checklist**

Fixed template, includes check items:
- Delivery completeness
- Product semantics
- Product principles (if PRD has design principles, list them)
- Architectural boundaries
- Testing
- Error handling
- Data and migration
- Compliance and security
- Engineering quality
- Documentation sync

**10. `.ai/decision-log.md` - Architecture Decision Records**

Initial content:

```markdown
# Architecture Decision Records (ADR)

> Record technical selections, architectural adjustments, important trade-offs. Format: title + context + decision + consequences + review conditions.

---

## ADR-001: Tech Stack Selection

**Date**: {Current Date}
**Status**: Adopted

### Context

Project startup phase, need to determine main tech stack.

### Decision

Adopt the following tech stack:
- {User-provided tech stack}

### Rationale

{If user provided reasoning in Stage 2, record it; otherwise write "User selected"}

### Consequences

- Advantages: {Fill based on tech stack characteristics}
- Disadvantages: {Fill based on tech stack characteristics}
- Migration cost: {Assess}

### Review Conditions

- Performance cannot meet requirements
- Team skill stack undergoes major changes
- Tech stack enters EOL status
```

#### Conditionally Generated Files

**11. `.ai/tasks/_TEMPLATE.md` - Plan Template** (If user chooses to need task file mechanism)

Fixed template:
```markdown
# Plan Template

> Usage: Claude copies this file as `.ai/tasks/<stage-number>-<short-identifier>.md` and fills in "Design" section;
> Codex reads it to start work, after completion **only appends "Implementation Record" at the end, does not modify plan body**.

---

# <Task Title>

- **Corresponding FR**: FR-x.x (PRD Chapter x.x)
- **Corresponding Plan Task**: plan.md Stage X Task X.X
- **Status**: To implement / Implementing / Pending Review / Merged

## Design (Claude fills)

### Problem Definition

What to solve. **Clearly define what NOT to solve** — prevent scope creep.

### Acceptance Criteria

Copy verbatim from PRD's acceptance criteria for this FR, and note **how each is tested**.

- [ ] Criterion 1 → Test: `tests/...`
- [ ] Criterion 2 → Test: `tests/...`

### Current State

What related code and data currently look like (read before writing).

### Solution

Core approach + key data structures + layer assignment.

### Trade-offs

Other solutions considered and reasons for rejection.

### Impact Scope

Which modules involved / migration needed / breaking changes.

### Product Principles Check

- Conflicts with design principles?
- What hard constraints involved?

### Risks

Potential failure points and responses.

---

## Implementation Record (Codex appends after completion)

- **Actually modified files**:
- **New tests**:
- **Deviations from plan and reasons**: (Write "None" if none)
- **Remaining issues / Follow-up todos**:
- **check.sh**: All green / Has skipped items (list them)
```

#### Supporting Files

**12. `GETTING_STARTED.md` - Follow-up Work Guidance**

```markdown
# Getting Started with DualForge Collaboration Framework

## ✅ Completed

- [x] PRD document (`PRD.md`)
- [x] Collaboration specifications (`CLAUDE.md` + `AGENTS.md`)
- [x] Script frameworks (`scripts/check.sh` + `build.sh` + `test.sh`)
- [x] Source directory (`src/`)
- [x] Project plan (`.ai/plan.md`)
- [x] Collaboration contract (`.ai/brief.md`)

## 📋 Next Steps (In Order)

### 1. Improve Scripts (First Task)

**Handoff to Codex:**
> Please improve specific commands in the three scripts under `scripts/`:
> - check.sh: Check commands for each stage
> - build.sh: Build command
> - test.sh: Test command
> 
> Tech stack: {User-provided tech stack}
> Reference: Comments and examples in the scripts

**Acceptance Criteria:**
- Each script has actually executable commands
- Can run correctly locally
- Clear error messages on failure

### 2. Improve Project Plan (If Needed)

Current `.ai/plan.md` is an outline auto-generated from PRD.
Suggest Claude adjust based on actual situation:
- Adjust task granularity (each task 0.5-2 days)
- Mark dependencies
- Identify critical path

### 3. Start First Feature Development

**Complete Process:**

```
You (propose requirement)
  ↓
Claude (analyze requirement → produce plan file → output handoff instruction)
  ↓ Copy handoff instruction
Codex (read plan → implement + test → check.sh → update status → request Review)
  ↓ Copy Review request
Claude (Review → give conclusion)
  ↓
You (decide whether to merge)
```

## 🔖 Quick Switch Phrases (`.ai/brief.md` end also has these)

### Handoff to Codex for Implementation
> Please implement according to plan file `.ai/tasks/<number>-<identifier>.md`, request Review after completion.

### Handoff to Claude for Review
> Task X.X completed, check.sh all green, please Review. Implementation record appended to plan file.

## 📚 Documentation Index

- `PRD.md` - Requirements single source of truth
- `CLAUDE.md` - Claude's work specifications
- `AGENTS.md` - Codex's work specifications
- `.ai/brief.md` - Project entry + collaboration contract
- `.ai/plan.md` - Project plan
- `.ai/review.md` - Review checklist
- `.ai/decision-log.md` - Architecture decision records
- `.ai/tasks/_TEMPLATE.md` - Plan template{if generated}

## ⚠️ Important Reminders

1. **PRD is single source of truth**: All requirements follow PRD, update PRD first if issues found
2. **Design before implementation**: Non-trivial tasks must have plan file first
3. **check.sh is gate**: No commit on red light
4. **Codex proactively requests Review**: Don't wait for manual prompting
5. **Human makes final decisions**: AI handles execution and suggestions, human handles decisions

## 🎯 First Milestone

Suggest using a small feature (1-2 days) to complete the entire process first, verify if collaboration model is smooth.
```

### Stage 4: Delivery and Explanation

After generating all files, output to user:

```markdown
## ✅ DualForge Collaboration Framework Setup Complete

### Generated Files

Created in project root directory:
- `PRD.md` - Product Requirements Document
- `CLAUDE.md` - Claude work specification
- `AGENTS.md` - Codex work specification
- `GETTING_STARTED.md` - Follow-up work guidance
- `scripts/check.sh` - Verification script framework
- `scripts/build.sh` - Build script framework
- `scripts/test.sh` - Test script framework
- `src/` - Source code root directory
- `.ai/brief.md` - Project entry + collaboration contract
- `.ai/plan.md` - Project plan
- `.ai/review.md` - Review checklist
- `.ai/decision-log.md` - Architecture decision records
{If plan template generated}
- `.ai/tasks/_TEMPLATE.md` - Plan template

### 📖 Suggest You Now

1. **Read `GETTING_STARTED.md`** to understand next steps
2. **Have Codex improve `scripts/check.sh`** as first task
3. **Pick a small feature to complete the full process** to verify collaboration model

### 🔄 Collaboration Flow

Remember this process:
```
You propose requirement → Claude gives plan → Codex implements → Claude Reviews → You decide
```

Each role only does what they're good at, responsibilities clear without overstepping.

### 💡 Quick Switch Phrases

Built into `.ai/brief.md` end, copy-paste when needed:
- Handoff to Codex: "Please implement according to plan file..."
- Handoff to Claude: "Completed, please Review..."

---

Best wishes for your project! Feel free to come back and adjust the framework if any issues arise.
```

## Key Implementation Details

### PRD Co-creation Techniques

**Small Project Example Conversation Flow:**
```
Claude: What problem does this project mainly solve? Who will use it?
User: [Answer]
Claude: What are the core features? (List 3-5 most important ones)
User: [Answer]
Claude: Any special technical requirements? Like performance, compatibility, security?
User: [Answer]
Claude: [Summary] My understanding is... Is this correct?
User: [Confirm/Correct]
Claude: Okay, PRD complete, starting to generate collaboration framework...
```

**Large Project Example Conversation Flow:**
```
Claude: Let's talk about project background and target users first...
[3-5 rounds of conversation to clarify problem domain]

Claude: Now let's organize functional requirements. Let's go module by module, starting with core process...
[10-15 rounds of conversation, each module one by one]

Claude: Each feature needs defined acceptance criteria, for example FR-1.1 xxx feature, how do we know it's done right?
[Confirm acceptance criteria one by one]

Claude: Does the project have any design principles? What priority for conflict resolution?
[Guide to extract 3-5 principles]

Claude: What is clearly out of scope for MVP?
[Define boundaries]

Claude: [Output complete PRD draft] Please confirm...
```

### File Generation Priority

1. **Generate `PRD.md` first** (immediately write after Stage 1 completion)
2. **Then generate core specifications** (`CLAUDE.md`, `AGENTS.md`, `.ai/brief.md`)
3. **Then generate supporting files** (`plan.md`, `review.md`, `decision-log.md`)
4. **Then generate scripts and directories** (`scripts/check.sh`, `scripts/build.sh`, `scripts/test.sh`, `src/`)
5. **Finally generate supporting files** (`GETTING_STARTED.md`, plan template if needed)

**Rationale**: PRD is information source for subsequent files, must land first; core specifications define collaboration rules; supporting files depend on core specification content; scripts and directories are infrastructure; supporting files generated last for easy summary.

### Dynamic Content Insertion

When generating files, need to dynamically insert user-provided information:

**CLAUDE.md needs to insert:**
- PRD file path (`AI_Character_Studio_PRD.md` → `PRD.md`)
- Design principles (if in PRD)
- Key technical constraints (if architectural layering requirements exist)

**AGENTS.md needs to insert:**
- Tech stack information
- Test coverage requirements
- Architectural layering constraints (if any)
- First task: "Improve the three scripts under scripts/ (check.sh, build.sh, test.sh)"

**brief.md needs to insert:**
- Project one-line definition
- Project background (from PRD)
- Core feature overview (from PRD)
- Design principles (if any)

**plan.md needs to insert:**
- Auto-generate task list based on PRD functional modules
- Each FR corresponds to at least one task
- Stage 0 fixed includes "Improve scripts under scripts/ (check.sh, build.sh, test.sh)"

### Script Generation Considerations

**check.sh:**
1. **Fixed stage order**: Structure check → boundary check → format → lint → types → tests
2. **Each stage independent**: Failure doesn't affect subsequent stage runs (for diagnosing multiple issues)
3. **Provide multi-tech-stack examples**: Common commands for TypeScript, Python, Go, Rust
4. **Clearly mark TODO**: Let Codex know what needs implementation
5. **Friendly error messages**: Tell user "This stage not yet implemented, please refer to comments for improvement"

**build.sh and test.sh:**
1. **Unified structure**: shebang + set -e + echo prompt + TODO comments + not-implemented message
2. **Multi-tech-stack examples**: List common tech stack commands in comments
3. **Clearly mark pending**: exit 1 ensures not mistaken as passed when unconfigured

### Task File Mechanism Description

If user chooses "Don't need task files":
- Don't generate `.ai/tasks/` directory
- In `CLAUDE.md` state: "Technical plans given in conversation, no need to write to file"
- In `AGENTS.md` state: "Plans obtained from conversation history"
- In `brief.md` adjust collaboration flow diagram (remove "plan file" node)

But still retain:
- `.ai/plan.md` (plan management still needed)
- Review mechanism (Codex still needs to proactively request)
- Status update mechanism (mark in plan.md)

## Notes

1. **Don't generate all files at once**: Generate while asking, give users chance to confirm
2. **PRD is most important**: If user-provided information insufficient for clear PRD, continue asking, don't generate vague requirements
3. **Respect user choices**: If user says "don't need task files", "relaxed test requirements", don't forcibly recommend strict mode
4. **Maintain consistency**: All files should reference PRD uniformly, avoid some writing `PRD.md`, others writing `requirements.md`
5. **Scripts are executable**: All generated scripts (check.sh, build.sh, test.sh) must be directly runnable (even if reporting "not implemented"), cannot have syntax errors
6. **Handoff phrases should be copyable**: Quick-switch phrases provided in brief.md should be concise, uniformly formatted

## Common Issue Handling

**Q: User says "I haven't figured out requirements yet"?**
A: Guide user to first describe problem domain and target users, help organize requirements. Need at least 3-5 core features to continue.

**Q: User says "My project is special, doesn't fit this model"?**
A: Ask specifically what doesn't fit, see if adjustable. If truly unsuitable (e.g., one-off script, purely experimental project, no collaboration needed), suggest user not use this skill.

**Q: User wants to modify project scale/tech stack mid-way?**
A: Can regenerate affected files. Already generated files won't auto-update, need to explicitly tell user which files need manual adjustment.

**Q: After generation user finds PRD has issues?**
A: PRD is single source of truth, can modify anytime. Remind user after modification need to check if other files' references need sync.

## Success Criteria

After framework setup completion, user should be able to:
1. Clearly understand Claude and Codex's respective responsibilities
2. Know how to start first task
3. Have clear PRD as requirements basis
4. Have executable verification script (even if partially pending)
5. Have clear collaboration flow path

If user still confused about "what to do next", indicates `GETTING_STARTED.md` not clear enough, need supplementary explanation.

---
> Source: [zc8163623/DualForge-Workflow](https://github.com/zc8163623/DualForge-Workflow) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-14 -->
