---
name: example-runner
description: Run and test spotify_sdk integration using the companion example app. Use when this capability is needed.
metadata:
  author: brim-borium
---

# Example App Runner (`example-runner`)

Run and test the plugin using the companion application in [example/](file:///Users/tobi/Projects/spotify_sdk/example).

## Setup

Create `.env` file at [example/.env](file:///Users/tobi/Projects/spotify_sdk/example/.env):
```ini
CLIENT_ID=your_spotify_client_id
REDIRECT_URL=your_spotify_redirect_url
```

## Running the App

### Mobile
```bash
cd example && flutter run
```

### Web
Run on Chrome with loopback IP for Spotify Web SDK compatibility:
```bash
cd example && flutter run -d chrome --web-hostname=127.0.0.1 --web-port=8080
```

---
> Source: [brim-borium/spotify_sdk](https://github.com/brim-borium/spotify_sdk) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-08-23 -->
