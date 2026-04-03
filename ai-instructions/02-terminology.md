# 01 — Project Overview

## Goal

Translate KDE `.po` files from **English (en)** to **Belarusian (be)** with high linguistic quality, full technical correctness, and strict consistency across all files.

---

## Language Pair

| Field | Value |
|-------|-------|
| Source language | English (`en`) |
| Target language | Belarusian (`be`) |
| PO `Language:` header value | `be` |
| Plural-Forms header | See [04-formatting.md](04-formatting.md) |

---

## Directory Structure

```
project-root/
├── AGENTS.md
├── ai-instructions/
│   ├── 01-overview.md        ← this file
│   ├── 02-terminology.md
│   ├── 03-process.md
│   ├── 04-formatting.md
│   ├── 05-ai-guidelines.md
│   └── 06-forbidden-practices.md
├── sources/
│   └── linguistic/
│       ├── glossaries/       ← TBX glossary files
│       └── tm's/             ← TMX translation memory files
└── work_dir/                 ← output directory for all translated files
```

### `sources/linguistic/glossaries/`

Contains **TBX** (TermBase eXchange) files with approved terminology. These have the highest priority. Every term found in a glossary **must** be translated exactly as specified.

### `sources/linguistic/tm's/`

Contains **TMX** (Translation Memory eXchange) files with previously approved translation segments. Use these for consistent phrasing when an exact or fuzzy match is found.

### `work_dir/`

**All output files must be saved here.** Filenames must match the source filenames exactly. Never write output anywhere else.

---

## Scope of Work

For each input `.po` file, the agent must:

1. Translate all entries where `msgstr` is empty.
2. Review and fix all entries marked `#, fuzzy` — update the translation to match the current `msgid`, then remove the fuzzy marker and all `#|` reference lines.
3. Preserve all already-translated entries that are neither empty nor fuzzy.
4. Preserve all file metadata (header block) unchanged, except `PO-Revision-Date` and `Last-Translator` if instructed to update them.
5. Preserve all obsolete entries (`#~`) unchanged.

---

## KDE Context

These translations are part of the KDE desktop environment localization. Strings appear in:
- Dialog windows, buttons, labels, tooltips
- Menu items and actions
- Status messages and notifications
- Settings panels

Translations must be natural, concise, and consistent with KDE Belarusian localization conventions. Always prefer established KDE terminology over literal translation.