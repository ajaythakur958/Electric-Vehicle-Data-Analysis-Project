# 🚗 Electric Vehicle (EV) Data Analysis Project  

## 📌 Project Overview  
This project focuses on analyzing a dataset of electric vehicles (EVs) to derive insights related to **price, battery capacity, range, performance, and efficiency**.  
It includes **data cleaning, visualization, statistical analysis, and building a simple EV recommender system** to help customers choose the right EV based on their preferences.

---

## 📊 Dataset Information  
- **Dataset File:** `Auta elektryczne.csv`  
- **Total Rows:** 53  
- **Columns:** 25  
- **Key Features:**  
  - `Car full name`, `Make`, `Model`  
  - `Minimal price (gross) [PLN]`, `Engine power [KM]`, `Battery capacity [kWh]`  
  - `Range (WLTP) [km]`, `Maximum torque [Nm]`, `Acceleration 0-100 kph [s]`  
  - `mean - Energy consumption [kWh/100 km]`

---

## 🛠 Libraries Used  
```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
from scipy.stats import ttest_ind
```

---

## 🔧 Data Preprocessing  
✅ Checked data types and duplicates  
✅ Handled missing values using `fillna()` with median and mode  
✅ Verified clean dataset after preprocessing  

---

## 📑 Tasks Performed  

### **📍 Task 1: Filtering EVs Based on Customer Requirement**  
**Requirement:**  
- Budget ≤ **350,000 PLN**  
- Minimum Range ≥ **400 km**  

Filtered EVs were sorted by **range** (descending) and **price** (ascending).  
Also calculated **average battery capacity per manufacturer**.  

📊 **Insights:**  
- **Audi** provides the highest battery capacity (95 kWh).  
- **Volkswagen ID.3 Pro S** & **Tesla Model 3 Long Range** are top recommendations within budget.

---

### **📍 Task 2: Outlier Detection**  
- Checked distribution of `mean - Energy consumption [kWh/100 km]`  
- Used **Boxplot** & **IQR Method** to detect outliers  

📊 **Insights:**  
- Data is slightly right-skewed  
- No major outliers under 1.5×IQR rule  
- Using 1×IQR rule, found one high outlier:  
  **Mercedes-Benz EQV (long)** → 28.2 kWh/100 km  

---

### **📍 Task 3: Relationship Between Battery Capacity & Range**  
Created **scatter plot** to visualize correlation.  

📊 **Insights:**  
- Strong **positive correlation** → higher battery capacity leads to higher range  
- Some outliers exist due to weight/efficiency differences

📷 **Visualization:**  
![Battery Capacity vs Range](https://github.com/user-attachments/assets/8bdf1023-6a5b-478b-9d44-ddf04b44eeb7)

---

### **📍 Task 4: EV Recommendation Class**  
Built a **class-based recommender**:  

```python
class EvRecommender:
    def __init__(self, ev_df):
        self.ev_df = ev_df

    def recommend(self, budget, min_range, min_battery):
        filtered_data = self.ev_df[
            (self.ev_df["Minimal price (gross) [PLN]"] <= budget) &
            (self.ev_df["Range (WLTP) [km]"] >= min_range) &
            (self.ev_df["Battery capacity [kWh]"] >= min_battery)
        ]
        filtered_data = filtered_data.sort_values(
            by=["Minimal price (gross) [PLN]", "Range (WLTP) [km]"],
            ascending=[True, False]
        )
        return filtered_data.head(3)[
            ["Car full name", "Make", "Model", "Minimal price (gross) [PLN]",
             "Battery capacity [kWh]", "Range (WLTP) [km]"]
        ]
```

🔧 **Usage:**  
```python
recommender = EvRecommender(df)
recommender.recommend(budget=250000, min_range=450, min_battery=60)
```

---

### **📍 Task 5: Hypothesis Testing**  
**Objective:** Test if there is a significant difference in average engine power between **Tesla** and **Audi**.

- **Null Hypothesis (H₀):** No significant difference in engine power  
- **Alternative Hypothesis (H₁):** Significant difference exists  

✅ **Welch’s t-test result:**  
- p-value = **0.1068 > 0.05** → Fail to reject H₀  
- **Conclusion:** No statistically significant difference between Tesla & Audi engine power in this dataset.

---

## 📈 Key Insights  
- **Battery capacity is the strongest predictor of range** — higher battery capacity is strongly correlated with longer driving range.  
- **No statistically significant difference** in average engine power between **Tesla** and **Audi**, based on hypothesis testing performed on the given dataset.  
- **Tesla Model 3** and **Volkswagen ID.3** provide excellent value for money considering price, range, and performance.  
- **Outliers in energy consumption are rare**, with most EVs falling within a reasonable efficiency range.

---

## 🎯 Conclusion  
This project demonstrates:  
- **Data cleaning & preprocessing**  
- **Exploratory Data Analysis (EDA)**  
- **Outlier detection & visualization**  
- **Hypothesis testing**  
- **Recommendation system using OOP**

---

## 🙏 Thank You  
Thanks for reading!  
📌 **Connect with me on LinkedIn:** [Ajay Thakur](https://www.linkedin.com/in/ajay-thakur-5158bb186/)  
