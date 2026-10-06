# Python DA Assignment 2 – Data Visualization

## 📌 Project Overview

This project focuses on analyzing and visualizing taxi trip data using **Python, Pandas, Matplotlib, and Seaborn**.

The main objective of this project is to clean and analyze taxi trip data, handle missing values, explore relationships between different variables, and create meaningful visualizations to understand fare, distance, tips, payment methods, and pickup locations.

---

## 🎯 Objectives

The objectives of this project are:

* Load and explore the Seaborn `taxis` dataset.
* Identify and handle missing values.
* Apply suitable imputation techniques for categorical data.
* Convert the pickup timestamp into datetime format.
* Perform basic data analysis using Pandas.
* Create different visualizations using Matplotlib and Pandas.
* Create advanced visualizations using Seaborn.
* Analyze relationships between fare, distance, tips, tolls, and total amount.
* Identify useful patterns and insights from taxi trip data.

---

## 📊 Dataset Information

The project uses the built-in **Taxis dataset from Seaborn**.

### Dataset Size

* **Rows:** 6,433
* **Columns:** 15
* **Domain:** Taxi / Transportation

### Dataset Loading

```python
import seaborn as sns

df = sns.load_dataset("taxis")
```

---

## 📋 Dataset Columns

| Column            | Description            |
| ----------------- | ---------------------- |
| `pickup`          | Pickup date and time   |
| `dropoff`         | Drop-off date and time |
| `passengers`      | Number of passengers   |
| `distance`        | Trip distance          |
| `fare`            | Taxi fare              |
| `tip`             | Tip amount             |
| `tolls`           | Toll amount            |
| `total`           | Total trip cost        |
| `color`           | Taxi color             |
| `payment`         | Payment method         |
| `pickup_zone`     | Pickup zone            |
| `dropoff_zone`    | Drop-off zone          |
| `pickup_borough`  | Pickup borough         |
| `dropoff_borough` | Drop-off borough       |

---

## 🛠️ Technologies Used

* **Python**
* **Pandas**
* **NumPy**
* **Matplotlib**
* **Seaborn**
* **Google Colab**
* **Jupyter Notebook**

---

## 🧹 Data Cleaning and Preparation

The following data preparation steps were performed:

### 1. Dataset Loading

The Seaborn `taxis` dataset was loaded using:

```python
df = sns.load_dataset("taxis")
```

### 2. Data Exploration

The dataset was explored using:

```python
df.head()
df.shape
df.columns
df.dtypes
df.info()
df.describe()
```

### 3. Missing Value Analysis

Missing values were checked using:

```python
df.isnull().sum()
```

Missing values were identified in the following categorical columns:

* `payment`
* `pickup_zone`
* `dropoff_zone`
* `pickup_borough`
* `dropoff_borough`

### 4. Missing Value Handling

Since the missing columns were categorical, the **mode** was used to replace missing values.

```python
for column in categorical_columns:
    df[column] = df[column].fillna(df[column].mode()[0])
```

The dataset was then checked again to confirm that the missing values had been handled.

### 5. Date and Time Conversion

The `pickup` column was converted into datetime format:

```python
df['pickup'] = pd.to_datetime(df['pickup'])
```

This allowed time-based analysis and visualization.

---

# 📈 Visualizations

## 1. Line Chart – Fare Over Time

A line chart was created to visualize how taxi fare changes over time.

* **X-axis:** Pickup time
* **Y-axis:** Fare

```python
plt.figure(figsize=(12, 6))

plt.plot(df['pickup'], df['fare'])

plt.title('Fare Over Time')
plt.xlabel('Pickup Time')
plt.ylabel('Fare')

plt.xticks(rotation=45)
plt.tight_layout()

plt.show()
```

### Insight

The line chart helps identify variations in taxi fares across different pickup times.

---

## 2. Bar Chart – Total Fare by Pickup Borough

The total fare was calculated for each pickup borough.

```python
borough_fare = df.groupby('pickup_borough')['fare'].sum()
```

A bar chart was then created to compare the total fare between boroughs.

### Insight

The visualization helps identify which pickup borough contributes the highest total fare.

---

## 3. Pie Chart – Payment Method Distribution

The number of trips for each payment method was calculated.

```python
payment_counts = df['payment'].value_counts()
```

A pie chart was created to show the percentage distribution of payment methods.

### Insight

The chart helps compare the popularity of different payment methods such as credit card and cash.

---

## 4. Histogram – Distance Distribution

A histogram was created to understand the distribution of taxi trip distances.

```python
plt.hist(df['distance'], bins=30)
```

### Insight

The histogram shows the most common trip-distance ranges and helps identify longer-distance trips.

