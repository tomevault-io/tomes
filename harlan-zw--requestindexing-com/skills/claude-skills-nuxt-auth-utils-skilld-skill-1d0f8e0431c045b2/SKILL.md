---
name: nuxt-auth-utils-skilld
description: ALWAYS use when writing code importing \"nuxt-auth-utils\". Consult for debugging, best practices, or modifying nuxt-auth-utils, nuxt auth utils. Use when this capability is needed.
metadata:
  author: harlan-zw
---

# atinux/nuxt-auth-utils `nuxt-auth-utils`

**Version:** 0.5.28 (Feb 2026)
**Deps:** @adonisjs/hash@^9.1.1, @nuxt/kit@^4.3.1, defu@^6.1.4, h3@^1.15.4, hookable@^6.0.1, jose@^6.1.3, ofetch@^1.5.1, openid-client@^6.8.2, pathe@^2.0.3, scule@^1.3.0, uncrypto@^0.1.3
**Tags:** latest: 0.5.29 (Feb 2026)

**References:** [package.json](./.skilld/pkg/package.json) — exports, entry points • [README](./.skilld/pkg/README.md) — setup, basic usage • [GitHub Issues](./.skilld/issues/_INDEX.md) — bugs, workarounds, edge cases • [Releases](./.skilld/releases/_INDEX.md) — changelog, breaking changes, new APIs

## Search

Use `skilld search` instead of grepping `.skilld/` directories — hybrid semantic + keyword search across all indexed docs, issues, and releases. If `skilld` is unavailable, use `npx -y skilld search`.

```bash
skilld search "query" -p nuxt-auth-utils
skilld search "issues:error handling" -p nuxt-auth-utils
skilld search "releases:deprecated" -p nuxt-auth-utils
```

Filters: `docs:`, `issues:`, `releases:` prefix narrows by source type.

## API Changes

This section documents version-specific API changes — prioritize recent major/minor releases.

