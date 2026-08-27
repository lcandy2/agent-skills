---
name: hidden-assumption-audit
description: |
  Audit code for decisions nobody made: places where the author (often an AI)
  faced an open question and silently answered it in code instead of asking.
  Six families: invented values (hardcoded timezones, locales, magic defaults),
  invented behavior (silent fallbacks, made-up failure handling), misplaced
  robustness (defense against the impossible while real failures go unhandled),
  invented structure (needless wrappers, premature abstraction, dead code),
  invented interpretation (ambiguous requirements resolved one way with no
  record, specified approaches silently swapped for simpler ones), and invented
  duplicates (re-answering questions the codebase already answered). Report
  only, never auto-fix; confirmed-intentional choices are recorded in a
  repo-root ASSUMPTIONS.md ledger and never re-asked.
  Use this whenever the user asks to review code for assumptions, hardcoded
  values, fallbacks, defensive bloat, over-engineering, or unnecessary nesting;
  says "会不会有问题 / 是不是写死了 / 逻辑对不对 / 这里为什么这么写"; after
  landing a large AI-written change; or when one suspicious pattern is spotted
  and the user wants to know what else was decided without them.
metadata:
  keywords: code review, hidden assumptions, hardcoded values, silent fallbacks, defensive code, over-engineering, AI-written code, ASSUMPTIONS.md
---

# Hidden assumption audit

Every finding this audit produces is the same event in a different costume:
**the code answers a question that was never asked.** Somewhere an author hit a
gap in what they knew, and instead of surfacing the question, they filled the
gap with a guess and kept typing. The guess might be a value, a behavior, a
guard, a layer of indirection, or a reading of an ambiguous request. The audit
finds the guesses and turns them back into questions.

Three rules frame the whole exercise:

1. **Report, never fix.** Whether a guess was right is the owner's call, not
   the auditor's. Produce findings; the user decides what changes.
2. **The repo outranks intuition.** Before reporting, hunt for evidence inside
   the project: the schema, sibling code, validators, docs. The strongest
   finding is "the project itself contradicts this guess". A pattern being
   *usually* bad is not evidence that it is bad here.
3. **Only the ledger settles a question.** A decision exists when the repo-root
   `ASSUMPTIONS.md` records it with a reason. Code comments, commit messages,
   and docs elsewhere do not settle anything; at most they point at a ledger
   entry. Everything else that looks decided is merely assumed, and assumed
   items go to the user as questions.

## The six families

Full recognition patterns live in `references/taxonomy.md`. Read it before
sweeping. The families, in one line each:

| Family | The silent answer | The question that was skipped |
|---|---|---|
| Invented values | a literal where a fact was needed: timezone, locale, limit, port, default | "what is this value really, and who says so?" |
| Invented behavior | a fallback or failure response the spec never mentioned | "what should actually happen when this is missing or fails?" |
| Misplaced robustness | guards where nothing can happen, nothing where failure is real | "can this case occur, and is this the right response to it?" |
| Invented structure | wrappers, layers, options, and dead code serving no current caller | "who asked for this?" |
| Invented interpretation | an ambiguous requirement implemented one way, or a specified approach quietly replaced | "did you mean this, or the other thing?" |
| Invented duplicates | a second answer to a question the codebase already answered | "did you know this already existed?" |

## Workflow

### 1. Scope

Default to the whole repository. A narrower scope (one package, one diff) is
fine when the user names it.

### 2. Read the ledger first

`ASSUMPTIONS.md` at the repository root is the exemption record. Every entry
is a decision already made: do not re-flag it, do not re-ask it. One exception:
if an entry's stated `Holds while` condition no longer holds, the exemption
has expired, and that is itself a finding.

Audit reports and process notes, if the user wants them kept, go under
`docs/`; they never substitute for ledger entries.

### 3. Sweep by reading, not by grepping

Review the code the way a careful human reviewer would: read every in-scope
file, with the six families as the lens. Pattern searches are a supplement
for breadth on a large repository, useful for surfacing candidate files, and
nothing more. A grep finds the literal `Asia/Shanghai`; only reading finds the
wrapper that swallows an error, the guard that can never fire, or the
interpretation that quietly narrowed a requirement.

On a large repository, work through it systematically (module by module), not
by sampling.

### 4. Verify each candidate

