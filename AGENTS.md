# AGENTS.md — Agent Instructions

> **All AI agents MUST read every file listed below in order before performing any translation work.**
> Do not skip sections. Do not begin translating before completing all required reading.

---

## Required Reading Order

| Step | File | Purpose |
|------|------|---------|
| 1 | [01-overview.md](ai-instructions/01-overview.md) | Project context, goals, directory structure |
| 2 | [02-terminology.md](ai-instructions/02-terminology.md) | Glossary and TM lookup rules; TMX/TBX parsing |
| 3 | [03-process.md](ai-instructions/03-process.md) | Step-by-step translation workflow |
| 4 | [04-formatting.md](ai-instructions/04-formatting.md) | PO file format, tags, placeholders, plural forms |
| 5 | [05-ai-guidelines.md](ai-instructions/05-ai-guidelines.md) | AI translation quality standards |
| 6 | [06-forbidden-practices.md](ai-instructions/06-forbidden-practices.md) | Hard restrictions — read carefully |

---

## Quick Reference

### Priority Order for Every Translation
```
Glossary (TBX)  >  Translation Memory (TMX)  >  Manual translation
```

### Directory Layout
```
project-root/
├── AGENTS.md                        ← you are here
├── ai-instructions/
│   ├── 01-overview.md
│   ├── 02-terminology.md
│   ├── 03-process.md
│   ├── 04-formatting.md
│   ├── 05-ai-guidelines.md
│   └── 06-forbidden-practices.md
├── sources/
│   └── linguistic/
│       ├── glossaries/              ← TBX files (highest priority)
│       └── tm's/                   ← TMX files (second priority)
└── work_dir/                        ← ALL output files go here
```

### Critical Rules at a Glance
- Output language: **Belarusian (be)**
- Output directory: **`work_dir/`** — no exceptions
- Encoding: **UTF-8**
- Quotation marks in `msgstr` values: **`"..."` only** — never `«»` or `„"`
- Fuzzy entries: **remove `#, fuzzy`**, remove `#| ...` lines, fix the translation
- Never translate: placeholders (`%1`, `%2`, `%i`), XML/HTML tags, accelerator markers

---

## Agent Checklist Before Starting

- [ ] Read all six instruction files in order
- [ ] Located and parsed all glossary files in `sources/linguistic/glossaries/`
- [ ] Located and parsed all TM files in `sources/linguistic/tm's/`
- [ ] Copied input `.po` file to `work_dir/`
- [ ] Identified all empty `msgstr` entries and all `fuzzy` entries
- [ ] Ready to apply: Glossary → TM → Manual translation priority