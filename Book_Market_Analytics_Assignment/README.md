# Book Market Analytics – Books to Scrape

**Data Science Assignment**  
End-to-end analysis of the [Books to Scrape](https://books.toscrape.com) catalogue: web scraping, data cleaning, exploratory analysis, and predictive modelling of book prices.

---

## Project Overview

This project scrapes the full 1 000-book catalogue from Books to Scrape, cleans and enriches the data (including genre mapping), performs exploratory data analysis, and builds a linear regression model to predict book price from available features (rating, title length, and genre).

**Key finding:** The selected features explain virtually none of the variance in price (R² ≈ −0.06). Price on this site appears largely independent of rating and genre — an important negative result.

---

## Repository Structure

```
Book_Market_Analytics_Assignment/
├── Book_Market_Analytics_Notebook.ipynb   # Full reproducible analysis
├── Book_Market_Analytics_Report.pdf       # Written report
├── README.md
│
├── books_raw.csv                          # Raw scraped listing data
├── books_with_genre.csv                   # After genre mapping
├── books_cleaned.csv                      # Final analysis-ready dataset
│
├── model_coefficients.csv                 # Linear regression coefficients
├── model_summary.json                     # Model performance metrics
│
└── plots/
    ├── 01_price_dist.png
    ├── 02_rating_dist.png
    ├── 03_price_by_rating.png
    ├── 04_avg_price_genre.png
    ├── 05_corr.png
    ├── 06_price_rating_scatter.png
    ├── 07_genre_counts.png
    ├── 08_residuals.png
    └── 09_actual_vs_pred.png
```

---

## Dataset

| File                    | Rows | Description                                      |
|-------------------------|------|--------------------------------------------------|
| `books_raw.csv`         | 1000 | Scraped title, price, rating, availability       |
| `books_with_genre.csv`  | 1000 | + genre (from category pages)                    |
| `books_cleaned.csv`     | 1000 | Fully cleaned & feature-engineered               |

**Final columns in `books_cleaned.csv`:**
- `title`
- `price` (float, GBP)
- `rating` (One–Five)
- `rating_num` (1–5)
- `availability`
- `in_stock` (1/0)
- `genre`
- `genre_grouped` (rare genres < 10 books → “Other”)
- `title_length`

**Price summary:** mean £35.07 | median £35.98 | range £10.00 – £59.99

---

## How to Reproduce

### 1. Environment

```bash
pip install requests beautifulsoup4 pandas numpy scikit-learn matplotlib seaborn
```

### 2. Run the notebook

Open `Book_Market_Analytics_Notebook.ipynb` in Jupyter / VS Code / Colab and run all cells sequentially.

> **Note:** The scraping section makes live requests to books.toscrape.com.  
> If you prefer not to re-scrape, the cleaned CSVs are already included.

### 3. Outputs

Running the notebook will regenerate:
- Cleaned CSVs
- All plots in the `plots/` folder
- Model coefficients and summary metrics

---

## Analysis Pipeline

1. **Data Acquisition**  
   - Scrape 50 catalogue pages (20 books each)  
   - Map genres by scraping individual category pages

2. **Cleaning & Feature Engineering**
   - Convert price (`£xx.xx` → float)
   - Map star ratings to numeric (1–5)
   - Create stock flag and title length
   - Group rare genres into “Other”

3. **Exploratory Data Analysis**
   - Price distribution
   - Rating counts
   - Price by rating & by genre
   - Correlation matrix
   - Scatter + regression of price vs rating

4. **Predictive Modelling**
   - One-hot encode `genre_grouped`
   - Features: `rating_num`, `title_length`, genre dummies
   - Linear Regression (80/20 train-test split)
   - Evaluation: R², RMSE, MAE + residual diagnostics

5. **Interpretation & Recommendations**
   - Documented in the notebook and PDF report

---

## Model Performance

| Metric     | Value     |
|------------|-----------|
| R²         | −0.060    |
| RMSE       | £14.92    |
| MAE        | £12.90    |
| Train size | 800       |
| Test size  | 200       |
| Features   | 27        |

The near-zero (slightly negative) R² indicates that rating, title length and genre together have almost no predictive power for price on this particular catalogue.

---

## Key Insights

- Prices are roughly uniformly distributed between £10 and £60.
- Star ratings are relatively balanced.
- Virtually no linear relationship exists between rating and price.
- Genre has only modest coefficient magnitudes; many of the largest effects belong to smaller categories.
- The catalogue appears to use a pricing scheme largely independent of the features available for scraping.

---

## Requirements

- Python 3.8+
- `requests`, `beautifulsoup4`, `pandas`, `numpy`
- `scikit-learn`, `matplotlib`, `seaborn`

---

## Author

Data Science 500 Assignment – Book Market Analytics

## My github link: 
