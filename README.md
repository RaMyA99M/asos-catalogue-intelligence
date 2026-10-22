# Inside the ASOS Catalogue
### Assortment concentration, brand price positioning and listed-price structure

**DATA INVESTIGATION / 001 · RETAIL ANALYTICS**

What can a fashion catalogue reveal about assortment composition and listed-price positioning, and what additional commercial data would be needed to answer?

This project explores a product-catalogue dataset using Python, Pandas, and Matplotlib. It moves from data quality and feature preparation to three descriptive investigations: brand representation, brand-level median listed prices, and the overall structure of listed prices.

The objective is not to infer sales or demand from listings. The goal is to build a defensible catalogue baseline, communicate what the evidence shows, and identify the next questions to test with richer data.

> **Scope:** This is an independent analysis of a collected product-catalogue dataset and is not affiliated with ASOS. Catalogue records are not transactions, units sold, profit, customer demand, or a live inventory feed.

---

## The investigation framework

![Inside the ASOS Catalogue — Investigation framework](visuals/analysis-process.png)

The investigation follows three connected questions:

- **Assortment:** How concentrated is catalogue representation across labels?
- **Price positioning:** How do listed-price medians vary across the more represented brands?
- **Price structure:** How do listed prices distribute overall, and how do original price labels relate to the numeric amounts?

The framework separates preparation, investigation, interpretation, and commercial implications so that the recommendations remain anchored to the analysis.

## Key findings

| Measure | Result | Interpretation |
|:--|--:|:--|
| Source records | 30,845 | Starting dataset size |
| Blank records excluded | 18 | Records missing all core analytical fields |
| Repeated analytical records removed | 837 | Repeated records removed using selected product fields |
| **Retained catalogue records** | **29,990** | Records used in the investigation |
| Brand extraction coverage | 98.1% | 29,419 records matched the curated brand list; coverage is not independently verified accuracy |
| Top 10 labels' catalogue share | **42.8%** | The ten most represented labels account for just under half of retained records |
| Largest label: ASOS DESIGN | **5,373 (17.9%)** | The largest label accounts for around one in six retained records |
| Median listed price | **32.00** | Half of retained records are listed at or below this amount |
| Records listed at 30 or below | **14,491 (48.3%)** | Nearly half of retained records fall at or below this threshold |

Price figures are shown without a currency symbol because the currency is not confirmed in the source fields.

---

## 01 / Assortment concentration

![Catalogue concentration across labels](visuals/catalogue-concentration.png)

**Question:** Which labels account for the largest share of the observed catalogue, and how quickly does cumulative representation build?

The ten most represented labels account for **42.8%** of retained catalogue records. ASOS DESIGN alone contributes **5,373 records (17.9%)**. Catalogue representation is therefore uneven: a relatively small group of labels accounts for a substantial share of the records, while the remainder is distributed across other labels.

### What this does and does not mean

This is evidence of **catalogue concentration**, not commercial dependence. More catalogue records do not establish more sales, customer demand, stock depth, revenue or profit. They do, however, affect the descriptive analysis: larger labels have more records contributing to their summaries, while smaller labels can have less stable estimates.

The next useful question is whether the larger represented labels also occupy different parts of the listed-price distribution. That is explored descriptively in the brand comparison below; it should not be treated as a causal relationship.

## 02 / Brand price positioning

![Listed price positioning across brands](visuals/price-positioning.png)

**Question:** How does median listed price vary across brands with sufficient catalogue representation?

The comparison uses brand-level median listed prices and a minimum threshold of **30 catalogue records per brand**. The median is a useful comparison measure because it is less affected than the mean by a small number of unusually high-priced records.

Interpretation should keep three things in view:

- **Representation:** read the price summary alongside the number of records behind it.
- **Scope:** this is a catalogue snapshot, not a time series or a measure of realised selling prices.
- **Meaning:** differences in medians describe observed listed-price positioning; they do not prove differences in brand strategy, quality, value, customer willingness to pay, revenue or margin.

A stronger next test would build a brand-level table containing record count, catalogue share, median listed price, and valid-price count, then quantify the association between representation and median price on the final cleaned dataset. The coefficient and direction should only be reported after that calculation is run. Category mix should also be examined before interpreting a brand-level relationship, because brands may have different product-category compositions.

## 03 / Listed-price structure

![Overall distribution of listed prices](visuals/price-distribution.png)

**Question:** Where do listed prices cluster, and how does the distribution extend beyond its midpoint?

Across the **29,990 retained records**, the median listed price is **32.00**, the mean is **40.73**, and the observed range is **3.00–550.00**. The mean being higher than the median indicates that higher-priced records pull the average above the midpoint. This is why the distribution is more informative than relying on the mean alone.

Nearly half of retained records (**14,491; 48.3%**) are listed at 30.00 or below.

### Price wording adds important context

The original price text was retained before extracting numeric amounts. Records were classified from their displayed wording as Standard, Sale (wording beginning with “Now”), or Starting price (wording beginning with “From”).

