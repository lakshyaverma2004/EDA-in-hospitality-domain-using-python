<!-- ================= HERO ================= -->

<h1 align="center">🏨 Exploratory Data Analysis — Hospitality Domain</h1>

<p align="center">
  <i>End-to-end analysis of hotel booking data using Python & pandas</i>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Python-EDA-blue?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/Library-pandas-black?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/Visualization-matplotlib-success?style=for-the-badge"/>
</p>

<br>

<!-- ================= INTRO ================= -->

<div align="center" style="background: linear-gradient(135deg,#0f172a,#1e293b); color:white; padding:28px; border-radius:16px; width:85%;">

📊 A complete exploratory data analysis project on hotel booking data
covering ingestion, cleaning, transformation, and insight generation

<br><br>

⚡ Built using Python and pandas to uncover real-world business patterns

</div>

---

<!-- ================= DATASET ================= -->

## 📁 Dataset

<p>The project uses <b>5 CSV files</b> organized in a star schema:</p>

<div style="background:#f8fafc; padding:18px; border-radius:12px; border:1px solid #e5e7eb;">

<table>
<tr>
<th>File</th>
<th>Type</th>
<th>Description</th>
</tr>

<tr>
<td><code>fact_bookings.csv</code></td>
<td>Fact</td>
<td>Individual booking transactions</td>
</tr>

<tr>
<td><code>fact_aggregated_bookings.csv</code></td>
<td>Fact</td>
<td>Daily aggregated bookings per property/room</td>
</tr>

<tr>
<td><code>dim_hotels.csv</code></td>
<td>Dimension</td>
<td>Hotel metadata (name, city, category)</td>
</tr>

<tr>
<td><code>dim_rooms.csv</code></td>
<td>Dimension</td>
<td>Room type mapping (RT1–RT4 → Standard, Elite, etc.)</td>
</tr>

<tr>
<td><code>dim_date.csv</code></td>
<td>Dimension</td>
<td>Date table with week/month/day-type info</td>
</tr>

</table>

</div>

---

<!-- ================= STRUCTURE ================= -->

## 🔍 Project Structure

<div style="background:#f1f5f9; padding:18px; border-radius:12px; border:1px solid #e2e8f0;">

<pre>
├── datasets/
│   ├── fact_bookings.csv
│   ├── fact_aggregated_bookings.csv
│   ├── dim_hotels.csv
│   ├── dim_rooms.csv
│   ├── dim_date.csv
│   └── new_data_august.csv
└── eda_hospitality_domain.ipynb
</pre>

</div>

---

<!-- ================= NOTEBOOK ================= -->

## 🧱 Notebook Walkthrough

### 1. Data Exploration

* Loaded all 5 datasets into pandas DataFrames
* Examined shapes, column types, and unique values
* Visualized booking platform distribution and hotel city spread

---

### 2. Data Cleaning

* <b>Invalid guests</b>: Removed records where <code>no_guests <= 0</code>
* <b>Revenue outliers</b>: Applied the mean ± 3σ rule to filter extreme values in <code>revenue_generated</code>
* <b>RT4 room analysis</b>: Validated that high <code>revenue_realized</code> values for presidential suites were not outliers
* <b>Null handling</b>: Filled missing <code>capacity</code> values with median; retained null ratings
* <b>Booking integrity</b>: Removed rows where <code>successful_bookings > capacity</code>

---

### 3. Data Transformation

* Derived <code>occ_pct</code> = <code>successful_bookings / capacity × 100</code>
* Merged fact and dimension tables for enriched analysis
* Appended new August data using <code>pd.concat</code>
* Converted date columns to <code>datetime</code>

---

### 4. Insights Generated

<div style="background:#f8fafc; padding:15px; border-radius:12px;">

<table>
<tr>
<th>#</th>
<th>Question</th>
<th>Method</th>
</tr>

<tr><td>1</td><td>Average occupancy rate per room category</td><td><code>groupby</code> + merge with dim_rooms</td></tr>
<tr><td>2</td><td>Average occupancy rate per city</td><td><code>groupby</code> after merging hotels</td></tr>
<tr><td>3</td><td>Weekday vs. weekend occupancy</td><td><code>groupby("day_type")</code></td></tr>
<tr><td>4</td><td>City-wise occupancy in June 2022</td><td>Filter + <code>groupby</code> + bar chart</td></tr>
<tr><td>5</td><td>Append August data</td><td><code>pd.concat</code></td></tr>
<tr><td>6</td><td>Revenue realized per city</td><td>Merge + <code>groupby</code></td></tr>
<tr><td>7</td><td>Month-by-month revenue trend</td><td>Merge + <code>groupby("mmm yy")</code></td></tr>
<tr><td>8</td><td>Revenue per hotel/property</td><td><code>groupby("property_name")</code></td></tr>
<tr><td>9</td><td>Average guest rating per city</td><td><code>groupby("city")</code></td></tr>
<tr><td>10</td><td>Revenue by booking platform</td><td>Pie chart via <code>groupby</code></td></tr>

</table>

</div>

---

<!-- ================= STACK ================= -->

## 🛠️ Tech Stack

* <b>Python 3</b>
* <b>pandas</b> — data manipulation and analysis
* <b>matplotlib</b> — visualizations (bar charts, pie charts)

---

<!-- ================= SETUP ================= -->

## 🚀 Getting Started

<div style="background:#f8fafc; padding:18px; border-radius:12px; border:1px solid #e5e7eb;">

<pre>
# Clone the repo
git clone https://github.com/your-username/eda-hospitality-domain.git
cd eda-hospitality-domain

# Install dependencies
pip install pandas matplotlib jupyter

# Launch the notebook
jupyter notebook eda_hospitality_domain.ipynb
</pre>

</div>

<p align="center">
📌 Ensure all CSV files are placed inside the <b>datasets/</b> folder before execution
</p>

---

<!-- ================= TAKEAWAYS ================= -->

## 💡 Key Takeaways

<div align="center" style="background:linear-gradient(90deg,#111827,#374151); color:white; padding:24px; border-radius:14px; width:85%;">

🏨 Presidential suites (RT4) generate high revenue without being statistical outliers

📅 Weekend occupancy consistently exceeds weekday occupancy

🌍 Certain cities outperform others in both revenue and occupancy

⭐ ~58% of bookings lack ratings, limiting reliability of rating-based insights

</div>

---

<!-- ================= FOOTER ================= -->

<div align="center" style="margin-top:25px;">

⭐ If you found this useful, consider giving it a star

<br><br>

⚡ Data processed… patterns discovered… insights delivered

<br><br>

🧟‍♂️ Raw data cleaned back to life
🧟‍♀️ Noise filtered… meaning extracted
🧟 Insights never die… they evolve

</div>
