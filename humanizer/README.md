# Humanizer

A skill for Claude Code and OpenCode that removes signs of AI-generated writing from text, making it sound more natural and human. Available in **English** (33 patterns) and **Traditional Chinese** (39 patterns: 33 cross-language + 6 Chinese-specific).

## Installation

### Claude Code — English (`/humanizer`)

```bash
mkdir -p ~/.claude/skills
git clone https://github.com/wolfgangyu/humanizer.git ~/.claude/skills/humanizer
```

Then use it:
```
/humanizer

[paste your text here]
```

### Claude Code — Traditional Chinese (`/humanizer-zh`)

繁體中文版是獨立的 skill 檔案。Clone repo 後，把 `SKILL_zh-TW.md` 拷到 skills 目錄：

```bash
mkdir -p ~/.claude/skills/humanizer-zh
git clone https://github.com/wolfgangyu/humanizer.git /tmp/humanizer
cp /tmp/humanizer/SKILL_zh-TW.md ~/.claude/skills/humanizer-zh/SKILL.md
```

> Claude Code 會根據 `SKILL.md` 的 `name` 欄位（`humanizer-zh`）自動觸發。`/humanizer-zh` 就是對應的斜線指令。

Then use it:
```
/humanizer-zh

[貼上你的文字]
```

### OpenCode

OpenCode 也掃描 `~/.claude/skills/`，所以同一個目錄可以給兩個工具用。

If you only use OpenCode:
```bash
mkdir -p ~/.config/opencode/skills
git clone https://github.com/wolfgangyu/humanizer.git ~/.config/opencode/skills/humanizer
```

For Chinese in OpenCode, copy the same way:
```bash
mkdir -p ~/.config/opencode/skills/humanizer-zh
cp /tmp/humanizer/SKILL_zh-TW.md ~/.config/opencode/skills/humanizer-zh/SKILL.md
```

## Usage

### Claude Code

```
/humanizer

[paste your text here]
```

### OpenCode

```
/humanizer

[paste your text here]
```

Or ask the model to humanize text directly in either tool:

```
Please humanize this text: [your text]
```

### 繁體中文版（Traditional Chinese）

For Chinese (Taiwan) text, use the separate `SKILL_zh-TW.md` skill:

```
/humanizer-zh

[貼上你的文字]
```

或直接請模型 humanize：

```
請帮我 humanize 這段文字：[你的文字]
```

繁體中文版包含 33 個跨語言模式，加上 6 個中文特有模式（中國用語汙染偵測、簡體字混入、語氣詞缺失、書面語過度、標點符號異常、段落均質化），共 39 個 pattern。

### Voice Calibration

To match your personal writing style, provide a sample of your own writing:

```
/humanizer

Here's a sample of my writing for voice matching:
[paste 2-3 paragraphs of your own writing]

Now humanize this text:
[paste AI text to humanize]
```

The skill will analyze your sentence rhythm, word choices, and quirks, then apply them to the rewrite instead of producing generic "clean" output.

## Overview

