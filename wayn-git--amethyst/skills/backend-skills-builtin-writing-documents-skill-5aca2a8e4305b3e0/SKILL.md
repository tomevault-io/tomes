---
name: writing-documents
description: > Use when this capability is needed.
metadata:
  author: Wayn-Git
---

# Writing a document

`create_artifact` writes a file **and** opens it in the panel beside the
conversation, streaming as you write. `write_file` writes a file and says
nothing. The difference is not where the bytes go — it is whether the user
watches the thing being made.

## Use `create_artifact` when the deliverable *is* the document

A report, a plan, a letter, meeting notes, a README, a script the user asked
for: call `create_artifact` once with the whole content. Do not paste the same
document into the reply as well. It is already on their screen, and a reply
that repeats it makes them read it twice to check the two copies match.

What to say instead: one or two lines about what you wrote and anything they
need to decide. That is the whole reply.

## Use `write_file` when the file is a step, not the point

Configuration you are editing, a fixture, a file another tool will read next.
Nobody wants a panel for it.

## One call, whole content

The panel opens on the first fragment of the call and fills as the arguments
arrive, so a document written in one `create_artifact` appears as it is
written. Writing it in pieces across several calls does not stream — it
replaces the document repeatedly, and the user watches it flicker.

## Give it a real title

The `title` is what labels the panel and the file list afterwards. "Report" is
not a title; "Q3 hiring plan" is.

---
> Source: [Wayn-Git/Amethyst](https://github.com/Wayn-Git/Amethyst) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-13 -->
