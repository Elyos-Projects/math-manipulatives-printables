# PLAN — math-manipulatives-printables

> Status: Draft · Version: 0.1.0 · Last updated: 2026-06-28 · Owner: TBD (maintainer) · Lane: donated

## Executive summary

Concrete manipulatives — counters, number lines, fraction tiles, base-ten blocks — are one of the
best-evidenced tools in early and elementary mathematics: they let a learner *see and touch* the
quantity behind a symbol before the symbol means anything. Commercial sets cost real money (a class
set of fraction tiles or base-ten blocks runs tens to hundreds of dollars), so the children who
would benefit most — under-resourced classrooms, homeschooling and unschooling families, refugee and
crisis-schooling settings, tutoring and after-school programs — are exactly the ones least likely to
have them. A free, **print-it-yourself** manipulative that works on an ordinary black-and-white
office printer closes that gap with paper and scissors.

`math-manipulatives-printables` produces **openly-licensed, print-ready PDFs** of the four core
manipulative families above (plus a sequenced backlog of ten frames, hundred charts, place-value
charts and more). The defining engineering decision is that every printable is **generated from a
parametric specification, not hand-drawn** — a TypeScript generator emits a vector PDF whose physical
dimensions are locked in millimetres and **machine-verified to a tolerance** before release. This is
the whole point of the project: a fraction tile that prints even 3 mm wrong, or a number line whose
intervals are unequal, does not merely look bad — it teaches a *false mathematical relationship*. So
dimensional exactness, not visual polish, is the quality bar.

The two real hazards are therefore (1) **print/dimensional fidelity** — the artifact must measure
correct *after it comes out of a real printer*, in both A4 and US Letter, without full-bleed, and
must remain usable in pure grayscale and ink-saver outline modes; and (2) **accessibility** — low
contrast, colour-only encodings, and tiny numerals lock out low-vision, colour-blind, and
print-disabled learners. Both are handled by hard, testable gates (an automated dimension check, a
physical print-and-measure test, a contrast/colour-blind audit, and a math-educator review), not by
trusting that a design "looks fine on screen."

This document is honest about what is not yet in place: **no distribution partner or classroom is
secured.** The pedagogical need is well established, but a *documented need* is not a *secured
delivery channel*. Until at least one channel (an OER repository, a teacher network, or an NGO
education programme) agrees to host and put these in front of learners, delivery-dependent tasks carry
`verifiedNeed = false`. M0 is a thin, end-to-end slice — one fully-verified manipulative family, in
both paper sizes, distributed and baselined — that earns the right to scale.

## Problem & beneficiaries

**Who is helped (primary beneficiaries):**

- **Learners in under-resourced classrooms** (low-income public schools, schools in low- and
  middle-income countries) where a class set of physical manipulatives is unaffordable, so children
  jump to abstract symbols without the concrete stage research says they need.
- **Homeschooling, unschooling, and out-of-school learners and their caregivers**, who teach without
  a school's procurement budget and rely on what they can print at home or at a library.
- **Tutoring, after-school, refugee/crisis-schooling, and community-education programmes** that need
  cheap, replaceable, hand-out-able manipulatives at scale.

**Secondary beneficiaries:**

- **Teachers and parents** generally, who get a free, dimensionally trustworthy, accessible set they
  can reprint whenever pieces are lost (the perennial failure mode of physical manipulatives).
- The **open educational resources (OER) commons** itself, which is comparatively thin on *verified*
  print-ready manipulatives with explicit dimensional and accessibility guarantees.

**The verified need.** The pedagogical value of concrete manipulatives in early/elementary
mathematics is well documented and not in dispute, and the cost barrier to physical sets is real and
widely reported. On that basis the project marks the *underlying* need as established.

**The partner gap (honest).** A documented need is not a secured channel. **No partner organisation,
school, OER repository, or NGO has yet agreed to host these printables and put them in front of
learners**, and no specific classroom or programme has prioritised a first set with us. **Partner /
distribution channel: TO BE SECURED.** Until ≥ 1 channel is confirmed, delivery-dependent tasks have
`verifiedNeed = false`; securing a channel is an M0 exit criterion. (Artifacts that are
self-evidently useful regardless of a specific partner — e.g. the published style guide — may be
`true`.)

## Goals and non-goals

**Goals**

- Produce **dimensionally exact**, openly-licensed, print-ready PDFs of counters, number lines,
  fraction tiles, and base-ten blocks (then more), generated from versioned parametric specs.
- Guarantee every release works on an **ordinary consumer/school printer**: no full-bleed, A4 *and*
  US Letter, and fully usable in **grayscale / ink-saver** as well as colour.
- Make every printable **accessible by default**: colour-blind-safe, high-contrast, with a
  large-print variant and an open, legible font.
