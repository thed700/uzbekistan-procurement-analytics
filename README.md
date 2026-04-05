# 🏛️ Uzbekistan Public Procurement Analytics
### Vendor Risk Intelligence · Spend Optimization · Contract Clustering

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.10+-3776AB?style=for-the-badge&logo=python&logoColor=white"/>
  <img src="https://img.shields.io/badge/Jupyter-Notebook-F37626?style=for-the-badge&logo=jupyter&logoColor=white"/>
  <img src="https://img.shields.io/badge/scikit--learn-ML-F7931E?style=for-the-badge&logo=scikit-learn&logoColor=white"/>
  <img src="https://img.shields.io/badge/Seaborn-Visualization-4ECDC4?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/Status-Complete-00D4AA?style=for-the-badge"/>
</p>

---

## 📌 Project Overview

This project delivers a **full data science pipeline** applied to Uzbekistan's government procurement registry — specifically the **direct contracts register** of a public entity (STIR: 201122919) covering Q4 2025.

Government procurement is one of the most impactful yet underanalyzed data domains. This analysis transforms raw contract records into **actionable intelligence** for policymakers, auditors, and transparency researchers.

### 🎯 Business Questions Answered

| # | Question | Method |
|---|----------|--------|
| 1 | Where does public money go? | Category-level Pareto analysis |
| 2 | Is there vendor concentration risk? | HHI index + Lorenz curve |
| 3 | Are there seasonal spending patterns? | Temporal trend analysis |
| 4 | Can contracts be segmented by risk profile? | K-Means + PCA clustering |
| 5 | What actions should procurement managers take? | Data-driven recommendations |

---

## 📊 Dataset

| Attribute | Value |
|-----------|-------|
| **Source** | Uzbekistan E-Procurement Portal (`xarid.uzex.uz`) |
| **Type** | Direct Contracts Registry |
| **Period** | September 22 – December 24, 2025 |
| **Records** | 98 contracts |
| **Columns** | 13 original + 8 engineered features |
| **Entity** | Single government buyer (STIR: 201122919) |

### Key Fields
```
contract_value  →  Contract amount in UZS
category        →  Procurement category (18 unique)
funding_source  →  Budget / Off-Budget / Reserve
vendor_id       →  Supplier tax ID (STIR)
delivery_days   →  Contractual delivery deadline
contract_date   →  Contract signing date
```

---

## 🔬 Methodology

```
Raw Excel Data
      │
      ▼
1. Data Cleaning & Normalization
   ├── Language normalization (Uz/Ru → Uz)
   ├── Column aliasing (PEP 8 names)
   └── Type casting & validation
      │
      ▼
2. Feature Engineering (8 new features)
   ├── log_value          → Handles value skewness
   ├── contract_month     → Seasonality signal
   ├── is_fast_delivery   → Urgency binary flag
   ├── spend_tier         → Quartile-based bucket
   └── funding_eng        → English funding label
      │
      ▼
3. Exploratory Data Analysis
   ├── Distribution & outlier analysis
   ├── Category Pareto (80/20 spend)
   ├── Temporal trend (monthly/quarterly)
   ├── Vendor concentration (HHI index)
   └── Correlation matrix + multivariate plots
      │
      ▼
4. Machine Learning — K-Means Clustering
   ├── Feature standardization (StandardScaler)
   ├── Optimal K via Elbow + Silhouette methods
   ├── PCA dimensionality reduction (2D projection)
   └── Cluster profiling & business labeling
      │
      ▼
5. Business Recommendations (5 actionable insights)
```

---

## 📈 Key Findings

### 💰 Spend Concentration — CRITICAL
- **1 vendor** (`200903001`) accounts for **~89% of total spend** in Waste Disposal
- **HHI Score > 7,000** — classified as *Highly Concentrated Market*
- Top 3 vendors control **>95% of all spend**

### 🔍 Vendor Transparency Gap
- **11 contracts (11.2%)** have anonymous vendor ID (`X`)
- All in Suvenir category — medium risk for compliance

