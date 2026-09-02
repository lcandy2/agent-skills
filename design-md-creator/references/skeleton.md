# The ten-section skeleton

This is the anatomy of Vercel's design.md (https://vercel.com/design.md,
369 lines), generalized so any org can be poured into it. For each section:
what it does, why it exists, and what to write. Sections are ordered as they
appear in the file. Omit a section rather than fill it with boilerplate; a
generic sentence teaches nothing and costs trust in the specific ones.

Throughout, "the agent" means the page-generating agent that will load the
finished design.md, not you.

## 1. Frontmatter

```yaml
---
name: <org>-brand-guidelines
description: "Design, build, or substantially improve <the artifact types
  from Phase 1, named the way users ask for them>."
---
```

The description is the only part of the file most agent harnesses always see,
so it carries the entire triggering burden. Vercel's names eight artifact
types explicitly (reports, proposals, briefs, benchmarks, comparisons,
narrative data pages, calculators, decision pages). Name the org's real ones;
"any design work" triggers on nothing.

## 2. Role framing

One or two sentences that cast the agent as a specific senior practitioner
and state the job at the right altitude. Vercel's:

> Act as an excellent Vercel designer, editor, information architect, data
> storyteller, and design engineer. Turn the available material into an
> official Vercel-authored website. Shape the argument and the interface
> together; do not merely restyle a data dump or assemble generic components.

The load-bearing part is the last clause: it defines the failure mode (a
restyled data dump) in the same breath as the role. Write the org's version
of that clause.

## 3. Brand context

Three things, each a short paragraph:

- **Voice adjectives, with their negations.** Vercel: "precise, calm,
  direct, technically literate, evidence-led, editorial, and restrained",
  immediately followed by what confidence must never come from ("hype,
  decoration, novelty, false certainty"). The negation is what makes
  adjectives executable; every brand claims "clean and modern".
- **Who reads the output and what they are trying to decide.** This is what
  lets the agent make hierarchy decisions on its own.
- **The core stance.** Vercel's is "start with the reader's job, not the
  document category". Find the org's one organizing conviction. If the
  interview surfaced none, leave this out rather than inventing one.

## 4. Priority order

A numbered list resolving conflicts when requirements compete, plus the rule
for when the agent may stop and ask versus proceed. Vercel's order: supplied
facts > caller's framework > reader clarity > brand authorship > composition
specificity > detail refinement. And the asking rule: ask once, as one
grouped set of questions, and only when proceeding could change commercial,
legal, or factual meaning; otherwise label the unknown honestly and
continue.

This section exists because without it, conflicts get resolved differently
every run, and the agent either stalls on questions or silently invents
facts. It is usually the highest-leverage twenty lines in the file.

## 5. Integration with the host project

How the file's guidance meets an existing codebase: preserve the host
framework and routes, where the stylesheet or tokens resolve from (public
URL for external agents, repo path for internal), what happens when loading
fails, and a network allowlist (which third-party assets, if any, are
permitted). The file typically lives a dual life, loaded as a skill by some
agents and fetched from a URL by others; Vercel handles it in one sentence
worth copying: resolve the asset from this skill's location, and if the
skill was opened from a URL, resolve against that original URL. Vercel forbids adding chart libraries, icon kits, and analytics
without authorization; most orgs should too, because dependencies are where
generated pages sneak in foreign design systems.

## 6. Working method

The largest section: a fixed sequence of passes the agent walks every time.
Vercel's four passes generalize well; keep the sequence even if the content
differs:

1. **Frame the reader's job** before designing: who opens this, what they
   must decide, the strongest supported answer, the caveat that could change
   it. Include the org's honesty rules here (Vercel: support an executive
   reading path and an audit path; simplify language, never the claim;
   never let a precise test condition become a broader human claim).
2. **Choose the composition.** The transferable move: privately name the
   obvious layout the artifact category suggests, then reject it unless the
   material earns it. When the material admits multiple structures, compare
   two materially different composition hypotheses before coding, differing
   in topology and evidence placement, not merely palette. Map data to geometry before picking components
   (magnitude to length, change to position, composition to proportion).
   Two cheap self-tests worth copying verbatim: the squint test (at a
   glance, is the dominant claim obvious?) and the text-mask test (with
   words blurred, does hierarchy still communicate?).