- **Distribute** through ≥ 1 real channel and measure that learners actually receive and use them —
  delivered, not merely published.
- Keep the whole toolchain (generator + verification) open so anyone can reproduce, audit, fix, and
  extend the set.

**Non-goals** *(constraints as identity — see §"Scope" and Appendix A)*

- **Not** interactive/digital manipulatives or an app — excellent open virtual manipulatives already
  exist; this project is deliberately *paper-first*.
- **Not** anything that *requires* colour, special paper, cardstock, lamination, or a print shop to be
  usable — those are optional enhancements, never preconditions.
- **Not** dimensionally approximate "good enough" art — exactness is the deliverable, not a nicety.
- **Not** freemium, ad-supported, watermarked, sign-up-walled, or "free sample then pay."
- **Not** curriculum-prescriptive — we *map to* standards as an aid, we do not dictate pedagogy.
- **Not** a hosted PDF-generation SaaS or upload service.
- **Not** medical/legal/safety content; no high-stakes advice of any kind.

## Success metrics (outcomes)

Outcome- and beneficiary-centric. **Downloads are not the headline metric** — *received, printed
correctly, and used by a learner* is. Where a target depends on an as-yet-unsecured channel, it is
marked accordingly rather than invented.

| Metric | Baseline | Target (first 2 quarters post-M0) |
|---|---|---|
| **Dimensional-accuracy conformance** of released printables (within tolerance, machine-verified) | n/a | **100%** — hard gate; nothing ships outside tolerance |
| **Physical print-fidelity pass rate** (printed on a real printer, measured with a ruler, within tolerance) | n/a | 100% of released sets pass on ≥ 1 A4 and ≥ 1 US-Letter printer |
| Core manipulative families published print-ready (both paper sizes, grayscale + colour, ≥1 accessible variant) | 0 | 4 (counters, number lines, fraction tiles, base-ten blocks) |
| **Accessibility conformance** (contrast ≥ WCAG AA for text; no colour-only encoding; large-print variant available) | n/a | 100% of released sets |
| **Educator-reviewed for mathematical/pedagogical correctness** | 0 | 100% of released sets |
| **Distribution**: sets received via a secured channel (the delivery proof) | 0 | ≥ 1 channel live; ≥ 1 set distributed |
| **Beneficiary validation**: educator/family confirms a *printed* set is correct and usable in practice | none | ≥ 1 qualitative validation per family of manipulative |
| Estimated **cost avoided** per adopting classroom (vs comparable commercial set) | n/a | reported (transparency metric, not a vanity count) |
| **Curriculum-standards mapping** coverage of released families | 0 | each released family mapped to ≥ 1 common standards framework |
| **License/provenance violations** (any non-open asset, font, or palette used) | 0 | **0** (hard gate; any violation is stop-the-line) |

**Dimensional tolerance (the core quality definition).** "Accurate" is not a vibe. Each printable
declares its intended physical dimensions in millimetres; a release passes only if **every verified
dimension is within ± 0.5 mm or ± 0.5 % of nominal, whichever is larger**, measured both (a)
automatically from the generated vector geometry and (b) physically with a ruler on a real print at
100 % / "actual size" scaling. *Relationships* are checked too: e.g. two halves must equal one whole
to within tolerance; ten unit cubes must equal one rod; number-line intervals must be equal to within
tolerance. A scale-calibration ruler (a printed 100 mm reference bar) is included on every sheet so
any user can confirm their own print came out true.

**Accessibility definition.** Text/numeral contrast ≥ WCAG 2.x AA; **no information conveyed by
colour alone** (fraction families and two-colour counters are distinguished by shape/label/pattern as
well as colour); a **large-print / high-contrast variant** of each family; an open, highly legible
font; cut lines that are followable by low-vision users and by scissors (not just guillotines).

## Scope

**In scope**

- Parametric generation of: **counters** (two-colour and plain), **number lines** (integer, fraction,
  decimal, and blank/open; multiple ranges and step sizes), **fraction tiles/bars** (halves through
  twelfths, dimensionally consistent so they compose), **base-ten blocks** (units, rods/tens,
  flats/hundreds, and a thousand-cube net).
- For each: **A4 and US Letter**, **colour + grayscale + ink-saver outline** modes, a **large-print**
  variant, an embedded **scale-calibration bar**, and **cut/fold guides** within safe printer margins.
- A versioned **manipulative-spec schema**, a **print & accessibility style guide**, and an
  **automated dimensional-verification harness**.
- Provenance + license records per release; curriculum-standards mapping; print-and-use instructions.

**Out of scope**

