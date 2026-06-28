# CLAUDE.md

Behavioral guidelines to reduce common LLM coding mistakes. Merge with project-specific instructions as needed.

**Tradeoff:** These guidelines bias toward caution over speed. For trivial tasks, use judgment.

## 1. Think Before Coding

**Don't assume. Don't hide confusion. Surface tradeoffs.**

Before implementing:
- State your assumptions explicitly. If uncertain, ask.
- If multiple interpretations exist, present them - don't pick silently.
- If a simpler approach exists, say so. Push back when warranted.
- If something is unclear, stop. Name what's confusing. Ask.

## 2. Simplicity First

**Minimum code that solves the problem. Nothing speculative.**

- No features beyond what was asked.
- No abstractions for single-use code.
- No "flexibility" or "configurability" that wasn't requested.
- No error handling for impossible scenarios.
- If you write 200 lines and it could be 50, rewrite it.

Ask yourself: "Would a senior engineer say this is overcomplicated?" If yes, simplify.

## 3. Surgical Changes

**Touch only what you must. Clean up only your own mess.**

When editing existing code:
- Don't "improve" adjacent code, comments, or formatting.
- Don't refactor things that aren't broken.
- Match existing style, even if you'd do it differently.
- If you notice unrelated dead code, mention it - don't delete it.

When your changes create orphans:
- Remove imports/variables/functions that YOUR changes made unused.
- Don't remove pre-existing dead code unless asked.

The test: Every changed line should trace directly to the user's request.

## 4. Goal-Driven Execution

**Define success criteria. Loop until verified.**

Transform tasks into verifiable goals:
- "Add validation" → "Write tests for invalid inputs, then make them pass"
- "Fix the bug" → "Write a test that reproduces it, then make it pass"
- "Refactor X" → "Ensure tests pass before and after"

For multi-step tasks, state a brief plan:
```
1. [Step] → verify: [check]
2. [Step] → verify: [check]
3. [Step] → verify: [check]
```

Strong success criteria let you loop independently. Weak criteria ("make it work") require constant clarification.

## 5. PR Title & Description

**A repo's own PR template always wins. Jira ticket is non-negotiable.**

Order of precedence:
1. If the repo has a PR template (e.g. `.github/PULL_REQUEST_TEMPLATE.md`, `.github/PULL_REQUEST_TEMPLATE/`, or `docs/`), follow it exactly. Check for one before drafting.
2. Otherwise, use the default structure below.

**Jira ticket (always required, regardless of template):**
- Every PR must reference its associated Jira ticket as a link at the top of the description (e.g. `[PROJ-123](https://<org>.atlassian.net/browse/PROJ-123)`). Do not put the ticket key in the title.
- If no ticket is known, ask the user for it before opening the PR.

**Title:** `<category>: <summary>`
- e.g. `fix: disable FF for ai-agents`
- Categories: `feat`, `fix`, `chore`, `refactor`, `docs`, `test`, `perf`, etc.

**Description** (when no repo template applies):
- **Summary** — human-readable, high-level: why this PR exists and how it works.
- **Description** — detailed breakdown/walkthrough (the kind genAI typically generates).
- **Testing** — checklist of how this was tested, or what should be tested further.

PR Etiquette: Always create PRs in DRAFT mode unless otherwise requested. Keep PR review comments to "med" and "high" findings, no "low" or NIT comments.

---

**These guidelines are working if:** fewer unnecessary changes in diffs, fewer rewrites due to overcomplication, and clarifying questions come before implementation rather than after mistakes.

