# HTS Duty Calculator

**Live:** _add your Vercel URL here after deploying — `/hts-calculator`_

An interactive HTS code lookup and duty calculator for US apparel imports. Built as a portfolio demonstration of applied trade compliance tooling, combining a step-by-step classification workflow with real-time duty calculation across base rates, Section 301 tariffs, IEEPA reciprocal tariffs, and FTA benefit offsets.

> **Disclaimer:** Duty rates are illustrative and require independent verification with USITC, CBP, and current USTR executive orders before making sourcing or entry decisions. This is not legal or customs advice.

---

## What it solves

HTS classification for apparel is a multi-variable problem: the correct 10-digit code depends on construction method, product type, fiber composition, special requirements, and gender/age category — in that order, following the USITC hierarchy. Most importers resolve this manually against the HTS schedule or via a customs broker.

This tool replicates that classification logic as a guided, progressive interface, then layers in the country-specific tariff adjustments (Section 301, IEEPA, FTA) that determine the actual landed duty cost.

---

## How it works

The calculator walks through six steps that progressively narrow the HTS code:

| Step | Input | What it reveals |
|---|---|---|
| 1 | Construction (Knitted / Woven) | HTS Chapter (61 or 62) |
| 2 | Product type | 4-digit heading |
| 3 | Fiber content | 6-digit subheading |
| 4 | Special requirement | 8-digit statistical suffix start |
| 5 | Gender / age group | Full 10-digit HTS code + base duty |
| 6 | Country of origin | Section 301, IEEPA, FTA adjustments → final duty |

Each step filters the available options based on prior selections, so only valid combinations are ever shown. The HTS code display updates progressively as each step is completed, filling in from left to right until the full 10-digit code is resolved.

---

## Duty calculation logic

Once the HTS code and country are selected, the calculator applies:

```
Final duty = (Base duty × (1 − FTA discount%)) + Section 301% + IEEPA%
```

Special cases:
- **FTA 100%** → displays as `FREE (FTA)` regardless of base rate
- **Compound rates** (e.g. `61.7¢/kg + 16%`) → displays the formula with any additive tariffs appended
- **Color coding** → green for low/free, red for high additional tariffs

---

## Features

- **Progressive HTS code builder** — code fills in character by character as each step is completed
- **Cascading dropdowns** — each step filters options based on all prior answers; no invalid combinations possible
- **Auto-advance** — if a step has only one valid option, it selects automatically
- **Country duty breakdown** — shows Base, Section 301, IEEPA, and FTA as separate line items before the final rate
- **In-browser CSV upload** — update reference data without touching code (see below)
- **Widget / embed mode** — pass `?widget=true` to hide the header and collapse to single-column for iframe embedding
- **Reset** — clears all selections and restarts from Step 1

---

## Updating the reference data

The calculator ships with embedded reference data. When new products are added, data can be updated without any code changes:

1. Update the relevant tab in the source Google Sheet
2. **File → Download → CSV** for each sheet
3. Open the calculator → click **⚙ Data** in the header
4. Drag and drop (or click to browse) the updated CSV into the relevant upload zone

Uploaded data is parsed in-browser and saved to `localStorage`. It persists across sessions and survives page refreshes. To revert to the built-in dataset at any time, click **↺ Restore built-in data**.

### CSV format — Reference Data

| Column | Description |
|---|---|
| Construction | `KNITTED` or `WOVEN` |
| ProductType | e.g. `T-Shirt (Short Sleeve)` |
| FiberContent | e.g. `Chief weight: Wool` |
| SpecialReq | e.g. `None`, `Long sleeves`, `Weighs ≤9 kg/dozen` |
| Gender | e.g. `Men's / Boys'`, `Women's / Girls'`, `Unisex` |
| HTSCode | 10-digit code with dots, e.g. `6109.90.8010` |
| DutyRate | e.g. `16%` or `61.7¢/kg + 16%` |
| Chapter | Numeric, e.g. `61` |
| Heading | e.g. `6109` |
| Subheading | e.g. `6109.9` |

### CSV format — Country Rates

| Column | Description |
|---|---|
| Country | Display name, e.g. `Vietnam` |
| Section301Rate | Numeric percentage, e.g. `7.5` |
| IEEPARate | Numeric percentage, e.g. `20` |
| FTADiscount | `100` for fully duty-free FTA, `0` for none |
| Notes | Free text explanation shown to the user |

---

## Embedding as a widget

```html
<iframe
  src="https://your-site.com/hts-calculator?widget=true"
  width="100%"
  height="720"
  frameborder="0"
  style="border-radius:12px">
</iframe>
```

Widget mode hides the header and footer and collapses to a single-column layout suitable for embedding in documentation, Notion, or other tools.

---

## Stack

| Layer | Tool |
|---|---|
| Structure | Plain HTML5 |
| Styling | Vanilla CSS (custom properties, CSS Grid) |
| Interactivity | Vanilla JavaScript — no framework, no build step |
| Data persistence | Browser `localStorage` |
| Deployment | Vercel — zero-config static hosting |

No npm. No bundler. Opens directly in a browser.

---

## Project structure

```
hts-calculator.html    # entire app — HTML, CSS, and JS in one file
vercel.json            # Vercel deployment config (iframe headers)
```

---

## Disclaimers

- HTS base duty rates are sourced from the USITC HTS schedule and are illustrative only
- Section 301 and IEEPA tariff rates reflect publicly available USTR executive orders as of the data's last update and are subject to rapid change
- FTA eligibility depends on rules of origin compliance, which must be verified per style
- Always confirm classification and duty rates with a licensed customs broker or CBP ruling before import
