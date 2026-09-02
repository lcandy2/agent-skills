# The eval loop

This is how Vercel turned a plausible draft into a file that measurably
works (their numbers: 39 named-pattern failures with the file versus 91
without, on matched runs). The loop is the method; the draft is just its
starting state.

## Choosing scenarios

Two or three, each meeting all four tests:

- **Recurring**: an artifact the org actually generates repeatedly. One-off
  pages teach one-off rules.
- **Real reader**: a person who would open it and decide something. "A demo
  page" has no reader, so nothing anchors hierarchy judgments.
- **Concrete inputs**: actual data, an actual customer shape, real copy.
  Lorem ipsum lets the agent skip every hard content decision, which is
  where brands actually diverge.
- **Different shapes**: if one scenario is evidence-heavy (a report), make
  another decision-heavy (a proposal) or tool-heavy (a calculator), so the
  file is not overfit to one composition.

Vercel's seven, for calibration: usage and performance report, renewal
proposal, benchmark report, interactive planning page, build-versus-buy
brief, security governance brief, presentation deck.

Freeze one more scenario than you will work with, and hide it: never review
its outputs while editing the file, run it once at the end. With only two or
three working scenarios, overfitting to them is the default failure, and the
holdout is the only cheap detector.

## Freezing

Pin each scenario as prompt + inputs + viewport, written down verbatim in
scenarios.md, together with a short rubric written before anything is
generated: did the supplied facts survive, is the reader's decision clear on
first read, did the corrections you keep making by hand actually get
resolved. The rubric predates the first run so scoring cannot drift toward
whatever the outputs happen to be good at. Frozen means nothing about the
scenario changes between runs;
the design.md is the only variable, so any output difference is attributable
to it. The moment you "improve the prompt a little" mid-loop, you can no
longer tell whether the file or the prompt caused the change.

## The loop

1. **Baseline.** Run each scenario with no design.md. Keep the outputs
   permanently; they are the control group for every future claim that the
   file works.
2. **Guided run.** Same scenario, design.md loaded.
3. **Score blind; review structure before styling.** Shuffle the guided
   and baseline outputs so the reviewer does not know which is which, and
   score both against the scenario's rubric before unblinding; knowing
   which page is yours is what feeds the failure mode of review, admiring
   nicer fonts. Then ask: does the guided page lead with a different thing
   than the baseline? Did sections merge, reorder, or
   disappear? Is evidence placed where the argument needs it? Vercel's
   first success signal was exactly this: the proposal restructured to lead
   with the recommendation, not that it got prettier.
4. **Encode each correction.** Phrase it as an observable behavior
   (a reviewer could check it on output without asking you), then place it
   with the triage tree from SKILL.md: judgment to prose, mechanics to the
   vocabulary, script-checkable failures to a deterministic check. The
   canonical example of the phrasing bar: not "make the table feel less
   cramped" but "an evidence table owns the full width of its section".
5. **Re-run the same frozen scenario.** The correction is encoded when the
   failure stops appearing on fresh first attempts, not when the rule reads
   well. A rule that fails re-run is almost always still a vibe; go back to
   step 4, not to the scenario.

Fresh first attempts, no retries: a rule that only works when the agent gets
three tries is not a rule the org can rely on.

Every stored run keeps its prompt, inputs, model and configuration, the
design.md version it used, the rendered output, and the feedback it got;
without the model and file version, a regression cannot be attributed to
anything. Run full rounds on at least two of the consumers the frontmatter
names. Different models read the same description differently, and closing
that gap is the reason the file exists.

## Measuring, honestly

When the user wants proof, run each scenario with and without the file,
fresh attempts, and count only failures the file names. Report it with the
caveats Vercel attached to their own numbers: the count covers known
failure modes only, small samples swing, and a page can pass every named
check and still not be shippable. Score these comparisons blind too, and let
the layer-3 deterministic checks do the counting where they exist; the
named-rejections list is the check list. The strong claim this supports is
narrow and useful: named and encoded failures tend to stay gone.

## scenarios.md format

Deliver beside the design.md:

```markdown
# Frozen scenarios for design.md

## 1. <scenario name>            <!-- mark the holdout scenario as such -->
- Reader: <who opens this and what they decide>
- Prompt: <verbatim>
- Inputs: <files / data, pinned>
- Viewport: <e.g. 1440x900 desktop>
- Rubric: <the 3-5 checks written before the first run>
- Models: <the consumers this runs on>
- Watch for: <the named failures this scenario tends to produce>
- Baseline: <path to the kept no-guidance output>
- Runs: <model + design.md version for each stored run>
```

## Maintenance

After shipping, corrections arrive as review comments, pull request notes,
and the chat threads where people steer the generators by hand, instead of
eval reviews. Same loop, longer period: collect them on a cadence, group the
repeats, triage each through the tree, and count per-complaint frequency.
After a rule lands, its complaint's count should fall; a count that holds
means the rule is still a vibe, or it landed in the wrong layer (usually
judgment that should have been a check).
