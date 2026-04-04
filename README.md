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
| M1 — Project Proposal | Complete |
| M2 — EDA, Cleaning, and Clustering | Complete |
| M3 — Final Analysis and Report | Complete |

---

## Repository Structure
```
Boarder-Crossing-Data-Mining/
│
├── data/
│   └── cleaned/
│       ├── cleaned_border_crossing.csv   ← Cleaned dataset (49,993 rows)
│       └── port_clusters.csv             ← K-Means clustering results (111 ports)
│
├── notebooks/
│   ├── cleaning.ipynb          ← Data ingestion and cleaning
│   ├── explore.ipynb           ← Exploratory data analysis (5 visualizations)
│   ├── clustering.ipynb        ← K-Means clustering with silhouette scoring
│   └── data_finding.ipynb      ← M3 expansion: decision tree + anomaly detection
│
├── .gitignore
└── README.md
---
```


## Project Status

### 1. Prerequisites
Make sure you have the following installed:
- [Anaconda](https://www.anaconda.com/download) (includes Python, Jupyter, pandas)
- [VS Code](https://code.visualstudio.com/) with the Python and Jupyter extensions
- [Git](https://git-scm.com/)

### 2. Clone the Repository
```bash
git clone https://github.com/CGrogan4/Boarder-Crossing-Data-Mining.git
cd Boarder-Crossing-Data-Mining

### 3. Install Required Libraries
Open **Anaconda Prompt** and run:
```bash
conda install pandas numpy matplotlib seaborn scikit-learn openpyxl
```

### 4. Download the Data
The raw data file is too large for GitHub. The notebooks load data directly
from the BTS public API — no manual download needed.

If you prefer to download manually:
1. Visit the [BTS dataset page](https://data.bts.gov/Research-and-Statistics/Border-Crossing-Entry-Data/keg4-3bc2/about_data)
2. Click **Export → CSV**
3. Save to `data/raw/border_crossing.csv`

### 5. Run the Notebooks
Run in this order for full reproducibility:
1. `cleaning.ipynb` — produces `cleaned_border_crossing.csv`
2. `explore.ipynb` — EDA visualizations
3. `clustering.ipynb` — K-Means clustering and silhouette scoring
4. `data_finding.ipynb` — decision tree and anomaly detection

Each notebook can also be run standalone if the cleaned CSV is already present.

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
- Used elbow method to select k=4
- Identified four port tiers based on volume and border type

---

## M3 Summary — What Was Done

### Clustering Improvements
- Expanded feature set from 3 to 5 features
- Added `personal_vehicle_ratio` — proportion of personal vs commercial traffic per port
- Added `seasonality_variance` — std dev of monthly crossing totals per port
- Added silhouette scoring alongside elbow method to justify k=4 (silhouette score: 0.585)

### Updated Cluster Profiles
| Cluster | Label | Ports | Personal Ratio | Seas. Variance | Border |
|---|---|---|---|---|---|
| 0 | Small quiet US-Canada | 64 | 0.891 | 14,563 | 100% Canada |
| 1 | High-volume seasonal | 12 | 0.880 | 359,278 | 75% Mexico |
| 2 | Commercial US-Canada | 16 | 0.514 | 20,509 | 100% Canada |
| 3 | Steady US-Mexico commuter | 19 | 0.964 | 69,758 | 100% Mexico |

### Decision Tree (New)
- Trained on cluster labels as class labels — classification as interpretability
- Perfect cluster separation (accuracy 1.0) confirmed clusters are genuinely distinct
- Volume features scored zero importance — clusters are defined by traffic type
  and seasonality, not port size
- Key rule: Canada ports with personal ratio ≤ 0.68 are commercial freight ports (Cluster 2)

### Anomaly Detection — LOF (New)
- Applied density-based Local Outlier Factor (LOF) to flag behavioral outliers
- 6 ports flagged out of 111 total (5.4%)
- **San Ysidro** — extreme on all features, confirmed category of its own
- **Blaine, WA** — Canada port that behaves like a high-volume Mexico port
- **Detroit, MI** — uniquely combines commercial freight and seasonal tourism
- **Champlain Rouses Point, Kenneth G Ward, Sault Sainte Marie** — sit at cluster boundaries

### Key Discoveries
1. Port volume has no bearing on behavioral cluster membership
2. 16 US-Canada ports form a hidden commercial freight cluster invisible in the M2 model
3. Seasonality variance threshold of 230,334 separates behavioral port types within Canada
4. Blaine, WA breaks the Canada/Mexico behavioral distinction
5. Detroit is the only port combining high seasonality variance and low personal ratio

---

## Discovery Questions
- **Q1:** How do border crossing volumes correlate with seasonal trade cycles over time?
- **Q2:** Are there identifiable shifts in trade flow between U.S.-Canada and
  U.S.-Mexico crossings over time?

See `data_finding.ipynb` and the M3 analysis document (PDF) for full findings.

---

## Data Source
**Bureau of Transportation Statistics — Border Crossing Entry Data**
- URL: https://data.bts.gov/resource/keg4-3bc2.csv
- Updated: Monthly
- License: U.S. Government Open Data (Public Domain)
