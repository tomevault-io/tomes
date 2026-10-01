---
name: connector-trouble
description: > Use when this capability is needed.
metadata:
  author: Wayn-Git
---

# When a connector is not answering

Connector tools come from separate processes that sign in on the user's behalf.
When one is not signed in, its tools are **not in your tool list at all** — they
do not appear and fail, they are simply absent.

## Say what is actually wrong

If the user asks for something that needs a connector you have no tools for,
say which connector is not connected and that they can sign in from **Skills &
connectors**. Do not:

- claim you did the thing anyway;
- substitute a different tool that writes to the wrong place — filing a GitHub
  issue by writing a file is not filing an issue;
- ask the user to paste credentials into the conversation. Nothing here ever
  needs that, and a key in a transcript is a key you cannot take back.

## The errors and what they mean

- **"was not authorized within Ns"** — a sign-in was started and nobody
  finished it in the browser. The user has to complete it; nothing you can do
  from here changes it.
- **"did not respond within Ns"** — the connector process is up but wedged.
  Worth one retry, then say so.
- A tool that returns an auth error mid-turn — the session expired. Stop and
  say which connector needs signing in again rather than retrying it in a loop.

## Do not paper over it

A turn that quietly produces a worse result because a connector was missing is
the failure the user will not catch. Two sentences naming the connector and the
page to fix it are worth more than a plausible answer built from the wrong
source.

---
> Source: [Wayn-Git/Amethyst](https://github.com/Wayn-Git/Amethyst) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-13 -->