### 📅 End-of-Year Spending Rush
- November–December show **significant activity spike**
- Classic sign of annual budget consumption pressure

### 🤖 ML Clustering Results (K=7, Silhouette-optimized)
| Cluster | Profile | Dominant Category |
|---------|---------|------------------|
| 0 | High-value, known vendors | Waste Disposal |
| 1 | Low-value, fast delivery | Souvenirs |
| 2 | Medium-value, budget-funded | Hotel Services |
| 3 | Off-budget, rapid procurement | Catering |
| 4 | Micro contracts, anonymous vendors | Souvenirs |
| 5 | Utility contracts, long-term | Energy/Heating |
| 6 | Travel & transport cluster | Aviation |

---

## 💡 Strategic Recommendations

| Priority | Recommendation | Expected Impact |
|----------|---------------|-----------------|
| 🔴 HIGH | Mandate competitive bidding > 5M UZS | Cost savings 10-20% |
| 🟡 MED | Require STIR for all vendors | Compliance improvement |
| 🟢 MED | Quarterly budget smoothing | Reduce year-end rush |
| 🔵 MED | Cluster-based audit targeting | Audit efficiency +40% |
| 🟣 LOW | Consolidate Suvenir purchases | Admin cost reduction |

---

## 🖼️ Visualizations

| Figure | Description |
|--------|-------------|
| `fig_01_distribution.png` | Contract value distribution (raw + log + tier) |
| `fig_02_category_spend.png` | Pareto spend analysis by category |
| `fig_03_funding_temporal.png` | Funding structure + monthly trends |
| `fig_04_vendor_concentration.png` | Vendor HHI + Lorenz curve |
| `fig_05_correlation.png` | Correlation matrix + multivariate scatter |
| `fig_06_optimal_k.png` | Elbow method + Silhouette score |
| `fig_07_pca_clusters.png` | PCA 2D cluster visualization |
| `fig_08_cluster_dashboard.png` | Cluster profile comparison dashboard |

---

## 🛠️ Tech Stack

```
Language   : Python 3.10+
Notebook   : Jupyter Notebook
Data       : pandas 2.x · numpy 1.x
ML         : scikit-learn (KMeans, PCA, StandardScaler, silhouette_score)
Viz        : matplotlib · seaborn
File I/O   : openpyxl
```

---

## 🚀 How to Run

### Prerequisites
```bash
pip install pandas numpy matplotlib seaborn scikit-learn openpyxl jupyter nbformat
```

### Clone & Run
```bash
# 1. Clone the repository
git clone https://github.com/thed700/uzbekistan-procurement-analytics.git
cd uzbekistan-procurement-analytics

# 2. Place the dataset
mkdir data
# Copy procurement_data.xlsx into the data/ folder

# 3. Launch notebook
jupyter notebook uzbekistan_procurement_analytics.ipynb

# OR run all cells non-interactively
jupyter nbconvert --to notebook --execute uzbekistan_procurement_analytics.ipynb
```

### Project Structure
```
uzbekistan-procurement-analytics/
├── data/
│   └── procurement_data.xlsx        ← Input dataset
├── uzbekistan_procurement_analytics.ipynb  ← Main notebook
├── fig_01_distribution.png
├── fig_02_category_spend.png
├── fig_03_funding_temporal.png
├── fig_04_vendor_concentration.png
├── fig_05_correlation.png
├── fig_06_optimal_k.png
├── fig_07_pca_clusters.png
├── fig_08_cluster_dashboard.png
└── README.md
```

---

## 👤 Author

**Akmal Toshpulatov**  
Junior Data Analyst | Termiz, Uzbekistan  
🔗 GitHub: [thed700](https://github.com/thed700)

*Certifications: Kaggle Python · Pandas · Intro to SQL · Advanced SQL*

---

## 📜 License

This project is licensed under the MIT License.  
Dataset is sourced from Uzbekistan's public procurement portal and is publicly available.

---

> *"Data is the new oil — but only if you refine it."*  
> This project demonstrates that even small government datasets can yield strategic intelligence when analyzed rigorously.
