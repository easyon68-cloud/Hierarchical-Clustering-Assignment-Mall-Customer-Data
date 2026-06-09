# 🛍️ Hierarchical Clustering — Mall Customer Segmentation

> **Unsupervised Machine Learning | Customer Segmentation | EDA + Clustering Pipeline**

---

## 📌 Project Overview

This project applies **Hierarchical Clustering** to segment mall customers based on their **Annual Income** and **Spending Score**. The goal is to identify distinct customer groups that can help a retail business tailor its marketing strategies, promotions, and services to specific audience segments.

The analysis follows a complete end-to-end machine learning workflow: from raw data exploration and visualization through feature engineering, dendrogram analysis, cluster validation, and final business-ready segmentation.

---

## 📂 Dataset

| Property        | Detail                                |
|-----------------|---------------------------------------|
| **File**        | `Mall_Customers.csv`                  |
| **Rows**        | 200 customers                         |
| **Columns**     | 5 features                            |
| **Source**      | Kaggle — Mall Customer Segmentation   |

### Features

| Column                    | Description                                      |
|---------------------------|--------------------------------------------------|
| `CustomerID`              | Unique identifier for each customer              |
| `Gender`                  | Customer gender (Male / Female)                  |
| `Age`                     | Customer age in years                            |
| `Annual Income (k$)`      | Annual income in thousands of dollars            |
| `Spending Score (1-100)`  | Score assigned by mall based on spending behavior|

---

## 🧪 Methodology

### Workflow Summary

```
Raw Data → EDA → Feature Selection → Scaling → Dendrogram → Silhouette Validation → Clustering → Analysis
```

### Steps

| Step | Description |
|------|-------------|
| **1** | Import libraries |
| **2** | Load dataset |
| **3** | Data understanding (shape, types, nulls) |
| **4** | Exploratory Data Analysis (EDA) |
| **5** | Feature selection & standard scaling |
| **6** | Dendrogram analysis (Ward, Complete, Average linkage) |
| **7** | Silhouette score validation to find optimal k |
| **8** | Apply Hierarchical Clustering (Ward, k=5) |
| **9** | Cluster profiling & visualization |
| **10** | Export results |

---

## 📊 Exploratory Data Analysis (EDA)

The EDA phase covers:

- **Distribution plots** — Histograms for Age, Annual Income, and Spending Score to understand data spread and skewness
- **Scatter plot** — Annual Income vs. Spending Score to visually detect natural groupings
- **Boxplots** — Outlier detection across all three numeric features
- **Gender bar chart** — Class balance check for Gender
- **Correlation heatmap** — Pearson correlations between Age, Annual Income, and Spending Score

### EDA Outputs

| File | Description |
|------|-------------|
| `eda_distributions.png` | Histograms of Age, Income, Spending Score |
| `eda_scatter.png` | Scatter plot — Income vs. Spending Score |
| `eda_boxplots.png` | Boxplots for outlier detection |
| `eda_gender.png` | Gender distribution bar chart |
| `eda_heatmap.png` | Feature correlation heatmap |

---

## ⚙️ Feature Engineering

Only **two features** were selected for clustering after EDA:

- `Annual Income (k$)`
- `Spending Score (1-100)`

**Reason:** The scatter plot of these two features clearly reveals five distinct natural clusters — making them the most informative variables for customer segmentation. Age shows less discriminative power in the scatter space.

**Standard Scaling** (`StandardScaler`) was applied to normalize both features to zero mean and unit variance, ensuring neither feature dominates due to scale differences.

```
Mean after scaling:  ≈ [0.0, 0.0]
Std after scaling:   ≈ [1.0, 1.0]
```

---

## 🌲 Dendrogram Analysis

Three linkage methods were evaluated visually via dendrograms:

| Linkage Method | Behavior |
|----------------|----------|
| **Ward**       | Minimizes within-cluster variance — produces compact, well-separated clusters ✅ |
| **Complete**   | Merges clusters based on maximum pairwise distance — tends toward equal-sized clusters |
| **Average**    | Uses mean pairwise distance — a balanced middle-ground approach |

**Selected Method: Ward Linkage**
The Ward dendrogram showed the clearest hierarchical structure with a natural cut at **5 clusters**.

---

## 📐 Optimal Cluster Selection — Silhouette Score

Silhouette scores were computed for k = 2 through 8 using Ward linkage labels:

