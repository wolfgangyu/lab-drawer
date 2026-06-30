---
name: claude-md
description: "Diagnose and optimize CLAUDE.md after /init. Infused with Ponytail spirit — ladder-driven YAGNI, deletion-first, root-cause diagnosis. Output in English for LLM readability."
version: 2.0.0
---

# CLAUDE.md Optimization Assistant

Diagnose and improve CLAUDE.md files. Think like the lazy senior dev with the long ponytail: before suggesting a fix, ask whether the thing needs to exist at all.

## Core Philosophy: The Ponytail Ladder

Before touching a single line, climb the ladder. Stop at the first rung that holds:

```
1. Does this rule/section need to exist?   → no: mark for deletion (YAGNI)
2. Already covered by another rule?        → merge or drop the duplicate
3. One sentence would do it?               → collapse the prose into one line
4. Table overkill for this data?           → replace with a short list or inline
5. Only then: suggest the minimal fix
```

The ladder runs **after** understanding the project, not instead of it. Read CLAUDE.md, trace what it actually controls, then climb. Lazy about the fix, never about the diagnosis.

## When to Use

- After `/init` to review or enhance the project's CLAUDE.md
- When CLAUDE.md feels bloated, outdated, or verbose
- When you want to verify if CLAUDE.md follows best practices
- When you suspect CLAUDE.md has dead rules that never fire

## Core Functions

### 1. Diagnosis

Scan CLAUDE.md and local `.claude/CLAUDE.md` files. Diagnosis has two tiers:

#### Tier 1: Ponytail Structural Scan (HIGH priority)

These checks ask "does this even need to be here?"

| Check | What it detects | Priority |
|-------|-----------------|----------|
| Dead sections | Sections describing features/rules that never trigger in practice | HIGH |
| Duplicate rules | Two or more rules saying the same thing in different words | HIGH |
| Over-described intent | Prose that could be one sentence but sprawls into paragraphs | HIGH |
| Bloated tables | Tables used for data that fits in a 3-item list | MEDIUM |
| Overly complex flows | ASCII diagrams or multi-step flows that = one sentence | MEDIUM |
| Never-violated rules | Rules that guard against things the project never does | MEDIUM |
| Redundant constraints | "Do NOT introduce" items already covered by repo structure | LOW |

#### Tier 2: Format & Completeness Scan

The original format checks — still useful, but secondary:

| Check | Threshold | Priority |
|-------|-----------|----------|
| Line count | ≤ 200 lines | HIGH |
| Missing "Do NOT introduce" | Required | HIGH |
| Fuzzy/unexecutable rules | Must be verifiable | HIGH |
| Missing "My Working Style" / equivalent | Required | HIGH |
| Missing MEMORY.md guidance | Recommended | MEDIUM |
| Stale content | > 30 days no update | MEDIUM |
| Missing project overview | 30-sec understanding test | HIGH |

#### Root Cause Analysis

When CLAUDE.md has issues, don't just name them — explain **why** they happened:

| Symptom | Root cause pattern | Fix direction |
|---------|-------------------|---------------|
| Too many lines | Architecture/knowledge dumped instead of referenced | Move to external docs, leave a pointer |
| Verbose rules | Author over-explained instead of trusting the LLM | Collapse to one executable sentence |
| Dead sections | Feature was added "just in case" (YAGNI violation) | Delete, re-add only when actually needed |
| Duplicate content | Multiple sections evolved independently | Merge into one canonical source |
| Bloated tables | Tabular format forced on non-tabular data | Replace with compact list or sentence |

**Diagnosis output format:**

```markdown
## Guardrail Diagnosis — v2.0

### 🐴 Ponytail Scan: What can go?

| # | Issue | Rung | Impact | Lines Saved |
|---|-------|------|--------|-------------|
| 1 | Dead section: PM-Specific Features never triggered | 1 (need to exist?) | HIGH | -8 |
| 2 | ASCII interaction flow diagram = one sentence | 3 (one-liner?) | MEDIUM | -12 |
| 3 | "Known pitfalls" is a duplicate of "Anti-Patterns" | 2 (already covered?) | MEDIUM | -6 |

### 🔍 Root Cause

**Problem:** CLAUDE.md at 247 lines (47 over target)
**Why:** 31% of content is architecture reference that lives in docs/ already. Another 18% is dead sections added "just in case."
**Fix:** Replace architecture dump with `See docs/architecture.md` + delete 2 dead sections.

### ✂️ Deletion Score
- Current: 247 lines
- Necessary: ~185 lines
- Safe to delete: 62 lines (25%)
- Quick wins (one-liner replacements + dead sections): 26 lines (instant)

### 📋 Format Issues (remaining after deletions)

| # | Issue | Location | Impact |
|---|-------|----------|--------|
| 1 | Missing "Do NOT introduce" list | CLAUDE.md | HIGH |
| 2 | Fuzzy rule: "keep it clean" (line 47) | CLAUDE.md:47 | HIGH |
```

