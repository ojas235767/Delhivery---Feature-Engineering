## 📦 Delhivery Logistics Optimization and Forecasting

-----

## 💡 Project Overview

This project focuses on using data analytics and machine learning techniques to understand and optimize the logistics operations of **Delhivery**. The primary goal is to transform raw logistics data into actionable insights and build intelligence that can be used for **predictive modeling** (specifically, forecasting accurate transit times).

The project covers data cleaning, feature engineering, statistical analysis, and provides key operational recommendations to improve delivery efficiency and resource planning.

-----

## 🎯 Problem Statement

Delhivery aims to tackle three core challenges:

1.  **Data Quality:** Clean and manipulate raw, segment-level operational data to extract high-value features for analysis.
2.  **Forecasting Intelligence:** Develop robust features (like speed and time ratios) crucial for training accurate models that predict true travel time.
3.  **Operational Optimization:** Derive data-driven insights to recommend improvements for routing, capacity planning, and reducing delivery time discrepancies.

-----

## ⚙️ Project Methodology and Analysis

The project pipeline involved the following key steps:

### 1\. Data Cleaning and Preprocessing

  * **Aggregation:** Consolidated $\sim145,000$ segment-level rows into unique $\sim15,000$ **trip-level** records using `trip_uuid`.
  * **Missing Values:** Handled null values in key columns like `source_name` and `segment_distance_time_ratio` using **Mode** (categorical) and **Median** (numerical) imputation.
  * **Outlier Treatment:** Applied **Interquartile Range (IQR)**-based capping to critical time and distance features (e.g., `actual_time`, `osrm_distance`) to reduce the impact of extreme values.

### 2\. Feature Engineering

Several new features were created to capture the dynamics of the trips:

| Feature Name | Description | Units |
| :--- | :--- | :--- |
| `trip_duration` | Total time from start to end scan. | Minutes |
| `time_to_cutoff` | Time from trip start to the cutoff event. | Minutes |
| `distance_time_ratio` | Actual distance traveled per unit of actual time. | $\text{km/min}$ |
| `time_efficiency` | Ratio of OSRM Time (Predicted) to Actual Time (Observed). | Unitless |

### 3\. Key Findings

  * **High Correlation:** A strong linear relationship exists between **Actual** and **OSRM** time and distance metrics (correlation $\ge$ 0.95), suggesting OSRM is a good baseline predictor for route length.
  * **Efficiency Gap (Hypothesis Testing):** An Independent Samples **t-test** confirmed a statistically **significant difference** between the mean actual time and the mean OSRM time (P-value $\approx$ 0.0000).
  * **Major Inefficiency:** The mean `time_efficiency` ratio is approximately **0.55**, indicating that the **actual delivery time is nearly double** the time predicted by routing software. This highlights that delays are primarily due to **non-travel factors** (e.g., loading, waiting, procedural delays) rather than just traffic.

-----

## 🚀 Recommendations

The analysis led to the following actionable recommendations:

  * **Prioritize Long/Inefficient Routes:** Focus on optimizing the process flows and resources for **FTL (Full Truck Load)** routes and trips with the lowest `time_efficiency` ratio.
  * **Capacity Planning:** Use the derived time-based patterns (e.g., high order volumes on certain days/months) to plan for labor and vehicle resources more accurately.
  * **Predictive Model Development:** Utilize the cleaned data and engineered features to build a machine learning model that accurately forecasts the **Actual Time** by accounting for the systemic delays missed by OSRM.

-----

## 🛠️ Technologies Used

  * **Python**
  * **Pandas** (Data manipulation and cleaning)
  * **NumPy** (Numerical operations)
  * **Scikit-learn** (Preprocessing and scaling)
  * **Matplotlib** / **Seaborn** (Visual Analysis)

-----

## 📂 Repository Structure

```
.
├── delhivery_data.csv        # The original dataset used for analysis
├── Delhivery_Analysis.ipynb  # Jupyter Notebook containing all the code and analysis
└── README.md                 # Project documentation
```

-----

## 🤝 Contribution

Feel free to fork this repository, explore the data, and suggest further analysis or model implementations\!

Would you like to add a section about **how to run the notebook** or any other details?
