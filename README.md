# california-housing-energy-analytics

An end-to-end Exploratory Data Analysis (EDA) challenge covering two very different worlds: **California housing prices** and the **Spanish electricity market**. The goal: uncover what drives housing costs in California, and whether renewable energy generation actually pushes electricity prices down.

---

## 📌 Overview

This repository contains two Jupyter Notebooks, each following the same rigorous EDA pipeline:

> **Initial Exploration → Cleaning & Preprocessing → Simple Analysis → Complex Analysis**

| Notebook | Dataset | Focus |
|---|---|---|
| `01_california_housing_eda.ipynb` | [California Housing Prices](https://www.kaggle.com/datasets/camnugent/california-housing-prices/data) | What makes houses expensive in California? |
| `02_spain_electricity_market.ipynb` | [Spanish Electricity Market](https://www.kaggle.com/datasets/manualrg/spanish-electricity-market-demand-gen-price/data) | Do renewables actually bring prices down? |

---

## 🏠 Part 1 — California Housing Prices

**Key steps:**
- Handled missing values in `total_bedrooms` via median imputation
- Flagged the **$500,001 price cap** (~4.7% of rows) with an `is_capped` column instead of dropping data
- One-hot encoded `ocean_proximity`
- Engineered new features: `rooms_per_household`, `bedrooms_per_room`, `population_per_household`

**Key findings:**
- `median_income` is by far the strongest predictor of `median_house_value` (positive correlation)
- Houses near the ocean / bay command higher median prices; `INLAND` areas are cheaper but have long tails of outliers
- `bedrooms_per_room` correlates **negatively** with price — a higher ratio of bedrooms to total rooms signals smaller, more basic homes with fewer non-bedroom amenities
- Geographic scatter plots confirm price hotspots align with coastal/urban areas (e.g. Los Angeles)

**Visualizations included:**
- Histograms of individual feature distributions
- Boxplots/violin plots segmented by `ocean_proximity`
- Correlation heatmap & pairplots
- Geographic scatter plot colored by price

---

## ⚡ Part 2 — Spanish Electricity Market

**Key steps:**
- Reshaped the dataset from long format (`id`/`name`/`value`) to wide format via pivot, isolating: Price (SPOT market), Real Demand, Wind generation, Solar PV generation, Nuclear generation
- Converted `datetime` to a proper index and interpolated the handful of missing daily values
- Extracted temporal features: year, month, day of week, season

**Key findings:**
- **Merit order effect confirmed**: electricity price correlates **negatively** with wind generation. When wind output is high, cheap renewable supply displaces expensive gas/coal plants, pulling the market-clearing price down.
- Price correlates **positively** with real demand, as expected from basic supply/demand economics
- Prices are lowest on **weekends** (lower industrial/commercial activity)
- Seasonal effect: **winter and autumn** show the highest and most volatile prices, driven by heating demand and scheduled nuclear maintenance

**Visualizations included:**
- Individual distribution histograms
- Boxplots segmented by day of week and season
- Correlation heatmap & pairplots (price vs. demand vs. generation sources)
- Time series plots (raw daily + monthly resampled)
- Dual-axis time series comparing price vs. wind generation

---

## 🛠️ Tools & Libraries

- Python 3.x
- Pandas & NumPy — data wrangling
- Matplotlib & Seaborn — visualization
- Jupyter Notebook

---

## 🚀 How to Run

```bash
# Clone the repo
git clone https://github.com/IvanOcampos/california-housing-energy-analytics.git
cd california-housing-energy-analytics

# Install dependencies
pip install pandas numpy matplotlib seaborn jupyter

# Launch Jupyter
jupyter notebook
```

Download the datasets from the Kaggle links above and place them in a `data/` folder before running the notebooks.

---

## 📂 Repository Structure

```
.
├── data/
│   ├── housing.csv
│   └── spain_electricity_market.csv
├── 01_california_housing_eda.ipynb
├── 02_spain_electricity_market.ipynb
└── README.md
```

---

## 📈 Kaggle

Both notebooks are also published on Kaggle, linked to their respective datasets: 
- *(https://www.kaggle.com/code/ivanocampos/california-housing)*
- *https://www.kaggle.com/code/ivanocampos/spanish-electricity-market*

---

*Built while pretending not to cry about California rent prices and Spanish winter electricity bills.* 🏖️💸
