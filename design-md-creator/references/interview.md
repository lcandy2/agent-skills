# Interviewing for the gaps

Adapted from Vercel's BOOTSTRAP.md workflow (vercel-labs/eve-design-template),
trimmed to what a design.md needs. Run this only after Phase 1 mining; every
question already answered by a source you read is a question you may not ask.

## Ground rules

- At most four related questions per message. A wall of questions gets
  skimmed answers, and skimmed answers become confident wrong rules.
- Label every answer as you record it:
  - **Explicit**: stated by an approved source or by the user.
  - **Proposed**: your inference, awaiting confirmation.
  - **Open**: unresolved, deliberately.
  Only Explicit material becomes an unmarked rule in the design.md.
- Treat interview answers as source material: read your record back for
  confirmation before building on it.
- Offer to stop early. A small confirmed corpus beats a large inferred one;
  scope, principles, and unknowns are enough to draft from, and Phase 3
  will surface what is actually missing.

## Topics, in order

### Scope

- Which artifact types keep being generated, and for whom?
- What is explicitly out of scope for this file?
- Who owns final design decisions (the person who confirms Proposed items)?

### Principles

- Voice in adjectives, and what those adjectives must never come from.
- Which existing pages or products are the reference for "looks like us",
  and what specifically makes them so?
- Which patterns should the agent always reject? (Seeds section 7.)
- When on-brand fights clarity, which wins? (Seeds the priority order.)

### Foundations

- Where do canonical tokens live? Which file wins if two disagree?
- Accessibility requirements beyond the WCAG AA floor?
- Typography: which faces, and what is each one for?
- Color policy: what may carry color, and what must stay neutral?

### Content and voice

- Terms the brand always uses, and terms it bans.
- Casing convention for headings and labels.
- How are errors, caveats, and unknowns worded on real pages?

### Unknowns

- When the file is silent, may the agent apply clearly labeled general
  design judgment, or must it stop and ask?
- Which gaps should stay open on purpose?
- Who resolves conflicts the priority order does not cover?

## Conflicts between sources

Do not merge conflicting guidance. Ask the user to rank the sources once,
early, and then apply the higher-ranked source throughout. Propose shipped
production above design files and brand PDFs as the default ranking: design
files go stale, production is what the org actually signed. If two sources of
equal rank disagree, record both positions in the draft and mark the rule
Open; a design.md that silently picked a side will be "corrected" back and
forth forever.