Based on [Wikipedia's "Signs of AI writing"](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing) guide, maintained by WikiProject AI Cleanup. This comprehensive guide comes from observations of thousands of instances of AI-generated text.

The skill also includes a final "obviously AI generated" audit pass and a second rewrite, to catch lingering AI-isms in the first draft.

### Key Insight from Wikipedia

> "LLMs use statistical algorithms to guess what should come next. The result tends toward the most statistically likely result that applies to the widest variety of cases."

## 33 Patterns Detected (with Before/After Examples)

### Content Patterns

| # | Pattern | Before | After |
|---|---------|--------|-------|
| 1 | **Significance inflation** | "marking a pivotal moment in the evolution of..." | "was established in 1989 to collect regional statistics" |
| 2 | **Notability name-dropping** | "cited in NYT, BBC, FT, and The Hindu" | "In a 2024 NYT interview, she argued..." |
| 3 | **Superficial -ing analyses** | "symbolizing... reflecting... showcasing..." | Remove or expand with actual sources |
| 4 | **Promotional language** | "nestled within the breathtaking region" | "is a town in the Gonder region" |
| 5 | **Vague attributions** | "Experts believe it plays a crucial role" | "according to a 2019 survey by..." |
| 6 | **Formulaic challenges** | "Despite challenges... continues to thrive" | Specific facts about actual challenges |

### Language Patterns

| # | Pattern | Before | After |
|---|---------|--------|-------|
| 7 | **AI vocabulary** | "Actually... additionally... testament... landscape... showcasing" | "also... remain common" |
| 8 | **Copula avoidance** | "serves as... features... boasts" | "is... has" |
| 9 | **Negative parallelisms / tailing negations** | "It's not just X, it's Y", "..., no guessing" | State the point directly |
| 10 | **Rule of three** | "innovation, inspiration, and insights" | Use natural number of items |
| 11 | **Synonym cycling** | "protagonist... main character... central figure... hero" | "protagonist" (repeat when clearest) |
| 12 | **False ranges** | "from the Big Bang to dark matter" | List topics directly |
| 13 | **Passive voice / subjectless fragments** | "No configuration file needed" | Name the actor when it helps clarity |

### Style Patterns

| # | Pattern | Before | After |
|---|---------|--------|-------|
| 14 | **Em/en dashes** | "institutions—not the people—yet this continues—" | Cut them: periods, commas, colons, or parentheses |
| 15 | **Boldface overuse** | "**OKRs**, **KPIs**, **BMC**" | "OKRs, KPIs, BMC" |
| 16 | **Inline-header lists** | "**Performance:** Performance improved" | Convert to prose |
| 17 | **Title Case Headings** | "Strategic Negotiations And Partnerships" | "Strategic negotiations and partnerships" |
| 18 | **Emojis** | "🚀 Launch Phase: 💡 Key Insight:" | Remove emojis |
| 19 | **Curly quotes** | `said “the project”` | `said “the project”` |
| 26 | **Hyphenated word pairs** | “cross-functional, data-driven, client-facing” | Drop hyphens on common word pairs |
| 27 | **Persuasive authority tropes** | "At its core, what matters is..." | State the point directly |
| 28 | **Signposting announcements** | "Let's dive in", "Here's what you need to know" | Start with the content |
| 29 | **Fragmented headers** | "## Performance" + "Speed matters." | Let the heading do the work |
| 30 | **Diff-anchored writing** | "This function was added to replace..." | Describe what it does, not what changed |
| 31 | **Manufactured punchlines / staccato drama** | "It had no preference. No prior. No nostalgia." | Use varied sentence lengths and concrete claims |
| 32 | **Aphorism formulas** | "Symmetry is the language of trust" | Replace the formula with the actual claim |
| 33 | **Conversational rhetorical openers** | "Honestly? It depends..." | Remove the fake-candid setup |

### Communication Patterns

| # | Pattern | Before | After |
|---|---------|--------|-------|
| 20 | **Chatbot artifacts** | "I hope this helps! Let me know if..." | Remove entirely |
| 21 | **Cutoff disclaimers** | "While details are limited in available sources..." | Find sources or remove |
| 22 | **Sycophantic tone** | "Great question! You're absolutely right!" | Respond directly |

### Filler and Hedging

| # | Pattern | Before | After |
|---|---------|--------|-------|
| 23 | **Filler phrases** | "In order to", "Due to the fact that" | "To", "Because" |
| 24 | **Excessive hedging** | "could potentially possibly" | "may" |
| 25 | **Generic conclusions** | "The future looks bright" | Specific plans or facts |

## References

- [Wikipedia: Signs of AI writing](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing) - Primary source
- [WikiProject AI Cleanup](https://en.wikipedia.org/wiki/Wikipedia:WikiProject_AI_Cleanup) - Maintaining organization

## Version History

- **3.0.0** - Major compression: removed Full Example, condensed DETECTION GUIDANCE, streamlined YAML frontmatter, trimmed pattern examples. Added Traditional Chinese version (`SKILL_zh-TW.md`, 33 cross-language patterns + 6 Chinese-specific patterns: China term contamination detection, simplified character mixing, modal particle absence, over-formal register, punctuation anomalies, homogeneous paragraph structure). 33 patterns in English, 39 in Chinese.
- **2.8.0** - Added style/cadence patterns #31-33 for manufactured punchlines, aphorism formulas, and conversational rhetorical openers; expanded #20 to catch offer-to-continue chatbot closers. 33 patterns total.
- **2.7.0** - Added pattern #30 (diff-anchored writing); made em/en dashes a hard cut rather than "overuse"; expanded #21 to cover speculative gap-filling ("maintains a low profile"). 30 patterns total.
- **2.6.0** - Cleanup pass: consolidated the duplicated workflow sections, gated the personality guidance to content where voice is wanted, removed the model-fingerprinting subsection, and condensed the worked example. No change to the 29 patterns.
- **2.5.1** - Added a passive-voice / subjectless-fragment rule, raising the total to 29 patterns
- **2.5.0** - Added patterns for persuasive framing, signposting, and fragmented headers; expanded negative parallelisms to cover tailing negations; tightened wording around em dash overuse; fixed frontmatter wording to use "filler phrases"
- **2.4.0** - Added voice calibration: match the user's personal writing style from samples
- **2.3.0** - Added pattern #25: hyphenated word pair overuse
- **2.2.0** - Added a final "obviously AI generated" audit + second-pass rewrite prompts
- **2.1.1** - Fixed pattern #18 example (curly quotes vs straight quotes)
- **2.1.0** - Added before/after examples for all 24 patterns
- **2.0.0** - Complete rewrite based on raw Wikipedia article content
- **1.0.0** - Initial release

## License

MIT
