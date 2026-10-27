---
name: english-with-translations
description: Answer in English as the primary language with Chinese glosses scaled to the learner's level, which is asked once on first use and stored in this file, and report the approximate number and difficulty of glossed terms. Use when the user asks for English practice, bilingual answers, Chinese vocabulary help, or English replies with translation aids.
---

# English With Translations

## Learner profile

<!-- learner-profile:start -->
- Status: `unset`
- Level: not recorded yet
- Source: —
- Recorded: —
<!-- learner-profile:end -->

This block is the skill's only state. Read it first: everything below that says "the learner's level" means the `Level` recorded here. Edit only inside the markers, never elsewhere in this file.

## Calibrate on first use (once)

If `Status` is `unset`, do this **before** answering the actual request:

1. Ask the user their English level with the question tool, one question, these options (adjust wording to the user's language, keep the anchors):
   - `A2 / 初级` — reads simple sentences; a few thousand words
   - `B1 / 中级` — CET-4 passed; can follow ordinary text with effort
   - `B1+ / 中级偏上` — CET-6 around 450 or IELTS 5.5–6
   - `B2 / 中高级` — CET-6 550+ or IELTS 6.5–7; reads academic text slowly
   - `C1 / 高级` — IELTS 7.5+; reads professional literature comfortably
2. When the answer arrives, rewrite the profile block to:
   - `Status: set`
   - `Level:` the chosen level plus its anchor (for example `B1+ (CET-6 450 / IELTS 5.5–6)`)
   - `Source:` `self-reported`
   - `Recorded:` today's date as `YYYY-MM-DD`
   Keep the `<!-- learner-profile:start/end -->` markers and leave the rest of the file untouched.
3. Then answer the original request at that level, and say in one line what you recorded, e.g. "Recorded B1+ — I will gloss B1+/B2 and technical terms from now on."
4. If the user declines or is unsure, leave the block `unset`, use the B1–B2 default below for this conversation, and do not ask again until the next conversation.

If `Status` is `set`, skip the question entirely — no confirmation, no re-asking. If the user later says their level changed (improved, or they want denser/sparser glosses), update the profile block the same way and say what changed.

## Level → gloss density

| Recorded level | Gloss | Leave alone |
|---|---|---|
| `A2` | nearly everything above A2, plus all technical terms | articles, pronouns, basic verbs |
| `B1` | B1+ and above, all collocations and academic verbs | A1–A2 everyday words |
| `B1+` (default when unset) | B1+/B2+ vocabulary, idioms, abstract nouns, all technical terms | A1–A2 everyday words |
| `B2` | B2+ and all technical or field-specific terms | ordinary academic vocabulary |
| `C1` | C1+ and technical or rare terms only | everything an educated reader knows |

## Overview

Answer the user in English and support a learner at the level recorded in the profile (B1–B2 roughly, until it is recorded). Add concise Chinese translations immediately after potentially unfamiliar words or phrases, e.g. `distribution(分布)`. Keep English as the main language so the user can learn from context.

## Learner calibration

Use the row of the table above that matches the recorded `Level`; until a level is recorded, use `B1+`. Within that row:

- Treat A1–A2 everyday words as known and normally leave them untranslated.
- Translate most words and phrases likely to be above the recorded level, including academic verbs, abstract nouns, uncommon collocations(固定搭配), idioms, and less common general vocabulary.
- Translate every domain-specific or technical term the learner may not know, even when its general CEFR level is uncertain.
- When a sentence contains several important unfamiliar terms, translate all of them rather than imposing an artificial one-term limit. Keep the Chinese glosses concise so the English remains readable.
- Do not assume that a word is familiar merely because it is common in native writing; prioritize likely comprehension over minimal annotation.

## Core output rules

1. **Use English as the primary language.** Write the explanation, reasoning, and examples in English. Do not replace whole sentences or paragraphs with Chinese unless the user asks for Chinese.
2. **Use the inline format.** Write `word(中文)` with no space before the parentheses. For a phrase, gloss the whole phrase: `machine learning(机器学习)`.
3. **Gloss the first occurrence.** Translate a term the first time it appears. Do not repeat the gloss every time unless the term reappears after a long gap or the meaning changes.
4. **Prefer context-appropriate meanings.** Give one short Chinese equivalent or a very brief explanation, not a full dictionary entry(词典释义). Choose the meaning used in the current sentence.
5. **Handle ambiguous terms carefully.** If a word has several relevant meanings, use `term(本句中的含义)` or explain the distinction in a short sentence.
6. **Keep proper nouns, brand names, code identifiers(代码标识符), file names, URLs, and syntax unchanged.** Explain them outside code rather than inserting translations inside identifiers or code blocks.

## Vocabulary count and difficulty report

For any substantive response (more than three sentences, or any technical/academic explanation), add a short report at the end:

```text
Vocabulary support
- Glossed terms: 24 unique words/phrases
- Approximate difficulty: 10 B1/B1+, 11 B2, 3 C1+/technical
```

Follow these counting rules:

- Count unique English words or phrases that received an inline Chinese gloss, not repeated occurrences.
- Count a multi-word expression as one term (for example, `catastrophic forgetting(灾难性遗忘)` counts as one).
- Assign an approximate level: B1/B1+ for intermediate academic or less-common vocabulary, B2 for clearly advanced general vocabulary, and C1+/technical for highly advanced, specialized, or field-specific terms.
- Mark the report as approximate; it is a reading-aid estimate, not a formal vocabulary test.
- If there are no glossed terms, say `Glossed terms: 0` rather than omitting the report.

For a very short conversational reply of three sentences or fewer, omit the report unless the user asks for it.

## Adjusting over time

Keep the recorded density as the standing default. If the user says that too many or too few words are translated, adjust the current response immediately and follow the latest preference; when the shift is a lasting one, move the recorded `Level` up or down one row so later conversations inherit it. Do not silently reduce the gloss density merely because a few terms seem familiar; reduce it only after the user says their vocabulary has improved or explicitly asks for fewer translations. When changing density, explain the new target briefly (for example, “I will now focus on B2+ and technical terms”) and continue reporting counts.

## Examples

Good:

- "This algorithm uses a **heuristic(启发式)** approach to speed up search."
- "The system is **scalable(可扩展的)**, so it can handle more users later."
- "Run `pip install` to download the **dependency(依赖项)** you need."

For a longer answer, finish with a count and level estimate, for example:

```text
Vocabulary support
- Glossed terms: 3 unique words/phrases
- Approximate difficulty: 2 B2, 1 C1+/technical
```

Avoid:

- Glossing every word: "This(这个) algorithm(算法) uses(使用) a(一个) heuristic(启发式) approach(方法)."
- Whole-sentence Chinese: "The system is scalable(可扩展的), 这样以后可以处理更多用户。"
- Translating identifiers or syntax: "`pip_install(安装pip)`"
- Asking the level question again once `Status` is `set`.

## Tailoring

Match gloss density(密度) to the recorded level, with the `B1+` row as the fallback while the profile is unset. If the user requests translations at the end of each paragraph, a separate glossary, no translations, or another format, follow that explicit preference over these defaults. Continue to provide the vocabulary count and difficulty report unless the user asks to remove it.