| Original price label | Records | Median listed price | Mean listed price |
|:--|--:|--:|--:|
| Standard | 17,889 | 36.00 | 46.92 |
| Sale | 12,029 | 25.00 | 31.52 |
| Starting price | 72 | 29.50 | 40.33 |

The median for Sale-labelled records is **11 lower** than the median for Standard-labelled records (25 versus 36). This is a difference between the observed groups, **not a measured discount**. Reliable original/current price pairs were not established, so discount depth cannot be calculated from this comparison. “From” prices may also be starting prices for products with multiple variants rather than a single fixed price.

All 29,990 retained price strings produced a numeric amount in the final preparation, with zero non-empty strings left unparsed. Successful parsing does not make all price types commercially equivalent; their original labels remain important.

---

## Data preparation and quality

### Dataset reconciliation

| Preparation step | Records |
|:--|--:|
| Source records | 30,845 |
| Blank records excluded | 18 |
| Repeated analytical records removed | 837 |
| **Retained catalogue records** | **29,990** |

Blank records were those missing all core analytical fields: name, SKU, price, and category.

Repeated analytical records were identified using the selected fields:

`sku`, `name`, `size`, `category`, `price`, `color`, `description`

URL and image fields were excluded from the deduplication key because they are not the product attributes being compared in this analysis.

### Brand extraction

| Metric | Result |
|:--|--:|
| Curated brand reference list | 212 brands |
| Matched brand records | 29,419 |
| Unmatched brand records | 571 |
| Extraction coverage | 98.1% |

Brand labels were extracted from product-detail text using a curated list of known brands and longest-first prefix matching. Unmatched records were retained rather than forcing uncertain classifications. Coverage measures successful matching under this method; it does not independently validate every label assignment.

### Price preparation

The original wording was preserved, price types were classified, and a numeric amount was extracted. The analysis distinguishes Standard, Sale, and Starting price records instead of treating every numeric amount as an identical price concept. The currency was not confirmed, so no currency symbol is applied.

---

## What the data can support

**Supported by this dataset**
- Catalogue-record counts and brand representation.
- Catalogue share and cumulative concentration.
- Descriptive comparisons of listed-price distributions.
- Differences between groups defined by original price wording.
- Data-cleaning and brand-matching coverage checks.

**Not established by this dataset**
- Sales, revenue, margin, profitability, sell-through or demand.
- Actual discount depth without reliable paired prices.
- Live stock availability or stockout rates.
- Causal explanations for catalogue representation or price differences.
- Currency denomination where the source does not identify it.

Catalogue records do not necessarily correspond to unique styles, units sold, or inventory quantities. This distinction is deliberate: strong analysis means making the strongest claim the data can defend, not the boldest claim imaginable.

---

## Commercial implications and next questions

The results establish a descriptive baseline. The practical value is in using that baseline to frame follow-up tests—not treating the current catalogue as a proxy for business performance.

1. **Assortment by category:** Does concentration differ across categories and price bands, or is the overall pattern driven by category mix?
2. **Brand and price:** Does the relationship between catalogue representation and median price remain after comparing like-for-like categories?
3. **Promotional pricing:** With reliably paired regular and current prices, what is the actual discount distribution by category and brand?
4. **Commercial performance:** With transaction, margin, and time-period data, does catalogue representation align with sales or profitability?
5. **Availability over time:** With timestamped product-level stock observations, how does availability change? A single catalogue snapshot cannot answer this.

These are proposed next analyses, not findings established by the current dataset.

---

## Tools and skills

**Tools:** Python · Pandas · NumPy · Matplotlib · Jupyter Notebook · Figma

**Skills demonstrated:** Exploratory Data Analysis · Data Cleaning · Data Quality · Feature Preparation · Data Visualisation · Retail Analytics · Business Interpretation

## Repository structure

```text
asos-catalogue-intelligence/
├── data/
├── notebooks/
├── src/
├── visuals/
│   ├── analysis-process.png
│   ├── catalogue-concentration.png
│   ├── price-positioning.png
│   └── price-distribution.png
├── requirements.txt
└── README.md
```

The notebook and source data are stored in their respective folders. Run the notebook cells in order so cleaning and derived fields are created before the summary statistics and charts. The source dataset is required to reproduce the analysis; confirm redistribution permissions before sharing raw product data.

Install the core analysis dependencies if needed:

```bash
pip install pandas numpy matplotlib jupyter
```

---

## Closing perspective

This investigation turns a large, imperfect product-catalogue extract into a structured view of **assortment concentration, brand-level listed-price positioning, and price distribution**. Its strength is the combination of transparent preparation, interpretable comparisons, and clear limits on what can be concluded.

The next step is to add category-level context and connect the catalogue baseline to transaction or time-series data where available. That would allow commercial hypotheses to be tested directly rather than inferred from listings alone.

---

*Independent exploratory retail analytics project.*
