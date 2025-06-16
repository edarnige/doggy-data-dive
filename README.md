# doggy-data-dive
🐾 A data exploration project focused on analyzing Printify merchandise data for a Shopify store. Includes cost breakdowns, pricing insights, and visualizations to support smarter product decisions.

---
---

# Printify Pricing Collector

`printify_pricing_collector.ipynb`

This Jupyter notebook automates the process of collecting pricing and shipping data for selected Printify product types. It creates temporary products via the Printify API to retrieve real-time variant pricing and standard US shipping rates, and saves the results to a CSV file.

## Features

- Fetches all blueprints from Printify’s product catalog
- Filters products by specified types (e.g., mug, hoodie, t-shirt)
- Creates temporary unpublished products to simulate real variants
- Retrieves variant costs and the cheapest US standard shipping rates
- Collects provider details (name, country, etc.)
- Outputs all collected data to a structured CSV file
- Deletes temporary products after analysis

## Requirements

- Python environment with the following packages:
  - `httpx`
  - `csv`
  - `re`
  - `time`
- Valid Printify API token and Shop ID

## Configuration

Update these variables at the top of the notebook:

```python
API_TOKEN = "your_token_here"
SHOP_ID = "your_shop_id_here"
```

## Output
- Results are saved to: results/pricing_results.csv
- CSV includes product cost, shipping details, provider info, and more

## Notes
- Temporary products are created for data collection and deleted automatically.
- API rate limits or failures are handled with basic error messages and retries.


---
---

# Pricing Analysis

`printify_pricing_collector.ipynb`

This Jupyter notebook processes and analyzes product pricing and shipping data collected from Printify. It cleans the dataset, filters for quality, identifies top providers, and visualizes the best options per product type.

## Features

- Loads data from `results/pricing_results.csv`
- Groups product variants and consolidates metadata
- Filters out:
  - Products with long handling times (≥ 10 days)
  - Products for children, pets, or babies
- Calculates total customer cost (`product_cost + shipping`)
- Identifies and retains the cheapest provider per product type
- Visualizes provider performance:
  - X-axis: Total customer cost
  - Y-axis: Average handling time
  - Color: Provider's country
- Ranks providers using a normalized score (lower cost + faster time)
- Selects top 5 providers per product type
- Saves final results to `results/final_filtered_products.csv`

## Requirements

- Python packages:
  - `pandas`
  - `matplotlib`
  - `seaborn`
  - `adjustText`
  - `scikit-learn`

## Output

- Visual analysis of cost vs. handling time
- Filtered and ranked list of top providers per product type
- Final CSV output: `results/final_filtered_products.csv`

## Notes

- A scoring system is used to balance affordability and shipping speed
- Higher `score_normalized` (0–10 scale) indicates a better provider
