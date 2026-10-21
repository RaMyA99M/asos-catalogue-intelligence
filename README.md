# Inside the ASOS Catalogue
### An investigation into assortment, price positioning & availability

**DATA INVESTIGATION / 001** · Exploratory retail analytics

*What can an online fashion catalogue reveal about assortment strategy, price positioning and product availability?*

---

## The Investigation

Online fashion catalogues provide a snapshot of the products, brands, prices and size availability presented to shoppers. Analysing these listings can reveal patterns in assortment and pricing, while raising questions about how reliably catalogue data represents the underlying retail operation.

This project investigates the ASOS product catalogue through three analytical lenses: **Assortment, Price positioning and Availability**. The objective is to translate product-level data into commercially relevant observations, distinguish evidence from assumptions, and identify where additional information would strengthen the analysis.

### At a glance

| | |
|---|---|
| **Dataset** | ASOS product listing data |
| Initial dataset | 30,845 rows |
| Analysed records | 30,827 rows |
| Brand extraction coverage | 98.1% (30,251 matched records) |
| Investigation themes | Assortment · Pricing · Availability |
| Tools | Python · Pandas · Matplotlib · Seaborn |
| Approach | Exploratory data analysis |



![Investigation process map](visuals/analysis-process.png)

---

## 01 / The brief

### What can the catalogue reveal?

The investigation is organised around three questions:

**A. Assortment**
- How are product listings distributed across extracted brand labels?
- How concentrated is the observed catalogue among the largest labels?

**B. Price positioning**
- How do product prices vary across brands?
- Is catalogue size associated with median price?

**C. Availability**
- What proportion of listed sizes is marked out of stock?
- How do the observed availability indicators vary across price segments?

These questions provide a structured way to explore the catalogue without assuming that listing counts, prices, or stock indicators directly measure commercial performance.

---

## 02 / Data quality

### Can we trust the evidence?

Before interpreting the results, the dataset and the assumptions behind the analysis need to be considered.

The dataset contains product URLs, names, size information, categories, prices, colours, SKUs, descriptions, and image references. Price values were converted to numeric format and rows without usable prices were excluded from the analysis.

Several additional data-quality considerations affect interpretation:

- **Repeated SKUs:** The audit identified 524 SKU groups appearing more than once. Repeated identifiers were retained rather than automatically deduplicated because repetition alone does not establish that records are erroneous.

- **Brand extraction:** Brand labels were extracted from product descriptions using a curated list of known brands. The latest reported coverage was 98.1%, with 576 records remaining unmatched. Matched labels may still contain classification errors, and parent brands and sub-brands are not consistently consolidated.

- **Price preparation:** Original price text was retained while numeric prices and price labels were extracted. All 30,827 analysed records had a valid parsed price. Records labelled “Sale” were not treated as evidence of a specific discount amount because reliable original-price comparisons were not available.

- **Availability indicators:** Stock status must be interpreted according to the actual structure and meaning of the size field. An out-of-stock metric should only be reported after verifying that the field consistently distinguishes available sizes from unavailable ones.

- **Catalogue representation:** Counts describe records in this dataset, not necessarily unique products or the complete ASOS catalogue.

These issues are important when interpreting brand rankings, catalogue concentration and availability patterns.

---

## 03 / Investigation

### Three lenses on the catalogue

### A. Assortment — where are listings concentrated?

![Catalogue concentration](visuals/catalogue-concentration.png)

This analysis compares listing counts across extracted brand labels and explores the distribution of catalogue representation.

**What to look for:** Which labels account for the largest share of observed listings? Does the distribution suggest that catalogue representation is concentrated among a relatively small number of labels?

**Business relevance:** Catalogue concentration can help frame questions about brand representation and assortment structure. Interpretation depends on the reliability of the extracted labels and the treatment of repeated records.

**Finding:** The 10 largest extracted brand labels account for 13,158 records, representing 42.7% of the 30,827 analysed records. ASOS DESIGN is the largest individual label, with 5,477 records, equivalent to approximately 17.8% of the dataset.

**Interpretation:** Catalogue representation is concentrated among a leading group of brand labels, with ASOS DESIGN substantially ahead of the next-largest label, Topshop, at 1,869 records.

**Caveat:** These figures represent catalogue records grouped by extracted labels, not verified unique products. Brand-level comparisons also retain distinctions between parent brands and sub-brands.

### B. Pricing — how does catalogue scale relate to price positioning?

![Price positioning](visuals/price-positioning.png)

This analysis compares brand-level catalogue size with median product price and examines price distributions across selected labels.

**What to look for:** Are larger catalogues associated with higher median prices, or do assortment scale and price positioning appear to vary independently?

**Business relevance:** Understanding these patterns can support further investigation into price positioning and assortment differences across brands.

