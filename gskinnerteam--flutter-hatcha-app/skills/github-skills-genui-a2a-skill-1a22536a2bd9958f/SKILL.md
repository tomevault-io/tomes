---
name: genui-a2a
description: Integration package connecting genui to A2A servers via the A2UI Streaming UI Protocol. Use when: working with A2uiAgentConnector, A2AClient, Transport, SseTransport, A2A protocol events, agent cards, task/context IDs, sending UI events to server, streaming A2UI messages over SSE, or configuring the A2A connection layer. Use when this capability is needed.
metadata:
  author: gskinnerTeam
---

# genui_a2a Package — API Reference

The `genui_a2a` package (v0.9.0, renamed from `genui_a2ui` at v0.8.0) connects the `genui` framework to A2A (Agent-to-Agent) servers via the [A2UI Streaming UI Protocol](https://a2ui.org). It provides `A2uiAgentConnector` — a `Transport` implementation that communicates over SSE with an A2A server, receives A2UI messages, and feeds them into `genui`'s rendering pipeline.

## When to Use

- Connecting a Flutter app to an A2A server endpoint
- Configuring `A2uiAgentConnector` as the transport for `Conversation`
- Handling A2A streaming events (status updates, artifacts)
- Managing `taskId` / `contextId` for stateful conversations
- Sending user interaction events back to the server
- Fetching agent cards for capability discovery
- Working with SSE or HTTP transports

---

## Architecture — Data Flow

```
User Input
 │
 ▼
Conversation
 │  submit(ChatMessage)
 ▼
A2uiTransportAdapter (wraps A2uiAgentConnector as Transport)
 │  delegates to connector
 ▼
A2uiAgentConnector
 │  converts ChatMessage → A2A Message
 │  manages taskId / contextId
 ▼
A2AClient
 │  JSON-RPC 2.0 over Transport (SSE or HTTP)
 ▼
A2A Server
 │
 │  streams back A2AStreamEvents
 ▼
A2uiAgentConnector
 │  extracts A2UI messages from DataParts
 │  emits Stream<A2uiMessage>
 ▼
SurfaceController
 │  handles A2uiMessage → SurfaceUpdate
 ▼
Surface renders dynamic UI
```

---

## A2uiAgentConnector

Manages the A2A protocol: SSE connection, message conversion, A2UI message extraction, and event sending.

### Constructor

```dart
A2uiAgentConnector({
  Uri? url,                 // Server URL — provide exactly one of url or client
  A2AClient? client,        // Pre-configured client — provide exactly one
  String? contextId,
})
```

> **v0.9 change**: Must provide exactly one of `url` or `client`. Providing both or neither throws.

### Key Members

| Member        | Type                  | Purpose                                           |
| ------------- | --------------------- | ------------------------------------------------- |
| `client`      | `A2AClient`           | Underlying A2A client                             |
| `stream`      | `Stream<A2uiMessage>` | Parsed A2UI messages extracted from A2A DataParts |
| `errorStream` | `Stream<Object>`      | Errors from A2A connection                        |
| `taskId`      | `String?`             | Current task ID (set by server responses)         |
| `contextId`   | `String?`             | Current context ID (set by server responses)      |

### Key Methods

| Method           | Signature                                                                                                   | Purpose                                       |
| ---------------- | ----------------------------------------------------------------------------------------------------------- | --------------------------------------------- |
| `connectAndSend` | `Future<String?> connectAndSend(ChatMessage, {clientCapabilities?, clientDataModel?, cancellationSignal?})` | Convert message → A2A, stream, extract A2UI   |
| `sendEvent`      | `Future<void> sendEvent(Map<String, Object?> event)`                                                        | Send user interaction event (requires taskId) |
| `getAgentCard`   | `Future<AgentCard> getAgentCard()`                                                                          | Fetch agent metadata                          |
| `dispose`        | `void dispose()`                                                                                            | Close streams                                 |

### connectAndSend Parameters (v0.9)

| Parameter            | Type                      | Purpose                                   |
| -------------------- | ------------------------- | ----------------------------------------- |
| `clientCapabilities` | `A2UiClientCapabilities?` | Widget catalog capabilities for the agent |
| `clientDataModel`    | `Map<String, Object?>?`   | Current client data model state           |
| `cancellationSignal` | `CancellationSignal?`     | Signal to cancel in-flight request        |

### Message Conversion Flow (connectAndSend)

1. Extracts `parts` from `ChatMessage` (text → `TextPart`, image → `FilePart`, data → `DataPart`)
2. Attaches `referenceTaskIds` and `contextId` if available
3. Attaches `clientCapabilities` and `clientDataModel` in message metadata
4. Streams `Event`s from server; for each `StatusUpdate`/`TaskStatusUpdate`:
   - Updates `taskId` and `contextId`
   - Extracts `DataPart`s containing A2UI JSON
   - Parses via `A2uiMessage.fromJson()` and emits on `stream`
5. Returns final text response (if any `TextPart` in last message)

### Event Sending (sendEvent)

Wraps interaction data in a `DataPart` with key `a2uiEvent`:

```json
{
  "actionName": "submit",
  "sourceComponentId": "btn_1",
  "timestamp": "2026-04-14T...",
  "resolvedContext": { ... }
}
```

---

## A2uiTransportAdapter

Wraps `A2uiAgentConnector` as a `Transport` (the genui interface). Used to connect the connector to `Conversation`.

```dart
A2uiTransportAdapter({
  required A2uiAgentConnector connector,
})
```

This class implements `Transport` from genui and delegates to the connector's `connectAndSend`.

---

## A2AClient

JSON-RPC 2.0 client for the A2A protocol. Re-exported from the `a2a_sdk` package.

### Constructor

```dart
A2AClient({
  required String url,
  Transport? transport,  // Defaults to SseTransport
  Logger? log,
})
```

### Static Factory

```dart
static Future<A2AClient> fromAgentCardUrl(String agentCardUrl, {Logger? log})
```

Fetches the agent card, selects the best transport (SSE if streaming supported), returns configured client.

### Key Methods

| Method                   | Signature           | Purpose                                |
| ------------------------ | ------------------- | -------------------------------------- |
| `getAgentCard()`         | `Future<AgentCard>` | Fetch agent card                       |
| `messageStream(message)` | `Stream<Event>`     | Send message, receive streaming events |
| `messageSend(message)`   | `Future<Task>`      | Send message, receive single response  |

---

## Transport (Interface)

Communication between `A2AClient` and an A2A server.

```dart
abstract class Transport {
  Map<String, String> get authHeaders;
  Future<Map<String, Object?>> get(String path, {Map<String, String> headers});
  Future<Map<String, Object?>> send(Map<String, Object?> request, {String path, Map<String, String> headers});
  Stream<Map<String, Object?>> sendStream(Map<String, Object?> request, {Map<String, String> headers});
  void close();
}
```

### Implementations

| Transport       | Purpose                                                                            |
| --------------- | ---------------------------------------------------------------------------------- |
| `SseTransport`  | SSE-based streaming (default). Accepts `authHeaders` including `X-A2A-Extensions`. |
| `HttpTransport` | Simple HTTP request/response. Used as fallback when streaming not supported.       |

---

## A2A Protocol Models (Freezed)

### Event (Sealed)

```dart
sealed class Event {
  factory Event.statusUpdate({taskId, contextId, status, final_})
  factory Event.taskStatusUpdate({taskId, contextId, status, final_})
  factory Event.artifactUpdate({taskId, contextId, artifact, append, lastChunk})
}
```

### Message

```dart
Message({
  required Role role,
  required List<Part> parts,
  Map<String, Object?>? metadata,
  List<String>? extensions,
  List<String>? referenceTaskIds,
  required String messageId,
  String? taskId,
  String? contextId,
})
```

### Part Types

| Type       | Factory            | Key Fields                                |
| ---------- | ------------------ | ----------------------------------------- |
| `TextPart` | `Part.text(text:)` | `text`                                    |
| `DataPart` | `Part.data(data:)` | `data: Map<String, Object?>`              |
| `FilePart` | `Part.file(file:)` | `file: FileType` (`.uri()` or `.bytes()`) |

### TaskState

```dart
enum TaskState {
  submitted, working, inputRequired, completed, canceled, failed, rejected, authRequired, unknown
}
```

### AgentCard

Agent metadata fetched from `/.well-known/agent-card.json`. Contains name, description, URL, capabilities (streaming, push notifications), supported extensions, security schemes.

---

## Error Handling

### A2AException (Freezed)

| Factory                          | Code   | Purpose                          |
| -------------------------------- | ------ | -------------------------------- |
| `taskNotFound`                   | -32001 | Task ID not found on server      |
| `taskNotCancelable`              | -32002 | Task cannot be canceled          |
| `pushNotificationNotSupported`   | -32006 | Push notifications not available |
| `pushNotificationConfigNotFound` | -32007 | Push notification config missing |
| `jsonRpc`                        | Custom | Generic JSON-RPC error           |
| `http`                           | —      | HTTP transport failure (non-2xx) |
| `network`                        | —      | Connection / network error       |
| `parsing`                        | —      | Malformed server response        |
| `unsupportedOperation`           | —      | Operation not supported          |

---

## Usage Pattern

```dart
// 1. Create the connector
final connector = A2uiAgentConnector(url: Uri.parse('http://localhost:8080'));

// 2. Create a SurfaceController
final controller = SurfaceController(catalogs: [BasicCatalog.asCatalog()]);

// 3. Wire connector stream to controller
connector.stream.listen(controller.handleMessage);

// 4. Create Conversation with transport adapter
final conversation = Conversation(
  transport: A2uiTransportAdapter(connector: connector),
  surfaceController: controller,
);

// 5. Render surfaces
Surface(host: controller, surfaceId: 'main');
```

---

## Migration from genui_a2ui (v0.7)

| Old (v0.7)                                   | New (v0.9)                                        |
| -------------------------------------------- | ------------------------------------------------- |
| `import 'package:genui_a2ui/...'`            | `import 'package:genui_a2a/...'`                  |
| `A2uiContentGenerator`                       | Use `A2uiAgentConnector` + `A2uiTransportAdapter` |
| `A2uiAgentConnector(url: ..., client: ...)`  | Provide exactly ONE of `url` or `client`          |
| `connectAndSend(msg, {clientCapabilities?})` | + `clientDataModel`, `cancellationSignal`         |
| `GenUiConversation`                          | `Conversation`                                    |
| `A2uiMessageProcessor`                       | `SurfaceController`                               |

---
> Source: [gskinnerTeam/flutter-hatcha-app](https://github.com/gskinnerTeam/flutter-hatcha-app) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-24 -->
