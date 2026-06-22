# supermarket-sale-analysis
Exploratory data analysis of supermarket sales using Python (pandas, seaborn, matplotlib) — 1,000 transactions across product lines, customer segments, and payment methods.
# Supermarket Sales Analysis

Exploratory analysis of 1,000 supermarket transactions (17 variables) in Python, looking at what actually drives revenue across product lines, customer types, and payment methods.

## Dataset

1,000 records, 17 columns, no missing values (checked with `df.isna().sum()`). Fields cover product line, customer type, gender, payment method, unit price, quantity, sales, cost, gross income and customer rating.

## What I found

Total sales come to about £322,967, averaging £323 per transaction.

The first thing worth flagging is the correlation heatmap. `Sales`, `cogs`, `Tax 5%` and `gross income` all correlate at exactly 1.0, but that isn't a finding. Those columns are just arithmetic versions of each other (Tax is 5% of cogs, Sales is cogs plus tax, gross income equals the tax). `gross margin percentage` is a flat 4.7619% on every single row, so it has zero variance and can't tell you anything. Once you strip those out, the only real numeric relationships are unit price and quantity feeding into sales, which is what you'd expect since they're the inputs to basket value.

Revenue is fairly flat across the six product lines. Food and beverages is highest at ~£56.1k and health and beauty is lowest at ~£49.2k, but the gap top to bottom is only around 14%, so no category really dominates.

Female customers account for noticeably more revenue, roughly £194.7k against £128.3k for male customers (about 60/40). The boxplot shows a higher median for female transactions too.

Payment methods are almost evenly split. Cash (£112.2k) edges out e-wallet (£110.0k) and credit card (£100.8k).

Rating barely moves with spend, |r| under 0.04 against every monetary column, so satisfaction and basket size look independent here.

## Limitations

This is a single snapshot, so there's no trend or seasonality to read into it, and nothing causal. Several columns are just restatements of each other and were ignored for that reason. With n = 1,000 the segment splits describe this sample rather than estimating anything about a wider population.

## Running it

```bash
git clone https://github.com/atharavmahajan/supermarket-sale-analysis.git
cd supermarket-sale-analysis
pip install pandas seaborn matplotlib jupyter
jupyter notebook supermarket_sales_analysis.ipynb
```

The notebook expects `SuperMarket Analysis.csv` in the same folder.

## Files

- `supermarket_sales_analysis.ipynb` — the analysis
- `SuperMarket Analysis.csv` — source data
