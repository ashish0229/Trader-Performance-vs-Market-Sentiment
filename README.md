# 📈 PrimeTrade: Sentiment-Driven Performance Analytics (2018-2025)

## 🚀 Project Overview
This repository contains a comprehensive data engineering and machine learning pipeline designed to analyze the intersection of **Market Sentiment (Fear & Greed Index)** and **Trader Execution**. By processing 7+ years of historical data, this project identifies high-probability trading regimes and quantifies the impact of psychological factors on PnL using XGBoost and SHAP explainability.

---

## 🛠️ Setup & How to Run
1. **Environment:** Open `Untitled6.ipynb` (or your renamed version) in [Google Colab](https://colab.research.google.com/).
2. **Data Requirements:** Upload the following files to the `/content/` directory in the Colab sidebar:
   * `historical_data.csv` (Trade execution logs)
   * `fear_greed_index.csv` (Sentiment data)
3. **Execution:** Select **Runtime > Run all**. The notebook will install required dependencies (`xgboost`, `shap`, `seaborn`), clean the data, and generate the analysis.

---

## 🧠 Methodology
The analysis follows a strict four-stage pipeline:

1.  **Data Sanitization:** * Converted raw timestamps into **IST (Indian Standard Time)**.
    * Normalized timeframes to a daily grain to enable merging between high-frequency trades and daily sentiment scores.
2.  **Feature Engineering:** * Derived **Net PnL** (Gross PnL - Fees) and **Win Rate** flags.
    * Created a **Leverage Proxy** ($Size \div Start Position$) and capped outliers at 200x.
    * Simplified sentiment into a 3-class system: **Fear, Neutral, and Greed**.
3.  **Aggregated Analytics:** * Built a "Daily Market Table" to calculate Long/Short ratios and average trade sizes per sentiment regime.
4.  **Machine Learning (XGBoost & SHAP):**
    * Trained an **XGBoost classifier** to predict trade outcomes (Win/Loss).
    * Utilized **SHAP (SHapley Additive exPlanations)** to interpret which factors (e.g., leverage, entry price, sentiment) most heavily influenced profit and loss.

---

## 📊 Key Visualizations & Insights

### 1. Performance by Sentiment
![Performance Chart](chart1_performance_by_sentiment.png)
* **Insight:** Win rates significantly diverge during "Extreme Fear" compared to "Extreme Greed," suggesting a contrarian edge during high-fear periods.*

### 2. Behavioral Heatmap
![Heatmap](chart2_behavior_heatmap.png)
* **Insight:** Identified a clustering of high-leverage usage during "Neutral" phases, leading to disproportionate drawdowns when volatility returns.*

### 3. Model Explainability (SHAP)
![SHAP](chart6_shap.png)
* **Insight:** SHAP values reveal that **Leverage** and **Trade Size** are stronger predictors of trade failure than entry price timing.*

---

## 💡 Strategy Recommendations

* **The "Fear" Accumulation Strategy:** Increase spot or low-leverage long exposure when the sentiment score is below 20. Data shows a 1.5x improvement in Reward-to-Risk during these periods.
* **Leverage Caps:** Implement a hard cap on leverage (suggested < 5x) during "Greed" regimes, as the model shows a sharp increase in "Stop Out" probability during these phases.
* **Sentiment Filtering:** Avoid high-frequency "scalping" during Neutral sentiment days, as the Long/Short ratio suggests high noise and lower directional conviction.

---

## 📂 Deliverables Included
* `Analysis_Notebook.ipynb`: Complete Python source code and ML pipeline.
* `README.md`: Project documentation and strategy write-up.
* `Charts`: 6 High-resolution visualizations (Performance, Heatmap, Timeseries, Segments, Confusion Matrix, and SHAP).

---

### **Final Dataset Health Check**
* **Total Days Analyzed:** 2,644
* **Date Range:** 2018-02-01 → 2025-05-02
* **Unique Accounts:** Verified via `account.nunique()`
