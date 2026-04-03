# 05 — AI Translation Guidelines

---

## Translation Priority (Reminder)

```
Glossary (TBX)  >  Translation Memory (TMX)  >  Manual translation
```

Never skip the glossary and TM lookup steps, even for short strings.

---

## Manual Translation Standards

Apply when no glossary or TM match is available.

### Language Quality

- Write natural, fluent Belarusian — not word-for-word English.
- Follow standard Belarusian grammar: case agreement, verb aspect, word order.
- Use the **Taraškievica-neutral** literary norm unless the project specifies otherwise.
- Avoid calques (direct structural borrowings from Russian or English) when a natural Belarusian equivalent exists.

### Register and Style

- Match the register of the source: formal UI labels → neutral Belarusian; error messages → direct but polite; tooltips → concise.
- Do not add words not present in the source (no padding, no explanations).
- Do not omit words that carry meaning in the source.
- Use **second person imperative** for button and action labels: `Дадаць`, `Захаваць`, `Выдаліць`, `Абраць`.
- Use **infinitive** for menu items when the source uses infinitive.

### KDE-Specific Conventions

| Context (`msgctxt`) | Convention |
|---------------------|------------|
| `@action:button` | Imperative verb: `Дадаць`, `Захаваць` |
| `@title:window` | Noun phrase or infinitive: `Наладжванне прынтара` |
| `@info:status` | Full sentence with punctuation |
| `@info:tooltip` | Full sentence, concise |
| `@label:textbox` | Noun + colon: `Адрас:` |
| `@option:check` | Verb phrase: `Дазволіць адлеглае адміністраванне` |
| `@info:usagetip` | Full sentence, instructional |

### Punctuation

- **Ellipsis**: use the Unicode character `…` (U+2026), not three dots `...`. Preserve it exactly where it appears in `msgid`.
- **Colon**: preserve trailing colons on labels.
- **Question marks and exclamation marks**: preserve from `msgid`.
- **Em dash**: use `—` (U+2014) for Belarusian em dash constructions; do not use hyphen `-` as a dash.

---

## Handling Specific String Types

### Empty or Trivially Untranslatable Strings

Some `msgid` values should be left unchanged in `msgstr`:

```po
msgid "new_queue"
msgstr "new_queue"

msgid "new_group"
msgstr "new_group"
```

These are internal identifiers, not UI strings. Leave them as-is.

### Strings With Only Placeholders or Tags

If `msgid` contains nothing but a placeholder or tag, copy it unchanged:

```po
msgid "%1"
msgstr "%1"
```

### Trademarked Names and Product Names

Do not translate:
- `CUPS`, `IPP`, `LPD`, `SMB`, `PackageKit`, `PostScript`, `PPD`
- Brand names: `Windows`, `JetDirect`
- Protocol acronyms

Translate surrounding text naturally.

### Version Strings, URLs, Email Addresses

Do not translate. Copy to `msgstr` unchanged.

### Error Messages

Translate fully. Use natural Belarusian sentence structure. Preserve all placeholders.

```po
msgid "Failed to configure printer: "
msgstr "Не ўдалося наладзіць прынтар: "
```

Note the trailing space and colon — preserve them exactly.

---

## Consistency Requirements

- Use the same Belarusian word for the same English term throughout **all** entries in a file and across files.
- If you translate "printer" as `прынтар` in one entry, use `прынтар` everywhere.
- Before finalising a manual translation, check all other entries in the current file for the same source term.

---

## Belarusian Grammar Notes

### Noun Cases in UI

| Context | Case | Example |
|---------|------|---------|
| Subject of sentence | Nominative | `Прынтар не знойдзены` |
| Direct object | Accusative | `Выдаліць прынтар` |
| After numerals 2–4 | Genitive singular | `2 прынтары` |
| After numerals 5+ | Genitive plural | `5 прынтараў` |
| Possession / "of" | Genitive | `Налады прынтара` |

### Verb Aspect

- **Imperative buttons**: use **perfective** aspect for one-time actions: `Дадаць`, `Захаваць`, `Выдаліць`, `Скасаваць`.
- **Ongoing actions**: use **imperfective**: `Усталёўванне…`, `Наладжванне…`.

### Capitalisation

- Window titles: capitalise only the first word and proper nouns.
- Button labels: capitalise only the first word.
- Menu items: capitalise only the first word.
- Do not use ALL CAPS unless the source does.

---

## Self-Review Before Finalising

For each translated entry, verify:

1. Does the translation convey the same meaning as `msgid`?
2. Is the Belarusian grammatically correct?
3. Are all placeholders and tags preserved?
4. Is the register appropriate for the `msgctxt`?
5. Is the terminology consistent with glossary and earlier entries?
6. Are there no `«»` quotation marks, fuzzy markers, or `#|` lines?