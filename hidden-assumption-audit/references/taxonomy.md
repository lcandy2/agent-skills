# The taxonomy: six families of decisions nobody made

Every pattern here is a place where an author faced an open question and
answered it silently in code. The families group the patterns by *what kind of
thing was invented*. Recognition signs are starting points, not verdicts: each
hit still goes through verification (counter-example, evidence hunt) before it
is anything.

While reading code, the one question to keep asking: **"who decided this?"**
If the answer is "nobody, it is just what got typed", the line belongs to one
of these families.

## Family 1: Invented values

A literal stands where a fact was needed. The author needed to know something
about the world (which timezone, which locale, how many, how big, how long)
and substituted a plausible constant.

Recognition signs:

- Literal region, zone, locale, currency, or language anywhere behavior
  depends on it.
- Numeric limits, caps, timeouts, retry counts, TTLs, and sizes with no
  comment saying where the number came from. `60`, `200`, `15000`: chosen or
  copied?
- Defaults for configuration that were never confirmed (`?? 8080`,
  `?? "en-US"`, `?? "UTC"`).
- Formats assumed rather than known: date layouts, ID shapes, path
  separators, encodings, epoch units (seconds vs milliseconds).
- Bare numbers whose unit or base lives only in the author's head: ms or s,
  cents or units, 0-based or 1-based, percent as 0.5 or 50. Two identifiers of
  the same primitive type that can be swapped and still compile.

The sharpest verification: search the project for a field, config, or schema
that already carries the fact the literal hardcodes. Data that contradicts the
constant upgrades the finding from "inflexible" to "ignores its own data".

## Family 2: Invented behavior

The spec described the happy path; the code needed a decision about the other
paths, and the author made one up. Fallbacks, degradation, retries, ordering,
and "reasonable" responses to absence are all behavior, and behavior belongs
to the owner.

Recognition signs:

- Silent fallbacks: `?? someDefault`, `|| fallback`, `.catch(() => value)`.
  For each one, ask: if this branch runs in production, should anyone find
  out? A fallback that masks a missing secret, config, or connection makes the
  system look healthy while being wrong.
- Failure handling nobody specified: retry policies, backoff choices,
  partial-write recovery, "skip and continue" loops. Each is a policy; where
  was it decided?
- Silent data repair: trimming, clamping, coercing, deduplicating, or
  reordering input the caller never agreed to have altered.
- Empty-state meanings chosen unilaterally: empty array treated as "all",
  null treated as "unlimited", missing field treated as "false".
- Unobservable fallbacks: nothing outside the function can tell whether the
  primary path ran or the fallback did. A benchmark, a prototype evaluation,
  or a health check that cannot distinguish the two is measuring nothing.
- Time, ordering, and equality semantics decided by implementation accident:
  which timestamp wins a tie, whether a comparison is case-sensitive, whether
  "first" means first-inserted or first-sorted.
- Cross-boundary optimism: trusting inbound headers, assuming the other side
  validated, assuming a private network stays private, assuming one instance
  and no concurrent writer. Each of these is a behavior decision about whose
  job safety is.

## Family 3: Misplaced robustness

Defensive code is a claim about what can happen, and AI-written code gets the
claim wrong in both directions at once: guards pile up where nothing can
happen, while the calls that genuinely fail (network, parse, disk) proceed
with no failure path at all. Defense against the impossible is not free: every
unreachable guard eventually acquires behavior of its own, and every catch
that converts a crash into a quiet default converts a loud bug into a silent
one.

Recognition signs:

- Guards on conditions the types or upstream validation already exclude: null
  checks after a validator guaranteed presence, `Array.isArray` on a typed
  parameter, re-validation at every layer with slightly different rules (which
  layer is authoritative?).
- Catch-all handlers that return defaults: `try { ... } catch { return [] }`.
  The bug still happens; now it happens invisibly.
- Optional chaining stacked through shapes that are guaranteed
  (`a?.b?.c?.d`): it documents distrust of the project's own types and hides
  real absence when it occurs.
- Branches unreachable by any current caller, kept "just in case".
- Swallowed errors on write paths, where the one thing that must not happen
  is pretending success.
- The mirror image, absent robustness: an external call, parse, or
  file read with no failure handling anywhere, in code otherwise dense with
  null checks. The defense landed where it was easy, not where it was needed.

