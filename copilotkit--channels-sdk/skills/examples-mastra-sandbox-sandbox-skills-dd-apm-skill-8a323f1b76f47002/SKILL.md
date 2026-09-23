---
name: dd-apm
description: Query Datadog APM services, dependencies, performance, and traces with Pup. Use when this capability is needed.
metadata:
  author: CopilotKit
---

# Datadog APM

Use the Datadog Labs Pup CLI for APM and trace investigations.

## Setup

```sh
brew tap datadog-labs/pack
brew install pup
pup auth login
```

## Services

Always pass `--env` to APM service commands.

```sh
pup apm services list --env prod
pup apm services stats --env prod --from 4h
pup apm services operations --env prod --service app-api
pup apm services resources --env prod --service app-api --name <operation>
pup apm dependencies list --env prod
pup apm flow-map --query "service:app-api" --env prod
```

List operations before querying resources and use an exact returned operation
name. Do not assume `http.request`.

## Traces

Trace commands are top-level. Durations are nanoseconds, so one second is
`1000000000`.

```sh
pup traces search --query="service:app-api" --from="1h"
pup traces search --query="service:app-api status:error" --from="1h"
pup traces search --query="service:app-api @duration:>1000000000" --from="1h"
pup traces aggregate \
  --query="service:app-api" \
  --compute="avg(@duration)" \
  --group-by="resource_name" \
  --from="1h"
```

Trace sampling means search results may not include every request. Avoid
high-cardinality tags such as user IDs and request IDs.

---
> Source: [CopilotKit/channels-sdk](https://github.com/CopilotKit/channels-sdk) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-16 -->
