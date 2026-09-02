---
name: design-md-creator
description: |
  Create a design.md for a project or organization: a skill-formatted brand
  guidance file that teaches page-generating AI (v0, Claude artifacts, eve
  agents, in-repo coding agents) to produce reports, proposals, marketing
  and product pages that look and read like the brand made them. Modeled on
  Vercel's published design.md and, more importantly, on the eval loop they
  used to distill it. The workflow: mine the repo and brand material for
  tokens and voice, interview only for the gaps, draft against a proven
  ten-section skeleton (role, brand context, priority order, four-pass
  working method, named rejections, bounded token vocabulary, private
  inspection), then validate with frozen baseline-vs-guided runs and triage
  every correction into prose, stylesheet, or deterministic check. Use
  whenever the user wants AI-generated pages to be on-brand; asks to
  create, improve, or review a design.md, a design section of AGENTS.md,
  brand guidelines for agents, or a "design system prompt"; complains that
  generated pages look generic, templated, or AI-flavored (AI 味, 不像我们的
  品牌, 太像模板了); or asks how to teach v0, Claude, or Cursor their design
  language.
metadata:
  keywords: design.md, brand guidelines, on-brand pages, AI slop, design tokens, v0, Claude artifacts, agent design guidance, eval loop, frozen scenarios, Vercel, 品牌规范, 设计规范, AI 味
---

# Create a design.md

A design.md turns "make it on-brand" into decisions an agent can execute. It
is itself a skill: YAML frontmatter with a triggering description, then prose
that any page-generating agent can load. Vercel publishes theirs at
https://vercel.com/design.md; this skill exists because their approach
transfers, but only if you copy the process, not the file.

The one fact that shapes everything below: **a design.md is distilled, not
written.** Vercel's file is the residue of 200-plus evaluated runs. Its
sharpest rules ("Tables own the full evidence width of their section",
"never turn a savings figure green merely because it is favorable") were
human corrections on real generated pages, rewritten into observable
behaviors. A design.md drafted in one sitting and never run against
real generations is a guess wearing the costume of a standard. So spend
little time making the first draft beautiful and most of the time in Phase 3.

## The three layers and the triage rule

A working system has three layers. The design.md is only one of them:

1. **Prose** carries judgment: how to frame the reader, what hierarchy means
   here, which instincts to reject.
2. **A bounded vocabulary** carries mechanics: tokens, type roles, CSS
   classes. Numbers live here so agents cannot invent their own. A
   stylesheet also loads at render time, so its bytes never enter the
   model's context; the budget stays with judgment, and the design.md
   should pass the same instruction on to its consumers (use the published
   class list, never read the CSS implementation into context).
3. **Deterministic checks** carry the mechanical failures: things a script
   can verify on rendered output.

Two gates before recording anything, both from Vercel's triage: does the
correction generalize beyond the output it came from (a one-off nit earns no
rule), and what did you have to repeat or steer manually (repeated steering
is a missing rule announcing itself). Then walk this tree:

```
A rule or correction you want to encode:
├── Could a script verify it on the output? (overflow, missing alt text,
│   a table narrower than its section, an unknown class name)
│       → note it as a deterministic check; keep only the intent in prose
├── Is it a number, color, size, spacing value, font, or class name?
│       → it belongs in the token vocabulary; prose says only when to use it
└── Otherwise it is judgment
        → prose, written as an observable behavior (see Phase 2)
```

This matters because prose numbers drift: an agent told "use 24px section
gaps" invents 20px and 32px variants under pressure, while an agent told
"between-group gaps use --space-6 through --space-8" cannot. And judgment
pushed into a checklist dies: "make hierarchy clear" as a lint rule checks
nothing. Each kind of rule survives only in its own layer.

This skill produces layer 1 plus the frozen scenarios that validate it. If
the project has no token file yet, the design.md you draft defines a minimal
vocabulary inline and marks it as proposed; derive it from the computed
styles of shipped pages when any exist (the de facto palette, type scale,
spacing), because a vocabulary distilled from shipped pixels needs far less
confirmation than an invented one. Extracting it to CSS is a noted next
step, not a blocker.