### 2. Generation

Generate optimized markdown snippets with the Ponytail mindset:

- **Deletion first** — show what can be removed before what can be added
- **One-liner replacements** — collapse verbose prose into single executable sentences
- **Pointer, not library** — reference external docs instead of dumping them
- Ready-to-copy sections
- Impact level (HIGH/MEDIUM/LOW) for each suggestion
- Lines-saved counter on each recommendation

Generation principles:
- ✗ Writing a 20-line "How to use" section when 2 lines + a link works
- ✓ `See CONTRIBUTING.md for full guidelines.`
- ✗ Explaining WHY a rule exists in 3 sentences
- ✓ State the rule. The LLM doesn't need the backstory.
- ✗ Adding a "Future considerations" section
- ✓ YAGNI. Add it when the future arrives.

### 3. Execution

**Default: Suggest-then-apply mode**
1. Present diagnosis (Tier 1 → Root Cause → Deletion Score → Tier 2)
2. Ask: "Apply all suggestions, or select which ones?"
3. Execute only after confirmation
4. Report before/after: lines removed, dead sections killed, readability improved

**Optional flags:**
- `--audit` — Read-only diagnosis, no suggestions
- `--apply-all` — Auto-apply all HIGH impact items
- `--trim` — Only run Ponytail scan + root cause (skip format checks)

## Interaction Flow

```
/guardrail
    ↓
Read: CLAUDE.md, .claude/CLAUDE.md, MEMORY.md (if exists)
    ↓
Run Tier 1: Ponytail structural scan
    ↓
Run Root Cause Analysis
    ↓
Run Tier 2: Format & completeness checks
    ↓
Present findings with Deletion Score (English output)
    ↓
"Apply which changes?"
    ↓
User confirms
    ↓
Execute edits (deletions first, then fixes)
    ↓
Report completion with before/after stats
```

## Anti-Patterns Detected

Based on Andrej Karpathy's observations and the Ponytail spirit:

- **Conceptual errors** — Wrong assumptions made without confirmation
- **Over-complexity** — Bloated APIs over simple solutions; 50-line sections that should be 3
- **Silent confusion** — Agent doesn't ask when confused
- **No trade-off presentation** — Just does instead of explaining options
- **YAGNI violations** — Rules, sections, or constraints added "just in case" that never fire
- **Dead weight** — Content that duplicates external docs instead of pointing to them
- **Prose sprawl** — Multi-sentence explanations where a one-liner rule suffices

## Quality Checklist

After any edits, CLAUDE.md should pass:

- [ ] The Ponytail test: "Does every line here earn its keep?" — no dead sections, no duplicates
- [ ] Someone unfamiliar can understand the project in 30 seconds
- [ ] All rules are executable (5-sec verification test)
- [ ] No fuzzy terms like "keep it clean" or "be efficient"
- [ ] Tech stack has explicit "Do NOT introduce" list
- [ ] Working style reflects user's actual preferences
- [ ] References external docs instead of dumping content
- [ ] Line count ≤ 200 (after removing architecture dumps + dead sections)

## Design Principles

- **Ponytail ladder first** — ask what can be deleted before asking what to fix
- **Deletion over addition** — a deleted line beats a well-written one
- **Root cause, not symptom** — "too many lines" is the symptom; "architecture dump" is the cause
- **One-liner when possible** — the best section is the one that doesn't need to exist
- **Output in English** — CLAUDE.md is read by LLMs, avoid Chinese
- **Original style** — reference others' principles, not copy their formats
- **PM-friendly** — assume user is a PM, not a developer; maintainability by AI