---

## 5. Box Plot – Tip Distribution by Pickup Borough

A box plot was created to compare tip amounts across pickup boroughs.

```python
df.boxplot(
    column='tip',
    by='pickup_borough'
)
```

### Insight

The box plot helps compare tip distributions, identify differences between boroughs, and detect potential outliers.

---

# 📊 Seaborn Visualizations

## 6. Count Plot – Trips by Pickup Borough

A Seaborn count plot was used to visualize the number of trips originating from each pickup borough.

```python
sns.countplot(
    data=df,
    x='pickup_borough'
)
```

### Insight

The count plot helps identify the pickup boroughs with the highest and lowest number of trips.

---

## 7. Scatter Plot – Distance vs Fare

A scatter plot was created to analyze the relationship between trip distance and fare.

```python
sns.scatterplot(
    data=df,
    x='distance',
    y='fare',
    hue='pickup_borough'
)
```

### Insight

The scatter plot helps understand whether longer taxi trips generally result in higher fares and allows comparison between pickup boroughs.

---

## 8. Heatmap – Correlation Analysis

A correlation matrix was created using:

* Distance
* Fare
* Tip
* Tolls
* Total

```python
numeric_columns = [
    'distance',
    'fare',
    'tip',
    'tolls',
    'total'
]

correlation_matrix = df[numeric_columns].corr()
```

The correlation matrix was visualized using a heatmap.

### Insight

The heatmap helps identify positive and negative relationships between numerical variables.

---

## 9. Pair Plot – Pairwise Relationships

A pair plot was created for:

* Distance
* Fare
* Tip
* Total

The points were colored based on `pickup_zone`.

```python
pairplot_data = df[
    ['distance', 'fare', 'tip', 'total', 'pickup_zone']
]

sns.pairplot(
    pairplot_data,
    hue='pickup_zone'
)
```

### Insight

The pair plot provides a detailed view of pairwise relationships between important numerical variables across different pickup zones.

---

## 10. Violin Plot – Fare by Payment Method

A violin plot was created to compare fare distributions across different payment methods.

```python
sns.violinplot(
    data=df,
    x='payment',
    y='fare'
)
```

### Insight

The violin plot shows the distribution, spread, and density of fares for each payment method.

---

# 🔍 Key Findings

The analysis produced the following major observations:

1. Taxi fares vary across different pickup times.
2. Different pickup boroughs contribute different amounts of total fare.
3. Payment methods have different levels of usage among taxi passengers.
4. Most taxi trips are concentrated within shorter distance ranges.
5. Tip amounts vary across pickup boroughs, with some higher-value observations and outliers.
6. Pickup boroughs have different numbers of taxi trips.
7. Trip distance and fare show a relationship that can be explored using the scatter plot.
8. The correlation heatmap highlights relationships between distance, fare, tip, tolls, and total.
9. Pairwise relationships between distance, fare, tip, and total can be compared across pickup zones.
10. Fare distributions vary across payment methods.

---

# 📄 Project Summary

A one-page summary of the project findings has also been prepared separately.

**Summary includes:**

* Project overview
* Data cleaning process
* Key findings
* Visualization insights
* Conclusion

---

# 🔗 Project Resources

* **Google Colab Notebook:** `https://colab.research.google.com/drive/1c1yhnVDRD5Z0cO6ev6odRoYmrPfOlQe0?usp=sharing`

---

# 📂 Project Structure

```text
Python-DA-Assignment-2-Data-Visualization/
│
├── Python_DA_Assignment_2_Data_Visualization.ipynb
├── Python_DA_Assignment_2_Summary.pdf
└── README.md
```

---

# 🎓 Learning Outcomes

Through this assignment, I learned and practiced:

* Loading datasets using Seaborn
* Exploring datasets using Pandas
* Identifying missing values
* Handling categorical missing values
* Converting columns to appropriate data types
* Grouping and aggregating data
* Creating visualizations using Matplotlib
* Creating visualizations using Seaborn
* Understanding correlation
* Analyzing relationships between variables
* Extracting insights from visualizations
* Presenting data analysis results clearly

---

# 🏁 Conclusion

This project demonstrates the use of Python-based data analysis and visualization techniques to understand taxi trip data. The dataset was cleaned, missing values were handled appropriately, and multiple visualizations were created using Matplotlib and Seaborn.

The analysis provides useful insights into **fare, trip distance, tips, payment methods, pickup locations, and relationships between numerical variables**. These insights demonstrate how data visualization can support better understanding and decision-making in transportation data.

---

## 👤 Author

**Gurucharan S**
**Data Analytics Student**

---

## ⭐ Project Status

**Completed ✅**
