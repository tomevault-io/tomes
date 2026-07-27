---
name: a2ui-agent-sdk
description: Python SDK for building A2UI agents. Use when: working with A2uiSchemaManager, a2ui.a2a.extension, a2ui.a2a.parts, a2ui.schema.constants, SendA2uiToClientToolset, BasicCatalog, CatalogConfig, A2uiStreamParser, InferenceStrategy, A2UI extension negotiation, or protocol constants (A2UI_OPEN_TAG, A2UI_CLOSE_TAG, DEFAULT_WORKFLOW_RULES). Use when this capability is needed.
metadata:
  author: gskinnerTeam
---

# a2ui-agent-sdk Package — API Reference

The `a2ui-agent-sdk` package (v0.2.1) provides Python tools for building A2UI-capable agents. It handles schema management, prompt generation, A2A extension negotiation, DataPart creation, response streaming/parsing, and catalog loading — everything a Python agent needs to emit structured A2UI JSON over the A2A protocol.

## When to Use

- Building a system prompt with catalog-aware schema injection via `A2uiSchemaManager`
- Activating the A2UI extension during A2A handshake
- Creating `DataPart`s from A2UI message dictionaries
- Using protocol constants (`A2UI_OPEN_TAG`, `A2UI_CLOSE_TAG`, `DEFAULT_WORKFLOW_RULES`)
- Loading catalog schemas from files or bundled resources
- Parsing/streaming A2UI responses (v0.8 and v0.9 formats)
- Using the experimental `SendA2uiToClientToolset` with Google ADK

> **Prerequisite**: Read the `ai-system` skill for the Two-Layer AI Architecture context and how Python agents use this SDK within the `hatcha_agent`.

---

## Package Structure

```
a2ui/
├── inference_strategy.py        # Abstract InferenceStrategy base
├── a2a/
│   ├── extension.py             # A2UI A2A extension negotiation
│   └── parts.py                 # DataPart creation/parsing/streaming
├── adk/
│   └── send_a2ui_to_client_toolset.py  # ADK toolset (experimental)
├── basic_catalog/
│   ├── constants.py             # BASIC_CATALOG_NAME, version paths
│   └── provider.py             # BundledCatalogProvider, BasicCatalog
├── parser/
│   ├── streaming.py             # A2uiStreamParser base
│   ├── streaming_v08.py         # v0.8 tag-delimited parser
│   ├── streaming_v09.py         # v0.9 tag-delimited parser
│   ├── payload_fixer.py         # JSON repair utilities
│   └── response_part.py         # ResponsePart model
├── schema/
│   ├── catalog.py               # A2uiCatalog, CatalogConfig, providers
│   ├── catalog_provider.py      # A2uiCatalogProvider interface
│   ├── constants.py             # Tags, versions, workflow rules
│   ├── manager.py               # A2uiSchemaManager
│   ├── validator.py             # Schema validation
│   └── utils.py                 # Bundled resource loading
└── template/
    └── manager.py               # A2uiTemplateManager (not yet implemented)
```

---

## A2uiSchemaManager

Primary class for generating system prompts with embedded catalog schemas and examples. Implements `InferenceStrategy`.

### Constructor

```python
from a2ui.schema.manager import A2uiSchemaManager

manager = A2uiSchemaManager(version="0.9", accepts_inline_catalogs=True)
```

| Parameter                 | Type   | Purpose                                                   |
| ------------------------- | ------ | --------------------------------------------------------- |
| `version`                 | `str`  | Protocol version (`"0.8"` or `"0.9"`)                     |
| `accepts_inline_catalogs` | `bool` | Whether to accept inline catalog definitions from clients |

### Methods

| Method                   | Signature                                                                         | Purpose                                     |
| ------------------------ | --------------------------------------------------------------------------------- | ------------------------------------------- |
| `generate_system_prompt` | See below                                                                         | Build a full system prompt with schema      |
| `get_selected_catalog`   | `(client_ui_capabilities?, allowed_components?, allowed_messages?) → A2uiCatalog` | Get catalog filtered by client capabilities |
| `load_examples`          | `(catalog: A2uiCatalog, validate: bool = False) → str`                            | Load example JSON for prompt injection      |

### `generate_system_prompt`

```python
prompt = manager.generate_system_prompt(
    role_description="You are a party planning assistant...",
    workflow_description="Ask the user questions one at a time...",
    ui_description="Use cards and buttons for responses.",
    client_ui_capabilities=None,       # Dict from client metadata
    allowed_components=None,           # List of component names to include
    allowed_messages=None,             # List of message types to include
    include_schema=False,              # Embed full JSON schema
    include_examples=False,            # Embed example payloads
    validate_examples=False,           # Validate examples against schema
)
```