- BREAKING: `oicd` renamed to `oidc` in OAuthProvider type — v0.5.28 corrected typo in provider type name [source](./.skilld/releases/v0.5.28.md#fixes)

- BREAKING: OIDC provider requires `PKCE` and `nonce` — v0.5.28 made these mandatory per OAuth specs (previously optional) [source](./.skilld/releases/v0.5.28.md#fixes)

- NEW: `aaguid` exposed on WebAuthn credentials — v0.5.27 added `aaguid` property to credentials in `onSuccess` callback, use to identify authenticator type with community AAGUIDS list [source](./.skilld/releases/v0.5.27.md#enhancements)

- NEW: OpenID Connect (OIDC) provider — v0.5.27 added generic OIDC provider via `defineOAuthOidcEventHandler`, supports `.well-known/openid-configuration` auto-discovery [source](./.skilld/releases/v0.5.27.md#enhancements)

- NEW: `loadStrategy: 'none'` option — v0.5.26 added ability to completely disable session fetching during SSR (added alongside existing `'client-only'` option from v0.5.24) [source](./.skilld/releases/v0.5.26.md#enhancements)

- NEW: `passwordNeedsRehash()` utility — v0.5.26 added server utility to check if password hash needs rehashing when scrypt settings change, call during login flow to trigger re-hash [source](./.skilld/releases/v0.5.26.md#enhancements)

- NEW: `loadStrategy: 'client-only'` option — v0.5.24 added option to fetch session only client-side (not during SSR), useful with prerendered/cached routes [source](./.skilld/releases/v0.5.24.md#enhancements)

- NEW: `openInPopup(route, { width?, height? })` method on useUserSession — v0.5.11 added popup window OAuth flow with auto-close on success, pass optional size object to control window dimensions [source](./.skilld/releases/v0.5.11.md#enhancements)

- NEW: WebSocket authentication support — v0.5.9 added `requireUserSession()` function for use in WebSocket `upgrade` handler to authenticate before connection, requires Nitro >= 2.9.7 [source](./.skilld/releases/v0.5.9.md#enhancements)

- NEW: Session ID auto-generation — v0.5.12 added generated `id` field on session object for session tracking [source](./.skilld/releases/v0.5.12.md#enhancements)

- BREAKING: WebAuthn dependency update — v0.5.0 updated simplewebauthn to v11, breaking changes in API (see simplewebauthn v11 migration) [source](./.skilld/releases/v0.5.0.md#breaking-changes)

- BREAKING: `useWebAuthn` composable allowCredentials fix — v0.5.1 changed how `allowCredentials` and `excludeCredentials` are processed in `useWebAuthn`, previously had bugs with options handling [source](./.skilld/releases/v0.5.1.md#fixes)

- NEW: WebAuthn (passkey) support — v0.4.0 added `defineWebAuthnRegisterEventHandler`, `defineWebAuthnAuthenticateEventHandler`, `useWebAuthn()` composable, `storeChallenge`/`getChallenge` hooks for challenge management [source](./.skilld/releases/CHANGELOG.md#webauthn-passkey-support)

- NEW: `hashPassword()` and `verifyPassword()` utilities — v0.4.0 added server-side password hashing with scrypt, use in login/register flows for secure password storage [source](./.skilld/releases/CHANGELOG.md#add-hashpassword--verifypassword-server-utils)

- BREAKING: OAuth handler renaming — v0.4.0 renamed `oauth<Provider>EventHandler` to `defineOAuth<Provider>EventHandler` (e.g., `defineOAuthGitHubEventHandler`) [source](./.skilld/releases/CHANGELOG.md#rename-oauthprovider-eventhandler-to-defineoauthprovider-eventhandler)

**Also changed:** OIDC X provider PKCE flow fixed · Shopify Customer Account API provider · Bluesky (AT Protocol) provider · generated session ID available on session · multiple OAuth providers (Okta, Ory, Kick, Gitea, etc.)

## nuxt-auth-utils Best Practices

## Best Practices

- Refresh the Vue composable after server-side session updates — when calling `setUserSession()` from server routes or hooks, use `useUserSession().fetch()` on client to ensure the session state stays synchronized [source](./.skilld/pkg/README.md:L595:604)

- Use `loadStrategy` to control session loading behavior — choose 'client-only' for hybrid-rendered apps, 'none' to disable auto-loading, or 'server-first' (default) for traditional SSR [source](./.skilld/releases/v0.5.24.md#enhancements)

- Extend `UserSession` type via module augmentation in a declaration file — create `auth.d.ts` and augment the `#auth-utils` module to get full type safety for custom session fields [source](./.skilld/pkg/README.md:L159:176)

- Access WebAuthn credential AAGUID in `onSuccess` to decorate passkeys — use `credential.aaguid` to look up authenticator metadata from the passkey-authenticator-aaguids list [source](./.skilld/pkg/README.md:L453:455)

- Implement challenge-based WebAuthn flow with `storeChallenge` and `getChallenge` — prevents replay attacks by storing single-use challenges in KV store and removing after validation [source](./.skilld/pkg/README.md:L502:526)

- Store sensitive data (tokens, API keys) in the `secure` field, not `user` — the secure field is server-only and never sent to the client, while user data is encrypted but queryable [source](./.skilld/pkg/README.md:L128:142)

- OIDC authentication requires both PKCE and nonce parameters — these are mandatory per OAuth spec and cannot be disabled; the provider's discovery endpoint must support them [source](./.skilld/releases/v0.5.28.md)

- Session data is limited to ~4KB due to cookie size constraints — store only essential identifiers and tokens; use database lookups in the 'fetch' hook to augment session with full user data [source](./.skilld/pkg/README.md:L178:180)

- Implement password hash rotation during login — call `passwordNeedsRehash()` to detect outdated hashes and re-hash with new cost parameters without breaking existing sessions [source](./.skilld/pkg/README.md:L304:313)

- Use `sessionHooks` for runtime session augmentation — hook into 'fetch' to enrich session data from your database, and 'clear' to log logout events [source](./.skilld/pkg/README.md:L576:589)

---
> Source: [harlan-zw/requestindexing.com](https://github.com/harlan-zw/requestindexing.com) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-28 -->
