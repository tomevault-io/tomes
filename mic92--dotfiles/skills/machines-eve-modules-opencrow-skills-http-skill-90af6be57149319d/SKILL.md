---
name: http
description: Make HTTP requests using hurl. Use for accessing websites/apis Use when this capability is needed.
metadata:
  author: Mic92
---

# hurl

```bash
# GET HTML
hurl <<'EOF'
GET https://example.org
HTTP 200
[Asserts]
xpath "normalize-space(//head/title)" == "Hello world!"
EOF

# Chain requests with captures
hurl <<'EOF'
POST https://api.example.com/login
Content-Type: application/json
{"user": "me", "pass": "secret"}
HTTP 200
[Captures]
token: jsonpath "$.token"

GET https://api.example.com/resource
Authorization: Bearer {{token}}
HTTP 200
EOF
```

Flags: `--variable key=val`, `--test` (assert mode).

---
> Source: [Mic92/dotfiles](https://github.com/Mic92/dotfiles) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-19 -->
