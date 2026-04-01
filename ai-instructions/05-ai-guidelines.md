## AI Instructions

### Translation Approach
- **Priority 1:** Use exact matches from glossary files in `sources/linguistic/glossaries/`
- **Priority 2:** Use exact matches from translation memory in `sources/linguistic/tm's/`
- **Priority 3:** Perform manual translation with consistency

### Quality Standards
- Maintain consistency with established KDE Belarusian terminology
- Use proper Belarusian grammar and syntax
- Preserve all formatting, placeholders (%1, %2, etc.), and XML/HTML tags
- Handle plural forms correctly (Belarusian: n%10==1 && n%100!=11 ? 0 : n%10>=2 && n%10<=4 && (n%100<12 || n%100>14) ? 1 : n%10==0 || n%10>=5 && n%10<=9 || n%100>=11 && n%100<=14 ? 2 : 3)

### Fuzzy Entry Processing
- Remove all `#, fuzzy` markers
- Remove all `#| msgctxt` and `#| msgid` reference lines
- Preserve `#, kde-format` and other formatting markers
- Update translations to match current context

### File Management
- All output files must be in `work_dir/` directory
- Maintain original filenames
- Use UTF-8 encoding
- Do not modify header metadata except translation date/language fields
