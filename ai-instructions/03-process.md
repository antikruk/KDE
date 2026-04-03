# 03 — Translation Workflow

Follow these steps in order for every `.po` file. Do not skip steps.

---

## Step 1 — Preparation

1. **Read all instruction files** (01 through 06) before doing anything else.
2. **Parse all TBX files** in `sources/linguistic/glossaries/`. Build `glossary_index`.
3. **Parse all TMX files** in `sources/linguistic/tm's/`. Build `tm_index`.
4. **Copy** the input `.po` file to `work_dir/` preserving the original filename.
5. All subsequent work is performed on the **copy in `work_dir/`**.

---

## Step 2 — File Analysis

Read the entire `.po` file and build a list of entries that require action:

| Entry type | Condition | Required action |
|------------|-----------|-----------------|
| Empty | `msgstr ""` (single string) or all `msgstr[n]` empty | Translate |
| Empty multiline | `msgstr ""\n""` with no content after | Translate |
| Fuzzy | Has `#, fuzzy` flag | Fix translation + remove fuzzy markers |
| Already translated | `msgstr` is non-empty and not fuzzy | Skip — do not modify |
| Obsolete | Lines starting with `#~` | Skip — do not modify |

---

## Step 3 — Entry-by-Entry Translation

For each entry requiring action, apply the following decision tree:

```
1. Extract msgid (and msgctxt if present).
2. Strip inline tags, placeholders, accelerators → get plain text terms.
3. Look up each term in glossary_index.
4. Look up full msgid in tm_index.
5. Choose translation source:
     a. Glossary match found → use glossary term(s) in translation.
     b. TM exact match → use TM translation.
     c. TM fuzzy ≥ 85% → adapt TM translation.
     d. No match → translate manually (see 05-ai-guidelines.md).
6. Reconstruct msgstr with all tags, placeholders, accelerators preserved.
7. Validate (see Step 4).
8. Write msgstr to the file.
```

### Fuzzy Entry Processing

When an entry has `#, fuzzy`:

1. Read the **current** `msgid` (not the `#| msgid` reference).
2. Translate the current `msgid` following the decision tree above.
3. Remove the `#, fuzzy` flag from the comment line.
4. Remove all `#| msgctxt` and `#| msgid` lines.
5. Keep `#, kde-format` and `#, kde-kuit-format` markers if present.
6. Write the corrected `msgstr`.

**Before:**
```po
#: src/foo.cpp:42
#, fuzzy, kde-format
#| msgctxt "@action:button"
#| msgid "Configure Print Server…"
msgctxt "@label:title"
msgid "Printing Device"
msgstr "Наладжванне сервера друкавання…"
```

**After:**
```po
#: src/foo.cpp:42
#, kde-format
msgctxt "@label:title"
msgid "Printing Device"
msgstr "Прылада друкавання"
```

---

## Step 4 — Validation

Before writing each translated entry, verify:

- [ ] All placeholders from `msgid` (`%1`, `%2`, `%i`, `%n`, etc.) are present in `msgstr`.
- [ ] All XML/HTML tags from `msgid` are present and properly closed in `msgstr`.
- [ ] `msgstr` uses straight double quotes `"..."` — never `«»` or `„"`.
- [ ] Escape sequences are correct: `\n`, `\t`, `\"`.
- [ ] For plural entries: all `msgstr[0]` through `msgstr[3]` are filled (Belarusian has 4 plural forms).
- [ ] The translation is not empty unless `msgid` itself is empty (the header entry).

If validation fails, correct the issue before writing.

---

## Step 5 — Output

- The translated file is already in `work_dir/` (copied in Step 1).
- Write all changes to that file.
- Do **not** create additional copies or rename the file.
- Encoding: UTF-8, no BOM.
- Line endings: LF (`\n`).

---

## Step 6 — Final Check

After translating all entries:

1. Confirm no `msgstr ""` entries remain (except the header and intentionally untranslated strings such as `new_queue`, `new_group` — leave these as-is if `msgid` equals `msgstr`).
2. Confirm no `#, fuzzy` markers remain.
3. Confirm no `#|` reference lines remain.
4. Confirm file encoding is UTF-8.