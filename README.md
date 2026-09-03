# 🚚 Supply Chain and Logistics – Machine Learning Project

### A Predictive Modeling Report for Logistics Planning and Delay Mitigation

## 📋 Summary

This project analyzes supply chain shipment data to predict lead times and identify the operational factors driving delivery delays. Two predictive models were built and compared — **Linear Regression** and **Decision Tree Regressor** — to determine which approach estimates lead times most reliably. The analysis focuses on shipment distance, transport mode, and weather conditions as the key drivers of delay, translating the results into insights for logistics planning. Key factors influencing lead time were identified, providing actionable insights for stakeholders.

Tooling: Python (Pandas, NumPy, Scikit-Learn).

## 🎯 Project Objective

The primary objective of this project was to develop a predictive model to accurately estimate the `Lead_Time_Days` for shipments. By predicting lead times, businesses can better plan logistics, manage inventory, and communicate realistic delivery expectations to customers, ultimately enhancing supply chain reliability and customer satisfaction.


## 🗂️ Data Overview and Preparation

### Data Source
The analysis used the supply chain data 2026 comprised of **5,000 records** and **13 features** related to shipment logistics.

### ✅ Data Quality
- No missing values were found across any columns.
- No duplicate entries were found.

### 🛠️ Feature Engineering
- The `Date` column was converted to datetime format.
- A new feature, `Month`, was extracted from the `Date` column to capture potential monthly seasonality in lead times.

### 🔢 Feature Selection and Encoding
- **Target Variable (y):** `Lead_Time_Days`
- **Independent Variables (x):** All other features except `Shipment_ID` and `Date` were used. Categorical fields (such as `Transport_Mode` and `Weather_Condition`) were converted to numeric form using one-hot encoding, which allows the models to use categorical information without imposing a false numeric order on it.

### ✂️ Train-Test Split
The data was split **80/20** into training and test sets, with a fixed random seed for reproducibility. The models were trained only on the training set and evaluated only on the held-out test set.


## 🤖 Model Building and Evaluation

Two regression models were evaluated for lead time prediction:

### a) Linear Regression

| Metric | Value |
|---|---|
| Mean Absolute Error (MAE) | 12.33 |
| Root Mean Squared Error (RMSE) | 18.97 |
| R-squared (R² Score) | 0.62 |

The Linear Regression model showed a moderate fit, explaining about 62% of the variance in lead time. A notable issue was the prediction of **negative lead times (229 instances)**, which are physically impossible. This was addressed by clipping negative predictions to 1 day for practical use.

### b) Decision Tree Regressor

| Metric | Value |
|---|---|
| Mean Absolute Error (MAE) | 1.50 |
| Root Mean Squared Error (RMSE) | 3.10 |
| R-squared (R² Score) | 0.99 |

The Decision Tree model demonstrated significantly superior performance compared to Linear Regression, with an R² score of 0.99, indicating it explains nearly all the variance in lead times. It also did not produce any negative lead time predictions, making its outputs directly interpretable and actionable.


## 📊 Feature Importance

The Decision Tree model's features identify which factors most strongly influence its predictions:

| Feature | Importance |
|---|---|
| 🌀 Weather Condition: Hurricane | 0.291 |
| 📏 Distance (km) | 0.275 |
| 🚢 Transport Mode: Sea | 0.273 |
| 🚚 Transport Mode: Road | 0.065 |
| 🚆 Transport Mode: Rail | 0.044 |

**Key Observation:** Weather conditions (specifically hurricanes), the distance of the shipment, and the mode of transport (Sea, Road, Rail) are the most critical factors influencing lead times.


## ✅ Conclusion and Recommendations

### Conclusion
The Decision Tree Regressor is the preferred model for predicting supply chain lead times due to its high accuracy and practical predictions. The analysis highlights those external factors like weather conditions, along with fundamental logistical aspects like distance and transport mode, are paramount in determining shipment duration.

### Recommendations

1. 🌩️ **Prioritize Weather Monitoring:** Implement advanced weather monitoring systems, especially for routes prone to hurricanes, to proactively adjust shipment schedules and mitigate delays.
2. 🗺️ **Optimize Route Planning:** Leverage the `Distance_km` and `Transport_Mode` insights to optimize routes and modes of transport for different product categories, balancing speed and cost.
3. 🔍 **Investigate Transport Mode Efficiencies:** Further analyze specific bottlenecks or efficiencies within Sea, Road, and Rail transport modes to identify areas for improvement.
4. 🔄 **Continuous Model Improvement:** Regularly update the model with new data and explore more advanced ensemble methods to maintain and improve predictive accuracy.
