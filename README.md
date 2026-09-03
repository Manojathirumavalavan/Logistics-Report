# Logistics Data Collection, Cleaning & Preprocessing

A Python-based data preprocessing project for logistics analytics using the **Brazilian E-Commerce Public Dataset by Olist**.

## 📌 Project Overview

This project simulates a logistics data preparation pipeline using Python. The main objective is to transform raw e-commerce and logistics-related data into a clean, reliable, and analysis-ready dataset.

The project focuses on identifying and resolving common data-quality problems such as missing values, duplicate records, incorrect data types, invalid values, and outliers. The cleaned data can be used for further logistics analysis, including delivery performance analysis, delay prediction, transportation cost analysis, customer segmentation, and route optimization.

## 🎯 Objectives

* Collect and understand a publicly available logistics-related dataset.
* Perform initial data profiling and quality assessment.
* Identify and handle missing values.
* Detect and remove duplicate records where appropriate.
* Convert data into suitable formats and data types.
* Identify potential outliers using statistical methods.
* Validate data using logistics-specific business rules.
* Create useful logistics-related features.
* Encode categorical variables.
* Normalize and standardize numerical variables.
* Prepare the dataset for future data analysis and machine-learning applications.

## 📊 Dataset

This project uses the **Brazilian E-Commerce Public Dataset by Olist**.

The dataset contains approximately 100,000 anonymized orders from 2016 to 2018 and includes several related tables, such as:

* Orders
* Order Items
* Customers
* Products
* Payments
* Reviews
* Sellers
* Geolocation

The dataset contains information that can be used to study delivery performance, freight costs, customer locations, product characteristics, and other logistics-related factors.

**Dataset Source:** Kaggle – Brazilian E-Commerce Public Dataset by Olist

The original dataset is not included in this repository. Please download it from Kaggle and place the required CSV files inside the `data/` folder.

## 🛠️ Technologies Used

* **Python**
* **Pandas** – Data loading, cleaning, transformation, and analysis
* **NumPy** – Numerical operations
* **Scikit-learn** – Data preprocessing and feature scaling
* **Matplotlib** – Data visualization
* **Git & GitHub** – Version control and project documentation

## 🔄 Data Preprocessing Workflow

```text
Raw Logistics Data
        ↓
Data Collection
        ↓
Data Profiling
        ↓
Duplicate Detection
        ↓
Data Type Conversion
        ↓
Missing Value Handling
        ↓
Business Rule Validation
        ↓
Outlier Detection
        ↓
Feature Engineering
        ↓
Categorical Encoding
        ↓
Numerical Scaling
        ↓
Final Quality Checks
        ↓
Analysis-Ready Dataset
```

## 🧹 Data Cleaning Techniques

### 1. Missing Values

Missing values are identified using Pandas.

Different strategies are applied depending on the importance and meaning of the column:

* Numerical values → median imputation when appropriate
* Categorical values → `"Unknown"` or mode
* Critical missing values → investigated or excluded from specific analysis
* Review information → kept missing rather than treating it as a zero score

### 2. Duplicate Records

Duplicate records are identified using Pandas.

For example, `order_id` should uniquely identify an order in the order-level table. However, multiple records for the same order are valid in the order-items table because one order may contain multiple products.

Therefore, duplicates are removed according to the structure of each table instead of blindly deleting repeated IDs.

### 3. Data Type Conversion

Timestamp columns are converted into proper datetime format so that delivery duration and delivery delay can be calculated correctly.

Example:

```python
orders["order_purchase_timestamp"] = pd.to_datetime(
    orders["order_purchase_timestamp"],
    errors="coerce"
)
```

### 4. Outlier Detection

The **Interquartile Range (IQR)** method is used to identify potential outliers.

Potential outliers may occur in:

* Freight value
* Product price
* Delivery duration
* Package weight
* Package dimensions

An extreme value is not automatically removed because it may represent a genuine logistics event.

### 5. Business Rule Validation

