# 🛒 Amazon India — Strategic Sales Intelligence Report

> **End-to-end business intelligence analysis of 1,400+ Amazon India SKUs across 9 product categories**
> — Pricing Strategy · Customer Satisfaction · Revenue Performance · Value Intelligence

---

## 📌 Project Overview

This project delivers a **professional-grade business intelligence report** built for a real-world analyst workflow. Using Amazon India's product catalogue data, the analysis moves from raw data wrangling through to **actionable strategic recommendations** — structured around four research questions directly relevant to e-commerce business decisions.

| | |
|---|---|
| **Author** | Athikarathparambil Surjith Indra Prasad |
| **Role** | Business Analyst |
| **Dataset** | [Amazon Sales Dataset — Kaggle](https://www.kaggle.com/datasets/karkavelrajaj/amazon-sales-dataset) |
| **Tool** | R + Quarto (multi-format) |
| **Output Formats** | HTML · PDF · RevealJS Presentation |

---

## 🔬 Research Questions

| # | Research Question | Business Decision |
|---|---|---|
| **RQ1** | How do discount levels affect customer ratings and review volume? | Pricing Strategy Optimisation |
| **RQ2** | Which categories and price tiers deliver the highest customer satisfaction? | Portfolio & Inventory Prioritisation |
| **RQ3** | Which products and categories generate the highest revenue potential? | Marketing Spend Allocation |
| **RQ4** | What is the relationship between price tier, discount depth, and perceived value? | Margin Management |

---

## 📂 Repository Structure

```
amazon-sales-intelligence/
│
├── amazon_sales_analysis.qmd   # Main Quarto source document
├── amazon.csv                  # Dataset (extracted from archive.zip)
├── README.md                   # This file
│
└── outputs/                    # Rendered report outputs
    ├── amazon_sales_analysis.html      # Interactive HTML report
    ├── amazon_sales_analysis.pdf       # PDF version
    └── amazon_sales_analysis_revealjs/ # Presentation slides
```

---

## 📊 Dataset

- **Source:** [Amazon Sales Dataset — Kaggle (karkavelrajaj)](https://www.kaggle.com/datasets/karkavelrajaj/amazon-sales-dataset)
- **Size:** 1,465 products × 16 variables
- **Market:** Amazon India (amazon.in)
- **Categories:** Electronics, Computers & Accessories, Home & Kitchen, Office Products, Musical Instruments, Home Improvement, Toys & Games, Car & Motorbike, Health & Personal Care

### Key Variables

| Column | Type | Description |
|---|---|---|
| `product_id` | chr | Unique ASIN identifier |
| `category` | chr | Hierarchical category path (pipe-separated) |
| `actual_price` | dbl | Original list price (₹) |
| `discounted_price` | dbl | Final selling price (₹) |
| `discount_percentage` | dbl | Percentage discount applied |
| `rating` | dbl | Average customer rating (1–5★) |
| `rating_count` | dbl | Total number of customer reviews |

### Engineered KPIs

| KPI | Formula | Business Purpose |
|---|---|---|
| `savings_inr` | `actual_price − discounted_price` | Absolute discount value |
| `revenue_proxy` | `discounted_price × rating_count` | Revenue exposure estimate |
| `value_score` | `rating × log(1 + rating_count)` | Quality-popularity composite |
| `price_tier` | `case_when(...)` | Budget / Mid / Premium / Luxury |
| `discount_band` | `case_when(...)` | Low / Moderate / High / Very High |

---

## 🛠️ Methodology

```
Raw CSV
  └─► Data Cleaning       (regex stripping ₹ symbols, type conversion, NA handling)
        └─► Feature Engineering  (5 derived KPIs, 3 segmentation tiers)
              └─► Exploratory Analysis   (skimr, janitor, count, tabyl)
                    └─► Statistical Testing   (Kruskal-Wallis, Pearson correlation)
                          └─► Visualisation        (ggplot2, plotly, patchwork, gt)
                                └─► Strategic Recommendations
```

### Statistical Methods Applied

- **Kruskal-Wallis non-parametric test** — validating rating differences across discount bands
- **Pearson correlation matrix** — relationships between price, discount, rating, and revenue
- **Loess regression smoothing** — discount vs. rating trend visualisation
- **Quadrant analysis** — Quality (rating) vs. Popularity (log review count) product mapping
- **PCA-inspired segmentation** — price tier × discount band satisfaction matrix

---

## 📦 R Libraries Used

```r
library(tidyverse)   # Data manipulation & visualisation
library(readr)       # CSV import
library(janitor)     # Tabyl cross-tabulation & cleaning
library(skimr)       # Statistical summary
library(scales)      # Number formatting
library(ggplot2)     # Static visualisations
library(plotly)      # Interactive visualisations
library(patchwork)   # Multi-plot layouts
library(gt)          # Publication-quality tables
library(stringr)     # String manipulation (regex)
library(forcats)     # Factor reordering
library(ggrepel)     # Non-overlapping plot labels
```

---

## 🚀 How to Render

### Prerequisites

- [R](https://www.r-project.org/) ≥ 4.2
- [Quarto](https://quarto.org/) ≥ 1.3
- Required R packages (install once):

```r
install.packages(c(
  "tidyverse", "readr", "janitor", "skimr", "scales",
  "plotly", "DT", "gt", "patchwork", "stringr",
  "forcats", "ggrepel"
))
```

### Rendering

Make sure `amazon.csv` and `amazon_sales_analysis.qmd` are in the **same folder**, then run:

```bash
# HTML (recommended — fully interactive)
quarto render amazon_sales_analysis.qmd --to html

# PDF
quarto render amazon_sales_analysis.qmd --to pdf

# RevealJS Presentation
quarto render amazon_sales_analysis.qmd --to revealjs

# All formats at once
quarto render amazon_sales_analysis.qmd
```

---

## 📈 Key Findings

**RQ1 — Pricing Strategy**
> The **40–60% discount band** is the optimal zone — maximising both review volume and average rating. Discounts above 60% drive volume but suppress ratings, risking long-term brand erosion.

**RQ2 — Customer Satisfaction**
> **Home & Kitchen** is the most consistently rated category across all price tiers. **Budget Electronics** shows the widest rating variance — the highest-risk segment for quality inconsistency.

**RQ3 — Revenue Performance**
> **Electronics** commands ~60%+ of total revenue proxy by value. The **Premium price tier (₹2,000–₹10,000)** is the single largest revenue contributor — the highest-priority segment for marketing investment.

**RQ4 — Value Intelligence**
> The "Star Product" quadrant (high rating + high review volume) is predominantly occupied by **Mid-Range to Premium products with moderate discounting** — confirming that sustainable value, not extreme discounting, drives long-term commercial success.

---

## 🎯 Strategic Recommendations

| Priority | Recommendation | Target KPI |
|---|---|---|
| 🔴 Critical | Rationalise Very High (>60%) discounts | Avg rating >4.1 post-cap |
| 🔴 Critical | Double down on Premium tier (₹2K–₹10K) | Increase Premium SKU count by 20% |
| 🟠 High | Address Budget Electronics quality gap | Reduce <3.5★ products by 30% |
| 🟠 High | Scale Home & Kitchen inventory | Expand across Mid & Premium tiers |
| 🟡 Medium | Delist low-volume, low-rated products | Reduce dead inventory by 15% |

---

## 🤖 Tools & Reproducibility

This report is **fully reproducible** — all data wrangling, analysis, and visualisation code is embedded in the `.qmd` source file with `code-fold: true` for clean presentation. Any analyst can re-run the full pipeline from raw CSV to final report with a single `quarto render` command.

---

## 👤 Author

**Athikarathparambil Surjith Indra Prasad**
Business Analyst

[![GitHub](https://img.shields.io/badge/GitHub-indrasaideva-181717?style=flat&logo=github)](https://github.com/indrasaideva)

---

*Dataset credit: [karkavelrajaj](https://www.kaggle.com/karkavelrajaj) on Kaggle*
