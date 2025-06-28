# World Happiness Data Analysis

This project analyzes the World Happiness dataset using Python. Every step, code, and visualization from the notebook is included here, fully documented and ready for review.

---

## Table of Contents

- [Introduction](#introduction)
- [Load the Dataset](#load-the-dataset)
- [Clean the Data](#clean-the-data)
- [Statistical & Analytical Questions](#statistical--analytical-questions)
    - [Q1: Average Happiness Score](#q1-average-happiness-score)
    - [Q2: Countries with High Economy & Freedom](#q2-countries-with-high-economy--freedom)
    - [Q3: High Health but Low Happiness](#q3-high-health-but-low-happiness)
    - [Q4: Happiness Score per Region](#q4-happiness-score-per-region)
    - [Q5: Top 5 Happiest Countries](#q5-top-5-happiest-countries)
    - [Q6: Top 5 in Happiest Region](#q6-top-5-in-happiest-region)
    - [Q7: Above-Average Economy & Health, Sorted by Freedom](#q7-above-average-economy--health-sorted-by-freedom)
- [Visualizations](#visualizations)
    - [Q8: Bar Chart - Average Happiness Score per Region](#q8-bar-chart---average-happiness-score-per-region)
    - [Q9: Scatter Plot - Economy vs Happiness Score](#q9-scatter-plot---economy-vs-happiness-score)
    - [Q10: Pie Chart - Countries per Region](#q10-pie-chart---countries-per-region)
- [Installation](#installation)
- [Dataset](#dataset)
- [Usage](#usage)
- [Dependencies](#dependencies)
- [Troubleshooting](#troubleshooting)
- [Contributors](#contributors)
- [License](#license)

---

## Introduction

This notebook-based project explores the "World Happiness" dataset to understand which factors drive happiness around the world. Using pandas, matplotlib, and seaborn, the project loads, cleans, analyzes, and visualizes global happiness data.

---

## Load the Dataset

We begin by loading the dataset using pandas.

> **Dataset file required:** `World Happiness.xlsx`

```python
import pandas as pd
df = pd.read_excel("World Happiness.xlsx")
df.head()
```

## Clean the Data

This step handles missing values, fixes data types, or removes unnecessary columns.  
(Customize this section with your own data-cleaning code if you add more later!)

```python
# Example cleaning steps (customize as needed)
df = df.dropna()  # Remove missing values
# df = df.astype({'Happiness Score': float}) # Fix data types if necessary
# df = df.drop(columns=['Unnecessary Column']) # Remove columns if any
```

## Statistical & Analytical Questions

We answer several analytical questions using pandas and Python.

### Q1: Average Happiness Score
### Goal: Calculate the global average happiness score.

```python
avg_happiness = df['Happiness Score'].mean()
print("Average Happiness Score across all countries:", round(avg_happiness, 2))
```
### Q2: Countries with High Economy & Freedom
### Goal: List countries with an Economy score greater than 1.0 and Freedom greater than 0.5.

```python
filter1 = df[(df['Economy'] > 1.0) & (df['Freedom'] > 0.5)]
filter1[['Country', 'Economy', 'Freedom']]
```

### Q3: High Health but Low Happiness
### Goal: Find countries where Health > 0.8 but Happiness Score < 5.

```python
filter2 = df[(df['Health'] > 0.8) & (df['Happiness Score'] < 5)]
filter2[['Country', 'Health', 'Happiness Score']]
```

### Q4: Happiness Score per Region
### Goal: Compute the average Happiness Score for each region.

```python
region_avg = df.groupby('Region')['Happiness Score'].mean().sort_values(ascending=False)
region_avg
```

### Q5: Top 5 Happiest Countries
### Goal: Identify the top 5 countries with the highest happiness scores.

```python
top_5 = df.sort_values('Happiness Score', ascending=False).head(5)
top_5[['Country', 'Happiness Score']]
```

### Q6: Top 5 in Happiest Region
### Goal: Find the top 5 happiest countries in the region with the highest average happiness score.

```python
top_region = region_avg.idxmax()
region_df = df[df['Region'] == top_region]
top_5_region = region_df.sort_values('Happiness Score', ascending=False).head(5)
top_5_region[['Country', 'Happiness Score']]
```

### Q7: Above-Average Economy & Health, Sorted by Freedom
### Goal: List countries with above-average Economy and Health, sorted by Freedom.

```python
econ_avg = df['Economy'].mean()
health_avg = df['Health'].mean()
combo_df = df[(df['Economy'] > econ_avg) & (df['Health'] > health_avg)]
combo_sorted = combo_df.sort_values('Freedom', ascending=False)
combo_sorted[['Country', 'Economy', 'Health', 'Freedom']]
```

### Visualizations

The following plots help visualize happiness across the world.

### Q8: Bar Chart - Average Happiness Score per Region
### This bar chart shows the average happiness score for each region.

```python
import matplotlib.pyplot as plt
plt.figure(figsize=(10, 5))
region_avg.plot(kind='bar')
plt.title("Average Happiness Score by Region")
plt.ylabel("Happiness Score")
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()
```

### Q9: Scatter Plot - Economy vs Happiness Score
### This scatter plot shows the relationship between Economy score and Happiness Score, colored by Region.

```python
import seaborn as sns
plt.figure(figsize=(7, 5))
sns.scatterplot(data=df, x='Economy', y='Happiness Score', hue='Region')
plt.title("Economy vs Happiness Score")
plt.xlabel("Economy")
plt.ylabel("Happiness Score")
plt.show()
```

### Q10: Pie Chart - Countries per Region
### This pie chart shows the proportion of countries in each region.

```python
region_counts = df['Region'].value_counts()
plt.figure(figsize=(7, 7))
region_counts.plot(kind='pie', autopct='%1.1f%%', startangle=140)
plt.title("Proportion of Countries per Region")
plt.ylabel("")
plt.show()
```

## Installation
Clone the repository:

```python
git clone https://github.com/yourusername/world-happiness-project.git
cd world-happiness-project
```
Install dependencies:
```python
pip install pandas matplotlib seaborn openpyxl
```

## Dataset

- Download the dataset from [Kaggle - World Happiness Report](https://www.kaggle.com/unsdsn/world-happiness).
- Rename the downloaded file to **World Happiness.xlsx**.
- Place the file in the project directory.

## Usage

- Open `World_Happines_Project.ipynb` in Jupyter Notebook or Google Colab.
- Run the notebook cells in order.
- All outputs, tables, and visualizations will appear as described above.

---

## Dependencies

- pandas
- matplotlib
- seaborn
- openpyxl

---

## Troubleshooting

- **FileNotFoundError:** Make sure `World Happiness.xlsx` is in the project directory.
- **Library Errors:** Install missing packages with the pip command above.
- **Excel Read Errors:** Make sure you have the latest version of `openpyxl`.

---

## Contributors

This project was developed solely by **Muhammad Adnan Mushtaq**.

---

## License

This project is licensed under the MIT License.





