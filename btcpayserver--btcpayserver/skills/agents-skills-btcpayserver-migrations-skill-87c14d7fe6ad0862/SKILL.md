---
name: btcpayserver-migrations
description: Use when creating or reviewing Entity Framework migrations in BTCPayServer. Contains repository-specific migration generation and cleanup rules.
metadata:
  author: btcpayserver
---

# BTCPayServer Migrations

## Creating Migrations

- Run `dotnet ef migrations add <migration-name>` to generate the migration.
- Copy the class attributes from the generated `.Designer.cs` file to the `.cs` migration file.
- Remove the generated `.Designer.cs` file.
- Remove the `Down()` method.
- Do not use `migrationBuilder.IsNpgsql()`; assume PostgreSQL is used.
- If a migration cannot be generated through `dotnet ef migrations`, add a migration file prefixed by date in the `Migrations` folder, for example `20260525115757_passkey.cs`, and use `migrationBuilder.Sql` to run raw SQL.
- Follow postgres naming conventions.

---
> Source: [btcpayserver/btcpayserver](https://github.com/btcpayserver/btcpayserver) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-25 -->