- Interactive/virtual/digital manipulatives, apps, or animations.
- Designs that require colour, cardstock, lamination, special paper, or commercial printing to work.
- Full-bleed / edge-to-edge designs that fail on consumer printers.
- Hosting a PDF-generation web service or accepting user uploads.
- Pre-cut/die-cut physical product manufacture, fulfilment, or shipping.
- Curriculum authoring, lesson sequencing, or grading (mapping to standards is in scope; prescribing
  pedagogy is not).
- Any medical/legal/safety content or high-stakes advice.
- Translation of instructional text and non-Western numeral systems in the first phases (valuable;
  sequenced to the backlog, not dropped).

## Solution approach & architecture

A **content-generation** project: deterministic code produces print artifacts, with human and
educator review gates. It runs in the **donated lane** — a human runs their own agent to author specs,
designs, and generator code, and Elyos prepares the task workspace and opens PRs. The CLI never runs
an agent headless and never authenticates one.

**Why generate, not draw.** Hand-drawn PDFs cannot be trusted to be dimensionally exact, cannot be
re-derived in a second paper size or an accessible variant for free, and cannot be machine-verified.
A parametric generator makes exactness, reproducibility, and variant-explosion (A4/Letter ×
colour/grayscale/ink-saver × standard/large-print) cheap and auditable.

**Pipeline (per manipulative release)**

1. **Author spec** — a versioned `manipulative-spec` JSON declares type, nominal physical dimensions
   (mm), denominations/ranges, colour mode, palette, accessibility variant, paper size, font, and
   cut-guide options. The spec is the single source of truth; one spec fans out to all variants.
2. **Generate** — the generator renders the spec to **SVG** (an exact, unit-aware vector format) and
   converts SVG → **print-ready PDF** with physical dimensions locked, margins kept inside a
   conservative consumer-printer safe area (no full-bleed), and the **scale-calibration bar** embedded.
3. **Automated dimensional verification** — a harness parses the generated geometry and asserts every
   declared dimension *and every declared relationship* (halves-make-a-whole; ten-units-make-a-rod;
   equal number-line intervals) is within tolerance. A failing release **cannot be published**.
4. **Automated accessibility checks** — contrast ratios computed against WCAG AA; a colour-blind
   simulation pass confirms no colour-only encoding; font legality and embedding confirmed.
5. **Physical print test (human)** — the release is printed at 100 % on a real A4 and US-Letter
   printer; a human measures key dimensions with a ruler against the calibration bar and records pass/
   fail per the tolerance.
6. **Math-educator review (human)** — an educator confirms mathematical/pedagogical correctness
   (e.g. fraction tiles compose correctly and are labelled unambiguously; the number line's
   zero/origin and direction are right; base-ten proportions teach the right place-value story).
7. **License/provenance record** — every font, palette, and any asset is confirmed open; the release
   record captures generator version, spec hash, license, attribution, reviewers, and verification
   results.
8. **Distribute & track to "used"** — publish to the secured channel; a release is "done" only when a
   beneficiary can obtain it *and* it is confirmed correct on a real print. Track toward beneficiary
   validation.

**Components**

- `specs/` — versioned `manipulative-spec` JSON files (the source of truth and a data deliverable).
- `generator/` — TypeScript engine: spec → SVG → print-ready PDF; variant expansion; calibration bar.
- `verify/` — dimensional-verification harness + accessibility (contrast / colour-blind / font) checks.
- `style-guide/` — the print & accessibility style guide (dimensions, tolerances, paper/margins,
  colour modes, palette, fonts, cut guides, large-print rules).
- `assets/` — vendored **open** fonts and palette definitions, each with a recorded license.
- `releases/` — generated PDFs (per family × paper size × colour mode × accessibility variant) plus a
  per-release provenance/verification record.
- `mappings/` — curriculum-standards mapping documents.

**Tech stack & conventions.** TypeScript, ESM, pnpm workspaces. Deterministic, dependency-light
SVG→PDF (no headless-browser dependency in the core path, to keep output reproducible and CI-friendly).
Generator/verification **code is MIT**; generated **content is CC-BY-4.0** (see §Data, licensing &
compliance). DCO sign-off (`git commit -s`) on all code and PRs. A changeset accompanies user-facing
changes.

**`manipulative-spec` data model (draft)**

