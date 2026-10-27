# english-with-translations

An agent skill that replies in English while glossing difficult words in Chinese, so a learner can
read real English and still keep up: `heuristic(启发式)`, `collocation(固定搭配)`, `perplexity(困惑度)`.

英语回答 + 难点词中文注释的技能。首次执行时会先问一次你的英语水平，然后把答案写回 `SKILL.md`，
之后的每次对话都按这个水平决定注释密度，不再重复提问。

## How the calibration works

`SKILL.md` carries a small state block near the top:

```markdown
<!-- learner-profile:start -->
- Status: `unset`
- Level: not recorded yet
- Source: —
- Recorded: —
<!-- learner-profile:end -->
```

- `Status: unset` → the agent asks one question (A2 / B1 / B1+ / B2 / C1) before doing the task,
  then rewrites this block to `set` with the chosen level and today's date.
- `Status: set` → the question is skipped forever; the recorded level drives the gloss density.
- Declining leaves it `unset`, and the skill falls back to the B1+ / B2 default.

The level maps to a gloss-density table so the recorded value is actionable, not decorative:

| Level | Gloss | Leave alone |
|---|---|---|
| A2 | nearly everything above A2, plus all technical terms | articles, pronouns, basic verbs |
| B1 | B1+ and above, all collocations and academic verbs | A1–A2 everyday words |
| B1+ (fallback) | B1+/B2+ vocabulary, idioms, abstract nouns, all technical terms | A1–A2 everyday words |
| B2 | B2+ and all technical or field-specific terms | ordinary academic vocabulary |
| C1 | C1+ and technical or rare terms only | everything an educated reader knows |

Every substantive answer ends with a short report:

```text
Vocabulary support
- Glossed terms: 11 unique words/phrases
- Approximate difficulty: 4 B1/B1+, 5 B2, 2 C1+/technical
```

## Install

Personal skill directory:

```bash
git clone https://github.com/YanBingtai/-skill.git
mkdir -p ~/.agents/skills
cp -R -- -skill ~/.agents/skills/english-with-translations
```

Or copy `SKILL.md` and `agents/` into `~/.agents/skills/english-with-translations/` by hand.

## Layout

```
.
├── SKILL.md            # instructions + learner-profile state block
├── agents/openai.yaml  # interface metadata (display name, default prompt)
└── README.md
```

## Notes

- The profile block is the only state; edit inside the markers and nothing else.
- If the learner says their level changed, move the recorded `Level` one row up or down.
