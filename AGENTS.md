# Translation Instructions

This file contains instructions for translating `.po` files from English to Belarusian for the KDE project.

## Core Tasks

1. **Translation Direction:** English (en) -> Belarusian (be).
2. **Translation Memory (TM):** Use all available files within the `KDE/tm's/` directory to ensure consistency in terminology.
3. **Glossary:** Always consult glossary files in `glossaries/` directory. Glossary terms have **highest priority** over TM and machine translation.
4. **Output Directory:** All processed files must be saved to the `KDE/work_dir/` directory.

## Glossary Usage

### Location

Glossary files are stored in `glossaries/` directory.

### Rules

1. **Priority Order:** Glossary > TM > Manual Translation
2. **Exact Match:** Use glossary translations exactly as written
3. **Context Notes:** Pay attention to context notes in the glossary
4. **Case Sensitivity:** Match case appropriately (capitalize if source is capitalized)
5. **Missing Terms:** If a term is not in the glossary, translate it consistently and add a comment for review

## Workflow

1. **File Analysis:** Read the input `.po` file.
2. **Glossary Lookup:** Check all terms against glossary files.
3. **TM Lookup:** For each `msgid` string, search for a match in the translation memory files located in `KDE/tm's/`.
4. **Translation Strategy:**
   - If a term is in the glossary, use the glossary translation.
   - If an exact match is found in the TM, use it.
   - If no match is found, perform a high-quality translation into Belarusian, adhering to KDE context and established terminology.
5. **Formatting Preservation:**
   - Retain all tags, escape sequences, and special characters.
   - Correctly handle plural forms (Belarusian uses three plural forms).
6. **Output:** Write the translated file to `KDE/work_dir/` while maintaining the original filename.

## Technical Requirements

- Use UTF-8 encoding.
- Do not modify file metadata (Headers) except for fields related to translation date and language, if necessary.
