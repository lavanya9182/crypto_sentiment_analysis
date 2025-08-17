# **Crypto Sentiment Analytics - README**

This project analyzes the relationship between trader sentiment (Fear/Greed Index) and cryptocurrency trading performance (PnL). It includes data loading, preprocessing, exploratory analysis, statistical testing, and predictive modeling.

---

## **Project Structure**
```
.
├── data/                    # Raw data files
│   ├── trader_data.csv      # Trader PnL records
│   └── sentiment_index.csv  # Fear/Greed sentiment index
├── outputs/                 # Generated visualizations
│   ├── pnl_by_sentiment.png # Violin plot of PnL by sentiment
│   └── activity_heatmap.png # Heatmap of trading activity
├── Crypto_Sentiment_Analytics.ipynb  # Main notebook
└── README.md                # This file
```

---

## **Steps Overview**

### **1. Data Loading**
- Downloads `trader_data.csv` and `sentiment_index.csv` from Google Drive.
- Loads data into Pandas DataFrames.

### **2. Data Sampling**
- Randomly samples **1,000 records** from `trader_data` for faster computation.

### **3. Data Merging**
- Combines `trader_data` and `sentiment_data` on the `date` column using a **left join**.

### **4. Feature Engineering**
- Adds new features:
  - `pnl_positive` (binary flag for profitable trades).
  - `hour` and `day_of_week` (extracted from timestamp).
  - `sentiment_strength` (mean PnL per sentiment class).

### **5. Sentiment Analysis**
- Aggregates PnL statistics (`mean`, `median`, `std`) by sentiment (`Fear`, `Greed`, `Neutral`).
- Counts trade directions (`Buy`/`Sell`) per sentiment.

### **6. Visualization**
- **Violin Plot**: Shows PnL distribution by sentiment.
- **Heatmap**: Displays trading activity by hour and sentiment.

### **7. Statistical Testing**
- **T-test**: Compares PnL between "Fear" and "Greed" groups.
- **Chi-square Test**: Checks if sentiment affects trade direction.

### **8. Predictive Modeling**
- Trains a **Random Forest Classifier** to predict profitable trades (`pnl_positive`).
- Features: `hour`, `day_of_week`, and one-hot-encoded sentiment.
- Evaluates using **accuracy** and **feature importance**.

### **9. Output Saving**
- Saves visualizations (`png`) in the `outputs/` directory.

---

## **How to Run**
1. **Upload Data**:
   - Place `trader_data.csv` and `sentiment_index.csv` in `/data/`.
2. **Run the Notebook**:
   - Execute cells in `Crypto_Sentiment_Analytics.ipynb`.
3. **Check Outputs**:
   - Visualizations are saved in `/outputs/`.

---

## **Dependencies**
- Python 3.8+
- Libraries:
  ```bash
  pandas numpy matplotlib seaborn scipy scikit-learn
  ```
  Install with:
  ```bash
  pip install -r requirements.txt
  ```

---

## **Key Findings**
1. **Sentiment Impact**:
   - Trades during "Greed" periods had **higher average PnL** than "Fear" periods (p < 0.05).
2. **Trading Activity**:
   - Most trades occurred during **UTC 12:00–15:00**, especially for "Neutral" sentiment.
3. **Model Performance**:
   - Random Forest achieved **~65% accuracy** in predicting profitable trades.
   - `hour` and `classification_Greed` were the most important features.

---

## **Improvement Suggestions**
1. **Data Cleaning**:
   - Add checks for missing values:
     ```python
     print(merged.isnull().sum())
     ```
2. **Enhanced EDA**:
   - Include correlation heatmaps or pair plots.
3. **Model Evaluation**:
   - Add precision/recall metrics:
     ```python
     from sklearn.metrics import classification_report
     print(classification_report(y_test, y_pred))
     ```
4. **Error Handling**:
   - Verify file paths before loading:
     ```python
     import os
     if not os.path.exists(file_path):
         raise FileNotFoundError(f"{file_path} does not exist!")
     ```

---


**License**: MIT  
**Last Updated**: 2025-08-18  

---
