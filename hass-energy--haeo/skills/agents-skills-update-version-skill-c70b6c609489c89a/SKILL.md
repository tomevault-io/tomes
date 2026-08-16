---
name: update-version
description: Bump the HAEO version consistently across pyproject.toml, manifest.json, and uv.lock. Use when asked to set, bump, or release a version, or when the version consistency gate fails. Use when this capability is needed.
metadata:
  author: hass-energy
---

# Update Version

Update the project version number to `$VERSION`.

If `$VERSION` starts with `v`, use the version without the leading `v` in project files.

1. Update `pyproject.toml`:

    ```toml
    version = "$VERSION"
    ```

2. Update `custom_components/haeo/manifest.json`:

    ```json
    {
      "version": "$VERSION"
    }
    ```

3. Run `uv lock` to regenerate the lockfile with the new version.

---
> Source: [hass-energy/haeo](https://github.com/hass-energy/haeo) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-08-16 -->
