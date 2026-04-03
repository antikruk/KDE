# 04 — PO File Formatting and Technical Requirements

---

## File Format Basics

- Encoding: **UTF-8**, no BOM.
- Line endings: **LF** (`\n`).
- Each entry: blank line separator between entries.
- `msgid` and `msgstr` values are always wrapped in double-quote strings `"..."`.
- Long strings may be split across lines; the first line is always `""`.

```po
msgid ""
"This is a long string that "
"spans multiple lines."
msgstr ""
"Гэта доўгі радок, які "
"займае некалькі радкоў."
```

---

## File Header

The header entry has an empty `msgid ""`. Do **not** modify any header fields except:
- `PO-Revision-Date` — update only if explicitly instructed.
- `Last-Translator` — update only if explicitly instructed.

Always preserve:
- `Plural-Forms` — do not change.
- `X-Crowdin-*` fields — do not change.
- `X-Generator` — do not change.

**Required `Plural-Forms` for Belarusian:**
```
Plural-Forms: nplurals=4; plural=(n%10==1 && n%100!=11 ? 0 : n%10>=2 && n%10<=4 && (n%100<12 || n%100>14) ? 1 : n%10==0 || n%10>=5 && n%10<=9 || n%100>=11 && n%100<=14 ? 2 : 3);
```

---

## Plural Forms

Belarusian has **4 plural forms** (not 3):

| Form index | Rule | Example count | Example |
|------------|------|---------------|---------|
| `msgstr[0]` | n%10==1 && n%100!=11 | 1, 21, 31 | 1 файл |
| `msgstr[1]` | n%10==2–4 && n%100∉12–14 | 2, 3, 4, 22 | 2 файлы |
| `msgstr[2]` | n%10==0 or 5–9 or n%100==11–14 | 0, 5, 11, 20 | 5 файлаў |
| `msgstr[3]` | all other cases (fractional) | 1.5 | 1,5 файла |

**All four `msgstr[n]` entries must be filled for every plural entry.**

Example:
```po
#, kde-format
msgid "One file"
msgid_plural "%1 files"
msgstr[0] "Адзін файл"
msgstr[1] "%1 файлы"
msgstr[2] "%1 файлаў"
msgstr[3] "%1 файла"
```

---

## Placeholders

Placeholders are positional arguments. They must appear in `msgstr` exactly as in `msgid`.

| Placeholder | Meaning |
|-------------|---------|
| `%1`, `%2`, … | Positional string/number arguments |
| `%i` | Integer |
| `%n` | The number used for plural selection |

**Rules:**
- Never translate a placeholder.
- Never reorder placeholders (KDE does not support reordering by default unless `kde-format` is used with explicit position).
- Never omit a placeholder.

---

## KDE Format Markers

| Marker | Meaning |
|--------|---------|
| `#, kde-format` | Entry uses `%1`-style placeholders |
| `#, kde-kuit-format` | Entry uses KDE UI Text format with XML-like tags |

Both markers must be **preserved** on the same comment line. Do not add or remove these markers.

---

## XML and HTML Tags

When `msgid` contains tags, they must appear in `msgstr` in the same positions with the same structure.

**KDE KUIT tags** (used with `kde-kuit-format`):
```
<interface>…</interface>   — UI element name
<command>…</command>       — command name
<filename>…</filename>     — file name
<nl/>                      — newline (self-closing)
```

**Rules:**
- Translate only the text content between tags.
- Never translate tag names or attribute names.
- Preserve self-closing tags (`<nl/>`) exactly.
- Preserve tag order and nesting.

Example:
```po
msgid "Click <interface>Add…</interface> to continue."
msgstr "Каб працягнуць, націсніце <interface>Дадаць…</interface>."
```

---

## Accelerators

Accelerators mark keyboard shortcuts in menu/button labels.

| Format | Example |
|--------|---------|
| Ampersand (`&`) | `&File` |
| Tilde (`~`) | `~File` |

**Rules:**
- Preserve the accelerator character in `msgstr`.
- Place it before the appropriate letter in the Belarusian translation.
- The accelerated letter should be unique within the dialog if possible.
- If no suitable position exists, place the accelerator before the first letter.

---

## Escape Sequences

| Sequence | Meaning |
|----------|---------|
| `\"` | Literal double quote inside `msgstr` |
| `\n` | Newline within a string |
| `\t` | Tab |
| `\\` | Literal backslash |

**Rules:**
- Preserve all escape sequences from `msgid` in `msgstr`.
- When the translation requires a literal quote character (e.g., around a UI element name), use `\"` — never `«»`.

---

## Quotation Marks Inside msgstr

When you need quotation marks around a word or phrase inside a `msgstr` value:

```po
# ✅ Correct
msgstr "Не ўдалося выдаліць прынтар: \"%1\""

# ❌ Wrong
msgstr "Не ўдалося выдаліць прынтар: «%1»"
```

The outer `"..."` delimit the PO string. Inner quotes must be escaped as `\"`.

---

## Comment Lines

| Prefix | Type | Action |
|--------|------|--------|
| `#` (space) | Translator comment | Preserve |
| `#.` | Extracted comment | Preserve |
| `#:` | Source location | Preserve |
| `#,` | Flag | Preserve (except remove `fuzzy` as specified) |
| `#|` | Previous msgid/msgstr | Remove when processing fuzzy entries |
| `#~` | Obsolete entry | Preserve entirely, do not translate |