Logistics-specific validation rules are applied to identify impossible or suspicious records.

Examples:

* Freight value should not normally be negative.
* Product price should not normally be negative.
* Delivery date should not occur before purchase date.
* Delivery duration should not be negative.

## ⚙️ Feature Engineering

The preprocessing pipeline creates useful logistics features, including:

### `delivery_days`

The number of days between order purchase and customer delivery.

### `delay_days`

The difference between actual delivery and estimated delivery.

### `is_late`

A binary indicator:

```text
1 → Delivered late
0 → Not delivered late
```

### `freight_ratio`

The relationship between freight cost and product price.

These features can later be used for logistics KPI analysis and machine-learning models.

## 📏 Data Scaling

Numerical variables can have very different ranges. Scaling makes them more suitable for many machine-learning algorithms.

This project demonstrates:

* `StandardScaler`
* `MinMaxScaler`

Example:

```python
from sklearn.preprocessing import StandardScaler

scaler = StandardScaler()

X_train_scaled = scaler.fit_transform(X_train)
X_test_scaled = scaler.transform(X_test)
```

The scaler is fitted only on the training data to avoid data leakage.

## 📁 Project Structure

```text
logistics-data-preprocessing/
│
├── README.md
├── preprocessing.py
├── requirements.txt
├── .gitignore
│
├── data/
│   └── README.md
│
└── docs/
    └── Week_2_Logistics_Data_Cleaning_Preprocessing_Report.docx
```

## 🚀 How to Run the Project

### Step 1: Clone the Repository

```bash
git clone https://github.com/Manojathirumavalavan/logistics-data-preprocessing.git
```

### Step 2: Open the Project

```bash
cd logistics-data-preprocessing
```

### Step 3: Install Dependencies

```bash
pip install -r requirements.txt
```

### Step 4: Download the Dataset

Download the Olist dataset from Kaggle and place the CSV files inside:

```text
data/
```

### Step 5: Run the Preprocessing Script

```bash
python preprocessing.py
```

The script will perform data profiling, cleaning, feature engineering, outlier detection, and numerical preprocessing.

## 📈 Expected Outcomes

After preprocessing, the project provides a cleaner and more reliable foundation for logistics analytics.

The prepared data can support:

* Delivery performance analysis
* On-time delivery analysis
* Delivery delay prediction
* Freight cost analysis
* Customer/location segmentation
* Transportation analysis
* Route optimization
* Supply-chain decision-making

## 💡 Business Impact

High-quality logistics data helps organizations make better operational decisions.

For example:

* Accurate delivery dates improve delivery-performance KPIs.
* Correct freight values improve transportation-cost analysis.
* Removing true duplicate records prevents shipment volumes from being overstated.
* Handling missing values appropriately improves analytical reliability.
* Detecting unusual values prevents extreme observations from unnecessarily distorting models.
* Standardized data improves the performance of many machine-learning algorithms.

Therefore, data preprocessing is an important foundation for efficient logistics and supply-chain analytics.

## 📚 Documentation

The detailed Week 2 report is available in:

```text
docs/Week_2_Logistics_Data_Cleaning_Preprocessing_Report.docx
```

The report provides a detailed explanation of the methodology, data-quality issues, preprocessing techniques, Python code, and reflection.

## 🔮 Future Enhancements

The project can be extended with:

* Exploratory Data Analysis dashboards
* Delivery-delay prediction models
* Freight-cost prediction
* Customer and location clustering
* Route optimization using Google OR-Tools
* Interactive logistics dashboards
* Automated data-quality reports
* Model performance evaluation

## 👩‍💻 Author

**Manoja T**

**B.Tech – Computer Science and Engineering**

This project was developed as part of a technical internship/task focused on logistics data analysis and Python-based data preprocessing.

## 📌 Note

The raw Olist dataset is not included in this repository. Users should download the publicly available dataset from Kaggle and place the required CSV files in the `data/` directory.