### Usage in This Project

```python
# agents/hatcha_agent/base_agent.py
from a2ui.schema.manager import A2uiSchemaManager

_SCHEMA_MANAGER = A2uiSchemaManager(version="0.9", accepts_inline_catalogs=True)

class BaseAgent:
    def __init__(self, ...):
        self.schema_manager = _SCHEMA_MANAGER
```

---

## Extension Negotiation — `a2ui.a2a.extension`

Handles the A2UI extension handshake within the A2A protocol.

### Functions

| Function                      | Signature                                                          | Purpose                                                                     |
| ----------------------------- | ------------------------------------------------------------------ | --------------------------------------------------------------------------- |
| `try_activate_a2ui_extension` | `(context: RequestContext, agent_card: AgentCard) → Optional[...]` | Match client extension URI against agent card; returns activation or `None` |
| `get_a2ui_agent_extension`    | `() → AgentExtension`                                              | Returns the `AgentExtension` object to include in the agent card            |

### Constants

| Constant                                      | Value      | Purpose                                 |
| --------------------------------------------- | ---------- | --------------------------------------- |
| `A2UI_EXTENSION_BASE_URI`                     | URI string | Base URI for the A2UI extension         |
| `AGENT_EXTENSION_ACCEPTS_INLINE_CATALOGS_KEY` | `str`      | Metadata key for inline catalog support |
| `AGENT_EXTENSION_SUPPORTED_CATALOG_IDS_KEY`   | `str`      | Metadata key for supported catalog IDs  |

### Usage in This Project

```python
# agents/hatcha_agent/__main__.py
from a2ui.a2a.extension import get_a2ui_agent_extension

agent_card = AgentCard(
    ...
    capabilities=AgentCapabilities(
        extensions=[get_a2ui_agent_extension()],
        streaming=True,
    ),
)

# agents/hatcha_agent/a2ui_protocol.py
from a2ui.a2a.extension import try_activate_a2ui_extension

def activate_a2ui_extension(context, agent_card):
    return try_activate_a2ui_extension(context, agent_card) is not None
```

---

## DataPart Helpers — `a2ui.a2a.parts`

Converts A2UI message dictionaries to/from A2A `DataPart` objects.

### Functions

| Function                   | Signature                                         | Purpose                                              |
| -------------------------- | ------------------------------------------------- | ---------------------------------------------------- |
| `create_a2ui_part`         | `(message: dict) → Part`                          | Wrap a single A2UI message dict as an A2A `DataPart` |
| `parse_response_to_parts`  | `(response: Any) → List[Part]`                    | Parse a complete response into A2A parts             |
| `stream_response_to_parts` | `(response: AsyncIterable) → AsyncIterable[Part]` | Stream response chunks as A2A parts                  |
| `get_a2ui_datapart`        | `(parts: List[Part]) → Optional[DataPart]`        | Extract the first A2UI DataPart from a list          |
| `is_a2ui_part`             | `(part: Part) → bool`                             | Check if a part is an A2UI DataPart                  |
| `has_a2ui_parts`           | `(parts: List[Part]) → bool`                      | Check if any part is A2UI                            |

### Constants

| Constant         | Value            | Purpose                         |
| ---------------- | ---------------- | ------------------------------- |
| `A2UI_MIME_TYPE` | MIME type string | Content type for A2UI DataParts |

### Usage in This Project

```python
# agents/hatcha_agent/a2ui_protocol.py
from a2ui.a2a.parts import create_a2ui_part

def messages_to_parts(messages, catalog_id=None):
    return [create_a2ui_part(_flatten_message(m, catalog_id)) for m in messages]
```

---

## Protocol Constants — `a2ui.schema.constants`

### Tags & Delimiters

| Constant                  | Value            | Purpose                                    |
| ------------------------- | ---------------- | ------------------------------------------ |
| `A2UI_OPEN_TAG`           | `'<a2ui-json>'`  | Opening delimiter for A2UI JSON blocks     |
| `A2UI_CLOSE_TAG`          | `'</a2ui-json>'` | Closing delimiter for A2UI JSON blocks     |
| `A2UI_SCHEMA_BLOCK_START` | String           | Start marker for schema section in prompts |
| `A2UI_SCHEMA_BLOCK_END`   | String           | End marker for schema section in prompts   |