```
schemaVersion       spec schema version
manipulativeType    counter | number-line | fraction-tile | base-ten-block | (future: ten-frame | ...)
variantName         e.g. "fraction-bars-halves-to-twelfths"
units               "mm" (canonical internal unit; everything physical is in mm)
dimensions          declared nominal physical sizes per element, in mm (e.g. unitCube = 10)
relationships       invariants to verify (e.g. "2×half == 1×whole", "10×unit == 1×rod")
denominations       fractions: [2,3,4,5,6,8,10,12]; number line: { min, max, step }
paperSize           "A4" | "US-Letter"
colorMode           "color" | "grayscale" | "ink-saver-outline"
palette             colorblind-safe palette id (with non-color redundancy: shape/label/pattern)
accessibilityVariant "standard" | "large-print" | "high-contrast"
font                open font id (e.g. "Atkinson-Hyperlegible")
numeralSystem       "western-arabic" (extensible; non-Western numerals are backlog)
cutGuides           boolean; safeMarginMm conservative consumer-printer margin
calibrationBar      always true (printed 100 mm reference for user self-check)
tolerance           { absMm: 0.5, relPct: 0.5 }  (max of the two)
license             "CC-BY-4.0"
attribution         author/source string
provenance          { generatorVersion, specHash, date, reviewers[] }
verification        { dimensional: pass|fail, accessibility: pass|fail, physicalPrint: pass|fail, measuredBy }
```

**Key decisions**

- *Spec-driven, machine-verified.* Exactness is enforced by code, not by eyeballing; the verification
  harness is as important a deliverable as the generator.
- *Grayscale/ink-saver is a first-class mode, not an afterthought.* The likely real printer is a B&W
  school/home laser; if it only works in colour, it doesn't work.
- *Calibration bar on every sheet.* Printers and "fit to page" settings silently rescale; an embedded
  reference bar lets any user (and our physical test) catch a bad print in seconds.
- *No full-bleed, both paper sizes from one spec.* Portability and printability are designed in, not
  patched later.

## Data, licensing & compliance

**This is the critical, conservative section.** Although this project *creates* original content
(rather than ingesting datasets), the licensing risk is concentrated in **embedded assets** — fonts,
palettes, glyphs, any clip-art or themed imagery — and in the **output license** of what we publish.

**Allowed assets (only these classes).**

- **Fonts:** only fonts under SIL OFL, Apache-2.0, or public domain (e.g. Atkinson Hyperlegible (OFL),
  Lexend (OFL)). The font must permit **embedding and redistribution**. No proprietary or
  unclear-license fonts, ever.
- **Palettes:** colour values are facts (not copyrightable), but we use named, documented
  colour-blind-safe palettes (e.g. Okabe–Ito, ColorBrewer for which terms permit reuse) and record
  the source.
- **Any imagery / themed counters:** only CC0 / public-domain / CC-BY assets with recorded
  attribution — and only inclusive, non-stereotyping imagery (see privacy/representation below).
  Default counters are abstract shapes requiring no third-party art.

**Hard asset-license gate.** Before any asset is vendored or shipped: its license must be verified to
permit reuse, modification, embedding, and redistribution; **unknown / all-rights-reserved /
non-commercial-where-it-conflicts = excluded.** The license id + attribution + source URL + retrieval
date are recorded in `assets/` and the release record.

**Output licensing.** Generated **content** (PDFs, SVGs, specs) is **CC-BY-4.0** so it is freely
usable, printable, modifiable, and redistributable, including in classrooms and other OER, with
attribution. Generator/verification **code** is **MIT**. (If a future channel requires CC0 or
CC-BY-SA, that is decided per channel and recorded; we never relicense third-party assets.)

**Privacy / PII stance.** The project handles **no personal data** — there is no user account, no
upload, no analytics that identify individuals. Distribution metrics are aggregate. If themed
counters ever depict people or cultural motifs, designs must be **inclusive and non-stereotyping**,
and any depiction-bearing asset must be openly licensed; the default abstract counters avoid this
entirely.

**Representation & non-discrimination.** Imagery, names, and examples (e.g. on themed counters or in
instructions) are reviewed for inclusivity and freedom from bias, per Elyos refusal guardrails.

**Automation policy.** Distribution honours each host channel's contribution/API terms and rate
limits; no scraping around access controls.

## Quality, review & risk gates

**Risk tier: low overall.** There is no medical/legal/safety content and no PII. *However*, two
review dimensions are treated as **domain-accuracy-critical (medium-flavoured)** and require a
qualified reviewer before release, because getting them wrong silently teaches falsehoods:

