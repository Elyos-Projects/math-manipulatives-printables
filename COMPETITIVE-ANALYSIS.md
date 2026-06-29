# Competitive & Improvement Analysis — `math-manipulatives-printables`

> Analyst review of PLAN.md v0.1.0 (2026-06-28) + TASKS.md. Web-researched, cited.
> Scope: open, print-accurate, pedagogically-sound printable manipulatives (counters, number
> lines, fraction tiles, base-ten blocks; backlog: ten-frames, hundred charts, clocks, nets,
> pattern blocks, rulers/protractors) for low-resource classrooms.

---

## 1. Correctness & completeness review of PLAN.md

The plan is unusually strong: it already identifies dimensional fidelity as the central thesis,
defines a numeric tolerance (± 0.5 mm / ± 0.5 %), mandates an embedded calibration bar, treats
grayscale/ink-saver as first-class, and gates on a physical print-and-measure test plus
math-educator review. The 25-item "Improvements applied" appendix shows the heavy correctness
lifting is largely done. The findings below are refinements and gaps, ordered by importance.

**PRINT-ACCURACY (the dimension that most distinguishes this project — and the most under-specified
risk).** The plan correctly names the hazard but the mitigation has exploitable holes:

- **The viewer scales before the printer does.** The plan's instructions assume the user controls a
  "100% / Actual Size" setting, but the dominant failure is *silent default scaling in the PDF
  viewer/print path*, not user error. Adobe Reader's default "Fit" shrinks the page without
  accounting for existing margins, expanding what looks like the margin and shrinking content
  ([Adobe](https://helpx.adobe.com/acrobat/kb/scale-or-resize-printed-pages.html),
  [TeX FAQ "acroantics"](https://texfaq.org/FAQ-acroantics)). Embedded/in-app viewers are worse:
  Microsoft's WebView2 defaults PDF printing to *Fit-to-Page, not Actual Size*
  ([WebView2 issue #3691](https://github.com/MicrosoftEdge/WebView2Feedback/issues/3691)). A school
  Chromebook printing from the browser preview is a realistic, common path that will mis-scale by
  default. **Implication:** the calibration bar is necessary but not sufficient — many users will
  not measure it. The plan should add (a) a **human-readable "FAIL if this is not exactly X"
  instruction printed adjacent to the bar**, (b) a **redundant, universally-recognised reference
  object** alongside the 100 mm bar — a **credit-card outline (ISO/IEC 7810 ID-1 = 85.60 × 53.98 mm)**
  that any user can physically overlay without owning a ruler
  ([ISO/IEC 7810](https://en.wikipedia.org/wiki/ISO/IEC_7810); this credit-card check is exactly the
  trick the printable-ruler community uses, e.g.
  [Inch Calculator](https://www.inchcalculator.com/printable-protractor/)), and (c) an explicit
  **PDF construction requirement** that MediaBox/page size equals true paper size with no internal
  scaling transform, so a viewer set to 100% reproduces mm exactly.

- **Calibration must be two-axis and corner-placed.** A single horizontal 100 mm bar does not catch
  *anisotropic* scaling (X vs Y differing — common with "fit to printable area" on non-square
  margins) or rotation. Recommend an **L-shaped / two-axis calibration mark plus registration ticks
  near all four corners**, so X-scale, Y-scale, and clipping are each independently verifiable. The
  tolerance definition should state it applies *per axis*.

- **The physical print test is under-powered as written.** "≥ 1 A4 and ≥ 1 US-Letter printer"
  validates two devices. Inkjet vs laser, and especially the viewer/driver matrix above, are the real
  variance sources. The backlog item `research-005` (more printer models) should be pulled to M1 and
  reframed as a **viewer × driver × printer matrix** (Adobe Reader, Chrome/Edge built-in, macOS
  Preview, mobile print) — that is where mis-scaling originates, not the printer hardware alone.

**Mathematical correctness.** Solid. Relationship invariants (2×half = whole, 10×unit = rod, equal
intervals) are the right machine-checkable properties. Two additions: (1) verify the
**number-line/ruler tick origin and zero-offset**, not just interval equality — a ruler whose 0 is
not at a tick, or set in from the paper edge by an unstated amount, is a classic real-world error;
(2) for any future **protractor/pattern-block/clock** family, add **angular tolerance** (e.g.
± 0.5°) as a first-class invariant distinct from linear mm tolerance — angle error is the analogue of
scale error and the plan currently only quantifies length. A mis-scaled protractor or unequal clock
hour-marks is exactly the "harmful artifact" the guardrails warn about.

**Pedagogy (CRA).** The plan asserts pedagogical value but does not name the **Concrete →
Representational → Abstract** progression that is the standard justification for manipulatives, nor
position the printables within it. This is worth making explicit in the style guide and curriculum
mapping: physical paper manipulatives are the *Concrete* stage, and the project should note the known
research caveat that manipulatives only transfer to abstract understanding when **bridged**
(structured fading), not used in isolation — which is why the print-and-use instructions and teacher
quick-starts (`writing-003`) are pedagogically load-bearing, not optional. Recommend the
educator-review gate explicitly check "does the accompanying guidance support CRA bridging," not only
"is the artifact mathematically correct."

**Accessibility (tactile/low-vision).** Strong on contrast, colour-blind safety, large-print, and
Atkinson Hyperlegible (a genuinely good, OFL choice). Gaps: (1) **tactile/low-vision beyond
large-print** — the deepest accessibility win for a *paper* manipulative is that it can be cut, felt,
and manipulated; the plan defers braille/tactile to a backlog "sibling project?" (`design-003`) but
should at minimum specify **emboss/cut-friendly geometry** (minimum stroke widths, no reliance on
fine print, raised-line-compatible outlines) now, since it is nearly free at generation time and hard
to retrofit. (2) **Cut-accuracy as an accessibility AND correctness issue** — a tile is only
dimensionally true if cut on the line; the plan should specify cut-line placement (cut *on centre* vs
inside/outside the true edge) because a 0.5 mm line cut on the wrong side reintroduces the very error
the tolerance forbids, and is harder for low-vision/low-dexterity users. (3) Consider **uncut
"whole-sheet" usage modes** (e.g. number lines, hundred charts, ten-frames used un-cut) so the
manipulative works for users who cannot cut precisely.

**Paper size (A4 vs Letter).** Handled well (both from one spec, no full-bleed). One subtlety: A4
(210 × 297 mm) and Letter (215.9 × 279.6 mm) differ in **both** dimensions, so a layout that fits
N tiles per row on Letter may not on A4 and vice-versa; the plan should state that the **manipulative
geometry is identical across paper sizes and only the sheet layout/pagination differs** — never
rescale the manipulative to fill the page. This is implicit but should be an explicit invariant the
harness checks (same spec → identical element mm in both outputs).

**Licensing of source assets.** Excellent and appropriately conservative ("unknown = excluded",
embedding+redistribution required, content CC-BY-4.0 / code MIT). Minor: confirm the chosen palette's
*terms* — Okabe–Ito is a published convention and effectively free to use, but **ColorBrewer is
licensed Apache-2.0 with a specific attribution/registration request**; record that nuance. Also
record that **standards-framework text** (e.g. Common Core) used in the curriculum mapping has its
own lic ense terms — map *to* standard identifiers descriptively rather than reproducing standards
text, to stay clean.

**Scope.** Coherent and disciplined (paper-first, not an app, not SaaS, not freemium). The strongest
scoping risk is the **unsecured distribution channel**, which the plan is admirably honest about
(`verifiedNeed=false`, kill/pivot criteria). One scope suggestion: the backlog already lists
**rulers, protractors, clocks** implicitly (pattern blocks/angle types) — given that measurement
tools are the *highest-stakes* print-accuracy artifacts, consider explicitly naming a
"measurement-tools" family with its own angular-tolerance gate rather than folding it into "pattern
blocks."

---

## 2. Competitive landscape

The market splits into three groups: (A) **free virtual/interactive** manipulatives (strong, but
screen-dependent — they need a device per child, which low-resource classrooms lack); (B) **free
printable worksheets** (proprietary "free to use" terms, not openly licensed, accuracy not
guaranteed); (C) **freemium/marketplace** (paywalled or single-teacher licensed). No incumbent
combines *open license + machine-verified print accuracy + accessibility-by-default + paper-first*.

| Competitor | What it is | Strengths | Weaknesses (vs this project) |
|---|---|---|---|
| **The Math Learning Center** (Bridges) — [free manipulatives](https://www.mathlearningcenter.org/free-manipulatives), [Number Line app](https://www.mathlearningcenter.org/apps/number-line) | Free virtual apps + some pre-printed/perforated manipulatives | Pedagogically respected (Bridges curriculum), polished, free to use | **All-rights-reserved**: apps terms forbid "copying, reproduction, distribution… or creation of derivative works… without express written permission" ([Apps Terms](https://www.mathlearningcenter.org/apps/apps-terms)). Not openly licensed, not remixable; apps are screen-based |
| **Mathigon Polypad** (now Amplify) — [mathigon.org/polypad](https://mathigon.org/polypad), [polypad.amplify.com](https://polypad.amplify.com/) | Best-in-class free virtual manipulatives: fraction bars, number/algebra tiles, polygons; 19 languages | Excellent UX, breadth, multilingual, free | **Device-dependent** (every learner needs a screen); now under commercial owner (Amplify); not designed for accurate *printing*; closed asset/code |
| **Didax Virtual Manipulatives** — [didax.com](https://www.didax.com/math/virtual-manipulatives.html), [Base Ten Blocks](https://www.didax.com/apps/base-ten-blocks/) | 19 free virtual manipulatives (base-ten, ten-frames, number lines, Rekenrek, algebra tiles) | Broad, free, vendor-backed, classroom-aligned | Virtual/screen-based; a **storefront** for physical product sales; proprietary; no print-accuracy guarantee |
| **NCTM Illuminations** | Standards-aligned interactive applets (Ten Frame, Geometric Solids, etc.) | Authoritative (NCTM), standards-mapped | Interactive/screen-based, aging Flash-era tooling, narrow set, not print-first or openly licensed |
| **Toy Theater** — [fraction strips](https://toytheater.com/fraction-strips/), [virtual manipulatives](https://toytheater.com/category/teacher-tools/virtual-manipulatives/) | Free K-3 web manipulatives (counters, place value, fraction strips, Rekenrek) | Genuinely free, simple, no login | Screen-based; ad-supported; narrow grade band; proprietary |
| **Math-Drills** — [math-drills.com](https://math-drills.com/), [fractions](https://math-drills.com/fractions.php), [base ten](https://math-drills.com/baseten.php) | 58k+ free printable worksheets incl. fraction strips & base-ten | Huge volume, genuinely printable, free for school/home | Worksheet-centric not manipulative-centric; **proprietary "Terms of Use" (not CC)**; no stated print-scale guarantee or calibration; accuracy unverified |
| **K5 Learning** — [fractions](https://www.k5learning.com/free-math-worksheets/topics/fractions), [base-ten](https://www.k5learning.com/free-math-worksheets/first-grade-1/base-ten-blocks) | Free worksheets + paid workbooks | Free tier, parent-friendly | Worksheets not true manipulatives; freemium; proprietary; no accuracy/accessibility guarantee |
| **Twinkl** — [premium](https://www.twinkl.com/premium/choose) | Massive freemium resource library | Enormous catalogue, polished | **Freemium/paywalled** (~$5+/mo; "free" tier limited); criticised for misleading pricing & download caps ([Teach Simple review](https://teachsimple.com/blog/reviews/twinkl/)); proprietary; redistribution restricted |
| **Teachers Pay Teachers** — [copyright policy](https://www.teacherspayteachers.com/Copyright-Policy) | Marketplace of teacher-made printables | Vast variety, some free items | **Single-teacher license**, no redistribution/posting; quality & accuracy uncontrolled; not openly licensed — antithesis of OER scale |
| **NRICH** (Cambridge) | Free rich problem-solving tasks | Free, high pedagogical quality | Not a printable-manipulative provider (problem/investigation focus) — adjacent, not a direct competitor |

**Net read:** Group A wins on interactivity but **fails the core constraint** — a screen per child is
exactly what under-resourced classrooms lack (the PLAN's own premise). Groups B/C are printable but
**none are openly licensed AND print-accuracy-verified AND accessibility-gated**. That triple is the
open niche.

---

## 3. Gaps we can fill

1. **Open license, genuinely.** Nearly every "free" competitor is proprietary or single-teacher
   licensed (MLC all-rights-reserved; TPT single-teacher; Math-Drills/Twinkl proprietary ToU). A
   **CC-BY-4.0** set that NGOs, OER repos, and textbook projects can *legally redistribute, remix,
   translate, and bundle* is structurally absent.
2. **Machine-verified print accuracy.** No incumbent advertises a dimensional tolerance, a
   calibration mark, or a verification harness. "Print accuracy you can trust and self-check" is
   unclaimed territory.
3. **Paper-first for the no-device classroom.** The strongest free tools are virtual; this project
   serves the population those tools exclude.
4. **Grayscale/ink-saver as a designed mode**, not a colour PDF that degrades badly on a B&W laser.
5. **Accessibility-by-default** (contrast AA, colour-blind-safe-with-redundancy, large-print, legible
   open font, cut-friendly) — rare-to-absent in printable competitors.
6. **Reproducible from open specs** — community can fix/extend/translate without the original author;
   competitors' assets are closed.
7. **Provenance & verification records** per release — auditable correctness, which no incumbent
   offers.
8. **Measurement tools done right** (rulers, protractors, clocks) — the category most plagued by
   mis-scaling and the one where open + verified + calibrated would be most differentiated.

---

## 4. Differentiators to win

1. **"Verified-true or it doesn't ship."** A published, per-axis dimensional tolerance + automated
   harness + physical print test + self-check marks = a *trust* claim no competitor makes. This is the
   brand.
2. **Self-verifiable artifacts** via the calibration bar **and** credit-card overlay — every PDF is
   independently checkable forever, even orphaned, with no ruler required.
3. **Truly open (CC-BY-4.0 + MIT engine)** — the only set an NGO/OER repo can legally scale and
   localise.
4. **No-device, no-colour, low-cost by design** — works on the worst realistic printer for the
   poorest realistic classroom.
5. **Accessibility as a gate, not a feature** — included learners competitors exclude.
6. **A parametric engine, not a PDF dump** — infinite variants (ranges, denominations, paper sizes,
   languages, large-print) for free, all inheriting verification.

---

## 5. Claude API leverage — and where Claude must NOT decide

**Where Claude adds leverage (drafting/translation/orchestration — always human/deterministically
verified):**

- **Parametric spec authoring & expansion** — Claude drafts/edits `manipulative-spec` JSON (new
  families, denominations, ranges) and explains trade-offs; the spec is then rendered
  *deterministically* by code.
- **Generator/harness code** — Claude writes the TypeScript SVG→PDF generator and the
  dimensional/relationship verification harness, including edge-case tests (anisotropic scale,
  origin-offset, angular tolerance).
- **Instructions, teacher quick-starts, CRA bridging guidance, print-settings copy** — natural-language
  deliverables Claude is well-suited to draft for educator review.
- **Translation / numeral i18n** (`code-009`, `writing-004`) — Claude drafts localisation; native
  + math-educator review gates it.
- **Curriculum-standards mapping drafts** — Claude proposes mappings to standard identifiers;
  educator verifies; cite sources.
- **License/provenance triage** — Claude can *summarise* an asset's license and flag risk, but a human
  records the final clearance.
- **Accessibility copy & alt-text, colour-blind palette rationale** — drafted by Claude, audited by
  the accessibility reviewer.

**Where Claude must NOT be the decider (hard rule — these are deterministic or human gates):**

- **Geometric/scale correctness is NEVER trusted to the LLM.** Element mm, interval equality,
  composition invariants (2×half=whole, 10×unit=rod), and angular accuracy are decided by
  **deterministic generation + a measurement test**, not by an LLM "looking at" output. An LLM may
  *write* the generator/harness; it may not *vouch* for a number.
- **Physical print fidelity** — proven only by the human print-and-measure test against the
  calibration mark; no model judgement substitutes.
- **Pedagogical soundness** — math-educator review gate; Claude drafts, educator decides.
- **License/provenance final sign-off** — human-recorded; "unknown = excluded" is a human call.
- **Accessibility conformance** — computed contrast ratios + colour-blind simulation + human reviewer,
  not LLM assertion.
- **Representation/inclusivity of any imagery** — human review per guardrails.

The governing principle: **Claude generates candidates and code; correctness is established by
determinism, measurement, and qualified humans.** This matches the PLAN's "exactness is enforced by
code, not eyeballing."

**Top 3 highest-leverage Claude ideas:** (1) build the parametric **generator + verification harness**
(force-multiplier: every future family inherits exactness for free); (2) **variant/i18n explosion**
from one spec (paper sizes × colour modes × large-print × languages × numeral systems); (3)
**educator-facing collateral** (print-settings instructions, CRA teacher quick-starts, standards
mappings) drafted at scale for review.

---

## 6. Ten concrete optimizations

1. **Add a credit-card (ISO/IEC 7810 ID-1, 85.60 × 53.98 mm) overlay box** beside the 100 mm bar so
   users with no ruler can self-verify scale ([ISO/IEC 7810](https://en.wikipedia.org/wiki/ISO/IEC_7810)).
2. **Make calibration two-axis** (L-mark + four-corner registration ticks) to catch anisotropic
   scaling, rotation, and clipping — not just one horizontal length.
3. **Specify the PDF construction contract**: MediaBox = true paper size, no internal scale transform,
   so a viewer at 100% yields exact mm; add a CI check that parses the PDF box and asserts it.
4. **Expand the physical test to a viewer × driver matrix** (Adobe Reader, Chrome/Edge, macOS Preview,
   mobile) — that is where silent "fit-to-page" scaling originates
   ([WebView2 #3691](https://github.com/MicrosoftEdge/WebView2Feedback/issues/3691),
   [TeX FAQ](https://texfaq.org/FAQ-acroantics)); pull `research-005` forward to M1.
4. **Print a plain-language fail instruction** next to the bar ("This line must measure exactly
   100 mm / fit one credit card. If not, set printing to 100% / Actual Size and reprint.").
5. **Define cut-line side convention** (cut on centre vs inside/outside true edge) in the style guide
   so cutting doesn't reintroduce dimensional error; design for scissor + low-dexterity users.
6. **Add per-axis + angular tolerance** to the spec/harness now (even before angle families ship), so
   rulers/protractors/clocks have a correctness gate from day one.
7. **Verify origin/zero placement** for number lines and rulers as an explicit invariant (zero on a
   tick; known edge offset), not only interval equality.
8. **Assert geometry-identical-across-paper-sizes** in the harness (same spec → identical element mm
   on A4 and Letter; only layout differs).
9. **Bake CRA bridging guidance into the educator-review checklist** and teacher quick-starts so
   artifacts ship with the pedagogy that makes manipulatives transfer.
10. **Pin a deterministic, headless-browser-free SVG→PDF toolchain early** and snapshot-test byte/geo
    output in CI to guarantee cross-machine reproducibility (open question already flagged; make it an
    M1 blocker).

---

## 7. Parallel & perpendicular spin-offs

**Parallel (same engine, sibling Elyos OER projects):**

- **`numeracy-from-zero`** — the printables are the *Concrete* stage of its CRA pathway; co-design so
  number lines/ten-frames/base-ten map directly onto its lesson sequence. Strongest synergy.
- **`handwriting-practice`** — shares the *exact-print + calibration + open-font + A4/Letter +
  accessibility* infrastructure almost wholesale (letter-sizing must also be true-to-scale); the
  style guide and harness are largely reusable.
- **`oer-science-labs`** — shares **measurement-tool accuracy** (rulers, protractors, spectroscope
  scales, graph paper, timers/clocks): the angular/linear tolerance harness transfers directly; a
  mis-scaled lab ruler is the same hazard.
- **`oer-everything`** — the natural distribution/index home; the provenance + verification record
  format could become a shared OER quality standard.

**Perpendicular (new capabilities the work unlocks):**

- **A reusable "parametric print-accurate-artifact generation engine"** — extract `generator/` +
  `verify/` (spec → SVG → verified PDF, calibration, variant/i18n fan-out, dimensional/angular
  harness) as a standalone open library usable by *any* project needing physically-exact printables
  (maps, sewing/woodworking templates, graph paper, fold-up nets, science tools). This is the highest-
  value perpendicular asset.
- **An MCP server** exposing the generator/verifier as tools (`generate_manipulative(spec)`,
  `verify_dimensions(pdf)`, `expand_variants(spec)`) so any agent can request a *verified* printable
  and receive a pass/fail report — turning print-accuracy-as-a-service into reusable infrastructure
  while keeping the LLM out of the correctness decision (the MCP tool returns deterministic
  measurements, not model judgement).
- **A public "print-true" self-test/calibration page** as a tiny standalone good deed usable by the
  whole printable-education ecosystem.

---

## 8. Open questions

- **Which channel first?** (PLAN's #1 gap.) An OER repo (legally easiest for CC-BY) vs a teacher/NGO
  network (best delivery-to-learner). Does the first channel's audience use A4 or Letter, and
  Western-Arabic numerals — which would reorder i18n priority?
- **What is the correct per-family tolerance?** Is ± 0.5 mm right for both large fraction wholes and a
  10 mm base-ten unit, or do small units need a tighter absolute bound? What angular tolerance for
  protractors/clocks/pattern blocks?
- **Which deterministic SVG→PDF toolchain** is reproducible across contributor machines and CI without
  a headless browser, and does it let us fix MediaBox + suppress scaling transforms?
- **How do we close the viewer-scaling hole** for non-measuring users — is the credit-card overlay
  enough, or do we need a printed "trim-to-edge" registration approach for the most error-prone print
  paths?
- **Cut-accuracy in the field** — does real cutting hold tolerance, and should some families ship as
  uncut whole-sheets to avoid the cut-error problem entirely (and aid low-dexterity users)?
- **Standards-text licensing** — map to standard *identifiers* only, to avoid reproducing
  copyrighted standards prose?
- **Tactile/braille** — pull cut-/emboss-friendly geometry constraints into the M0 style guide
  (cheap now) even if full tactile variants stay backlog?

---

### Sources

- Math Learning Center — [Free Manipulatives](https://www.mathlearningcenter.org/free-manipulatives),
  [Number Line app](https://www.mathlearningcenter.org/apps/number-line),
  [Apps Terms of Use](https://www.mathlearningcenter.org/apps/apps-terms)
- Mathigon Polypad — [mathigon.org/polypad](https://mathigon.org/polypad),
  [polypad.amplify.com](https://polypad.amplify.com/)
- Didax — [Virtual Manipulatives](https://www.didax.com/math/virtual-manipulatives.html),
  [Base Ten Blocks](https://www.didax.com/apps/base-ten-blocks/)
- Toy Theater — [Fraction Strips](https://toytheater.com/fraction-strips/),
  [Virtual Manipulatives](https://toytheater.com/category/teacher-tools/virtual-manipulatives/)
- Math-Drills — [home](https://math-drills.com/), [fractions](https://math-drills.com/fractions.php),
  [base ten](https://math-drills.com/baseten.php)
- K5 Learning — [fractions](https://www.k5learning.com/free-math-worksheets/topics/fractions),
  [base-ten](https://www.k5learning.com/free-math-worksheets/first-grade-1/base-ten-blocks)
- Twinkl — [premium pricing](https://www.twinkl.com/premium/choose),
  [Teach Simple review](https://teachsimple.com/blog/reviews/twinkl/)
- Teachers Pay Teachers — [Copyright Policy](https://www.teacherspayteachers.com/Copyright-Policy)
- Print scaling — [Adobe: scale/resize printed pages](https://helpx.adobe.com/acrobat/kb/scale-or-resize-printed-pages.html),
  [TeX FAQ "acroantics"](https://texfaq.org/FAQ-acroantics),
  [WebView2 default Fit-to-Page issue #3691](https://github.com/MicrosoftEdge/WebView2Feedback/issues/3691)
- Printable ruler/protractor calibration — [Inch Calculator](https://www.inchcalculator.com/printable-protractor/),
  [LabelValue printable ruler](https://www.labelvalue.com/resources/printable-ruler)
- Calibration reference — [ISO/IEC 7810 (ID-1 = 85.60 × 53.98 mm)](https://en.wikipedia.org/wiki/ISO/IEC_7810)
