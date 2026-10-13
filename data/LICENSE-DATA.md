# Data license and attribution

*Türkçe sürüm: [LICENSE-DATA.tr.md](LICENSE-DATA.tr.md)*

The data files in this folder (`osmanlica_koken.csv`, `train.csv`, `val.csv`, `test.csv` and, if present, `cache_*.json`) are derived from the English edition of Wiktionary (https://en.wiktionary.org).

## Source and license

The original text of Wiktionary entries is dual-licensed under the **Creative Commons Attribution-ShareAlike 4.0 License (CC BY-SA 4.0)** and the **GNU Free Documentation License (GFDL)** (see https://en.wiktionary.org/wiki/Wiktionary:Copyrights).

Accordingly, the derived data files in this folder are shared under **CC BY-SA 4.0**:

- **Attribution:** The data is the work of Wiktionary contributors. Source: https://en.wiktionary.org
- **ShareAlike:** If you modify and share this data, you must use the same license.
- License text: https://creativecommons.org/licenses/by-sa/4.0/

## Changes made

- Words were collected from Wiktionary's "Ottoman Turkish terms ..." etymology categories and labeled Arabic, Persian or Turkish according to the category.
- Only lemmas, single-word entries written in Arabic script were kept; diacritics (harakat) were removed.
- 101 words that appeared in more than one class were removed; 4 one-letter entries were removed; zero-width non-joiner (ZWNJ) characters were deleted.
- Proper nouns are flagged in the `ozel_isim` column.
- The data was split 70% train, 15% validation and 15% test, preserving class proportions (`random_state=42`).

Collection date: no later than 7 October 2026. The proper-noun category was fetched in October 2026 (the exact day was not recorded).

## Code license

The code outside this folder (the notebook) is released under the MIT License (see `LICENSE` in the repository root).