For every suspect, attempt two things:

- **A counter-example**: concrete input or state, and the wrong outcome it
  produces, in one or two sentences. For structure findings, the equivalent is
  a concrete cost: what a reader or the next change pays for the extra layer.
- **An evidence trail**: does the project itself contradict the guess (a field
  that already carries the hardcoded fact, a validator that makes the guard
  unreachable, a caller that never uses the flexibility)? Does anything
  support it?

A candidate where both come up empty is still listed, but in its own section,
clearly marked unverified. Suspicion is information; it is just not a verdict.

### 5. Sort into piles

- **Settled**: a ledger entry covers it, conditions intact. Skip, list under
  `Covered`.
- **Defect**: the counter-example contradicts something the project itself
  states, *or* it shows harm no intent could justify: a secret that falls back
  to a committed literal, a write that silently loses data, a check that admits
  what it exists to refuse. Nobody needs to be asked whether they meant that.
  Goes in the report as a finding.
- **Assumed**: plausible either way, and no ledger entry records a decision.
  The counter-example shows a *different* behavior, not a harmful one. These
  are exactly the questions that were skipped; they go to the user.
- **Unverified**: suspicion with no counter-example and no evidence either
  way. Listed, not asked.

### 6. Deliver the report, then ask

Finish the sweep and deliver the full report before asking anything: the user
rules better with the whole picture in front of them, and a scan of any size
should not arrive as a drip of interruptions.

Then take the `Open questions` section through the question tool
(AskUserQuestion or equivalent), batched, up to four per call, until the pile
is empty or the user stops. For each, offer:

- **Intended, record it**: append to the ledger; not a finding.
- **Not intended**: it stands as a finding.
- **Intended for now**: record in the ledger with the `Holds while` condition
  under which it must be revisited.

If the session cannot ask (a headless or background run), stop after the
report; the `Open questions` section already contains everything needed to
rule later.

### 7. Record what was confirmed

The ledger is the one file this audit writes. Create `ASSUMPTIONS.md` at the
repository root if it does not exist. One entry per confirmed assumption:

```markdown
## <kebab-slug>

- **Assumes**: the premise, in one sentence.
- **Where**: file, line, and function, precise enough to jump to
  (`src/accession.ts:217, autoLink`). Several sites, several lines.
- **Holds while**: the condition that keeps this acceptable.
- **Invalidated by**: the event that should reopen it.
- **Confirmed**: date, by whom, in what context.
```

Line numbers drift as files change; the function name is what keeps the entry
findable after a refactor. Both, not either.

The slug is the anchor. If the user wants code to carry a pointer, suggest a
one-line comment (`// assumption: <slug>, see ASSUMPTIONS.md`) in the report's
suggestions; do not add it yourself.

### 8. Report

ALWAYS use this structure:

```markdown
# Hidden assumption audit: <scope>

## Findings
Ordered by blast radius. One subsection each:
### <n>. [family] <one-line claim>
- **Where**: file:line, function
- **The silent answer**: what the code decided without asking
- **Why it is wrong**: the counter-example or the concrete cost, with the
  in-repo evidence woven in
- **Direction**: a sentence, not a patch

## Open questions
The assumed pile: same shape, minus the verdict. These get asked interactively
after the report is delivered; in a headless run they simply stay here.

## Unverified suspicions
One line each: location, the suspicion, why no counter-example was found.

## Covered
Already settled by the ledger, one line each with slug.
```

Ledger entries written after the asking round are reported as a short
addendum, one line each, rather than as a section written in advance.

## What not to report

Credibility is spent on every noisy finding. Do not report:

- Style and formatting preferences with no failure path and no reader cost.
- Assumptions that require the project to become a different project before
  they matter. The ledger's `Holds while` field exists for the honest version
  of this concern.
- Anything the ledger already covers, unless its conditions are violated.
- Internals of frameworks the project cannot change.

Test code is in scope, not excluded. Tests carry their own characteristic
assumptions: fixtures that hardcode a timezone or locale the CI machine
happens to share, cases that pass only in execution order, sleeps that bet on
timing, and assertions that restate the implementation instead of the
requirement. A test that assumes is a test that stops guarding.

One finding with a counter-example outweighs ten pattern matches. When the
report is long, that is usually a sign the verification step was skipped, not
a sign the code is that bad.
