# TODOS

## Framework Extraction (P2, after SD coach improvements complete)

**What:** Extract domain-independent teaching patterns (marked with `<!-- FRAMEWORK: Reusable -->` comments) from SD coach into a reusable `teaching-framework/` directory.

**Why:** User plans to build LeetCode coach and Go language coach. Shared patterns: Feynman Gate, Phase Gates, progress tracking, tiered scoring, session breakpoints, mistake registry.

**When:** After SD coach improvements are stable and tested. Start when building the second skill.

**How:** Find all `<!-- FRAMEWORK: Reusable -->` markers in SKILL.md and references/. Extract those sections into `teaching-framework/` with placeholder slots for domain-specific content.

**Depends on:** All CEO review improvements complete + eval passing.