The verification question is always the pair: **can this case occur?** If no,
the guard is noise with a future. If yes, **is the invented response the right
one**, or did the author just pick something so the function would compile?

## Family 4: Invented structure

Indirection, abstraction, and flexibility are answers to questions about the
future. When no one asked those questions, the layers are guesses, and every
layer is a place intent drifts and a place every reader must visit.

Recognition signs:

- Wrappers that add a name and nothing else, especially chains of them
  (`loadData` calling `getData` calling `fetchData` calling `fetch`).
- Functions with exactly one caller, whose body would read better inlined.
- Options objects where one field is ever set; flags never passed as anything
  but the default; parameters no caller supplies.
- Abstraction built "for reuse" with a single concrete use, or generics with
  one instantiation.
- Layers that only forward arguments downward and results upward.
- Helper hierarchies deeper than the logic they organize.
- Residue of abandoned attempts: exports nothing imports, flags nothing sets,
  branches for an approach that was replaced mid-session.
- Comments that narrate syntax instead of recording intent; they are the
  prose form of the wrapper that adds a name and nothing else.

The verification is mechanical: imagine the layer deleted and its body
inlined. If nothing got worse, the layer was a decision nobody made. The cost
side of the report entry is concrete: what a reader traverses, what a change
must touch twice, what the indirection lets silently diverge.

## Family 5: Invented interpretation

The request was ambiguous; the code is specific. Somewhere between the two, a
reading was chosen, and nothing records that another reading existed. This is
the family the user most cares about with AI-written code: "assume 我的意思是
某种方式但不确定，也没有提问".

Recognition signs:

- A requirement with two reasonable readings, implemented as one, with no
  comment, no question in the history, no ledger entry. "Sort by date":
  ascending or descending? "Latest": by creation or by update?
- Boundary semantics chosen silently: inclusive or exclusive ranges,
  tie-breaking order, what happens at exactly the limit.
- Scope narrowing that was never announced: the request said "all", the code
  handles the common case; the request named a behavior, the code implements
  "close enough".
- Extra features nobody requested, shipped alongside what was asked, as if
  agreed.
- Terminology drift: the request's words and the code's names disagree,
  suggesting the implementation went somewhere the request did not point.
- Approach substitution: the request named a method or algorithm, and behind
  an innocuous condition sits a much simpler stand-in that actually runs.

Verification here is the asking flow itself: these findings convert directly
into questions ("did you mean X or Y?"), and confirmed answers convert into
ledger entries. The audit exists to ask, late, what should have been asked at
writing time.

## Family 6: Invented duplicates

The codebase already answered this question; the new code answers it again,
usually slightly differently, because the author could not see or did not look
for the first answer. Two answers to one question always eventually disagree.

Recognition signs:

- A helper functionally identical to an existing one, under a different name,
  sometimes in the same file.
- Validation or normalization re-implemented at a second site with subtly
  different rules; which one is authoritative is now undecided.
- Types or shapes hand-copied from another module or service instead of
  imported, free to drift from the original.
- The same policy constant (a limit, a timeout, a format) declared in more
  than one place with more than one value.
- Near-identical blocks pasted and tweaked where a parameter would have done.

Verification is a search: find the earlier answer, put the two side by side,
and show where they already disagree or soon will.

## Cross-cutting lenses

Not families of their own; sharpeners that apply across all five. Use them
when the code's domain touches them:

- **Time**: day boundaries, DST, calendar arithmetic, mixed epoch units,
  wall-clock vs monotonic, "now" read more than once in one operation.
- **Text**: length as bytes vs code points vs graphemes, case folding
  surprises, normalization, truncation splitting characters.
- **Numbers**: floats for money, integer range past 2^53 in languages with
  one number type, rounding direction, division by zero.
- **Concurrency**: check-then-act gaps, non-idempotent retries, in-memory
  state in anything that replicates, one dedup path guarded while a sibling
  path is not.
- **Scale**: unbounded queries and arrays, offset pagination on growing data,
  limits that make part of the collection permanently unreachable.
- **Staleness**: creation time used where change time is meant, config read
  once in long-lived processes, caches shared across things that do not share
  memory.
- **Dependencies**: semantics assumed of third-party calls (synchronous,
  retrying, thread-safe, sorted output), deprecated usage carried in from old
  training data, methods that sound right for the library but do not exist in
  the installed version.
