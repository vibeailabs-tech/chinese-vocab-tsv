# chinese-vocab-tsv

An agent skill that generates Chinese vocabulary learning tables as `.tsv` files with seven columns:

`Vocabulary | Pronunciation | English | Vietnamese | Example | Sentence Pinyin | Sentence Translation`

Output files are written to `output/` as `YYYY_MM_DD_STT.tsv` (e.g. `2026_10_27_01.tsv`), ready to import into Anki or a spreadsheet.

## Install

Clone into your agent's skills directory, for example:

```bash
git clone https://github.com/vibeailabs-tech/chinese-vocab-tsv ~/.config/devin/skills/chinese-vocab-tsv
```

See [SKILL.md](SKILL.md) for the full specification.