### Workflow Rules

| Constant                 | Value             | Purpose                                 |
| ------------------------ | ----------------- | --------------------------------------- |
| `DEFAULT_WORKFLOW_RULES` | Multi-line string | Standard rules for A2UI response format |

Key rules from `DEFAULT_WORKFLOW_RULES`:

- Responses can contain one or more A2UI JSON blocks
- Each block wrapped in `<a2ui-json>` / `</a2ui-json>` tags
- Conversational text allowed between/around blocks
- JSON must validate against the provided schema
- Top-down component ordering within `components` lists

### Version Constants

| Constant           | Value   | Purpose                          |
| ------------------ | ------- | -------------------------------- |
| `VERSION_0_8`      | `"0.8"` | Protocol version 0.8             |
| `VERSION_0_9`      | `"0.9"` | Protocol version 0.9 (current)   |
| `SPEC_VERSION_MAP` | `dict`  | Maps version → schema file paths |

### Other Keys

| Constant                       | Purpose                              |
| ------------------------------ | ------------------------------------ |
| `A2UI_CLIENT_CAPABILITIES_KEY` | Metadata key for client capabilities |
| `CATALOG_COMPONENTS_KEY`       | Key for components in catalog schema |
| `CATALOG_ID_KEY`               | Key for catalog identifier           |
| `CATALOG_SCHEMA_KEY`           | Key for catalog schema content       |
| `CATALOG_STYLES_KEY`           | Key for catalog styles               |
| `INLINE_CATALOGS_KEY`          | Key for inline catalog definitions   |
| `SUPPORTED_CATALOG_IDS_KEY`    | Key for supported catalog IDs list   |
| `SURFACE_ID_KEY`               | Key for surface identifier           |

### Usage in This Project

```python
# agents/hatcha_agent/prompts/shared.py
from a2ui.schema.constants import A2UI_OPEN_TAG, A2UI_CLOSE_TAG, DEFAULT_WORKFLOW_RULES

A2UI_DELIMITER = f"{A2UI_OPEN_TAG}\n{{json}}\n{A2UI_CLOSE_TAG}"
```

---

## Catalog System — `a2ui.schema.catalog`

### A2uiCatalog

Loaded catalog with methods for rendering and pruning.

| Method                       | Signature                                                | Purpose                                         |
| ---------------------------- | -------------------------------------------------------- | ----------------------------------------------- |
| `render_as_llm_instructions` | `() → str`                                               | Render the catalog as LLM-readable instructions |
| `with_pruning`               | `(allowed_components?, allowed_messages?) → A2uiCatalog` | Return filtered copy                            |
| `load_examples`              | `(path?, validate?) → str`                               | Load example JSON from path                     |

### CatalogConfig

Configuration for loading a catalog.

```python
from a2ui.schema.catalog import CatalogConfig

config = CatalogConfig(
    name="my_catalog",
    provider=my_provider,
    examples_path="/path/to/examples/",
)

# Or from a filesystem path:
config = CatalogConfig.from_path(
    name="my_catalog",
    catalog_path="/path/to/catalog.json",
    examples_path="/path/to/examples/",
)
```

### A2uiCatalogProvider (Interface)

```python
class A2uiCatalogProvider:
    def load(self) -> Dict[str, Any]:
        """Load and return the catalog schema dictionary."""
        ...
```

### FileSystemCatalogProvider

```python
from a2ui.schema.catalog import FileSystemCatalogProvider

provider = FileSystemCatalogProvider("/path/to/catalog.json")
schema_dict = provider.load()
```

---

## Basic Catalog — `a2ui.basic_catalog`

Provides access to the bundled basic catalog (standard A2UI components).

```python
from a2ui.basic_catalog import BasicCatalog

config = BasicCatalog.get_config(version="0.9", examples_path=None)
```

| Method       | Signature                                             | Purpose                                  |
| ------------ | ----------------------------------------------------- | ---------------------------------------- |
| `get_config` | `(version: str, examples_path?: str) → CatalogConfig` | Get config for the bundled basic catalog |

---

## SendA2uiToClientToolset (ADK Integration — Experimental)

An ADK `BaseToolset` that exposes a `send_a2ui_json_to_client` tool to the LLM. The LLM calls this tool instead of emitting raw tagged JSON.

### Constructor

```python
from a2ui.adk.send_a2ui_to_client_toolset import SendA2uiToClientToolset

toolset = SendA2uiToClientToolset(
    a2ui_enabled=True,                    # bool or async provider
    a2ui_catalog=my_catalog,              # A2uiCatalog or async provider
    a2ui_examples="example JSON string",  # str or async provider
)
```