**Finding:** ASOS DESIGN combines the largest catalogue representation (5,477 records) with a median listed price of 30. Across the full dataset, the median listed price is 32, while the mean is 41.02. Approximately 47.7% of records are priced at 30 or below.

The median listed price for Sale-labelled records is 25.50, compared with 36.00 for Standard-labelled records.

**Interpretation:** The catalogue contains a substantial share of lower-priced listings, while the difference between the overall mean and median suggests that higher-priced records pull the mean upward. Sale-labelled and Standard-labelled records also occupy different price positions in this snapshot.

**Caveat:** These are descriptive comparisons. They do not establish a relationship between catalogue size and price across all brands, prove that sale labels represent a particular discount, or measure sales performance.

![Price distribution](visuals/price-distribution.png)

### C. Availability — what do size-level indicators reveal?

The availability analysis uses size information to calculate the proportion of listed sizes marked out of stock, then explores how this indicator varies across price segments.

**What to look for:** Are there differences in the observed out-of-stock indicators between price segments? How consistent is the pattern across listings?

**Business relevance:** These indicators can help identify questions for further inventory investigation. They cannot establish customer demand, unmet demand or lost revenue without additional evidence.

**Status:** Pending validation of the size-level availability indicator.

The next step is to verify how the source represents sizes and out-of-stock states, then calculate the out-of-stock proportion and compare it across price segments if the data supports a consistent measure.

**Caveat:** No availability conclusion is reported until the field semantics and calculation have been validated.

---

## 04 / Interpretation

### From patterns to evidence-backed findings

The results should be interpreted according to what the dataset can actually establish.

For each investigation, the final analysis will distinguish between:

- **Observed patterns:** What the available records and calculations show.
- **Interpretation:** What those patterns may suggest in a retail context.
- **Limitations:** How data quality, measurement choices and missing information affect confidence.
- **Further investigation:** What evidence would help test the interpretation.

In particular, associations between catalogue size, price and availability should not be presented as evidence of causation. Brand-level conclusions also depend on the reliability of the extracted brand labels.

### Summary of findings

| Investigation | Validated finding | Confidence / caveat |
|---|---|---|
| Assortment | Top 10 extracted brand labels account for 42.7% of analysed records; ASOS DESIGN accounts for 17.8%. | Depends on brand-label accuracy and interpretation of repeated records. |
| Price positioning | Median listed price is 32; 47.7% of records are priced at 30 or below. Sale-labelled records have a lower median than Standard-labelled records. | Descriptive snapshot; no evidence of sales performance or discount size. |
| Availability | Pending validation. | Requires verification of size-level stock indicators before reporting a result. |

---

## 05 / Commercial implications

### From catalogue data to decisions

The analysis provides a starting point for further retail investigation rather than a definitive assessment of commercial performance.

**1. Review assortment representation**

Use validated brand and product counts to understand catalogue concentration. Before making assortment decisions, establish whether the observed distribution reflects the intended brand strategy and complete product coverage.

**2. Investigate price positioning**

Compare price distributions across reliably identified brands and relevant product categories. Further analysis could explore whether differences persist when comparing similar product types rather than entire brand assortments.

**3. Connect availability to inventory and demand**

Combine catalogue-level size indicators with inventory snapshots, sales transactions and demand measures. This would help establish whether observed stock gaps correspond to meaningful availability issues.

### What additional data would strengthen the analysis?

- Reliable product and brand identifiers
- Inventory snapshots over time
- Product views, conversion rates and sales
- Historical prices and promotional activity
- Product categories and other comparable product attributes

With these data sources, the analysis could progress from exploratory catalogue patterns towards more robust commercial evaluation.

---

## Methodology and project files

The analysis was conducted in Python using Pandas for data preparation and aggregation, with Matplotlib and Seaborn for visual exploration.

The accompanying notebook documents the analytical workflow and calculations.

### Repository structure

```text
asos-catalogue-intelligence/
├── README.md
├── notebook/
│   └── BrandStrategyAnalysis.ipynb
├── visuals/
│   ├── analysis-process.png
│   ├── catalogue-concentration.png
│   ├── price-positioning.png
│   └── availability-analysis.png
├── findings/
│   └── recommendations.md
├── data/
│   └── README.md
└── requirements.txt
```

The raw dataset is not included unless redistribution is permitted. See `data/README.md` for dataset information and access instructions.

## Limitations

This is an exploratory analysis of product listing data. The findings are limited by the quality and coverage of the source records, the reliability of extracted brand labels, potentially repeated SKUs and the use of text-based size availability indicators.

The dataset does not independently establish sales performance, customer demand, inventory history or actual revenue lost due to unavailable sizes. Recommendations should therefore be treated as proposed next steps, not proven commercial outcomes.

---

*Independent portfolio project. Not affiliated with or endorsed by ASOS.*