| k (Clusters) | Silhouette Score |
|:------------:|:----------------:|
| 2            | moderate         |
| 3            | moderate         |
| 4            | good             |
| **5**        | **best ✅**       |
| 6            | lower            |
| 7            | lower            |
| 8            | lower            |

> **Conclusion:** k = 5 yields the highest silhouette score, confirming the visual observation from the dendrogram. This is the optimal number of customer segments.

---

## 🎯 Final Clustering Results

**Algorithm:** Hierarchical Clustering — Ward Linkage — 5 Clusters

### Cluster Profiles

| Cluster | Income Level | Spending Score | Profile Label |
|:-------:|:------------:|:--------------:|---------------|
| 1       | Low          | Low            | 💤 Budget-Conscious |
| 2       | Low          | High           | 🎯 Impulsive Spenders |
| 3       | Medium       | Medium         | 📊 Average Customers |
| 4       | High         | Low            | 💼 Conservative High-Earners |
| 5       | High         | High           | 🌟 Target VIP Customers |

> *Profile labels are derived from cluster mean values of Annual Income and Spending Score.*

### Output File

| File | Description |
|------|-------------|
| `mall_customers_with_clusters.csv` | Original dataset with `Cluster` column appended |
| `final_clusters.png` | Scatter plot of 5 color-coded clusters |
| `cluster_profiles.png` | Bar charts of average Age, Income, and Spending Score per cluster |

---

## 📁 Project Structure

```
📦 Hierarchical_Clustering_Mall_Customer_Segmentation/
├── 📓 Hierarchical_Clustering_Mall_Customer_Data.ipynb   ← Main notebook
├── 📄 Mall_Customers.csv                                 ← Raw dataset
├── 📄 mall_customers_with_clusters.csv                   ← Output with cluster labels
├── 🖼️ eda_distributions.png                              ← EDA: histograms
├── 🖼️ eda_scatter.png                                    ← EDA: income vs spending
├── 🖼️ eda_boxplots.png                                   ← EDA: boxplots
├── 🖼️ eda_gender.png                                     ← EDA: gender distribution
├── 🖼️ eda_heatmap.png                                    ← EDA: correlation heatmap
├── 🖼️ final_clusters.png                                 ← Final 5-cluster scatter plot
├── 🖼️ cluster_profiles.png                              ← Cluster feature bar charts
└── 📄 README.md                                          ← This file
```

---

## 🔧 Libraries & Requirements

```python
pandas          # Data loading and manipulation
numpy           # Numerical operations
matplotlib      # Plotting and visualization
seaborn         # Statistical visualizations (heatmap)
scipy           # Hierarchical clustering (linkage, dendrogram, fcluster)
sklearn         # StandardScaler, silhouette_score
```

### Install Dependencies

```bash
pip install pandas numpy matplotlib seaborn scipy scikit-learn
```

---

## 🚀 How to Run

1. Clone or download this repository
2. Place `Mall_Customers.csv` in the same directory (or update the file path in Step 2)
3. Open the notebook in **Google Colab** or **Jupyter Notebook**
4. Run all cells sequentially from top to bottom

> ⚠️ The dataset path in Step 2 uses a Google Drive path. Update it to your local path if running locally:
> ```python
> df = pd.read_csv('Mall_Customers.csv')
> ```

---

## 📈 Key Findings

- **5 distinct customer segments** were identified with high cluster cohesion (best silhouette score)
- **Ward linkage** outperformed Complete and Average linkage for this dataset
- **Annual Income and Spending Score** are the most informative features — Age had weaker discriminative power
- The **High Income / High Spending** cluster (Cluster 5) represents the most valuable customers for targeted marketing
- The **Low Income / High Spending** cluster (Cluster 2) represents impulsive buyers who may respond well to promotions

---

## 🤝 Business Applications

| Cluster Type | Recommended Strategy |
|---|---|
| VIP High-Earners & High-Spenders | Loyalty programs, exclusive offers, premium products |
| Conservative High-Earners | Quality-focused marketing, premium demonstrations |
| Impulsive Spenders | Flash sales, limited-time deals, trendy products |
| Budget-Conscious | Discount promotions, value bundles |
| Average Customers | Broad general campaigns, seasonal offers |

---

## 👤 Author

**Mall Customer Segmentation — Hierarchical Clustering Assignment**
Machine Learning | Unsupervised Learning | Customer Analytics

---

## 📜 License

This project is for academic and educational purposes.
