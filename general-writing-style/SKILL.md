---
name: general-writing-style
description: |
  Soleil (citron)'s general writing and expression style, for any text written by
  them or on their behalf, in English or Chinese: documents, READMEs, articles,
  release notes, announcements, bios, emails, PR descriptions, UI copy, social
  posts, presentation text. Not tied to any one project. Apply it whenever
  producing prose the user will sign or ship, even when they don't mention style;
  several rules are hard bans (em-dash narration, the middle dot, pluralized Apple
  product names, chatbot openers) that they enforce everywhere, and the text must
  not read as machine-written.
metadata:
  keywords: writing style, English, Chinese, em-dash, middle dot, Apple product names, README, release notes, UI copy, copywriting, AI writing signs
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

6. **No chatbot openers.** Never begin with "Certainly!", "Sure!", "Here's",
   "I'd be happy to", "Great question", or any assistant throat-clearing. The
   first sentence is already the content.

7. **No unrendered Markdown in front of a reader.** Bold, headings, and inline code
   are fine where Markdown actually renders (a .md file, a README, a chat that
   renders it). They are a defect anywhere it doesn't: a UI string, an email body,
   a plain-text field, a social post, where the reader sees literal `**stars**`
   and `## hashes`. When you cannot tell whether the destination renders
   Markdown, ask the user with the question tool before writing; don't guess.

## Signals of machine writing

Readers now recognize AI text by a short list of habits (Pangram's published
frequency data: em dashes at 10x the human rate, bullet lists 9x, symmetric
triads 4x, "not just X but Y" 3x). The user has ruled on each; the bans above
cover the hard cases, and these are the soft ones. Not forbidden, but a reader
who spots two of them stops believing a person wrote it.

- **Template phrases.** Not recommended: "delve into", "crucial to note that",
  "in today's fast-paced world", "navigate the complexities of", "tapestry",
  "profound connection", "a testament to", "game changer". These are not a
  blacklist; they are examples of a class. The principle is small words and
  specific words over grand stock words. If a phrase could open any article on
  any subject, it is not carrying anything here.
- **Bullet lists where prose belongs.** Default to paragraphs. Use a list only
  when the content genuinely is a list of parallel items (steps, options, specs).
  A list of three sentences that could have been one paragraph is the tell.
