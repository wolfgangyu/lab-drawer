---
name: claude-md
description: "Diagnose and optimize CLAUDE.md after /init. Check for completeness, best practices, and generate actionable suggestions. Output in English for LLM readability."
---

# CLAUDE.md Optimization Assistant

Diagnose and improve CLAUDE.md files to make them effective guides for LLMs.

## When to Use

- After `/init` to review or enhance the project's CLAUDE.md
- When CLAUDE.md feels neglected or outdated
- When you want to verify if CLAUDE.md follows best practices

## Core Functions

### 1. Diagnosis

Scan CLAUDE.md and local CLAUDE.md files for:

| Check | Threshold | Priority |
|-------|-----------|----------|
| Line count | ≤ 200 lines | HIGH |
| Missing "Do NOT introduce" | Required | HIGH |
| Fuzzy/unexecutable rules | Must be verifiable | HIGH |
| Missing "My Working Style" | Required | HIGH |
| Missing MEMORY.md guidance | Recommended | MEDIUM |
| Stale content | > 30 days no update | MEDIUM |
| Missing project overview | 30-sec understanding test | HIGH |

**Diagnosis output format:**

```markdown
## CLAUDE.md Diagnosis

### Issues Found
| # | Issue | Location | Impact |
|---|-------|----------|--------|
| 1 | Line count exceeds 200 | CLAUDE.md:247 | HIGH |
| 2 | Missing "Do NOT introduce" list | CLAUDE.md | HIGH |

### Recommendations
- **Impact: HIGH** Add "Do NOT introduce" section listing banned tech
- **Impact: MEDIUM** Trim to 200 lines by referencing external docs
```

### 2. Generation

Generate optimized markdown snippets:

- Ready-to-copy sections
- Impact level (HIGH/MEDIUM/LOW) for each suggestion
- Follow "pointer not library" principle:
  - ✗ Dumping architecture docs in CLAUDE.md
  - ✓ Reference: `See docs/architecture.md`

### 3. Execution

**Default: Suggest-then-apply mode**
1. Present diagnosis
2. Ask: "Apply all suggestions, or select which ones?"
3. Execute only after confirmation

**Optional flags:**
- `--audit` — Read-only diagnosis, no suggestions
- `--apply-all` — Auto-apply all HIGH impact items

## PM-Specific Features

| Feature | When Triggered |
|---------|----------------|
| Requirement clarification | User says "我要..." (I want...) |
| Tech decision support | User picks a new tech stack |
| Stale content alert | CLAUDE.md not modified in 30+ days |
| Known pitfalls tracking | After bugs are discovered |

## Anti-Patterns Detected

Based on Andrej Karpathy's observations and industry best practices:

- **Conceptual errors** — Wrong assumptions made without confirmation
- **Over-complexity** — Bloated APIs over simple solutions
- **Silent confusion** — Agent doesn't ask when confused
- **No trade-off presentation** — Just does instead of explaining options

## Interaction Flow

```
/claude-md
    ↓
Read: CLAUDE.md, .claude/CLAUDE.md (local), MEMORY.md (if exists)
    ↓
Run diagnosis checks
    ↓
Present findings (English output)
    ↓
"Apply which changes?"
    ↓
User confirms
    ↓
Execute edits
    ↓
Report completion
```

## Quality Checklist

After any edits, CLAUDE.md should pass:

- [ ] Someone unfamiliar can understand the project in 30 seconds
- [ ] All rules are executable (5-sec verification test)
- [ ] No fuzzy terms like "keep it clean" or "be efficient"
- [ ] Tech stack has explicit "Do NOT introduce" list
- [ ] Working style reflects user's actual preferences
- [ ] References external docs instead of dumping content

## Design Principles

- **Output in English** — CLAUDE.md is read by LLMs, avoid Chinese
- **Original style** — Reference others' principles, not copy their formats
- **PM-friendly** — Assume user is a PM, not a developer; maintainability by AI