---
name: publish
description: | Use when this capability is needed.
metadata:
  author: crystian
---

# publish

La única skill que corres cuando el sitio está listo para salir.

## Pasos
1. Corre la skill [check-links](../check-links/SKILL.md) sobre las páginas en public/. Si reporta enlaces rotos, frena y arréglalos primero.
2. Si una página necesita un arreglo de contenido, pasale el cambio a [content-editor](../content-editor/SKILL.md).
3. Sigue el [runbook de despliegue](../../../docs/DEPLOY.md): regenera las páginas, corre el chequeo de enlaces, inicia el servidor.

---
> Source: [crystian/skill-map](https://github.com/crystian/skill-map) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-17 -->
