---
name: add-entity
description: >- Use when this capability is needed.
metadata:
  author: MAIF
---

# Add a domain entity / cross-layer feature in Daikoku

Adding a persisted concept in Daikoku touches many layers, in a consistent order. Skipping one
(e.g. forgetting to register the Postgres table or the JSON format) fails at runtime, not compile
time — so work through the whole checklist.

Read [`docs/DOMAIN.md`](../../../docs/DOMAIN.md) first to place the concept in the model. In the
steps below, `X` is the entity name and `XId` its id type.

## Backend checklist (`daikoku/app/fr/maif/daikoku`)

1. **Id type** — `domain/entities.scala`
   Add `case class XId(value: String) extends ValueType with CanJson[XId]`.

2. **Entity** — the relevant `*Entities.scala` (`apiEntities.scala`, `teamEntities.scala`,
   `tenantEntities.scala`, `userEntities.scala`, or `entities.scala`)
   Add `case class X(id: XId, tenant: TenantId, ...) extends CanJson[X]` with its `asJson`.

3. **JSON codecs** — `domain/json.scala`
   Add `XIdFormat` and `XFormat` (`new Format[X] { ... }`). Every field must be (de)serialized.

4. **Storage trait + accessor** — `storage/api.scala`
   Add `trait XRepo extends TenantCapableRepo[X, XId]` (or `Repo[X, XId]` if not tenant-scoped) and
   `def xRepo: XRepo` on the `DataStore` trait.

5. **Postgres implementation** — `storage/drivers/postgres/PostgresDataStore.scala`:
   - `case class PostgresTenantCapableXRepo(...) extends PostgresTenantCapableRepo[X, XId] with XRepo`
   - register the table in the tables map: `"xs" -> true`
   - instantiate `_xRepo` and `override def xRepo: XRepo = _xRepo`
   - add the relevant `CREATE INDEX IF NOT EXISTS ...` statements
   - add the repo to the export `collections` list and the import `case ("xs", payload) => ...`

6. **GraphQL** (only if exposed via GraphQL) — `domain/SchemaDefinition.scala`
   Add the `ObjectType` and the `HasId[X, XId]` wiring.

7. **Controller + routes**
   Add/extend a controller in `controllers/` and declare endpoints in `conf/routes`
   (`fr.maif.daikoku.controllers.XController.method(...)`). Errors go through `AppError`.

8. **Business logic** — `services/` if there is non-trivial logic beyond CRUD.

## Frontend checklist (`daikoku/javascript/src`)

9. **Types** — `types/*.ts` (`api.ts`, `team.ts`, `tenant.ts`, or `types.ts`); export the `IX`
   interface from `types/index.ts`.

10. **API client** — `services/index.ts`
    Add functions using `customFetch`, e.g.
    `export const getX = (id: string): PromiseWithError<IX> => customFetch(\`/api/xs/${id}\`);`

11. **UI / forms** — components under `components/{adminbackoffice,backoffice,frontend,inputs}`.
    Forms use `@maif/react-forms`. Data fetching uses TanStack Query.

## i18n (do not skip)

12. **Backend messages** — add keys to **both** `conf/messages.en` and `conf/messages.fr`.
13. **Frontend translations** — add keys to **both** `javascript/src/locales/en/translation.json`
    and `javascript/src/locales/fr/translation.json`.

## Verify

- Backend compiles: `sbt "Test/compile"` from `daikoku/` (or `sbt compile`).
- Frontend typechecks: `npm run build` in `daikoku/javascript` (runs `tsc`), and `npm run lint`.
- Run tests for the touched area: `mise run test:back` (backend) / `mise run test:front:ldap`
  (frontend Playwright).
- Format before committing: scalafmt (backend), `npm run prettier` (frontend).

## Conventions reminder

English only, everywhere. Conventional-Commits style messages. See [`CLAUDE.md`](../../../CLAUDE.md).

---

_A recent entity that touched all of these layers is `Keyring` — handy as a worked example, but note
it is atypical (Otoroshi binding, aggregation), not a plain CRUD entity._
</content>

---
> Source: [MAIF/daikoku](https://github.com/MAIF/daikoku) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-26 -->
