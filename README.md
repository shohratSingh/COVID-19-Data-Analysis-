# COVID-19 Data Analysis with World Happiness Report

## 📌 Project Overview

This project analyzes how COVID-19 infection rates relate to various socio-economic and happiness factors across different countries. By combining the **COVID-19 Confirmed Cases Dataset** with the **World Happiness Report**, the project explores whether factors such as **GDP per capita**, **Social Support**, **Healthy Life Expectancy**, and **Freedom to make life choices** have any connection with the spread of COVID-19.

---

## 🎯 Objectives

- Clean and preprocess COVID-19 data.
- Calculate the **maximum daily infection rate** for each country.
- Merge COVID-19 data with the **World Happiness Report**.
- Analyze and visualize correlations between infection rates and happiness indicators.
- Draw meaningful insights and conclusions.

---

## 📂 Datasets Used

| Dataset | Description | Source |
|---------|-------------|--------|
| `covid19_Confirmed_dataset.csv` | Daily confirmed COVID-19 cases by country. | Johns Hopkins University |
| `worldwide_happiness_report.csv` | Happiness scores and socio-economic indicators of countries. | World Happiness Report |

---

## ⚙️ Technologies Used

- Python
- NumPy
- Pandas
- Matplotlib
- Seaborn

---

## 🛠️ Data Processing Workflow

### 1. Load the COVID-19 Dataset
```python
dataset = pd.read_csv("/content/covid19_Confirmed_dataset.csv")
```

### 2. Data Cleaning
- Remove unnecessary columns:
```python
dataset.drop(['Lat', 'Long'], axis=1, inplace=True)
```

### 3. Group Data by Country
```python
corona_data_aggregated = dataset.groupby('Country/Region').sum()
```

### 4. Calculate Maximum Daily Infection Rate
```python
max_infection_rates = []
for country in corona_data_aggregated.index:
    max_infection_rates.append(corona_data_aggregated.loc[country].diff().max())
corona_data_aggregated['max_infection_rates'] = max_infection_rates
```

### 5. Load and Clean Happiness Report Data
```python
happiness_report = pd.read_csv('/content/worldwide_happiness_report.csv')
happiness_report.drop(['Overall rank', 'Score', 'Generosity', 'Perceptions of corruption'], axis=1, inplace=True)
happiness_report.set_index('Country or region', inplace=True)
```

### 6. Merge Both Datasets
```python
corona_data = pd.DataFrame(corona_data_aggregated['max_infection_rates'])
data = corona_data.join(happiness_report, how='inner')
```

---

## 📈 Exploratory Data Analysis

### 🔹 Correlation Matrix
```python
data.corr()
```

### 🔹 Scatter Plot with Regression
Example:
```python
x = data['GDP per capita']
y = data['max_infection_rates']
sns.regplot(x=x, y=y)
```

Analyzed relationships between:
- GDP per capita vs Infection Rate  
- Social support vs Infection Rate  
- Health expectancy vs Infection Rate  
- Freedom to make life choices vs Infection Rate  

---

## ✅ Key Insights

- Countries with higher GDP and stronger healthcare systems reported higher early infection rates due to better testing and transparency.
- Social support shows mild correlation with infection spread — more connected societies may spread the virus faster.
- Freedom and happiness do not directly influence infection rates but could impact management and response strategies.

---

## 📌 Conclusion

This project shows how data analytics can combine health statistics and socio-economic indicators to derive meaningful insights. While happiness doesn't prevent infection, economic and healthcare infrastructure show weak relationships with COVID-19 spread.

---

Feel free to use, modify, and improve this project! 🌍
