---
name: tilemap-review
description: | Use when this capability is needed.
metadata:
  author: valkor-ai
---

# TileMap Review

Post-implementation reviewer for Godot TileMap code. Checks against known gotchas that LLMs consistently get wrong.

## When to trigger

After TileMap-related code is written or modified. Look for:
- TileMapLayer, TileSet, TileSetAtlasSource, TileSetScenesCollectionSource nodes
- Cell operations (`set_cell`, `erase_cell`, `set_cells_terrain_connect`)
- TileData access (`get_cell_tile_data`)
- Collision/navigation polygon configuration on tiles
- `y_sort_enabled` on TileMapLayer
- NavigationRegion2D with TileMapLayer children

## Review process

1. Read `gotchas.md`
2. Scan the implemented code against each gotcha
3. For each hit:
   - Cite the gotcha ID (e.g. G1)
   - Show the offending code
   - Provide the fix
4. If no hits, report clean
5. Optionally run `checklist.md` static checks for automated verification

When you need specific API details, delegate to the **godot-api** skill.

---
> Source: [valkor-ai/loom](https://github.com/valkor-ai/loom) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-19 -->
