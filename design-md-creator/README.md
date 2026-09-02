# design-md-creator

One of the skills in [lcandy2/agent-skills](https://github.com/lcandy2/agent-skills), for Claude Code and any other agent that reads `SKILL.md`. The skill itself is [SKILL.md](SKILL.md); this page is for people.

## Install

With the [skills CLI](https://www.skills.sh/docs):

```bash
npx skills add lcandy2/agent-skills --skill design-md-creator
```

`-g` installs for the user instead of the current project.

## What it does

Create a design.md for a project or organization: a skill-formatted brand guidance file that teaches page-generating AI (v0, Claude artifacts, eve agents, in-repo coding agents) to produce reports, proposals, marketing and product pages that look and read like the brand made them. Modeled on Vercel's published design.md and, more importantly, on the eval loop they used to distill it. The workflow: mine the repo and brand material for tokens and voice, interview only for the gaps, draft against a proven ten-section skeleton (role, brand context, priority order, four-pass working method, named rejections, bounded token vocabulary, private inspection), then validate with frozen baseline-vs-guided runs and triage every correction into prose, stylesheet, or deterministic check. Use whenever the user wants AI-generated pages to be on-brand; asks to create, improve, or review a design.md, a design section of AGENTS.md, brand guidelines for agents, or a "design system prompt"; complains that generated pages look generic, templated, or AI-flavored (AI 味, 不像我们的 品牌, 太像模板了); or asks how to teach v0, Claude, or Cursor their design language.

## Keywords

design.md, brand guidelines, on-brand pages, AI slop, design tokens, v0, Claude artifacts, agent design guidance, eval loop, frozen scenarios, Vercel, 品牌规范, 设计规范, AI 味
