# hidden-assumption-audit

One of the skills in [lcandy2/agent-skills](https://github.com/lcandy2/agent-skills), for Claude Code and any other agent that reads `SKILL.md`. The skill itself is [SKILL.md](SKILL.md); this page is for people.

## Install

With the [skills CLI](https://www.skills.sh/docs):

```bash
npx skills add lcandy2/agent-skills --skill hidden-assumption-audit
```

`-g` installs for the user instead of the current project.

## What it does

Audit code for decisions nobody made: places where the author (often an AI) faced an open question and silently answered it in code instead of asking. Six families: invented values (hardcoded timezones, locales, magic defaults), invented behavior (silent fallbacks, made-up failure handling), misplaced robustness (defense against the impossible while real failures go unhandled), invented structure (needless wrappers, premature abstraction, dead code), invented interpretation (ambiguous requirements resolved one way with no record, specified approaches silently swapped for simpler ones), and invented duplicates (re-answering questions the codebase already answered). Report only, never auto-fix; confirmed-intentional choices are recorded in a repo-root ASSUMPTIONS.md ledger and never re-asked. Use this whenever the user asks to review code for assumptions, hardcoded values, fallbacks, defensive bloat, over-engineering, or unnecessary nesting; says "会不会有问题 / 是不是写死了 / 逻辑对不对 / 这里为什么这么写"; after landing a large AI-written change; or when one suspicious pattern is spotted and the user wants to know what else was decided without them.

## Keywords

code review, hidden assumptions, hardcoded values, silent fallbacks, defensive code, over-engineering, AI-written code, ASSUMPTIONS.md
