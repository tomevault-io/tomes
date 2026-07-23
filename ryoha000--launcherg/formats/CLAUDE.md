# launcherg

> Launchergは、Tauriベースのデスクトップアプリケーションで、ゲームの管理と起動を行うランチャーです。

## Usage

Add this to your project's CLAUDE.md to activate this skill:

```
Read and follow the instructions in .claude/skills/launcherg/SKILL.md
```

Or copy the instructions below directly into your CLAUDE.md:

## プロジェクト概要

Launchergは、Tauriベースのデスクトップアプリケーションで、ゲームの管理と起動を行うランチャーです。

## 通信プロトコル

- 拡張機能 <-> native-messaging-host の通信する内容は ProtoBuf で定義されたものを使い、tauri 内の frontend(TypeScript) <-> backend(Rust) はJSONでやり取りする。

## CLIで実行するコマンド

CLIで完結するコマンドのみを実行すること
アプリケーションの起動（`npm run dev`、`npm run tauri dev`など）は実行しないこと

### データベース
- SQLiteを使用、マイグレーションは`src-tauri/migrations/`に配置

---
> Source: [ryoha000/launcherg](https://github.com/ryoha000/launcherg) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:claude_md:2026-07-23 -->
