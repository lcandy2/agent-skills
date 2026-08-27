---
name: general-writing-style
description: |
  Soleil (citron)'s general writing and expression style, for any text written by
  them or on their behalf, in English or Chinese: documents, READMEs, articles,
  release notes, announcements, bios, emails, PR descriptions, UI copy, social
  posts, presentation text. Not tied to any one project. Apply it whenever
  producing prose the user will sign or ship, even when they don't mention style —
  several rules are hard bans (em-dash narration, the middle dot, pluralized Apple
  product names) that they enforce everywhere.
---

# Soleil's writing style

How to write so it reads like Soleil wrote it, regardless of the project or medium.
The voice in one sentence: quiet confidence, carried by concrete nouns and small
words, with zero typographic decoration. Every rule below was confirmed by the user
item by item; treat the bans as settled law, not taste suggestions.

## Hard bans

Violating these means the text comes back.

1. **No em-dash narration.** Never use 「——」 or "—" as a thought-break or aside.
   Restructure with a colon, a semicolon, a comma, or a separate sentence. The en
   dash in numeric ranges ("13:40–15:12", "2019–2024") is fine. Code comments are
   exempt.

2. **No middle dot 「·」 anywhere.** Not in titles, bylines, footers, lists, or
   metadata. Separate with commas ("Soleil Chao, Design Engineer"), with "at"
   ("Cosmos at Photon"), or with a plain hyphen.

3. **Apple product names never take a plural "s".** Write "Mac devices", "the Mac
   fleet", "iPhone units". Never "Macs", "iPhones", "iPads". Singular use ("a Mac
   that isn't there") is fine.

4. **No small-size all-caps labels.** In any headed document, headings and section
   labels are sentence case; hierarchy comes from weight and placement, never from
   uppercase plus letterspacing.

5. **No unanchored adjectives.** Adjectives are allowed, but wherever one appears
   there must be a concrete thing nearby carrying it; the specific is what keeps
   the adjective from going hollow. "Seamless" alone is a placeholder; "seamless:
   one panel glides across the bar instead of reopening" is a claim. If no
   specific exists to anchor an adjective, cut the adjective.

## The moves

The recognizable patterns of the voice. This is a palette, not a checklist: reach
for them where they fit, don't force all of them into every text.

**Colon elaboration** (optional, explicitly not a requirement). State the claim,
then unpack it after a colon with a few concrete items:

> I care deeply about craft: the shadows, the easing curves, the half-pixels that
> make an interface feel considered.

**Triads.** Three-beat lists give rhythm without ornament:

> enrolled, monitored, and ready to serve

**Semicolon-paired claims.** Two related assertions share a sentence; the second
sharpens the first:

> Green, amber, and red are verdicts; they belong to health alone.

**The short closer.** After a dense passage, end on a plain short sentence. It
reads as confidence:

> The part I care most about is the interface.
> Try it.

**Comma titles.** Titles and names use a comma where others reach for a dash or a
dot: "Cosmos, the infra". Separators inside a title are a comma, "at", or a hyphen.

**Headings with a twist.** Headings are compact noun phrases, sentence case, often
with one unexpected word doing the work: "Color as grammar", "Time, told honestly",
"Density with mercy".

**Personified mechanics.** When explaining a system, give it quiet agency; it reads
faster than specification language:

> A busy fleet doesn't get to look like a healthy one.
> There is no point advertising "Allocated" on a Mac that isn't there.
> Most of the work below is about making those realities boring.

## Substance rules

What the text says matters as much as how it sounds.

- **Numbers carry claims.** Prefer concrete figures over intensifiers ("more than
  250 physical Mac devices", not "a huge fleet"). There is no cap on how many
  numbers a passage may hold; the only requirement is that each one is real.
- **Truth first, then the art.** Before writing any claim, check the real source,
  product, or data; writing unverified is forbidden, and inventing examples,
  features, or quotes is forbidden absolutely. On top of verified facts, the art
  of language is fair game: amplify, frame favorably, emphasize strengths and pass
  over weaknesses. The line is traceability: framing may flatter, but every
  individual statement must survive being traced back to the source as literally
  true. Selective is acceptable; false is not.

## Both languages

The rules hold in Chinese as written: 「——」和「·」同样禁用，用冒号、分号、逗号或
拆句重构；标题层级靠字重与位置，不靠大写；产品名不加复数。The voice translates
too: short declaratives, concrete nouns, restraint.

## Pre-ship checklist

Before delivering any prose, scan for these:

- `—` or `——` outside numeric ranges and code comments (grepable)
- `·` anywhere (grepable)
- `Macs`, `iPhones`, `iPads`, or any Apple name + "s" (grepable)
- ALL-CAPS labels or headings
- adjectives with no concrete anchor nearby
- claims you did not verify against the real source
