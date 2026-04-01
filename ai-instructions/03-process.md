## Workflow

1. **File Copy:** Copy the input `.po` file to `work_dir/` directory.
2. **Complete File Analysis:** Read the entire copied `.po` file from `work_dir/` to identify all empty `msgstr` entries that need translation.
3. **Glossary Lookup:** Check all terms against glossary files.
4. **TM Lookup:** For each `msgid` string, search for a match in the translation memory files located in `sources/linguistic/tm's/`.
5. **Translation Strategy:**
   - If a term is in the glossary, use the glossary translation.
   - If an exact match is found in the TM, use it.
   - If no match is found, perform a high-quality translation into Belarusian, adhering to KDE context and established terminology.
6. **Formatting Preservation:**
   - Retain all tags, escape sequences, and special characters.
   - Correctly handle plural forms (Belarusian uses three plural forms).
7. **Output:** The translated file is already in `work_dir/` with the original filename maintained.
