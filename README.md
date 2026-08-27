# agent-skills

Skills for Claude Code and any other agent that reads `SKILL.md`. One directory per skill.

This repository is a mirror. The source is a private repo; a GitHub Action copies the skills marked public there into this one on every push, and each commit here names the upstream commit it mirrors. Nothing is edited by hand, this file included. Pull requests are welcome: they get applied upstream and arrive here with the next sync.

## Install

With the [skills CLI](https://www.skills.sh/docs):

```bash
npx skills add lcandy2/agent-skills
```

`--skill general-writing-style` takes one skill instead of all of them, `-g` installs for the user instead of the current project, and `--list` shows what is here without installing anything.

## Skills

| Skill | Keywords |
| --- | --- |
| [general-writing-style](general-writing-style/SKILL.md) | writing style, English, Chinese, em-dash, middle dot, Apple product names, README, release notes, UI copy, copywriting, AI writing signs |
| [hidden-assumption-audit](hidden-assumption-audit/SKILL.md) | code review, hidden assumptions, hardcoded values, silent fallbacks, defensive code, over-engineering, AI-written code, ASSUMPTIONS.md |

## Skill descriptions

### general-writing-style

Soleil (citron)'s general writing and expression style, for any text written by them or on their behalf, in English or Chinese: documents, READMEs, articles, release notes, announcements, bios, emails, PR descriptions, UI copy, social posts, presentation text. Not tied to any one project. Apply it whenever producing prose the user will sign or ship, even when they don't mention style; several rules are hard bans (em-dash narration, the middle dot, pluralized Apple product names, chatbot openers) that they enforce everywhere, and the text must not read as machine-written.

### hidden-assumption-audit

Audit code for decisions nobody made: places where the author (often an AI) faced an open question and silently answered it in code instead of asking. Six families: invented values (hardcoded timezones, locales, magic defaults), invented behavior (silent fallbacks, made-up failure handling), misplaced robustness (defense against the impossible while real failures go unhandled), invented structure (needless wrappers, premature abstraction, dead code), invented interpretation (ambiguous requirements resolved one way with no record, specified approaches silently swapped for simpler ones), and invented duplicates (re-answering questions the codebase already answered). Report only, never auto-fix; confirmed-intentional choices are recorded in a repo-root ASSUMPTIONS.md ledger and never re-asked. Use this whenever the user asks to review code for assumptions, hardcoded values, fallbacks, defensive bloat, over-engineering, or unnecessary nesting; says "会不会有问题 / 是不是写死了 / 逻辑对不对 / 这里为什么这么写"; after landing a large AI-written change; or when one suspicious pattern is spotted and the user wants to know what else was decided without them.
