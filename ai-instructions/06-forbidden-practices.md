# 06 — Forbidden Practices

These rules are **absolute**. No exception, no matter how reasonable it may seem.

---

## 1. Wrong Quotation Marks in msgstr

**NEVER** use Belarusian or typographic quotation marks as PO string delimiters or inside `msgstr` values as quotation marks.

```po
# ❌ FORBIDDEN — Crowdin will reject the file
msgstr «Адкрыць чаргу друку»

# ❌ FORBIDDEN — parser cannot read this
msgstr „Адкрыць чаргу друку"

# ✅ CORRECT — use ASCII double quotes
msgstr "Адкрыць чаргу друку"
```

When the translation needs quotation marks around a word, escape them:

```po
# ✅ CORRECT
msgstr "Будзе выдалена: \"%1\"."
```

---

## 2. Leaving fuzzy Markers in Output

**NEVER** leave `#, fuzzy` in an entry after processing it.

```po
# ❌ FORBIDDEN
#, fuzzy, kde-format
msgstr "Нейкі стары пераклад"

# ✅ CORRECT — marker removed, translation updated
#, kde-format
msgstr "Актуальны пераклад"
```

---

## 3. Leaving #| Reference Lines in Output

**NEVER** leave `#| msgctxt`, `#| msgid`, or `#| msgstr` lines in the file after processing a fuzzy entry.

```po
# ❌ FORBIDDEN
#| msgctxt "@action:button"
#| msgid "Configure Print Server…"
msgctxt "@label:title"
msgid "Printing Device"
msgstr "Прылада друкавання"

# ✅ CORRECT
msgctxt "@label:title"
msgid "Printing Device"
msgstr "Прылада друкавання"
```

---

## 4. Translating Placeholders

**NEVER** translate, rename, or reorder placeholders.

```po
# ❌ FORBIDDEN
msgid "Failed to configure printer: %1"
msgstr "Не ўдалося наладзіць прынтар: %адзін"

# ✅ CORRECT
msgstr "Не ўдалося наладзіць прынтар: %1"
```

---

## 5. Removing or Adding Format Markers

**NEVER** remove `#, kde-format`, `#, kde-kuit-format`, `#, qt-format`, or `#, c-format` from entries that have them. **NEVER** add them to entries that do not.

```po
# ❌ FORBIDDEN — marker removed
#: src/foo.cpp:10
msgctxt "MozhiTTSProvider|"
msgid "Cannot connect to Mozhi instance: %1"
msgstr "Не ўдалося падключыцца да асобніка Mozhi: %1"

# ✅ CORRECT — marker preserved
#: src/foo.cpp:10
#, qt-format
msgctxt "MozhiTTSProvider|"
msgid "Cannot connect to Mozhi instance: %1"
msgstr "Не ўдалося падключыцца да асобніка Mozhi: %1"
```

---

## 6. Modifying Already-Translated Non-Fuzzy Entries

**NEVER** change a `msgstr` that is already filled and not marked fuzzy, unless explicitly instructed. Only empty and fuzzy entries are within scope.

---

## 7. Modifying the File Header Metadata

**NEVER** change header fields unless explicitly instructed. Specifically, do not modify:

- `Project-Id-Version`
- `POT-Creation-Date`
- `Language-Team`
- `Language`
- `MIME-Version`
- `Content-Type`
- `Content-Transfer-Encoding`
- `Plural-Forms`
- `X-Generator`
- `X-Crowdin-*`

---

## 8. Modifying Obsolete Entries

**NEVER** translate or alter lines starting with `#~`. These are obsolete entries kept for history. Leave them exactly as found.

---

## 9. Outputting Files Outside work_dir/

**NEVER** write output files to any directory other than `work_dir/`. Not to the source directory, not to a temp directory, not to the project root.

---

## 10. Translating Internal Identifiers

**NEVER** translate strings that are clearly internal identifiers (not user-visible text). If `msgid` and existing `msgstr` are identical and the string has no spaces and looks like a code identifier, leave it unchanged.

```po
# Leave as-is — internal identifier
msgid "new_queue"
msgstr "new_queue"
```

---

## 11. Leaving Missing Plural Forms

**NEVER** leave a plural entry with fewer than 4 `msgstr[n]` entries. Belarusian requires exactly 4 forms: `msgstr[0]` through `msgstr[3]`.

```po
# ❌ FORBIDDEN — only 2 forms
msgstr[0] "Адзін файл"
msgstr[1] "%1 файлы"

# ✅ CORRECT — all 4 forms
msgstr[0] "Адзін файл"
msgstr[1] "%1 файлы"
msgstr[2] "%1 файлаў"
msgstr[3] "%1 файла"
```