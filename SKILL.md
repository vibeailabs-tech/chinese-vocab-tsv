---
name: chinese-vocab-tsv
description: >
  Generate Chinese vocabulary learning tables as a .tsv file with exactly seven columns:
  Vocabulary, Pronunciation, English, Vietnamese, Example, Sentence Pinyin, and Sentence Translation.
  Use this skill whenever the user asks for a Chinese vocabulary table, Chinese word list, HSK/topic vocabulary,
  Chinese learning examples, bilingual English/Vietnamese meanings, or explicitly asks for TSV file output.
---

# Chinese Vocabulary TSV Generator

Generate a tab-separated vocabulary table file for Chinese learning.

## Output Contract

Create a `.tsv` file in the `output/` directory. Do not merely print the TSV in chat unless the user explicitly asks to preview it.

### Default Filename

- Use `YYYY_MM_DD_STT.tsv`, for example `output/2026_09_08_01.tsv` and `output/2026_09_08_02.tsv`.
- `YYYY_MM_DD` is the reading date: four-digit year, two-digit month, and two-digit day. Use the current date in the user's timezone unless the user specifies a reading date.
- `STT` is the reading's sequence number within that date, starting at `01` each day and padded to at least two digits.
- Before creating a new output, inspect existing `.tsv` filenames in `output/` for that date and use the next sequence number after the highest existing number; use `01` if none exist. Never overwrite an existing file when creating a new reading output.
- Apply this method by default without adding a topic or source to the filename. It supports multiple unrelated readings in one day, distinguished by their order.
- Respect an explicitly requested `.tsv` filename. If the user explicitly requests inline TSV, return raw TSV text instead of creating a file.

After creating the file, reply with the file path and a brief validation summary.

Do not output a markdown table. Do not wrap TSV content in a code block unless the user explicitly asks for inline TSV.

The TSV must have exactly seven columns in this order:

Vocabulary	Pronunciation	English	Vietnamese	Example	Sentence Pinyin	Sentence Translation

## Column Rules

- Vocabulary: Chinese characters only.
- Pronunciation: pinyin with tone marks.
- English: concise English meaning.
- Vietnamese: concise Vietnamese meaning.
- Example: one natural, easy Chinese sentence using the vocabulary.
- Sentence Pinyin: full pinyin with tone marks for the entire example sentence.
- Sentence Translation: English translation of the example sentence.

## Generation Rules

- Ensure the `output/` directory exists before writing the file.
- Always include the header row.
- Separate columns with a single tab character.
- Put each vocabulary item on its own row.
- If the user provides specific words, include exactly those words, no extra vocabulary.
- If the user provides a topic instead of specific words, generate a useful beginner-friendly set unless the user gives a count.
- If the user gives a count, generate exactly that many vocabulary rows.
- Keep example sentences easy and natural.
- Ensure the vocabulary word appears in the Chinese example sentence.
- Do not use tab characters inside cell content.
- Prefer simplified Chinese unless the user requests traditional Chinese.
- After writing the file, verify the row count and confirm every row has exactly seven tab-separated fields.

## Input Handling

- For Chinese characters, add pinyin, English, Vietnamese, and an example sentence.
- For pinyin, infer the most likely Chinese word from context when clear.
- For English or Vietnamese topics, generate appropriate Chinese vocabulary.
- If a pinyin-only or ambiguous input could map to multiple common words, choose the most useful beginner-learning option.