## Phase 1: Gather

Read before asking. Interview time is expensive and everything already
written down is free:

- **Tokens and mechanics**: design token files, global CSS, theme files,
  component libraries, Tailwind config. This becomes the bounded vocabulary,
  so record exact names. Never rename or alias while collecting.
- **Voice**: existing brand or writing guidelines, then the marketing site,
  docs, and release notes as evidence of voice in practice. Collect five to
  ten phrases they actually publish and any words they visibly avoid.
- **Authorship furniture**: how existing pages open and close. Logo
  placement, header metadata, footer weight. Agents get these wrong first.
- **The artifact inventory**: which page types keep being generated
  (reports? proposals? changelogs? landing pages?). The design.md's
  frontmatter description must name these, because they are its triggers.
- **The correction stream**: the last ten or so corrections the org keeps
  giving, in design reviews, pull requests, and the chat threads where
  people already steer v0 or Claude by hand. Rewritten observably, this
  list alone is a first design.md (that is Vercel's own starting advice),
  and it seeds the org-specific half of the rejections list.

When sources disagree, shipped production outranks design files and brand
PDFs by default; propose that ranking and let the user confirm it. Design
files go stale while production is what the org actually signed, so voice
and authorship furniture come from live pages first.

Fetch only URLs the user gives or approves; do not crawl outward from them.

Then interview for gaps only, in batches of at most four questions, following
`references/interview.md`. Label every answer Explicit (stated by a source or
the user), Proposed (your inference awaiting confirmation), or Open. Only
Explicit material becomes a rule; Proposed material enters the draft clearly
marked. The labels exist because a design.md speaks with the brand's own
authority, and an inferred rule stated confidently is indistinguishable from
a real one until it misleads an agent.

Two answers you must have before drafting, because they change the file's
shape:

- **Who consumes it.** External agents (v0, Claude artifacts, eve) cannot
  read the repo: the file must be self-contained and every asset it names
  must be a public URL. In-repo agents can be pointed at repo paths. If both,
  write for external and let repo paths be an explicitly marked alternative.
- **What decides conflicts.** When on-brand fights readability, or supplied
  facts fight visual polish, which wins? This becomes the priority-order
  section, and without it agents resolve conflicts differently every run.

## Phase 2: Draft

Draft against the ten-section skeleton in `references/skeleton.md`. Read it
before writing; it is the anatomy of Vercel's file with the reasoning for
each section and a starter rejection list. The skeleton is a checklist of
questions the file must answer, not a template to fill with boilerplate: a
section that would only hold generic advice ("use whitespace well") should
be omitted until the org has something real to say there.

Writing rules for the file itself:

- **Observable, never vibes.** Every rule must be checkable by a reviewer
  looking at output. "Tables feel less cramped" fails this test; "an
  evidence table owns the full width of its section" passes. If you cannot
  phrase the rule observably, you have not yet understood the correction it
  came from; go look at the failing output again.
- **Why on every rule that could be misapplied.** Bare rules get applied
  blindly where they should not be. "Use color only when it encodes
  meaning, because a favorable number tinted green reads as advocacy and
  undermines the evidence" travels to cases you never wrote down.
- **Negative space is half the file.** Name the failure patterns this brand
  never wants to see, specifically enough that an agent recognizes them in
  its own draft. Then add the counterweight sentence: avoiding slop must not
  collapse into a sterile anti-design of thin rules and empty margins.
  Seed from the universal list in the skeleton, then grow it in Phase 3;
  named failures are the part of the file the eval loop writes for you.
- **The vocabulary is closed.** List the tokens and classes agents may use,
  say they are the only ones, and forbid inventing, aliasing, or
  extrapolating names. An open vocabulary is how every generated page ships
  its own private design system.
- **The frontmatter description is the trigger.** Name the artifact types
  from Phase 1 the way a user would ask for them. A design.md that never
  loads teaches nothing.
- **One page-length test.** Vercel covers a full brand system in 369 lines.
  If the draft passes 400, it is repeating itself or hoarding mechanics that
  belong in layer 2.

## Phase 3: Validate

This phase is the method. Follow `references/eval-loop.md`. Compressed:

1. **Freeze two or three scenarios, plus one hidden holdout.** Each is a
   real, recurring artifact with a real reader and concrete inputs (actual
   data, actual customer shape), pinned as prompt + inputs + viewport, with
   a short rubric written before anything is generated: the supplied facts
   survived, the reader's decision is clear, the corrections you keep
   making by hand got resolved. The holdout is never reviewed mid-loop and
   runs once at the end, to catch a file overfit to its working scenarios.
   Frozen means the only variable across runs is the design.md, so every
   output change is attributable to it.
2. **Run the baseline first**: each scenario without the design.md, outputs
   kept. Ugly baselines are the point; they are what the file is for, and
   later they prove whether it works.
3. **Run with the design.md, then score blind: structure, not styling.**
   Shuffle guided and baseline outputs and grade both against the rubric
   before learning which is which; knowing which page is yours is how
   reviewers end up admiring fonts. The file is failing if the guided page
   is merely the baseline with nicer typography. It is working when the
   page leads with a different thing, orders evidence differently, and
   drops sections the baseline padded. Record the model and design.md
   version on every stored run, and run rounds on at least two of the
   consumers the frontmatter names: different models read the same
   description differently, which is the gap the file exists to close.
4. **Turn every correction into a rule via the triage tree**, phrased
   observably, placed in its layer. Then re-run the scenario. A correction
   that does not survive a re-run is not yet encoded; usually the phrasing
   is still a vibe.
5. **Deliver the scenarios with the file** (a scenarios.md beside the
   design.md): name, reader, frozen prompt, inputs, and the named failures
   to watch for. They are the file's test suite; without them the next
   person editing it is guessing again.

## Phase 4: Ship and maintain

- **Approval.** The file speaks with the brand's authority, so the named
  owner explicitly approves it before it ships; corrections and partial
  agreement are not approval. Confirm the org has the right to publish
  everything captured into it, and keep confidential guidance on a private
  URL or repo.
- **Placement: one canonical skill, aliases everywhere else.** The file is
  already skill-formatted, so the canonical copy lives as a skill
  (`.claude/skills/<org>-brand-guidelines/SKILL.md`, scenarios.md beside
  it) and every other surface is a view of it: a symlink at the repo root
  `design.md` for in-repo agents, referenced from AGENTS.md or CLAUDE.md
  so agents that do not load skills still find it; and a published copy at
  a stable public URL, conventionally `<domain>/design.md`, for external
  consumers. Publishing needs a copy or build step, not a symlink (GitHub
  raw and most hosts serve a symlink as the path text). Two hand-edited
  versions will drift, and an agent will find the drift first. The dual
  life is also why the guidance stays in one self-contained file that
  never leans on a references/ directory: a URL fetch cannot follow it.
  Vercel's file handles both identities in one line worth copying:
  "Resolve the asset from this skill's location. If the skill was opened
  from a URL, resolve the asset against that original URL." Assets on
  public URLs, stylesheet linked not inlined, everything else inline.
- **Feedback loop.** Corrections keep arriving: review comments, pull
  request notes, and the chat threads where people steer the generators by
  hand. Collect them on a cadence, group the ones that repeat, and triage
  each through the same tree into prose, vocabulary, or check. The metric
  is per-complaint frequency: after a rule lands, its complaint's count
  should fall; a count that holds means the rule is still a vibe. The
  named-rejections list doubles as the layer-3 check list, which is also
  what keeps the counting cheap. Vercel's phrasing of the success
  condition: once a failure is named and encoded, it tends to stay gone.

## Deliverables checklist

- `design.md`: frontmatter (name, triggering description) + the sections
  from the skeleton that had real content, under ~400 lines.
- Delivery structure: the canonical copy as a skill directory; the repo
  root `design.md` and any public URL are aliases or build-step copies of
  it, never separately edited files.
- `scenarios.md`: 2-3 frozen scenarios plus one hidden holdout, each with
  its rubric; baseline outputs kept.
- Noted next steps for layers 2 and 3 (token extraction, deterministic
  checks) if they do not exist yet.
- Everything Proposed still marked Proposed, with the owner named who can
  confirm it.
