# Customer Segmentation for Personalised Market Basket Analysis
An RFM-based K-Means and Apriori/FP-Growth pipeline applied to an e-commerce 
retail dataset, evaluating whether segmenting customers before running Market 
Basket Analysis reveals more informative purchasing patterns than analysing 
the full customer base as one group.

## Objectives

1. Clean and engineer Recency, Frequency, and Monetary (RFM) features for clustering.
2. Apply K-Means clustering to identify distinct customer segments, evaluated 
   through Silhouette score, Davies-Bouldin Index, Elbow method, and cluster profiling.
3. Interpret and label each segment based on its RFM behaviour.
4. Apply Apriori and FP-Growth to extract association rules within each segment.
5. Evaluate rule quality using support, confidence, and lift.
6. Compare segment-level rules against a full-dataset baseline to test whether 
   segmentation reveals patterns the aggregate view misses.

## Data Source

[Online Retail II](https://archive.ics.uci.edu/dataset/502/online+retail+ii) 
(UCI Machine Learning Repository) — real transactional data from a UK-based 
online retail company, 2009-2011. This project uses one year of data (2010-2011), 
~542,000 transaction records.

## Tools

Python 3.12, pandas, NumPy, scikit-learn (KMeans, MinMaxScaler, RobustScaler, 
silhouette_score, silhouette_samples, davies_bouldin_score), mlxtend (apriori, 
fpgrowth, association_rules, TransactionEncoder), matplotlib, seaborn.

## Techniques

- RFM feature engineering
- Outlier treatment: IQR removal and percentile trimming
- Feature scaling: MinMaxScaler vs. RobustScaler
- K-Means clustering with K-Means++ initialisation testing
- Multi-metric cluster evaluation (Silhouette, Davies-Bouldin, Elbow, cluster profiling)
- Manual cluster refinement
- Apriori & FP-Growth association rule mining
- Rule evaluation via support, confidence, and lift

## Pipeline

| Notebook | Description |
|---|---|
| `00_preparing_data.ipynb` | Data cleaning and RFM feature engineering |
| `01_clustering_application.ipynb` | Outlier treatment, scaling, and K-Means configuration comparison |
| `02_customer_segmentation.ipynb` | Manual refinement, cluster profiling, and segment naming |
| `03_market_basket_analysis.ipynb` | Apriori/FP-Growth per segment, association rule findings |

## Getting Started

**1. Clone the repo and install dependencies:**
```bash
git clone https://github.com/vinikcabral/Customer-Segmentation-Market-Basket-Analysis-PYTHON.git
cd Customer-Segmentation-Market-Basket-Analysis-PYTHON
pip install -r requirements.txt
```

**Requirements:** Python 3.12

**2. Decompress the datasets:**
The processed datasets are provided as `.zip` files in `datasets/` due to file size. Unzip them into 
the same folder before running the notebooks:
```bash
cd datasets
unzip 01_cleaned_data.zip
unzip 01_rfm_df.zip
unzip 02_clustered_customers.zip
unzip 02_customer_segments.zip
cd ..
```

**3. Download the raw dataset:**
Download the "Online Retail II" dataset from the 
[UCI Machine Learning Repository](https://archive.ics.uci.edu/dataset/502/online+retail+ii), 
and place the file in the `datasets/` folder.

**4. Run the notebooks in order:**
Run `code/00_preparing_data.ipynb` through `code/03_market_basket_analysis.ipynb` 
sequentially — each notebook reads the output of the one before it.

## Key Insights

- K-Means clustering identified **4 core segments** based on RFM behaviour; 
  manual refinement — reintegrating outlier customers and splitting out a 
  new-customer subgroup — expanded this into **6 final segments**: Champions, 
  VIP, Occasional, Inactive, Lost, and New, each with a clearly differentiated 
  RFM profile.
- **VIP and Champions**, despite representing the smallest customer base 
  combined, contribute disproportionately to overall revenue and order 
  frequency — a small group of customers driving a large share of the business.
- Segmenting before running Market Basket Analysis revealed **substantially 
  more association rules** than the full-dataset baseline (e.g. Champions: 
  994 rules vs. 162 in the aggregate dataset), with average lift across 
  segments ranging from 13.70 (Champions) to 43.80 (Lost) — confirming 
  genuine, non-random purchasing patterns.
- Each segment showed a **distinct product identity** — herb marker sets 
  dominate Inactive and Lost, wooden decoration sets are exclusive to VIP, 
  and party/celebration items define Champions — patterns invisible in the 
  full-dataset baseline, where Regency tableware and Poppy's Playhouse sets 
  dominate instead.

**Overall**, this study provides evidence that integrating customer 
segmentation with Market Basket Analysis offers a more granular and 
informative analytical approach than applying MBA to the full dataset alone 
— a methodological contribution to how e-commerce retailers could better 
understand customer purchasing behaviour.

## Full Report

See [Report.pdf](./Report.pdf) for the complete methodology, literature 
review, and results.

## Author

Vinicius Carrarini Cabral  
[LinkedIn](https://www.linkedin.com/in/viniciuscarrarini/) · [GitHub](https://github.com/vinikcabral)
