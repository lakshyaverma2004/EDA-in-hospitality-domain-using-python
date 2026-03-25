# 🏨 Exploratory Data Analysis — Hospitality Domain

A end-to-end EDA project on hotel booking data, covering data ingestion, cleaning, transformation, and insight generation using Python and pandas.

---

## 📁 Dataset

The project uses 5 CSV files organized as a star schema:

| File | Type | Description |
|---|---|---|
| `fact_bookings.csv` | Fact | Individual booking transactions |
| `fact_aggregated_bookings.csv` | Fact | Daily aggregated bookings per property/room |
| `dim_hotels.csv` | Dimension | Hotel metadata (name, city, category) |
| `dim_rooms.csv` | Dimension | Room type mapping (RT1–RT4 → Standard, Elite, etc.) |
| `dim_date.csv` | Dimension | Date table with week/month/day-type info |

---

## 🔍 Project Structure

```
├── datasets/
│   ├── fact_bookings.csv
│   ├── fact_aggregated_bookings.csv
│   ├── dim_hotels.csv
│   ├── dim_rooms.csv
│   ├── dim_date.csv
│   └── new_data_august.csv
└── eda_hospitality_domain.ipynb
```

---

## 🧱 Notebook Walkthrough

### 1. Data Exploration
- Loaded all 5 datasets into pandas DataFrames
- Examined shapes, column types, and unique values
- Visualized booking platform distribution and hotel city spread

### 2. Data Cleaning
- **Invalid guests**: Removed records where `no_guests <= 0`
- **Revenue outliers**: Applied the mean ± 3σ rule to filter extreme values in `revenue_generated`
- **RT4 room analysis**: Validated that high `revenue_realized` values for presidential suites were not outliers
- **Null handling**: Filled missing `capacity` values in aggregated bookings with the column median; retained null ratings (too many to drop or impute meaningfully)
- **Booking integrity**: Removed rows where `successful_bookings > capacity`

### 3. Data Transformation
- Derived `occ_pct` (occupancy percentage) = `successful_bookings / capacity × 100`
- Merged fact and dimension tables to enrich data with city, room class, and date info
- Appended new August data using `pd.concat`
- Converted date columns to `datetime` for time-based analysis

### 4. Insights Generated

| # | Question | Method |
|---|---|---|
| 1 | Average occupancy rate per room category | `groupby` + merge with `dim_rooms` |
| 2 | Average occupancy rate per city | `groupby` after merging hotels |
| 3 | Weekday vs. weekend occupancy | `groupby("day_type")` |
| 4 | City-wise occupancy in June 2022 | Filter + `groupby` + bar chart |
| 5 | Append August data | `pd.concat` |
| 6 | Revenue realized per city | Merge bookings + hotels, `groupby` |
| 7 | Month-by-month revenue trend | Merge with date dim, `groupby("mmm yy")` |
| 8 | Revenue per hotel/property | `groupby("property_name")` |
| 9 | Average guest rating per city | `groupby("city")["ratings_given"].mean()` |
| 10 | Revenue by booking platform | Pie chart via `groupby` |

---

## 🛠️ Tech Stack

- **Python 3**
- **pandas** — data manipulation and analysis
- **matplotlib** — basic visualizations (bar charts, pie charts)

---

## 🚀 Getting Started

```bash
# Clone the repo
git clone https://github.com/your-username/eda-hospitality-domain.git
cd eda-hospitality-domain

# Install dependencies
pip install pandas matplotlib jupyter

# Launch the notebook
jupyter notebook eda_hospitality_domain.ipynb
```

> Make sure all CSV files are placed inside a `datasets/` folder at the project root before running.

---

## 💡 Key Takeaways

- Presidential suites (RT4) command significantly higher revenue but don't exhibit outlier behavior within their segment.
- Weekend occupancy is higher than weekday occupancy across properties.
- Certain cities consistently outperform others in both occupancy and revenue — useful signal for resource allocation.
- A meaningful fraction of bookings (~58%) lack guest ratings, making rating-based analysis less reliable without imputation strategies.
