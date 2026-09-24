# Reconciliation Findings 2026 — Finance-Ops Screening Submission

A portfolio site of seven working papers on UAE finance-operations practice, built as a
job-screening deliverable. Every page is a standalone HTML document; every numeric figure
cited in the prose is anchored to a primary UAE government source and reproduced verbatim
in the relevant table.

**Live site:** <https://rams-lab-01.github.io/reconciliation-findings-2026/>

---

## Contents

- [The seven pages](#the-seven-pages)
- [Reading order](#reading-order)
- [Technology and accessibility](#technology-and-accessibility)
- [Source verification posture](#source-verification-posture)
- [Errata and post-submission corrections](#errata-and-post-submission-corrections)
- [Corrections made in this pass](#corrections-made-in-this-pass)
- [Repository layout](#repository-layout)
- [Running the site locally](#running-the-site-locally)
- [Authoritative sources used](#authoritative-sources-used)
- [A note on the screening context](#a-note-on-the-screening-context)

---

## The seven pages

| # | Page | Subject | Live link |
|---|------|---------|-----------|
| 1 | Task 1 · Reconciliation | Two-record reconciliation of an Aug 2026 cash account, plus a discovered control finding on cheque 0470 | [reconciliation-findings.html](https://rams-lab-01.github.io/reconciliation-findings-2026/reconciliation-findings.html) |
| 2 | Task 2 · Payables review | Document-by-document decisions on a queued payables run, with the four hold decisions and three VAT corrections itemised | [payables-review.html](https://rams-lab-01.github.io/reconciliation-findings-2026/payables-review.html) |
| 3 | Task 3 · Funding plan | November cash-trajectory under three scenarios: with USD 75k draw on Wed 4, with no funding at all, and against the AED 25k buffer floor | [funding-plan-november-2026.html](https://rams-lab-01.github.io/reconciliation-findings-2026/funding-plan-november-2026.html) |
| 4 | Task 4 · Spend review | Three-month FinOps executive dashboard with 14 spend categories, anomaly register, and one-line KPI tiles | [spend-review.html](https://rams-lab-01.github.io/reconciliation-findings-2026/spend-review.html) |
| 5 | Task 5 · Automation design | Monthly-close automation on Make.com, Claude, Google Workspace and Todoist: an 8-step pipeline with 3 human gates, failure modes, data-security posture and the verbatim first prompt | [task-5-automation-design.html](https://rams-lab-01.github.io/reconciliation-findings-2026/task-5-automation-design.html) |
| 6 | Task 6 · Rules verification | Twelve-statement verdict on an AI-generated briefing memo, source-by-source | [task-6-finance-rules-check.html](https://rams-lab-01.github.io/reconciliation-findings-2026/task-6-finance-rules-check.html) |
| 7 | Task 6 · Audit response | Independent audit of the Task 6 verdict sheet against the criteria of the page that produced it | [task-6-audit-response.html](https://rams-lab-01.github.io/reconciliation-findings-2026/task-6-audit-response.html) |

An index page carries the top-line navigation, the errata block, and the per-page links:
[index.html](https://rams-lab-01.github.io/reconciliation-findings-2026/index.html).

A formal one-page business-letter memorandum accompanies the spend review:
[spend-review-memorandum.html](https://rams-lab-01.github.io/reconciliation-findings-2026/spend-review-memorandum.html).

---

## Reading order

For a quick read in roughly fifteen minutes:

1. `index.html` — top-line navigation and post-submission corrections
2. `reconciliation-findings.html` — the centrepiece; demonstrates the working method
3. `payables-review.html` — applies the same method to a release-or-hold decision
4. `funding-plan-november-2026.html` — three-trajectory scenario modelling
5. `spend-review.html` — the dashboard, all fourteen categories in one place
6. `task-5-automation-design.html` — the Make.com monthly-close pipeline (8 steps, 3 human gates)
7. `task-6-finance-rules-check.html` and `task-6-audit-response.html` — the rule-by-rule verification pair

The two Task 6 pages are intended to be read together: the verification sheet stands on its own
and shows the twelve-statement verdict; the audit response shows that the verdict sheet
itself satisfies the criteria the original AI brief failed on.

---

## Technology and accessibility

The site is plain HTML with no build step and no JavaScript bundler. The only runtime
dependencies are two CDN scripts:

- **Chart.js 4.4.4** for all numeric visualisations except the Task 5 flowchart
- **Mermaid 10** for the Task 5 process flowchart only

Both are loaded with `integrity` and `crossorigin` attributes; the SRI hashes are
**computed at publish time** by SHA-384 of the actual file as served by jsDelivr, not
copied from a third-party table.

### Charts per page

| Page | Charts |
|------|--------|
| Task 1 | Chart A: four signed reconciling items (nets to AED 13,063.75 cashbook error). Chart B: CHQ 0470 timing exposure, kept on a separate axis because it is a zero-cashbook-difference control item. |
| Task 2 | One stacked bar: six released components tie exactly to AED 74,905.00; eight prevented components tie exactly to AED 91,838.38. |
| Task 3 | Three-series line: with-funding path, no-funding path, and the AED 25,000 buffer floor as the third series. X-axis dates are body-verbatim, not assumed. |
| Task 4 | Five charts: cash-flow grouped bar, monthly-deficit bar, anomaly impact by finding, all fourteen categories (replacing the original four-bucket pie with the full body list), and annualised-recurring exposure. |
| Task 6 | Verdict doughnut: seven WRONG / three CORRECT / two INCOMPLETE = twelve. |

### Accessibility

Every `<canvas>` carries `role="img"` and `aria-describedby`, pointing at a paragraph
that reads the chart's data aloud in prose. Adjacent to every chart is a
`<table class="visually-hidden">` holding the same numbers in tabular form, so a screen
reader can navigate the data row by row rather than only as a single image description.
The `.visually-hidden` utility is the standard clip-rect technique — not `display:none`,
which screen readers skip.

The site respects the user-side `prefers-reduced-motion` media query and disables all
chart animation when that flag is set. The print stylesheet hides the top navigation
and constrains canvas and SVG heights so each task prints on a defined page count
without splitting a chart across pages.

---

## Source verification posture

The site's central claim is that every numeric figure cited in the prose is anchored
to a primary UAE government or FTA source and is reproducible in the prose body. Each
page also carries a "Sources" section naming the official domain used.

| Source | Domain | Used for |
|--------|--------|----------|
| Federal Tax Authority | [tax.gov.ae](https://www.tax.gov.ae) | VAT thresholds and returns, CT return deadline, SBR threshold and sunset, natural-person basis, administrative penalties |
| Ministry of Finance | [mof.gov.ae](https://www.mof.gov.ae) | E-invoicing programme, Cabinet Decision 43/2025 |
| Central Bank of the UAE | [centralbank.ae](https://www.centralbank.ae) | Cheques FAQ, Federal Decree-Law 50/2022 partial payment |
| Official UAE Government | [u.ae](https://u.ae) | Corporate tax rules, Wages Protection System scope |
| Ministry of Human Resources | [mohre.gov.ae](https://www.mohre.gov.ae) | WPS applicability |

Two non-government secondary sources are quoted only where they corroborate a primary
text and are flagged as such in-line.

The site holds a **strict no-invented-numbers rule**. Any figure that does not appear
in a primary source cited on the same page is annotated as **[DERIVED]** with the
arithmetic shown, or as a derivation from a body-verbatim figure. The chart captions
expose this commitment: every component plotted can be reconciled line by line to a
figure in the page's body table.

---

## Errata and post-submission corrections

Three items were corrected after the original submission on 22 September 2026. The
errata block at the top of `index.html` documents each one and the legal source that
drove the correction:

| # | Page | Original claim | Corrected position | Authority |
|---|------|----------------|--------------------|-----------|
| 1 | Task 2 | "Recover the reverse-charge VAT in VAT 201 Box 9" | The correct box is **Box 10**. The Box 9 exclusion list states expressly that purchases subject to reverse charge are recovered in Box 10, not Box 9. | FTA VAT Returns User Guide |
| 2 | Task 6 | "E-invoicing service-provider appointment deadline" | Deadline is **30 October 2026**, moved from 31 July 2026 by Ministerial Resolution No. 66 of 2026. Mandatory issuance begins 1 January 2027 for large taxpayers. | Ministerial Resolution 66/2026 amending 244/2025 |
| 3 | Task 6 | Statement 7 verdict on Small Business Relief | Threshold remains **AED 3 million** unchanged; relief extended by Ministerial Decision No. 131 of 2026 to tax periods ending on or before **31 December 2029**. SBR remains unavailable to a Qualifying Free Zone Person. | MD 131/2026 |

Two additional corrections from the original AI brief are folded into the verdict sheet
itself: Statement 4's penalty was reduced from AED 20,000 to AED 10,000 by Cabinet Decision
No. 49 of 2021, and Statement 8's cheque-bouncing rule is grounded in Federal Decree-Law
No. 14 of 2020 and Article 648(2) of Federal Decree-Law No. 50 of 2022 (partial
payment), with Article 667 reserved for the executive-instrument provision.

---

## Corrections made in this pass

Three further corrections were applied in this commit. All three were present on the
live site as a result of transcription drift introduced when the chart layer was
written; the corrections restore body-verbatim figures everywhere.

| Page | What was wrong | What is now right |
|------|----------------|-------------------|
| Task 2 | The payables-review chart and decisions table recorded D8 at AED 33,600.00 | D8 is now recorded at AED **31,500.00** (the brief shows 30,000 base + 1,500 VAT for QTN-0881) |
| Task 2 | The chart's D5 and D6 vendor labels read "Marina (corrected)" and "Horizon (net)" — Marina Yacht Club is the Task 4 anomaly A5, not a Task 2 vendor | D5 is now "Horizon Office Supplies LLC (INV-9142, stationery/toner, corrected VAT)"; D6 is now "Emirates Secure Couriers (ESC-4471, no TRN)" |
| Task 2 | The KPI tile led with "Diversion attempt intercepted AED 6,300.00" — 6,300 is the genuine invoice value, but the cash stopped tonight is 6,800 | The tile now reads "Diversion attempt intercepted AED 6,800.00", with 6,300 carried in the subtext as the genuine invoice still owed to the real vendor on 28 August |

With D8 corrected, the eight prevented components on the chart
(D7 + D8 + D9 + D10 cash + D4 reduction from D10 credit + D3 non-resident VAT
+ D5 VAT overclaim + D6 VAT withheld, no TRN) sum exactly to the page-stated
AED 91,838.38. The clerk's run of AED 166,743.38 also reconciles line by line
to the queued-amounts body table. There is no residual.

---

## Repository layout

```
reconciliation-findings-2026/
├── index.html                            Top-line navigation and post-submission corrections
├── reconciliation-findings.html          Task 1 — reconciliation working paper
├── payables-review.html                  Task 2 — document-by-document decisions
├── funding-plan-november-2026.html       Task 3 — three-trajectory cash model
├── spend-review.html                     Task 4 — FinOps dashboard
├── spend-review-memorandum.html          Companion formal one-page memo to Task 4
├── task-5-automation-design.html         Task 5 — Make.com close pipeline, 8 steps / 3 gates
├── task-6-finance-rules-check.html       Task 6 — twelve-statement verdict
├── task-6-audit-response.html            Task 6 audit — independent review
└── README.md                             This file
```

Every page is standalone. There is no shared CSS file and no shared JavaScript file.
Each page inlines its styles and scripts. This is intentional: a reviewer who pulls
a single HTML file from the URL bar gets a complete document with no relative-path
dependencies, which matters when GitHub Pages renames the upstream repo.

---

## Running the site locally

Because each page is self-contained, previewing requires only a static file server.

```bash
# From the repository root, any of these works:
python -m http.server 8000
# or
npx serve .
# or
ruby -m webrick .
```

Open `http://localhost:8000/index.html` and follow the in-page links.

Charts load from `https://cdn.jsdelivr.net/npm/chart.js@4.4.4/...` and Mermaid from
`https://cdn.jsdelivr.net/npm/mermaid@10/...`. Both are loaded with the `defer` attribute
and an `integrity` value computed from the actual file as served.

To verify the SRI of the current Chart.js release yourself:

```bash
curl -sL "https://cdn.jsdelivr.net/npm/chart.js@4.4.4/dist/chart.umd.min.js" \
  | openssl dgst -sha384 -binary \
  | openssl base64 -A \
  | awk '{print "sha384-"$0}'
```

The result should match the value in the `integrity` attribute of every Chart.js
script tag on the site.

---

## Authoritative sources used

- **Federal Decree-Law No. 8 of 2017** — VAT
- **Federal Decree-Law No. 47 of 2022** — Corporate Tax
- **Federal Decree-Law No. 14 of 2020** — cheques criminalisation
- **Federal Decree-Law No. 50 of 2022** — Commercial Transactions, Article 648(2) (partial payment), Article 667 (executive instrument)
- **Cabinet Decision No. 43 of 2025** — e-invoicing programme
- **Cabinet Decision No. 49 of 2021** — late-registration penalty AED 10,000 (reduced from AED 20,000 with effect 28 June 2021)
- **Cabinet Decision No. 55 of 2023** — Qualifying Free Zone Person
- **Cabinet Decision No. 75 of 2023** — late-filing penalties (AED 500 lower tier, AED 1,000 upper tier, 14% per annum on unpaid tax)
- **Cabinet Decision No. 32 of 2023** — transfer-pricing and record-keeping
- **Cabinet Decision No. 106 of 2025** — e-invoicing violations and administrative penalties
- **Ministerial Decision No. 73 of 2023** — Small Business Relief original sunset
- **Ministerial Decision No. 131 of 2026** — SBR extension to tax periods ending on or before 31 December 2029
- **Ministerial Resolution No. 244 of 2025** — e-invoicing service-provider appointment (original)
- **Ministerial Resolution No. 66 of 2026** — moved service-provider deadline from 31 July 2026 to 30 October 2026
- **CBUAE Cheques FAQ** — Federal Decree-Law 50/2022 cheque practice

---

## A note on the screening context

This site was prepared as a single deliverable for a job-screening application in UAE
finance operations. The seven tasks are not unrelated — they are the same set of skills
(procurement and reconciliation, cash-flow modelling, vendor and anomaly review,
automation scoping, rule-by-rule verification, and audit-of-audit) applied to a single
office's books. A reviewer who reads the site in the order above should be able to see
the working method carry across tasks, including the corrections that were made both
before submission (Statements 4 and 8) and after (Box 10, e-invoicing deadline, SBR
extension).

The repository contains only published HTML, so that every commit in the public
history is also a deployable artifact. There are no private drafts, no staging
branches, and no build artifacts in the source history.

---

*Last updated 23 September 2026.*
