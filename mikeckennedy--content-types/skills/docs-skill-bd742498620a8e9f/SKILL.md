---
name: content-types
description: > Use when this capability is needed.
metadata:
  author: mikeckennedy
---

# content-types

A library to map file extensions to content types and vice versa.

## Installation

```bash
pip install content-types
```

## API overview

### Forward lookup

Map a filename, bare extension, Path, or URL to its MIME / content type.

- `get_content_type`: Return the most specific, commonly accepted MIME type for a filename or extension

### Reverse lookup

Map a MIME / content type back to its file extension(s) — the inverse of get_content_type.

- `guess_extension`: Return the canonical file extension for a MIME / content type
- `guess_all_extensions`: Return every known file extension for a MIME / content type, canonical first

### Mapping data

The underlying extension -> content-type table (364 entries; keys have no leading dot).

- `EXTENSION_TO_CONTENT_TYPE`: dict() -> new empty dictionary

### Shortcut constants

Precomputed content types for very common formats, exposed as module-level attributes.

- `webp`: str(object='') -> str
- `png`: str(object='') -> str
- `jpg`: str(object='') -> str
- `mp3`: str(object='') -> str
- `json`: str(object='') -> str
- `pdf`: str(object='') -> str
- `zip`: str(object='') -> str
- `xml`: str(object='') -> str
- `csv`: str(object='') -> str
- `md`: str(object='') -> str
- `parquet`: str(object='') -> str
- `ipynb`: str(object='') -> str
- `pkl`: str(object='') -> str
- `yaml`: str(object='') -> str
- `toml`: str(object='') -> str
- `sqlite`: str(object='') -> str

## Resources

- [Full documentation](https://mkennedy.codes/docs/content-types/)
- [llms.txt](llms.txt) — Indexed API reference for LLMs
- [llms-full.txt](llms-full.txt) — Comprehensive documentation for LLMs
- [Source code](https://github.com/mikeckennedy/content-types)

---
> Source: [mikeckennedy/content-types](https://github.com/mikeckennedy/content-types) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-20 -->
