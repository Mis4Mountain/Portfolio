# Student Nutrition Impact Dashboard

**Live demo:** (https://tfss-dashboard.vercel.app/)

A fully interactive, single-page analytics dashboard built to demonstrate data analyst skills in a non-profit / public-sector context. The dashboard visualises program reach, food procurement, financial allocation, and health service outcomes for a school nutrition program — modelled on the publicly available annual reports and strategic plan of the [Toronto Foundation for Student Success (TFSS)](https://www.tfss.ca).

> **Portfolio disclaimer:** All data marked `~ Illustrative` is synthetically generated for demonstration purposes. Verified data points (marked `✓ Annual Report`) are sourced from the publicly available TFSS Annual Report 2023–24 and Strategic Business Plan 2023–26. This is not an official TFSS product.

---

## Problem this solves

TFSS publishes narrative-first annual reports with high-level pie charts but no interactive drill-down. A data analyst joining the team would be expected to build dashboards that connect program outputs (meals, students, schools) to financial inputs (grants, spend per category) and enable questions like:

- What is our cost per meal trend over five years?
- Which schools receive the most meals, and how did COVID affect them?
- Where exactly does program delivery spend go — drivers, food, equipment?
- What specific produce items make up our food procurement budget?

This dashboard answers all of those questions interactively.

---

## Stack

| Layer | Tool |
|---|---|
| Structure | Plain HTML5 |
| Styling | Vanilla CSS (custom properties, CSS Grid, Flexbox) |
| Charts | [Chart.js 4.4](https://www.chartjs.org/) via CDN |
| Interactivity | Vanilla JavaScript (no framework) |
| Deployment | [Vercel](https://vercel.com) — zero-config static hosting |
| Version control | GitHub |

No build step. No npm. No framework. Opens directly in a browser.

---

## Data sources

| Data point | Source | Status |
|---|---|---|
| Total meals served (36.7M, FY 2023–24) | TFSS Annual Report 2023–24 | ✓ Verified |
| Active programs (846, FY 2023–24) | TFSS Annual Report 2023–24 | ✓ Verified |
| Revenue split (82% grants / 15% donations / 3% investment) | TFSS Annual Report 2023–24 | ✓ Verified |
| Expense split (94% programs / 4% fundraising / 2% admin) | TFSS Annual Report 2023–24 | ✓ Verified |
| City of Toronto as largest single funder | TFSS Annual Report 2023–24 | ✓ Verified |
| Strategic priorities (data/digital, CDS migration, BNG) | TFSS Strategic Business Plan 2023–26 | ✓ Verified |
| All monthly breakdowns | Synthetically generated | ~ Illustrative |
| Prior-year figures (2019–20 to 2022–23) | Proportionally scaled estimates | ~ Illustrative |
| School-level meal volumes | Synthetically generated | ~ Illustrative |
| Donor names and grant amounts | Synthetically generated | ~ Illustrative |
| Expense sub-categories | Synthetically generated | ~ Illustrative |
| Food procurement item detail | Synthetically generated | ~ Illustrative |

---

## Key features

- **5-year fiscal year switcher** — all KPIs, charts, tables, and financials update in sync; 2020–21 shows COVID impact across every section
- **Top 10 schools table** — re-ranks by selected year; each school has an expandable 5-year trend chart
- **Clickable revenue breakdown** — clicking any revenue source (grants, donations, investment) expands a horizontal bar breakdown of funders and donors
- **Expense accordion** — three-level drill-down from category → sub-category → line items (drivers, van fuel, kitchen equipment, etc.)
- **Food procurement detail** — five category tabs (Fresh Produce, Grains & Bread, Dairy & Protein, Canned & Pantry, Packaging) with item-level quantity, unit cost, and total spend
- **Data provenance panel** — collapsible panel at the top clearly distinguishes verified from illustrative data, with source citations
- **Inline source badges** — every section and KPI card labelled `✓ Annual Report` or `~ Illustrative`; badges update dynamically when switching years

---

## Screenshots

<img width="1920" height="965" alt="Dashboard 5" src="https://github.com/user-attachments/assets/bfd23104-dde6-4536-8949-ac597ec4d62a" />
<img width="1918" height="864" alt="Dashboard 4" src="https://github.com/user-attachments/assets/dac44376-0faa-43f0-8cf4-88f713ec1f6a" />
<img width="1284" height="497" alt="Dashboard 3" src="https://github.com/user-attachments/assets/d895732a-dc72-4971-8eee-ad104f87ac23" />
<img width="1914" height="965" alt="Dashboard 2" src="https://github.com/user-attachments/assets/9ca4b3f7-9f2b-4aaa-8e5a-ccc9e80d1e0b" />
<img width="1917" height="969" alt="Dashboard 1" src="https://github.com/user-attachments/assets/050ac7c5-6db1-48c6-87b5-b22c580d4504" />


- Full dashboard overview (2023–24 selected)
- Schools table with one history chart expanded
- Revenue card with Government Grants expanded
- Expense accordion open on Program Delivery
- Food Procurement tab showing Fresh Produce items

---

## Running locally

No install needed. Just open the file:

```bash
git clone https://github.com/YOUR_USERNAME/YOUR_REPO_NAME.git
cd YOUR_REPO_NAME
open index.html        # macOS
# or double-click index.html in your file explorer
```

The only external dependency is Chart.js, loaded from CDN. An internet connection is required for charts to render.

---

## Deploying to Vercel

### One-click (recommended)

1. Push this repo to GitHub
2. Go to [vercel.com](https://vercel.com) → **Add New Project**
3. Import your GitHub repo
4. Vercel settings:
   - **Framework preset:** Other
   - **Build command:** _(leave blank)_
   - **Output directory:** `.` (root)
   - **Install command:** _(leave blank)_
5. Click **Deploy**

That's it — no environment variables, no build pipeline.

### Using Vercel CLI

```bash
npm i -g vercel
vercel --prod
```

---

## Project structure

```
.
├── index.html       # entire dashboard — HTML, CSS, and JS in one file
├── vercel.json      # Vercel deployment config
├── .gitignore
└── README.md
```

---

## About the analyst

Built by Marcus Wong as a portfolio piece for a Data Analyst application, demonstrating:

- Dashboard design for non-profit / public-sector reporting contexts
- Ability to build semantic data models connecting program outputs to financial inputs
- Replacing manual Excel-based tracking with structured, interactive reporting
- Communicating clearly about data provenance and confidence levels