- **The symmetric triad.** "X, Y, and Z" with three matched items is the single
  most machine-flavored rhythm in English prose. Use the rhythm patterns below
  instead; if three items are real, break the symmetry (see "Broken-third
  triad").
- **Phantom rebuttals.** Defending a claim nobody challenged, in any syntactic
  shape: "not just X but Y", "X, not Y", "copies the process, not the file",
  "it's not about Z, it's about W". The test is not the sentence pattern; it
  is whether the reader had the objection you are preemptively refuting. If
  nobody was thinking "maybe it copies the file", then "not the file" is
  answering a ghost. Say the thing directly; cut the negation clause. This is
  one of the hardest AI habits to catch because it sounds like precision, but
  it reads as insecurity: the writer is justifying themselves before anyone
  asked. This also includes filler intensifiers that answer a doubt nobody
  had: "整个过程" (who said it was partial?), "完全一致" (who said it wasn't?),
  "真正的" (who said it was fake?), "全面覆盖" (who said it was missing
  something?). These words feel like precision but they are preemptive
  defense in disguise. Scan every sentence that contains "not", "不是", or an
  unnecessary intensifier ("整个", "完全", "真正", "全面") preceded by a
  positive claim and ask: did anyone dispute this?
- **Register whiplash.** Technical language and casual language in the same
  sentence, or a warm human-sounding closer bolted onto a paragraph of
  mechanical description. A passage maintains one register; if you need to
  shift, start a new sentence or paragraph, don't splice within one.
- **Metaphor domain hopping and performative verbs.** AI picks the most "vivid"
  verb per clause without noticing the metaphors collide: 挖 (mining) + 冻结
  (physics) + 味 (taste) + 织 (weaving) in one paragraph. A human metaphor
  holds for a few sentences before switching. Also avoid AI's favorite
  figurative verbs specifically: 挖掘/深挖, 编织/交织, 解锁, 赋能, 打造. In
  English: "delve", "weave/tapestry", "unlock", "empower", "craft" (as a verb
  for non-physical things). Note: describing a process is fine when the verbs
  are literal. "It reads your repo, drafts one, runs comparison tests" works;
  "It mines your repo, distills a draft, freezes scenarios" does not. The
  difference is whether each verb is saying what happens or performing
  vividness. Four direct verbs in a row read as clear; four figurative verbs
  in a row read as a machine trying to sound interesting.
- **Jargon as texture.** Technical words must be precise, not atmospheric. If a
  term could be replaced by a more common word with zero loss of meaning, it
  was there for texture, not information. "Token" is precise when discussing
  tokenizers; it is texture when it means "word" or "signal". A made-up
  compound ("冻结场景", "frozen scenario") that sounds like a methodology but
  just means "fixed test case" is the same problem.
- **Forced intimacy.** Warmth is earned by what the text does, not by sprinkling
  in casual address. Don't open with "你家", "朋友", "fellow creators", or any
  familiarity the conversation hasn't built yet. The first sentence should be
  about the subject, not about the reader-writer relationship.
- **Decorative Unicode.** Symbols are welcome when they mean something: "上海 →
  广州" for a route, "≈" for a real approximation. Avoid symbols used as ornament
  or as bullet substitutes (box-drawing, arrows as flourishes, ★ ✦). The user
  makes things and likes these characters; the test is whether the symbol carries
  meaning, not whether it exists.
- **UI-flavored emoji.** Avoid ✅ ❌ ❗ and keycap numbers (1️⃣) in prose; they read
  as generated output. Face emoji in messages or posts, where a person would use
  them, are fine.

## The moves

The recognizable patterns of the voice. This is a palette, not a checklist: reach
for them where they fit, don't force all of them into every text.

**Colon elaboration** (optional, explicitly not a requirement). State the claim,
then unpack it after a colon with a few concrete items:

> I care deeply about craft: the shadows, the easing curves, the half-pixels that
> make an interface feel considered.

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

## Rhythm, learned from Apple

Apple's copy from 1984 to 2026 was surveyed for this skill (archived product pages
for iPod 2001, iPhone 2007, MacBook Air 2008, iPhone 4, iPad 2, iPhone 5, 6, 6s, 7,
X, XS, MacBook Air 2018 and 2020, MacBook Pro 2021, iPhone 14 Pro, Vision Pro, the
2026 pages, the 1984 Macintosh brochure, Think Different, and a per-product
tagline record). The finding: Apple's headline unit is two beats, not three. Where
a third item appears it is period-separated and the third breaks the pattern; the
comma-and triad shows up only in spec copy. These are the patterns, each with
dated evidence. Use them for headlines, subheads, and the first sentence of
anything.

**The turn pair.** Two fragments; the second reverses or answers the first. Apple's
workhorse for thirty years:

> So many innovations. So little space. (MacBook Air, 2008)
> Less in your hands. More at your fingertips. (iPad 2, 2011)
> Makes a splash. Takes a splash. (iPhone 7, 2016)
> Devours tasks. Sips battery. (MacBook Air, 2020)
> Out of range. Not out of reach. (iPhone, 2026)

**The echo pair.** Same structure twice; the repetition is the emphasis:

> Truly helpful. Truly yours. (macOS, 2026)
> Choose your size. Choose your chip. (MacBook Pro, 2021)
> Four million pixels. One brilliant debut. (MacBook Air, 2018)

**The self-fold.** A line that turns back on itself:

> Hello. Again. (iMac, 1998)
> This changes everything. Again. (iPhone 4, 2010)
> Bigger than bigger. (iPhone 6, 2014)
> The only thing that's changed is everything. (iPhone 6s, 2015)
> Your wallet. Without the wallet. (Apple Pay, 2014)

**The broken-third triad.** When there really are three, separate them with
periods and let the third break the symmetry. This is the only triad shape to use:

> Rip. Mix. Burn. (iTunes, 2001)
> Faster. Greener. Still mini. (Mac mini)
> Redesigned. Reengineered. Re-everythinged. (MacBook, 2008)
> 12MP pictures. 4K videos. Live Photos. Lasting memories. (iPhone 6s, 2015)

**The idiom hijack.** Take a phrase everyone knows and change one word:

> Think different. (1997)
> The plot thins. (PowerBook, 1999)
> Thinnovation. (MacBook Air, 2008)
> For your ears only. (AirPods Pro, 2026)
> Might takes flight. (MacBook Air, 2026)

**The number headline.** The figure is the headline; it needs no adjective:

> 1,000 songs in your pocket. (iPod, 2001)
> 960 by 640 by Wow. (iPhone 4, 2010)
> Over 4 million pixels. Under 3.6 pounds. (MacBook Pro, 2012)
> Two sizes. Five finishes. (iPhone 7, 2016)
> Up to 18 hours of battery life. That's 6 more hours, free of charge. (2020)

**Setup and landing.** A longer sentence sets it up; a short one lands it:

> A funny thing happens when you design a computer everyone can use. Everyone
> uses it. (Macintosh brochure, 1984)
> It's hard to believe we could fit so many great ideas into something so thin.
> (iPad, 2010)

**Long-form cadence.** For manifestos, intros, and anything over a paragraph, the
1984 brochure and Think Different share one method: short sentences in sequence,
direct address to "you", a question answered in the next line, and a closing
line that echoes the opening. Fragments are sentences. "Here's to the crazy ones.
The misfits. The rebels. The troublemakers."

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
拆句重构；标题层级靠字重与位置，不靠大写；产品名不加复数；不以客服腔开场；
不在不渲染 Markdown 的地方留下 `**` 和 `##`。The voice translates too: short
declaratives, concrete nouns, restraint, two beats over three.

## Review protocol (mandatory)

After writing, do NOT deliver. Read the text back and check every sentence
against **every rule defined in this skill**. Not a subset. Not a summary. Every
rule, for every sentence. A sentence can violate a rule without containing the
exact words or symbols named in that rule's examples; the examples are
illustrations of a principle, not an exhaustive list. You must understand what
each rule is trying to prevent and judge whether the sentence does that thing,
in any form.

**How to do the pass:** For each sentence, walk through these sections of the
skill in order and ask whether the sentence violates anything in them. If it
does, rewrite before moving to the next sentence.

1. **Hard bans** (§1–7): em-dash narration, middle dot, Apple plural, all-caps
   labels, unanchored adjectives, chatbot openers, unrendered Markdown. These
   are the only rules where character-level scanning works.
2. **Phantom rebuttals**: Is this sentence defending against an objection nobody
   raised? Any negation clause ("not X", "不是 X", "rather than", "instead of",
   "而非") or filler intensifier ("整个", "完全", "真正", "全面") that
   preemptively answers a doubt the reader does not have.
3. **Template phrases**: Does this sentence use a stock phrase that could appear
   in any article on any subject?
4. **Bullet lists**: Is a list being used where a paragraph would be more
   natural?
5. **Symmetric triad**: Three matched parallel items joined by commas and "and"?
6. **Register whiplash**: Does this sentence switch between technical and casual
   mid-sentence, or bolt a warm closer onto mechanical prose?
7. **Metaphor domain hopping and performative verbs**: Does this sentence use a
   metaphor from a different domain than the surrounding sentences? Does it
   use a flagged verb (挖掘/编织/解锁/赋能/打造, delve/weave/unlock/empower/
   craft)? Is a verb here chosen for vividness rather than accuracy?
8. **Jargon as texture**: Is a technical term here for precision, or for
   atmosphere? Could it be replaced by a common word with zero meaning loss?
9. **Forced intimacy**: Does this sentence address the reader with a familiarity
   the text has not yet earned?
10. **Decorative Unicode and UI emoji**: Is a symbol here carrying meaning, or
    is it ornament?
11. **Adjective anchor** (re-check from §5): Is every adjective in this sentence
    anchored by a concrete thing nearby?
12. **Factual verification**: Does this sentence state a fact? Has it been
    checked against the real source?

After the per-sentence pass, re-read the full text once for flow. Do not
re-introduce anything the pass removed.
