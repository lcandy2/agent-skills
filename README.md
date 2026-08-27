# agent-skills

Skills for Claude Code and any other agent that reads `SKILL.md`. One directory per skill.

This repository is a mirror. The source is a private repo; a GitHub Action copies the skills marked public there into this one on every push, and each commit here names the upstream commit it mirrors. Nothing is edited by hand. Pull requests are welcome: they get applied upstream and arrive here with the next sync.

## Skills

- [hidden-assumption-audit](hidden-assumption-audit/SKILL.md): finds the decisions nobody made. Hardcoded timezones and magic defaults, silent fallbacks, defense against the impossible, needless wrappers, requirements resolved one way with no record, questions the codebase had already answered. Report only, never auto-fix; choices confirmed as intentional go into an `ASSUMPTIONS.md` ledger and are never asked again.
- [general-writing-style](general-writing-style/SKILL.md): Soleil's writing voice for English and Chinese prose, from READMEs to release notes to UI copy. Five hard bans (em-dash narration, the middle dot, pluralized Apple product names, small all-caps labels, unanchored adjectives), the sentence patterns behind the voice, and one substance rule: every claim traces back to a real source.

## Install

Clone, then symlink the skill you want into your agent's skill directory:

```bash
git clone https://github.com/lcandy2/agent-skills.git
ln -s "$(pwd)/agent-skills/hidden-assumption-audit" ~/.claude/skills/hidden-assumption-audit
```

Claude Code reads `~/.claude/skills`; other agents have their own directory, for example `~/.agents/skills`.
