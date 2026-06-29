# TASKS — math-manipulatives-printables

> Status: Draft · Version: 0.1.0 · Last updated: 2026-06-28 · Owner: TBD (maintainer) · Lane: donated

Backlog for the `math-manipulatives-printables` good-deed project. Read alongside `PLAN.md` (same
directory).

## How these tasks map to Elyos

Every task here becomes a **Task JSON** validated by `packages/schema/src/schemas.ts`. Field mapping:

- `id` — stable, e.g. `math-manip-spec-001` (the table's ID column).
- `title` — the task title.
- `project` — `"math-manipulatives-printables"` for all tasks.
- `type` — one of `code | research | writing | data | design-spec | maintenance` (per task). Generator/
  harness work → `code`; spec/PDF-generation runs → `data`; design references → `design-spec`; style
  guide / mappings / instructions → `writing`; channel-securing / audits / validation → `research`;
  upkeep → `maintenance`.
- `lane` — `"donated"` for all tasks (the human runs their own agent; CLI preps workspace + PR). No
  `funded` tasks here, so `fundedBudgetUsd` is not required.
- `priority` — `high | medium | low`.
- `domain` — array, e.g. `["education","mathematics","open-content","accessibility"]`.
- `riskTier` — `low | medium | high`. **Project is low risk overall.** Tasks whose correctness is
  *domain-accuracy-critical* (dimensional/relationship verification, math-educator-reviewed designs,
  curriculum mapping, accessibility) are set to `medium` to force a qualified reviewer; routine
  authoring/tooling is `low`. **No `high` tasks exist** (no medical/legal/safety content).
- `urgent` — boolean (default `false`; nothing is time-critical).
- `deliverable` — `pr | dataset | document | translation`. Code → `pr`; generated PDFs/specs →
  `dataset`; style guide / mappings / instructions → `document`; numeral i18n of text → `translation`.
- `tokenEstimate` — `small | medium | large` (the table's Size column).
- `status` — `open | in-progress | review | delivered | done` (all start `open`).
- `context`, `objective`, `acceptanceCriteria[]`, `resources[]`, `output` — task body fields.
- `requestor` — proposer/maintainer.
- `verifiedNeed` — **`false`** for delivery-dependent tasks until a distribution channel is secured
  (see PLAN "partner gap"); **`true`** only where the artifact is self-evidently useful and not
  channel-dependent (e.g. the style guide, the spec schema, the verification harness).
- `outputLicense` — **MIT** for code; **CC-BY-4.0** for generated content/specs/docs (host license if
  a secured channel requires otherwise).

The production pattern is fan-out by **(manipulative family × paper size × colour mode × accessibility
variant)** — all derived from one parametric spec. The `*-gen-*` and `*-spec-*` tasks below are the
templates for that fan-out.

---

## Milestone M0 — Foundation & cold-start

Prove one manipulative family can travel from spec → dimensionally + physically verified →
distributed.

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
|---|---|---|---|---|---|---|---|
| math-manip-style-001 | Author print & accessibility style guide v1 | writing | small | low | document | — | Maintainer + Accessibility reviewer |
| math-manip-spec-001 | Define `manipulative-spec` schema + provenance/verification record | data | small | low | dataset | style-001 | Maintainer |
| math-manip-research-001 | Open-asset license clearance (fonts + palettes) | research | small | low | document | — | Maintainer |
| math-manip-research-002 | Secure ≥1 distribution channel (OER repo / teacher network / NGO) | research | medium | low | document | — | Maintainer + Steward |
| math-manip-design-001 | Reference design + dimensional spec: fraction tiles (halves–twelfths) | design-spec | medium | medium | document | style-001, spec-001 | Math-educator reviewer |
| math-manip-data-001 | Generate + dimensionally verify cold-start fraction-tile set (A4+Letter, colour+grayscale) | data | medium | medium | dataset | design-001, research-001 | Math-educator + Print-test reviewer |
| math-manip-writing-001 | Print-and-use instructions + recommended print settings | writing | small | low | document | data-001 | Maintainer |
| math-manip-pr-001 | Distribute cold-start set via secured channel + establish baseline tracking | maintenance | small | low | pr | research-002, data-001, writing-001 | Steward |

**Sequencing — securing a channel gates the "delivered" claim.** `research-002` blocks `pr-001`: no
set is *published as delivered* until ≥ 1 channel is confirmed. The cold-start family (`design-001`,
`data-001`) can be built and verified in parallel since the artifacts are self-evidently useful and
reusable. **Kill/pivot:** if the time-boxed channel-securing effort confirms no channel, pivot to the
next candidate or pause distribution while keeping the verified artifacts public (per PLAN).

**Key task acceptance criteria**

- **math-manip-style-001** (print & accessibility style guide v1)
  - [ ] Defines the canonical unit (mm) and the verification **tolerance** (± 0.5 mm or ± 0.5 %,
        whichever is larger), plus the requirement to verify *relationships* (e.g. halves compose to a
        whole), not only element sizes.
  - [ ] Specifies **A4 + US Letter**, conservative no-full-bleed safe margins, and the mandatory
        embedded **100 mm calibration bar** on every sheet.
  - [ ] Defines colour modes (**colour / grayscale / ink-saver outline**) and forbids colour-only
        encoding (shape/label/pattern redundancy required).
  - [ ] Defines accessibility rules: contrast ≥ WCAG AA, large-print + high-contrast variants, an
        open legible font, and scissor-followable cut guides.
  - [ ] Published, versioned, licensed **CC-BY-4.0**.

- **math-manip-research-002** (secure distribution channel)
  - [ ] Evaluates candidate channels in priority order (OER repos → teacher/homeschool networks/NGOs →
        project-owned repo fallback) with each one's acceptance posture and submission/attribution
        terms.
  - [ ] Identifies ≥ 1 concrete channel that will **host and surface** the printables to learners
        (the fallback repo alone does **not** satisfy this).
  - [ ] Records that channel's required output license + attribution format and any submission process.
  - [ ] States the time-box and kill/pivot criteria; on success flips `verifiedNeed=true` for
        delivery-dependent tasks targeting that channel.

- **math-manip-design-001** (fraction-tile reference design + dimensional spec)
  - [ ] Declares nominal physical dimensions (mm) for the whole and each denomination (halves through
        twelfths) such that they **compose exactly** (e.g. 2 halves == 1 whole within tolerance).
  - [ ] Specifies labelling that is unambiguous (e.g. "1/3") and non-colour-dependent distinctions
        between fraction families.
  - [ ] Conforms to style-guide v1 (paper sizes, margins, calibration bar, colour modes,
        large-print).
  - [ ] **Math-educator reviewed** for mathematical/pedagogical correctness; reviewer recorded.

- **math-manip-data-001** (generate + verify cold-start set)
  - [ ] A4 + US Letter × colour + grayscale generated from the spec.
  - [ ] **Automated dimensional verification passed** — all declared dimensions *and relationships*
        within tolerance.
  - [ ] **Physical print test passed** — printed at 100 % on a real A4 and a real US-Letter printer
        and measured with a ruler against the calibration bar, within tolerance; result recorded.
  - [ ] Accessibility checks passed (contrast AA; no colour-only encoding; legal embedded font).
  - [ ] Only **open** (OFL/Apache/PD) fonts/palettes used; license + attribution recorded.

**M0 Definition of Done:** style guide v1 + spec schema published; open-asset licenses cleared; ≥ 1
distribution channel confirmed; cold-start fraction-tile set generated, **dimensionally + physically +
accessibility verified and math-educator-reviewed**, distributed via the channel with print-and-use
instructions; baseline outcome tracking established; zero license violations.

---

## Milestone M1 — Generator & core set

Turn the manual cold-start into a parametric generator + automated verification, and ship all four
core families.

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
|---|---|---|---|---|---|---|---|
| math-manip-code-001 | Build parametric generator engine (spec → SVG → print-ready PDF) | code | large | low | pr | spec-001, design-001 | Maintainer |
| math-manip-code-002 | Automated dimensional + relationship verification harness (CI gate) | code | large | medium | pr | spec-001 | Maintainer + Math-educator reviewer |
| math-manip-code-003 | Counters generator (two-colour + plain) | code | medium | low | pr | code-001, code-002 | Math-educator reviewer |
| math-manip-code-004 | Number-line generator (integer/fraction/decimal/blank; ranges + steps) | code | large | medium | pr | code-001, code-002 | Math-educator reviewer |
| math-manip-code-005 | Base-ten blocks generator (unit/rod/flat + thousand-cube net) | code | large | medium | pr | code-001, code-002 | Math-educator reviewer |
| math-manip-design-002 | Colour-blind-safe palette + grayscale/ink-saver design system | design-spec | small | medium | document | style-001 | Accessibility reviewer |
| math-manip-data-002 | Generate + verify full core set (4 families, both paper sizes, colour+grayscale) | data | large | medium | pr | code-003, code-004, code-005, design-002 | Math-educator + Print-test reviewer |

**Key task acceptance criteria**

- **math-manip-code-002** (verification harness)
  - [ ] Parses generated geometry and asserts every declared dimension within tolerance.
  - [ ] Asserts declared **relationship invariants** (e.g. 10×unit == 1×rod; equal number-line
        intervals; denomination tiles compose to a whole).
  - [ ] Runs in **CI and blocks** any out-of-tolerance release; emits an auditable report (no secrets).
  - [ ] Includes accessibility sub-checks: contrast ≥ AA, colour-blind simulation (no colour-only
        encoding), embedded-font legality.

- **math-manip-code-001** (generator engine)
  - [ ] Deterministic spec → SVG → PDF with physical dimensions locked in mm; reproducible across
        machines (no required headless browser in the core path).
  - [ ] One spec fans out to **A4/Letter × colour/grayscale/ink-saver × standard/large-print**.
  - [ ] Embeds the 100 mm calibration bar and conservative no-full-bleed margins automatically.
  - [ ] MIT-licensed; DCO-signed.

- **math-manip-code-004** (number-line generator)
  - [ ] Supports integer, fraction, decimal, and blank/open lines with configurable range + step.
  - [ ] **Intervals are provably equal** and origin/direction correct (verified by harness +
        math-educator review).
  - [ ] Works in grayscale; labels legible at standard and large-print sizes.

- **math-manip-data-002** (full core set)
  - [ ] All four families generated, dimensionally + accessibility verified, **physically print-tested**
        on A4 + US Letter, and math-educator-reviewed.
  - [ ] Each family distributed through ≥ 1 channel; zero license violations.

**M1 Definition of Done:** generator + verification harness live with CI gating; all four core
families generated, verified, educator-reviewed, physically print-tested, and distributed; zero
license violations.

---

## Milestone M2 — Accessibility, breadth & validation

Ship accessible variants and more denominations/ranges, and validate with real learners.

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
|---|---|---|---|---|---|---|---|
| math-manip-code-006 | Large-print + high-contrast variants of all four core families | code | medium | medium | pr | code-001, design-002 | Accessibility reviewer |
| math-manip-research-003 | Accessibility audit (contrast ratios + colour-blind simulation) across the set | research | small | medium | document | data-002, code-006 | Accessibility reviewer |
| math-manip-research-004 | Beneficiary validation: educator/family uses printed sets | research | small | low | document | data-002 | Maintainer + Steward |
| math-manip-writing-002 | Curriculum-standards mapping for the four families | writing | medium | medium | document | data-002 | Math-educator reviewer |
| math-manip-data-003 | Expand denominations/ranges; publish expanded verified set | data | medium | medium | pr | code-004, code-005, research-004 | Math-educator + Print-test reviewer |

**Key task acceptance criteria**

- **math-manip-research-004** (beneficiary validation)
  - [ ] ≥ 1 educator/family per manipulative family **prints and uses** a set and confirms it is
        dimensionally correct and usable in practice.
  - [ ] Findings (legibility, cut difficulty, mislabels, print issues) fold back into specs/style
        guide as concrete change requests.

- **math-manip-research-003** (accessibility audit)
  - [ ] Confirms contrast ≥ WCAG AA for all text/numerals across colour and grayscale.
  - [ ] Colour-blind simulation confirms no information lost without colour for any family.
  - [ ] Large-print variant confirmed adequate for low-vision use; gaps logged as tasks.

- **math-manip-writing-002** (curriculum-standards mapping)
  - [ ] Each released family mapped to ≥ 1 common standards framework, descriptively (non-prescriptive,
        non-partisan).
  - [ ] Sources cited; mapping published CC-BY-4.0.

**M2 Definition of Done:** large-print/high-contrast variants released and verified; accessibility
audit passed; ≥ 1 beneficiary validation per family with findings folded back; curriculum mapping
published; expanded set verified and distributed.

---

## Milestone M3 — Broaden & sustain

Add more manipulative types and a durable maintenance model.

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
|---|---|---|---|---|---|---|---|
| math-manip-code-007 | Generators: ten frames, hundred charts, place-value charts | code | large | medium | pr | code-001, code-002 | Math-educator reviewer |
| math-manip-code-008 | Pattern blocks / geometric shapes (angle + edge accuracy) | code | large | medium | pr | code-001, code-002 | Math-educator reviewer |
| math-manip-code-009 | Internationalised numerals (≥1 additional numeral system) | code | medium | medium | translation | code-001 | Math-educator + native reviewer |
| math-manip-writing-003 | Teacher quick-start guides per manipulative family | writing | medium | low | document | data-002 | Maintainer |
| math-manip-maint-001 | Outcome dashboard + generator/font/toolchain maintenance | maintenance | medium | low | pr | data-002 | Maintainer |

**M3 Definition of Done:** ≥ 3 additional families (incl. one angle-critical) generated and verified;
≥ 1 additional numeral system shipped; teacher guides published; outcome dashboard live; documented
maintainer + reviewer rotation in effect.

---

## Backlog / future (sized, unscheduled)

| ID | Title | Type | Size | Risk | Deliverable | Notes |
|---|---|---|---|---|---|---|
| math-manip-code-010 | Algebra tiles / integer chips extension | code | medium | medium | pr | New family; relationship invariants critical |
| math-manip-code-011 | Clock faces / time manipulatives | code | medium | low | pr | Angle accuracy matters |
| math-manip-code-012 | Money manipulatives (currency-neutral templates) | code | medium | low | pr | Avoid implying any specific legal-tender reproduction |
| math-manip-writing-004 | Instructional-text translation (multilingual) | writing | large | medium | translation | Pull forward if first channel is non-English |
| math-manip-research-005 | Cross-printer print-fidelity testing (more printer models) | research | medium | low | document | Strengthens physical-print confidence |
| math-manip-design-003 | Tactile/braille-friendly manipulative variants (sibling project?) | design-spec | large | medium | document | High accessibility value; may exceed scope |
| math-manip-code-013 | Print-saver layouts (max pieces per sheet) per family | code | small | low | pr | Reduces paper/ink cost for high-volume use |

---

## Example task JSON

Complete, schema-valid Task JSON for the first M0 task. `verifiedNeed` is `true` here: a published,
openly-licensed print & accessibility style guide is a self-evidently useful artifact and does not
depend on a distribution channel being secured (unlike the `pr`/distribution tasks, which are `false`
until M0's channel is confirmed).

```json
{
  "id": "math-manip-style-001",
  "title": "Author print & accessibility style guide v1",
  "project": "math-manipulatives-printables",
  "type": "writing",
  "lane": "donated",
  "priority": "high",
  "domain": ["education", "mathematics", "open-content", "accessibility"],
  "riskTier": "low",
  "urgent": false,
  "deliverable": "document",
  "tokenEstimate": "small",
  "status": "open",
  "context": "Printable math manipulatives (counters, number lines, fraction tiles, base-ten blocks) are only useful if they print at the correct physical size on ordinary printers and are accessible to all learners. A dimensionally wrong fraction tile or an unequal number line teaches a false mathematical relationship. Before any manipulative is designed or generated, the project needs one versioned style guide so that every printable from many parallel AI sessions is exact, printable on consumer printers in both A4 and US Letter, usable in grayscale, and accessible by default.",
  "objective": "Write and publish version 1 of the print & accessibility style guide that all design and generation tasks will follow.",
  "acceptanceCriteria": [
    "Defines the canonical unit (mm) and the verification tolerance (+/- 0.5 mm or +/- 0.5%, whichever is larger), and requires verifying relationships (e.g. two halves compose to one whole), not only individual element sizes.",
    "Specifies support for both A4 and US Letter, conservative no-full-bleed safe margins, and a mandatory embedded 100 mm calibration bar on every sheet.",
    "Defines colour modes (colour / grayscale / ink-saver outline) and forbids colour-only encoding (shape, label, or pattern redundancy is required).",
    "Defines accessibility rules: text/numeral contrast at least WCAG AA, large-print and high-contrast variants, an open legible font, and scissor-followable cut guides.",
    "Is published, versioned, and licensed CC-BY-4.0."
  ],
  "resources": [
    "C:\\code\\elyos\\planning\\projects\\math-manipulatives-printables\\PLAN.md",
    "WCAG 2.x contrast and non-text-content guidance",
    "SIL Open Font License; Okabe-Ito colour-blind-safe palette"
  ],
  "output": "A versioned style-guide document (style-guide/print-accessibility-style-guide.md), CC-BY-4.0, covering units and tolerance, paper sizes and safe margins, the calibration bar, colour modes, accessibility rules, fonts, and cut guides.",
  "requestor": "jdev1977",
  "verifiedNeed": true,
  "outputLicense": "CC-BY-4.0"
}
```

## Review sign-off

- **Schema validity:** every task maps to required Task fields; `type`, `deliverable`, `riskTier`,
  `tokenEstimate`, `status`, `priority`, `lane` use only enum values; example JSON uses
  `additionalProperties`-safe keys and ASCII-safe strings (no raw `±` in JSON). ✔
- **Honesty:** delivery-dependent tasks (`pr-001`, distribution) carry `verifiedNeed=false` until a
  channel is secured; channel-independent artifacts (style guide, spec schema, harness) are `true`. ✔
- **Risk:** low overall; `medium` reserved for domain-accuracy-critical tasks (verification, math-
  educator-reviewed designs, accessibility, curriculum mapping); **no `high` tasks** (no medical/
  legal/safety). ✔
- **Coverage:** 25 tasks across 4 milestones + 7 backlog (8 in M0, 7 in M1, 5 in M2, 5 in M3),
  each with size/risk/reviewer, acceptance criteria for the key tasks, and milestone DoD; aligned to
  PLAN.md roadmap exit criteria. ✔
- **Correction during review:** money-manipulative backlog item annotated to avoid implying
  reproduction of any specific legal-tender currency (kept currency-neutral).
