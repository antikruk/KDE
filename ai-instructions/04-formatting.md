## Technical Requirements

- Use UTF-8 encoding.
- Do not modify file metadata (Headers) except for fields related to translation date and language, if necessary.
- **Fuzzy Translation Handling:** When encountering fuzzy translations, review and correct them to match the current context. Remove the `#, fuzzy` marker and any `#| msgctxt` and `#| msgid` lines, but preserve `#, kde-format` markers if present.
