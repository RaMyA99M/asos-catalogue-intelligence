# Inside the ASOS Catalogue
### An investigation into assortment, price positioning & catalogue composition

**DATA INVESTIGATION / 001 · RETAIL ANALYTICS**

What does a fashion retailer's product catalogue reveal about its assortment structure, brand concentration and price positioning?

This project investigates the ASOS catalogue through exploratory retail analytics, examining how catalogue records are distributed across brands, how listed prices vary, and where the assortment is concentrated.

Rather than treating a large catalogue as evidence of commercial success, the analysis focuses on what the available product-level data can reliably tell us.

---

## The investigation

A large assortment can create variety for shoppers, but its composition matters just as much as its size.

This investigation explores three questions:

1. **Catalogue composition** — How concentrated is the catalogue across brands and labels?
2. **Price positioning** — How do listed price levels differ across brands?
3. **Price distribution** — What does the overall distribution of listed prices reveal about the catalogue's price structure?

## Key findings

| Metric | Finding |
|:--|--:|
| Retained catalogue records | 29,990 |
| Brand extraction coverage | 98.1% |
| Top 10 labels' catalogue share | 42.8% |
| Largest label: ASOS DESIGN | 5,373 records |
| ASOS DESIGN catalogue share | 17.9% |
| Median listed price | 32.00 |
| Mean listed price | 40.73 |
| Records priced at 30 or below | 48.3% |

### 01 / A concentrated catalogue

The top 10 labels account for **42.8% of retained catalogue records**, with ASOS DESIGN alone representing **17.9%**.

This establishes a measurable concentration in the catalogue's composition. The distribution offers a useful starting point for understanding how assortment breadth is allocated across labels.

### 02 / A broad listed-price distribution

The median listed price is **32.00**, compared with a mean of **40.73**.

The difference suggests that higher-priced records pull the average above the midpoint. Almost half of retained records (**48.3%**) are listed at 30.00 or below.

This describes the observed price structure, not what customers actually spend.

### 03 / Price positioning varies across labels

Comparing median listed prices across sufficiently represented brands provides a view of their relative price positioning within the catalogue.

The brand comparison uses a minimum record threshold of 30 to reduce the influence of labels with very small representation.

These comparisons describe listed-price differences. They do not establish brand value, customer willingness to pay or commercial performance.

---

## Visual investigation

### 01 / Catalogue concentration

![Catalogue concentration across the largest labels](visuals/catalogue-concentration.png)

Which labels occupy the largest share of the assortment, and how quickly does cumulative catalogue coverage build?

### 02 / Brand price positioning

![Listed price positioning across brands](visuals/price-positioning.png)

How does median listed price vary across brands with sufficient catalogue representation?

### 03 / Overall price distribution

![Overall distribution of listed prices](visuals/price-distribution.png)

Where do listed prices cluster, and how does the distribution extend beyond its median?

---

## Analytical approach

The investigation follows a structured exploratory workflow.

**01 — Prepare the catalogue**

- Load and inspect the source dataset.
- Exclude records missing all core analytical fields: name, SKU, price and category.
- Remove repeated analytical records using SKU, name, size, category, price, color and description.
- Preserve the original price wording for traceability.

**02 — Structure the data**

- Extract brand labels from product details using a curated list of 212 known brands.
- Match brand names using longest-first prefix matching.
- Retain unmatched records rather than forcing uncertain classifications.
- Parse numeric listed prices and classify their original wording.

**03 — Investigate assortment composition**

- Count catalogue records by brand.
- Calculate catalogue shares and cumulative concentration.
- Identify the largest labels and the contribution of the top 10.

**04 — Investigate price positioning**

- Compare median listed prices across brands.
- Apply a minimum brand representation threshold of 30 records.
- Examine the overall price distribution and descriptive statistics.
- Compare price summaries across the observed price types.

**05 — Communicate the findings**

Translate the analysis into visual outputs and business-oriented observations, distinguishing descriptive findings from conclusions that would require additional data.

---

## Methodology & data quality

### Dataset preparation

| Data preparation | Records |
|:--|--:|
| Source records | 30,845 |
| Blank records excluded | 18 |
| Repeated analytical records removed | 837 |
| **Retained catalogue records** | **29,990** |

Repeated analytical records were identified using:

`sku`, `name`, `size`, `category`, `price`, `color`, `description`

URLs and image fields were excluded from the deduplication key.

### Brand extraction

- Curated brand reference list: **212 brands**
- Matched records: **29,419**
- Unmatched records: **571**
- Extraction coverage: **98.1%**

Brand extraction uses product-detail text and a curated matching approach. Coverage indicates successful extraction under this method, not independently verified brand accuracy.

### Listed-price preparation

Prices were classified using their original wording:

| Price type | Records |
|:--|--:|
| Standard | 17,889 |
| Sale | 12,029 |
| Starting price | 72 |
| **Total** | **29,990** |

Numeric amounts were extracted from the listed prices. All non-empty price values were successfully parsed in the final analysis.

**Important interpretation notes**

- *Starting price* may represent a lower-bound price for a product with multiple variants.
- *Sale* and *Standard* are classifications based on the displayed wording, not independently verified promotional status.
- The analysis does not estimate discount depth because reliable original/current price pairs are not established.
- The currency is not confirmed in this analysis; price figures are therefore presented without a currency symbol.
- Catalogue records represent the analysed listings, not unique styles, units sold or inventory quantities.

---

## What this analysis can and cannot tell us

**What it can tell us**
- How catalogue representation is distributed across labels.
- How listed-price levels vary across the observed assortment.
- Where the catalogue is concentrated and how its prices are distributed.

**What it cannot tell us**
- Which brands generate the most revenue or profit.
- Whether customers prefer particular brands or price points.
- Actual product availability, sell-through or inventory performance.
- Whether pricing differences cause differences in demand.

Connecting catalogue structure to commercial outcomes would require additional data, such as sales, transactions, inventory history and product-level performance.

---

## Tools & skills

**Python** · Pandas · NumPy · Matplotlib · Jupyter Notebook · Exploratory Data Analysis · Data Cleaning · Data Quality · Retail Analytics · Data Visualisation · Business Storytelling

---

## Repository structure

```text
asos-catalogue-intelligence/
│
├── Inside_the_ASOS_Catalogue_Analysis.ipynb
├── products_asos.csv
├── visuals/
│   ├── catalogue-concentration.png
│   ├── price-positioning.png
│   └── price-distribution.png
└── README.md
```

---

## Reproduce the analysis

1. Clone or download this repository.
2. Install the required Python libraries.
3. Open the notebook in Jupyter Notebook or JupyterLab.
4. Run the notebook cells in order.

Install dependencies:

```bash
pip install pandas numpy matplotlib jupyter
```

The source dataset is required to reproduce the analysis. Chart images are provided in the `visuals/` directory.

---

## Closing perspective

A catalogue is more than a collection of products. Its composition and price structure provide a useful lens through which to investigate assortment strategy.

This project establishes that baseline: **where the catalogue is concentrated, how listed prices are distributed, and how price positioning differs across labels.**

The next analytical step would be to connect these patterns with sales and inventory data to evaluate whether catalogue structure translates into commercial performance.

---

*An independent exploratory retail analytics project.*
