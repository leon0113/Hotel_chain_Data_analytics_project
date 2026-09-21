# 🏨 AtliQ Hotels: Exploratory Data Analysis with Pandas

An end-to-end exploratory data analysis (EDA) of hotel booking data for **AtliQ Hotels**, a hospitality chain operating seven hotel brands across four Indian cities. The project covers the full analysis workflow: loading and joining multiple tables, cleaning messy data, engineering new metrics, and answering business questions on occupancy, revenue, and customer ratings.

> **Tech stack:** Python 3.10 · Pandas · NumPy · Matplotlib · Jupyter Notebook

---

## 📌 Project Objective

To practice and demonstrate practical **Pandas** skills on a realistic, multi-table business dataset, and to turn raw booking records into insights a hotel revenue manager could act on.

---

## 🗂️ Dataset Overview

The analysis uses a star-schema style dataset with fact and dimension tables:

| Table | Type | Description |
|---|---|---|
| `fact_bookings.csv` | Fact | Individual bookings (134,590 rows × 12 columns): guests, room category, platform, status, ratings, revenue |
| `fact_aggregated_bookings.csv` | Fact | Daily successful bookings vs. room capacity, per property and room category |
| `dim_hotels.csv` | Dimension | Property name, category, and city |
| `dim_rooms.csv` | Dimension | Room IDs mapped to room classes (Standard, Elite, Premium, Presidential) |
| `dim_date.csv` | Dimension | Calendar attributes: month, week number, weekday/weekend flag |
| `new_data_august.csv` | Fact | Additional August data, appended to the existing dataset |

**Coverage:** May – July 2022 · 25 properties · 4 cities (Mumbai, Delhi, Bangalore, Hyderabad) · 4 room classes · 7 booking platforms

---

## 🔍 What I Did

### 1. Data Exploration
- Inspected shape, data types, and unique values of categorical columns (room category, booking platform, booking status)
- Visualized booking volume per platform
- Computed total successful bookings per property and identified the highest-capacity property

### 2. Data Cleaning
| Issue found | How I handled it |
|---|---|
| Invalid guest counts (zero or negative, e.g. -17) | Filtered out records where `no_guests <= 0` |
| Extreme revenue outliers (e.g. ₹28,560,000 for a single booking) | Applied a statistical cut-off of **mean + 3 × standard deviation** (≈ ₹294,498) and removed values above it (5 records) |
| Missing `capacity` values in aggregated data | Imputed with the **median** |
| Records where `successful_bookings > capacity` (logically impossible) | Identified and filtered out |
| Mixed date formats in `check_in_date` | Standardized using `pd.to_datetime(format="mixed", dayfirst=True)` |

### 3. Data Transformation
- Created a new metric, **Occupancy %** = `successful_bookings / capacity × 100`, formatted with `.apply()` and a lambda function
- Merged fact and dimension tables using `pd.merge()` on different key names (`left_on` / `right_on`)
- Combined new monthly data with existing data using `pd.concat()`

### 4. Business Questions Answered

- Average occupancy by room class
- Average occupancy by city
- Weekday vs. weekend occupancy
- June 2022 occupancy by city
- Revenue realized per city
- Month-by-month revenue
- Revenue realized per hotel brand
- Average customer rating per city
- Revenue share by booking platform (pie chart)

---

## 📊 Key Findings

- **Weekends drive occupancy:** average occupancy is about **72.3% on weekends vs. 50.9% on weekdays**, a gap of over 21 percentage points.
- **Presidential rooms have the highest occupancy** (~59.3%), while Standard rooms have the lowest (~57.9%). Differences across room classes are small.
- **Delhi led June 2022 occupancy** (~62.5%), and Bangalore was lowest (~56.4%).
- **Mumbai generates the most revenue** by a wide margin among the four cities.
- **Atliq Exotica is the top-earning hotel brand** by realized revenue (~₹320M), while **Atliq Seasons is the lowest** (~₹66M).
- **Delhi has the highest average customer rating** (3.78), and Bangalore the lowest (3.41).
- Monthly revenue realized stayed fairly stable across May, June, and July 2022 (≈ ₹554M – ₹582M).

---

## 🛠️ Pandas Skills Demonstrated

| Category | Functions / Techniques |
|---|---|
| **Loading & inspection** | `read_csv`, `head`, `shape`, `info`, `describe`, `unique`, `value_counts` |
| **Filtering & selection** | Boolean masking, `loc`, `idxmax` |
| **Cleaning** | `isnull().sum()`, `isna`, `fillna`, `drop`, outlier removal (3σ rule) |
| **Transformation** | Derived columns, `apply` with lambda, `round`, `to_datetime` |
| **Combining data** | `merge` (inner join), `concat` |
| **Aggregation** | `groupby` with `sum`, `mean`, `sort_values` |
| **Visualization** | Bar, horizontal bar, and pie charts via `.plot()` |

---

## 📁 Repository Structure

```
├── Atliq_hotel_EDA.ipynb     # Main analysis notebook
├── datasets/                 # Source CSV files (see Dataset Overview)
│   ├── fact_bookings.csv
│   ├── fact_aggregated_bookings.csv
│   ├── dim_hotels.csv
│   ├── dim_rooms.csv
│   ├── dim_date.csv
│   └── new_data_august.csv
└── README.md
```

---

## 🚀 How to Run

1. **Clone the repository**
   ```bash
   git clone https://github.com/<your-username>/<your-repo-name>.git
   cd <your-repo-name>
   ```

2. **Install dependencies**
   ```bash
   pip install pandas numpy matplotlib jupyter
   ```

3. **Launch the notebook**
   ```bash
   jupyter notebook Atliq_hotel_EDA.ipynb
   ```

Make sure the `datasets/` folder sits next to the notebook, since the file paths are relative.

---

## 🔭 Possible Next Steps

- Rebuild the revenue analysis on the fully cleaned bookings table for consistency with the cleaning steps
- Add cancellation and no-show rate analysis by platform and city
- Build an interactive dashboard (Power BI, Tableau, or Streamlit) on top of the merged dataset
- Extend the visualizations with Seaborn or Plotly, including time-series trends

---

## 👤 Author

**<Your Name>**
📧 <your-email> · 💼 [LinkedIn](https://linkedin.com/in/<your-profile>) · 🐙 [GitHub](https://github.com/<your-username>)

*Feedback and suggestions are welcome. Feel free to open an issue or reach out.*
