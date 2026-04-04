# Border Crossing Entry Data — Data Mining Project
**Dataset:** [U.S. Border Crossing Entry Data — BTS](https://data.bts.gov/Research-and-Statistics/Border-Crossing-Entry-Data/keg4-3bc2/about_data)

---

## Project Overview
This project performs end-to-end data mining on U.S. border crossing entry data
published by the Bureau of Transportation Statistics (BTS). The dataset contains
monthly records of crossings at ports along the US-Canada and US-Mexico borders,
including crossing type, volume, and geographic information.

---

## Project Status
| Milestone | Status |
|---|---|
| M1 — Project Proposal |
| M2 — EDA, Cleaning, and Clustering |
| M3 — Final Analysis and Report | In Progress |

---

## Repository Structure
```
Boarder-Crossing-Data-Mining/
│
├── data/                       ← Raw data (not uploaded, see download instructions)
│   └── cleaned/
│       ├── cleaned_border_crossing.csv   ← Cleaned dataset (49,993 rows)
│       └── port_clusters.csv             ← K-Means clustering results
│
├── notebooks/
│   ├── final_analysis.ipynb        ← Main notebook (runnable top to bottom)
│   ├── cleaning.ipynb              ← Standalone cleaning notebook
│   ├── eda.ipynb                   ← Standalone EDA notebook
│   └── clustering.ipynb            ← Standalone clustering notebook
│
├── .gitignore
└── README.md
```

---

## Setup Instructions

### 1. Prerequisites
Make sure you have the following installed:
- [Anaconda](https://www.anaconda.com/download) (includes Python, Jupyter, pandas)
- [VS Code](https://code.visualstudio.com/) with the Python and Jupyter extensions
- [Git](https://git-scm.com/)

### 2. Clone the Repository
```bash
git clone https://github.com/CGrogan4/Boarder-Crossing-Data-Mining.git
cd Boarder-Crossing-Data-Mining
```

### 3. Install Required Libraries
Open **Anaconda Prompt** and run:
```bash
conda install pandas numpy matplotlib seaborn scikit-learn openpyxl
```

### 4. Download the Data
The raw data file is too large for GitHub. The notebook loads it directly
from the BTS public API — no manual download needed.

If you prefer to download manually:
1. Visit the [BTS dataset page](https://data.bts.gov/Research-and-Statistics/Border-Crossing-Entry-Data/keg4-3bc2/about_data)
2. Click **Export → CSV**
3. Save to `data/raw/border_crossing.csv`

### 5. Run the Notebook
1. Open VS Code
2. Open the project folder
3. Navigate to `notebooks/final_analysis.ipynb`
4. Click **Run All** or press `Ctrl + Shift + P` → **Jupyter: Restart Kernel and Run All Cells**

---

## M2 Summary — What Was Done

### Data Cleaning
- Loaded 50,000 rows from the BTS API
- Dropped 7 rows with missing location data (latitude, longitude, point)
- Converted date column from string to datetime64
- Standardized text columns (whitespace, casing)
- Retained 4 zero-value rows as legitimate closed-port data
- **Final cleaned dataset: 49,993 rows, 0 missing values**

### Exploratory Data Analysis
Five visualizations were produced and interpreted:
1. **Crossings Over Time** — COVID-19 drop in 2020, recovery through 2022
2. **US-Canada vs US-Mexico** — US-Mexico sees 4x more crossings
3. **Crossings by Measure Type** — Personal vehicles dominate over commercial traffic
4. **Top 10 Busiest Ports** — San Ysidro leads by a large margin
5. **Seasonality** — July/August peak, February slowest

### Clustering (K-Means)
- Applied K-Means clustering to group ports by behavioral similarity
- Used elbow method to select optimal k=4
- Identified four distinct port tiers:

| Cluster | Label | # Ports | Description |
|---|---|---|---|
| 0 | Small/Quiet | 83 | Low volume, mostly rural US-Canada ports |
| 2 | Medium | 18 | Mid-volume, mixed border ports |
| 1 | Large | 9 | High volume US-Mexico ports |
| 3 | Unique | 1 | San Ysidro alone |

---

## M3 Plan
- Validate clustering with silhouette score and deeper cluster profiling
- Explore time series forecasting on personal vehicle crossings
- Run border-specific analyses (US-Mexico vs US-Canada separately)
- Treat San Ysidro separately in any predictive modeling
- Produce final report and complete notebook

---

## Data Source
**Bureau of Transportation Statistics — Border Crossing Entry Data**  
- URL: https://data.bts.gov/resource/keg4-3bc2.csv  
- Updated: Monthly  
- License: U.S. Government Open Data (Public Domain)
