# Translation Instructions

This file contains instructions for translating `.po` files from English to Belarusian for the KDE project.

## Core Tasks

1. **Translation Direction:** English (en) -> Belarusian (be).
2. **Translation Memory (TM):** Use all available files within the `KDE/tm's/` directory to ensure consistency in terminology.
3. **Output Directory:** All processed files must be saved to the `KDE/work_dir/` directory.

## Workflow

1. **File Analysis:** Read the input `.po` file.
2. **TM Lookup:** For each `msgid` string, search for a match in the translation memory files located in `KDE/tm's/`.
3. **Translation Strategy:**
   - If an exact match is found in the TM, use it.
   - If no match is found, perform a high-quality translation into Belarusian, adhering to KDE context and established terminology.
4. **Formatting Preservation:**
   - Retain all tags, escape sequences, and special characters.
   - Correctly handle plural forms (Belarusian uses three plural forms).
5. **Output:** Write the translated file to `KDE/work_dir/` while maintaining the original filename.

## Technical Requirements

- Use UTF-8 encoding.
- Do not modify file metadata (Headers) except for fields related to translation date and language, if necessary.