### Provider Types

```python
# Type aliases
A2uiEnabledProvider = Callable[[ReadonlyContext], bool | Awaitable[bool]]
A2uiCatalogProvider = Callable[[ReadonlyContext], A2uiCatalog | Awaitable[A2uiCatalog]]
A2uiExamplesProvider = Callable[[ReadonlyContext], str | Awaitable[str]]
```

### Integration with ADK Agent

```python
from google.adk.agents.llm_agent import LlmAgent

agent = LlmAgent(
    tools=[
        SendA2uiToClientToolset(
            a2ui_enabled=check_enabled,
            a2ui_catalog=get_catalog,
            a2ui_examples=get_examples,
        ),
    ],
)
```

### A2uiPartConverter

Converts tool call results into A2A parts. Retrieved via `get_part_converter(ctx)`.

### A2uiEventConverter

Event converter that automatically injects the A2UI catalog into part conversion.

> **Note**: This project does NOT currently use `SendA2uiToClientToolset`. Agents use the tag-based `<a2ui-json>` approach managed by `BaseAgent` + `a2ui_protocol.py`. The toolset is available for future migration to structured tool calling.

---

## Streaming Parsers — `a2ui.parser`

### A2uiStreamParser

Base class for parsing streaming A2UI responses.

### A2uiStreamParserV09

Parser for the v0.9 `<a2ui-json>...</a2ui-json>` tag-delimited format.

### Message Type Constants

| Constant                     | Value                | Purpose                   |
| ---------------------------- | -------------------- | ------------------------- |
| `MSG_TYPE_CREATE_SURFACE`    | `"createSurface"`    | Create a new surface      |
| `MSG_TYPE_UPDATE_COMPONENTS` | `"updateComponents"` | Update surface components |
| `MSG_TYPE_UPDATE_DATA_MODEL` | `"updateDataModel"`  | Update surface data model |
| `MSG_TYPE_DELETE_SURFACE`    | `"deleteSurface"`    | Delete a surface          |
| `MSG_TYPE_BEGIN_RENDERING`   | `"beginRendering"`   | Signal rendering start    |
| `MSG_TYPE_TEXT`              | `"text"`             | Plain text response       |

---

## InferenceStrategy (Abstract Base)

Base class for prompt generation strategies. `A2uiSchemaManager` implements this.

```python
from a2ui.inference_strategy import InferenceStrategy

class InferenceStrategy(ABC):
    @abstractmethod
    def generate_system_prompt(
        self,
        role_description: str,
        workflow_description: str = "",
        ui_description: str = "",
        client_ui_capabilities: Optional[dict[str, Any]] = None,
        allowed_components: Optional[list[str]] = None,
        allowed_messages: Optional[list[str]] = None,
        include_schema: bool = False,
        include_examples: bool = False,
        validate_examples: bool = False,
    ) -> str: ...
```

---

## Common Patterns in This Project

### 1. Schema Manager Singleton

```python
# base_agent.py — created once, shared by all agents
_SCHEMA_MANAGER = A2uiSchemaManager(version="0.9", accepts_inline_catalogs=True)
```

### 2. Extension in Agent Card

```python
# __main__.py
from a2ui.a2a.extension import get_a2ui_agent_extension

agent_card = AgentCard(
    capabilities=AgentCapabilities(
        extensions=[get_a2ui_agent_extension()],
        streaming=True,
    ),
)
```

### 3. Prompt Building with Schema Block

```python
# prompts/shared.py
from a2ui.schema.constants import A2UI_OPEN_TAG, A2UI_CLOSE_TAG, DEFAULT_WORKFLOW_RULES

def a2ui_schema_block(schema_manager, allowed_components=None):
    catalog = schema_manager.get_selected_catalog(
        allowed_components=allowed_components
    )
    schema_text = catalog.render_as_llm_instructions()
    examples = schema_manager.load_examples(catalog)
    return f"{schema_text}\n\n{examples}"
```

### 4. Response → DataParts

```python
# a2ui_protocol.py
from a2ui.a2a.parts import create_a2ui_part

def messages_to_parts(messages, catalog_id=None):
    return [create_a2ui_part(_flatten_message(m, catalog_id)) for m in messages]
```

---
> Source: [gskinnerTeam/flutter-hatcha-app](https://github.com/gskinnerTeam/flutter-hatcha-app) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-24 -->