- **Mathematical/pedagogical correctness** → **math-educator review** (the project's "specialist").
- **Dimensional/print fidelity** → automated verification **plus** a physical print-and-measure test.

There is **no high-risk path** in this project. If any future item drifts toward high-stakes content
(it should not), it falls out of scope rather than being escalated here.

**Required gates before a release is "done":**

1. **Asset-license check passed** (every font/palette/asset open; recorded license + attribution).
2. **Automated dimensional verification passed** — all declared dimensions *and relationships* within
   tolerance; release is blocked otherwise.
3. **Automated accessibility checks passed** — contrast ≥ AA; no colour-only encoding; legal embedded
   font; large-print variant exists.
4. **Physical print test passed** — printed at 100 % on a real A4 and a real US-Letter printer and
   measured with a ruler against the calibration bar, within tolerance.
5. **Math-educator review passed** — mathematical correctness, labelling, and pedagogical soundness
   confirmed; reviewer recorded in provenance.
6. **Style-guide conformance** — paper/margins, colour modes, cut guides, calibration bar present.

**Definition of Shipped (project-level).** A printable is **published under an open license through a
secured channel, verified dimensionally + physically + for accessibility, and educator-reviewed**, so
a real learner can obtain it and print a *correct, usable* manipulative. Generated-but-unverified, or
verified-but-undistributed, ≠ shipped.

## Roadmap & milestones

Phased; each milestone has measurable exit criteria. M0 is a deliberately thin, end-to-end slice that
must prove one manipulative family can travel from spec → verified print → distributed before anything
scales.

**M0 — Foundation & cold-start (prove one end-to-end deed).**
Goal: publish the style guide and spec schema, clear open assets, secure ≥ 1 distribution channel, and
ship **one** fully-verified manipulative family (recommended: **fraction tiles, halves–twelfths**,
because composition makes dimensional errors obvious) in both paper sizes and colour + grayscale.

**Sequencing — securing a channel is a hard gate.** The channel-securing task **blocks**
distribution: no release is *published as delivered* until ≥ 1 channel is confirmed. The cold-start
family can still be *built and verified* in parallel (it is self-evidently useful and reusable), but
the "delivered" claim and `verifiedNeed=true` wait on a channel. **Kill/pivot criteria:** if, after a
time-boxed channel-securing effort, no channel will host/distribute, the project **pivots** (next
candidate channel) or **pauses distribution** — it keeps the verified, openly-licensed artifacts
public (still a public good) rather than over-investing in scale with no delivery path.

**Candidate distribution channels (priority order, with acceptance posture):**
1. **OER repositories / libraries** (OER Commons-style, open-courseware libraries) — clearest path for
   openly-licensed downloadable content; *posture: generally welcoming to CC-BY OER; per-repo
   submission terms to confirm.*
2. **Teacher / homeschool networks & NGOs** running education programmes — highest *delivery-to-learner*
   value; *posture: needs a named contact and a hand-off mechanism; TO BE SECURED.*
3. **A project-owned open repository + index page** as a fallback so artifacts are always public; *not*
   a substitute for a channel that puts them in front of learners.

Exit criteria:
- Print & accessibility **style guide v1** published (dimensions, tolerances, paper/margins, colour
  modes, palette, fonts, cut guides, large-print, calibration bar).
- **`manipulative-spec` schema v1** + provenance/verification record format finalised.
- **Open-asset license clearance** complete for the fonts/palettes used (recorded).
- **≥ 1 distribution channel confirmed** (closes the partner gap for the first family; gates the
  "delivered" claim).
- Cold-start family **generated and verified**: dimensional check passed; accessibility checks passed;
  **physical print test passed on A4 + US Letter**; **math-educator review passed**; A4 + Letter ×
  colour + grayscale produced.
- Cold-start family **distributed** via the secured channel with print-and-use instructions; baseline
  outcome tracking established.

**M1 — Generator & core set (make it repeatable).**
Goal: turn the manual cold-start into a parametric generator + automated verification, and ship all
four core families.
Exit criteria:
- `generator/` produces SVG→print-ready PDF from spec; one spec fans out to A4/Letter ×
  colour/grayscale/ink-saver.
- `verify/` dimensional-verification harness runs in CI and blocks out-of-tolerance releases;
  automated contrast/colour-blind/font checks run too.
- **All 4 core families** (counters, number lines, fraction tiles, base-ten blocks) generated,
  verified, educator-reviewed, and physically print-tested.
- Each family distributed through ≥ 1 channel.

**M2 — Accessibility, breadth & validation (prove it works for real learners).**
Goal: ship accessible variants and more denominations/ranges, and validate with real users.
Exit criteria:
- **Large-print + high-contrast variants** of all four families released and verified.
- Accessibility audit (contrast + colour-blind simulation) passed across the set.
- **≥ 1 beneficiary validation per family** — an educator/family uses a *printed* set and confirms it
  is correct and usable; findings fold back into specs/style guide.
- **Curriculum-standards mapping** published for each released family.

**M3 — Broaden & sustain (more types, durable ops).**
Goal: add more manipulative types and a maintenance model.
Exit criteria:
- Additional families (ten frames, hundred charts, place-value charts, and at least one angle-critical
  type such as pattern blocks) generated and verified.
- **Internationalised numerals** for ≥ 1 additional numeral system.
- Documented maintainer + reviewer rotation; **outcome dashboard** (distributed/used per family,
  cost-avoided estimate) maintained; sustainability plan in effect.

## Work breakdown

The itemised, schema-mapped backlog lives in **`TASKS.md`** (same directory): organised by the
milestones above, one task per work unit, stable IDs (`math-manip-<area>-NNN`), a size/risk/reviewer
table per milestone, acceptance criteria for the key tasks, milestone Definitions of Done, a backlog,
and a complete, schema-valid example Task JSON for the first M0 task. The production pattern is
fan-out by **(manipulative family × paper size × colour mode × accessibility variant)**, all derived
from one parametric spec.

## Governance, roles & stakeholders

- **Maintainer (Owner):** TBD — owns the style guide, spec schema, generator, verification harness,
  and the overall quality bar.
- **Math-educator reviewer(s):** the project specialist(s); confirm mathematical/pedagogical
  correctness of every release. At least one with early/elementary mathematics experience.
- **Accessibility reviewer:** confirms contrast, colour-blind safety, large-print adequacy, and
  cut-guide usability for low-vision users.
- **Print-test reviewer:** performs the physical print-and-measure test on real A4 and US-Letter
  printers (can rotate among contributors with the equipment).
- **Steward (last-mile owner):** owns the relationship with each distribution channel and shepherds
  releases to *distributed and used* — accountable for "delivered, not merged."
- **Partner / requestor:** TO BE SECURED — the OER repo / teacher network / NGO that hosts and
  surfaces the printables and that can prioritise families and confirm beneficiary use.
- **Beneficiary validators:** educators/families/learners who confirm a *printed* set is correct and
  usable.

## Dependencies & integrations

- **Open fonts** (SIL OFL / Apache-2.0 / PD) — e.g. Atkinson Hyperlegible, Lexend — vendored with
  recorded licenses; must permit embedding + redistribution.
- **Colour-blind-safe palettes** — e.g. Okabe–Ito; documented source/terms.
- **SVG→PDF toolchain** — a deterministic, dependency-light library (no required headless browser in
  the core path) so output is reproducible and CI-verifiable.
- **Distribution channel(s)** — OER repository / teacher network / NGO (TO BE SECURED); each has its
  own submission terms and attribution requirements.
- **Curriculum-standards frameworks** — public standards documents to map against (mapping is
  descriptive; non-prescriptive; non-partisan).
- **Elyos platform pieces** — `packages/cli` (task workspace + PR prep, donated lane), the Task schema
  (`packages/schema`), and `adapters/` for any channel-specific publishing code. The CLI never runs an
  agent headless.

## Risks & mitigations

| Risk | Likelihood | Impact | Mitigation | Owner |
|---|---|---|---|---|
| Printable measures wrong after printing (scale/"fit to page"/printer drift) → teaches false relationships | High | High | Automated dimensional + relationship verification; **embedded 100 mm calibration bar** on every sheet; mandatory **physical print-and-measure test** on A4 + US Letter at 100 % before release | Maintainer / Print-test reviewer |
| Design only works in colour; real printer is B&W | High | Medium | Grayscale + ink-saver outline are first-class modes; no colour-only encoding (shape/label/pattern redundancy); accessibility check enforces it | Maintainer / Accessibility reviewer |
| Non-open or non-embeddable font/asset shipped | Low | High | Hard asset-license gate ("unknown = excluded"); only OFL/Apache/PD fonts that permit embedding; recorded license per asset; stop-the-line on violation | Steward / Maintainer |
| Mathematically/pedagogically wrong artifact (mislabelled fractions, wrong origin, bad proportions) | Medium | High | Mandatory math-educator review; declared *relationship* invariants verified in code; composition tests (halves make a whole; ten units make a rod) | Math-educator reviewer |
| No distribution channel secured → nothing reaches learners | Medium | High | M0 exit requires a confirmed channel; `verifiedNeed=false` until secured; keep verified artifacts public as fallback; kill/pivot criteria | Maintainer / Steward |
| Inaccessible output excludes low-vision / colour-blind learners | Medium | High | Accessibility checks (contrast AA, colour-blind sim) + large-print/high-contrast variants required before release; accessibility reviewer | Accessibility reviewer |
| Full-bleed / margin clipping on consumer printers | Medium | Medium | Conservative safe-margin design; no full-bleed; physical print test catches clipping | Maintainer |
| Spec/generator regression silently degrades a previously-good release | Medium | Medium | Verification harness in CI; spec hashing; regenerate-and-verify on every change; changesets | Maintainer |
| Themed imagery introduces bias/stereotype or license risk | Low | Medium | Default to abstract counters; any imagery openly-licensed + inclusivity-reviewed | Maintainer / Reviewers |
| Reviewer/print-test capacity becomes the bottleneck at scale | Medium | Medium | Reviewer rotation; batch by family; only scale fan-out to review/print-test capacity | Maintainer |

## Security & privacy

- **Threat surface.** Low and mostly content-integrity, not classic security: wrong dimensions,
  inaccessible output, or a non-open asset slipping in. Publishing may touch an external channel's API
  (e.g. a repo PR).
- **Secrets handling.** Any channel API tokens are supplied via the human's own environment, never
  written to logs, receipts, records, or committed files (per CLAUDE.md). Donated lane: the human uses
  their own account; Elyos stores no agent credentials.
- **PII / privacy.** None collected — no accounts, uploads, or person-level analytics; metrics are
  aggregate. No personal data ever enters the pipeline.
- **Abuse / misuse prevention.** Output is benign educational content; the main guardrail is refusing
  any non-open asset and any biased/stereotyping imagery. Refuse and flag (per Elyos guardrails) any
  request that would introduce non-open assets, primarily benefit a for-profit, or add non-inclusive
  content.

## Sustainability & maintenance

- **Durable artifacts.** The published CC-BY PDFs/SVGs/specs are self-contained public goods that
  remain usable indefinitely; because they regenerate from versioned specs, they can be re-rendered
  for new paper sizes, fonts, or fixes without redrawing.
- **Reproducible by anyone.** The open generator + verification harness mean the community can audit,
  fix, and extend the set without the original maintainer — the strongest sustainability guarantee.
- **Maintenance.** The maintainer keeps the generator current with the SVG→PDF toolchain and font
  updates and re-runs verification on changes; reviewer/print-test rotation keeps capacity alive.
- **Outcome tracking.** A lightweight dashboard tracks distributed/used counts and a cost-avoided
  estimate per family over time, so impact is visible after the active push.
- **Wind-down.** If a channel closes, artifacts stay public in the project repo with their provenance
  records; the calibration bar means even an orphaned PDF can be self-verified by any future user.

## Open questions

- Which distribution channel is secured first — a specific OER repository, a teacher/homeschool
  network, or an NGO education programme? (Blocks the M0 "delivered" claim.)
- Which exact open font(s) and colour-blind-safe palette become the project defaults, and do all
  permit embedding + redistribution under our CC-BY output?
- Which SVG→PDF toolchain is deterministic and dependency-light enough for reproducible CI output
  across contributor machines?
- What is the right verification tolerance per manipulative family — is ± 0.5 mm / ± 0.5 % correct for
  fraction tiles *and* base-ten blocks, or do small units need a tighter absolute bound?
- Which curriculum-standards framework(s) do target channels care about for the mapping?
- Should instructional text and numerals be internationalised in M2 rather than M3, if the first
  secured channel serves a non-English / non-Western-numeral audience?
- What recommended print settings (paper weight, "actual size", duplex off) belong in the standard
  instructions to maximise correct prints?

## References

- `C:\code\elyos\CLAUDE.md` — Elyos work rules, lanes, quality bar, refusal guardrails.
- `C:\code\elyos\docs\good-deed-definition.md` — good-deed criteria and risk tiers.
- `C:\code\elyos\packages\schema\src\schemas.ts` — Task JSON schema.
- `C:\code\elyos\planning\ROADMAP.md` — portfolio roadmap (this project listed under Track 3).
- `C:\code\Ofelia\plan.md` — exemplar plan (depth/structure reference).
- WCAG 2.x — contrast and non-text-content accessibility guidance.
- Creative Commons license suite (CC-BY-4.0, CC0) and SIL Open Font License.
- Okabe–Ito / ColorBrewer — colour-blind-safe palette references.

---

## Appendix A — Improvements applied

The following 25 specific improvements were identified against an earlier draft of this plan and
**have been applied** to the text above. They are recorded here so the iteration is auditable.

1. **Reframed the headline quality bar from "looks good" to dimensional exactness**, because a wrong
   measurement teaches a false relationship — now the central thesis (Exec summary, §Solution).
2. **Defined a concrete numeric tolerance** (± 0.5 mm or ± 0.5 %, whichever is larger) instead of a
   vague "accurate" — made it the formal definition under Success metrics.
3. **Added relationship invariants** (halves-make-a-whole, ten-units-make-a-rod, equal number-line
   intervals) as separately-verified properties, not just per-element sizes.
4. **Added an embedded 100 mm scale-calibration bar on every sheet** so any user (and the physical
   test) can detect a mis-scaled print immediately — and so orphaned PDFs stay self-verifiable.
5. **Made grayscale + ink-saver a first-class mode**, since the realistic printer is a B&W laser; added
   "no colour-only encoding" as an accessibility rule and a risk row.
6. **Required both A4 and US Letter from one spec**, designing portability in rather than patching it.
7. **Chose parametric generation over hand-drawing** explicitly, with the rationale (exactness,
   reproducibility, cheap variant explosion, machine verifiability).
8. **Elevated the verification harness to a named deliverable** (`verify/`) and a CI gate that blocks
   out-of-tolerance releases — not a manual afterthought.
9. **Added a mandatory physical print-and-measure test** on real printers as a distinct gate, because
   on-screen geometry can still print wrong.
10. **Specified accessibility concretely** (WCAG AA contrast, large-print + high-contrast variants,
    colour-blind-safe palette, legible open font, scissor-followable cut lines).
11. **Tightened the licensing section onto the real risk surface — embedded assets (fonts/palettes)** —
    with a hard "unknown = excluded" gate and an embedding+redistribution requirement for fonts.
12. **Set explicit output licensing** (content CC-BY-4.0, code MIT) and stated we never relicense
    third-party assets.
13. **Made distribution a success metric and a Definition-of-Shipped condition** ("delivered, not
    merged"), separating it from mere publishing/downloads.
14. **Marked the partner/channel as TO BE SECURED** and wired `verifiedNeed=false` to it, with a
    candidate-channel priority list, a decision posture, and kill/pivot criteria.
15. **Replaced downloads-as-success with beneficiary outcomes** (received, printed correctly, used;
    cost-avoided; educator-validated) per Elyos's outcome-based bar.
16. **Recommended fraction tiles (halves–twelfths) as the cold-start family** specifically because
    composition makes any dimensional error visually and mathematically obvious — a stronger proof.
17. **Named a math-educator review gate** as the project specialist and made it mandatory per release,
    capturing the "domain-accuracy = medium" nuance while keeping overall risk low.
18. **Stated there is no high-risk path** and that any high-stakes drift falls out of scope rather than
    being escalated — honest scoping per the good-deed definition.
19. **Sharpened the non-goals into a constraints-as-identity list** (no freemium, no colour-required,
    no full-bleed, no app, no SaaS, not curriculum-prescriptive) matching the exemplar's discipline.
20. **Added a representation/non-discrimination stance** for any themed imagery, defaulting to abstract
    counters to avoid both bias and license risk.
21. **Added a deterministic/dependency-light SVG→PDF requirement** (no required headless browser) so
    output is reproducible across contributor machines and in CI.
22. **Added spec hashing + regenerate-and-verify-on-change** to catch silent regressions, plus a risk
    row for it.
23. **Built sustainability around reproducibility** — open generator + specs mean the community can
    maintain/extend without the original author; orphaned PDFs remain self-verifiable via the bar.
24. **Added recommended print-settings guidance** (actual size, paper, duplex-off) as an open question
    and an instructions deliverable, to maximise correct prints in the field.
25. **Sequenced internationalised numerals and instructional-text translation to the backlog** (not
    dropped), with a trigger to pull them forward if the first secured channel serves a non-Western
    audience.

## Review sign-off

**Reviewer pass (self-review against PLAN_SPEC, CLAUDE.md, and the good-deed definition):**

- **Structure:** all 17 required H2 sections present and in spec order; metadata header present. ✔
- **Honesty:** partner/channel marked **TO BE SECURED**; `verifiedNeed=false` for delivery-dependent
  work; no invented partners, baselines, or vanity metrics; percentage targets deferred where no
  baseline exists. ✔
- **Guardrails:** open/PD/CC-only assets with a hard license gate; output CC-BY-4.0 / code MIT; no PII
  (none collected); non-discrimination stance on imagery; no medical/legal/safety content; refusal
  guardrails referenced. ✔
- **Quality bar:** Definition of Shipped is "delivered, not merged" (open-licensed + verified +
  educator-reviewed + distributed + usable on real print). ✔
- **Risk tier:** low overall, with two domain-accuracy review gates (math-educator + dimensional/
  physical) explicitly justified; no high-risk path, stated honestly. ✔
- **Lane:** donated; CLI never runs an agent headless; secrets stay in the human's environment. ✔
- **Corrections made during review:** (a) added the *physical* print test as a gate distinct from the
  automated check (an earlier draft conflated them); (b) added relationship invariants to the
  verification definition, not just element sizes; (c) clarified that the fallback project-owned
  repo is **not** a substitute for a learner-facing channel, so a "delivered" claim is never
  self-satisfied; (d) tied `verifiedNeed=true` for the style guide explicitly to its
  channel-independence, mirroring TASKS.md.
- **Outstanding human decisions:** which distribution channel is secured first; default font/palette
  and SVG→PDF toolchain; per-family tolerance confirmation. (Tracked in Open questions.)

**Sign-off:** Draft v0.1.0 is internally consistent, spec-conformant, and honest about its gaps;
ready for maintainer review and channel-securing. Not yet "done" — delivery depends on a secured
channel (M0 exit).
