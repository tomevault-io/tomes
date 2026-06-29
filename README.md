# TomeVault Tomes

Complete Tomes, distributed by [TomeVault](https://tomevault.io).

A Tome is the kit, not a component. It bundles a project config file (`CLAUDE.md`, `AGENTS.md`, and the rest) with the related skill files from the same project, plus a `tome.json` manifest, into one unit you install at once. The config tells an agent how a project works. The skills give it specific capabilities. Together they are more useful than either alone.

Each directory in this repository is one Tome, named `owner--repo`.

## Install

```bash
npx tomevault add <tome-name>
```

The CLI places the config and skills in the right locations for your agent, in the right format. See [tomevault.io/install](https://tomevault.io/install).

## Browse

Search, filter, and read the verdict for any Tome at [tomevault.io](https://tomevault.io).

---

One source of truth for your AI instructions. [tomevault.io](https://tomevault.io)
