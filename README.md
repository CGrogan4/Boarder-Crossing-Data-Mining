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
---
<img width="854" height="398" alt="image" src="https://github.com/user-attachments/assets/9ca43a41-cf49-4b38-9faa-4736ea7acb73" />

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
The raw data file is too large for GitHub. The notebooks load data directly
from the BTS public API — no manual download needed.

**API endpoint used in this project:**
`https://data.bts.gov/resource/keg4-3bc2.csv?$limit=100000`
This returns all available records with no date range filter. If the API
changes its default response window, use the `$limit=100000` parameter
above to ensure the full dataset is retrieved.