3. **Apply the visual system.** Open with the authorship shell: where the
   wordmark and logo sit, the little metadata the header may carry (Vercel
   caps it at two sourced fields), and the stable asset URLs that render
   them. This is where Phase 1's authorship furniture lands, and it is the
   block agents get wrong first. Then the org-specific mechanics: grid,
   type roles, color policy, spacing rhythm, evidence rules for tables and
   charts, motion policy. Reference the bounded vocabulary of section 8;
   this prose says when, the vocabulary says what. If the org has no
   system yet, state the smallest one that matches their existing pages
   and mark it Proposed.
4. **Inspect privately, deliver only the work.** An ordered self-review
   (Vercel's order: first read, language, composition, typography,
   evidence, restraint, themes, accessibility) ending with an instruction
   that the critique stays internal. Without that instruction, agents ship
   a self-congratulatory audit appendix with every page.

## 7. Named rejections

The section evals write. List the failure patterns this brand never wants,
concretely enough that an agent recognizes them in its own draft. Seed it
twice: first from the org's own correction stream gathered in Phase 1 (those
carry the most authority, being things reviewers actually keep deleting),
then from the universal list below (all from Vercel's file, all generic
AI-generation reflexes). Delete what does not apply, and let Phase 3
corrections grow it:

- All-caps or letterspaced eyebrows, kickers, and decorative section numbers.
- Decorative gradients, glows, blobs, glass effects, textures, fake depth.
- A centered hero followed by a grid of cards.
- Repeated metric boxes where one composed relationship would be clearer.
- Badges and pills wrapping ordinary metadata.
- Cards nested inside cards; borders used to repair weak hierarchy.
- Icon tiles, oversized icons, mixed icon styles, icons as decoration.
- Tiny muted prose; arbitrary font sizes; misaligned peer values.
- A narrow table floating in a wide section, or a wide table crushed into
  broken words.
- Charts that decorate rather than prove; legends where direct labels fit;
  color without encoded meaning.
- Identical section silhouettes regardless of content.
- Summary, rationale, and conclusion sections that restate each other.
- Narrating the authoring process on the page.

Close the section with the counterweight, which Vercel learned to need:
avoiding these must not produce a sterile anti-design. State what the
brand's restraint positively is (for Vercel: precise hierarchy, excellent
typography, deliberate tension), so the agent has somewhere to go after
deleting the slop.

## 8. Bounded vocabulary

The closed list of what the agent may use: token names by family (surfaces,
text, borders, data colors, spacing, type sizes and weights), CSS classes
or components by group, and the closure rules. The three rules that make it
closed, worth adapting nearly verbatim:

- Use exact published names; never invent, alias, or redeclare a token.
- Never extrapolate a name from a pattern (Vercel's example: seeing
  `vbg-series-fill` and `vbg-series-1` does not license `vbg-series-fill-1`).
- When nothing fits, use a clearly namespaced escape hatch
  (`<prefix>-custom-*`) rather than guessing at private names.

List names only, not values; values live in the CSS, and the file should
say so the way Vercel's does: use the public API, "do not read the
stylesheet implementation into context". The stylesheet loads when the page
renders, so its bytes never cost model context; that saving is the point of
keeping mechanics in layer 2. If the org has no tokens yet, define the
minimal set inline (mark Proposed) and note extraction to a stylesheet as
the layer-2 next step.

## 9. Accessibility and responsive floor

Short and non-negotiable: semantic HTML, landmarks, one h1, ordered
headings, visible focus, WCAG AA contrast, never color alone, reflow
without horizontal overflow, readable type at every width. This section is
brand-independent; its presence in the file is what makes it enforceable in
review ("the design.md says").

## 10. The closing line

One sentence naming the target. Vercel's: "The target is Vercel judgment,
not Vercel decoration." It reads as garnish but functions as a tiebreaker
the agent can apply when no specific rule matches. Write the org's version;
if section 3 found the core stance, this line restates it as an instruction.
(In Vercel's file it closes the final section rather than owning a heading;
the placement is free, the presence is not.)
