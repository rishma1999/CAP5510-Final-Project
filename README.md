# CAP5510-Final-Project
##  Gene Expression-Based Classification of Leukemia Using Machine Learning and Neural Network Methods

### Dataset and Preprocessing
To identify the most informative genes for distinguishing **ALL** and **AML** leukemia samples, we performed a multi-step feature-ranking procedure combining three independent statistical metrics. This approach ensures that the selected genes are consistently important across variance-based, correlation-based, and class-separation criteria.

## Feature Ranking Metrics Used

Each gene was evaluated using:

* **ANOVA F-Score**
  Quantifies how well each gene separates the two leukemia classes by comparing between-group and within-group variance.

* **Pearson Correlation Coefficient**
  Measures the strength of the linear relationship between each gene’s expression level and the binary class label.

* **PCA Loading Magnitude (PC1)**
  Represents how strongly each gene contributes to the primary direction of variance captured by PCA.

## Combined Ranking Strategy

Each metric produces its own ranking.
To avoid bias toward any single method, we compute a **combined rank**:

```
combined_rank = rank(ANOVA) + rank(Correlation) + rank(PCA Loading)
```

Genes with the **lowest combined score** are considered the most informative.

From this ranked list, we extract the **Top 40 genes**, which form the final reduced feature set used for training ML classifiers.

## Visualization

The bar chart below displays the combined importance score for the top 40 genes.
Higher bars indicate genes with stronger overall predictive value.

**Figure: Top 40 Most Informative Genes**

![Top 40 Ranked Genes](<img width="3570" height="1466" alt="top40_features (1)" src="https://github.com/user-attachments/assets/b0756e7b-377f-4921-aaa7-c1632f508194" />
)

## Why This Matters

* Reduces dimensionality from thousands of genes → 40 key biomarkers
* Improves model performance and generalization
* Removes noisy or redundant features
* Ensures selected genes are supported by multiple statistical perspectives

This feature-selection pipeline forms a critical step in building robust leukemia-classification models.
---

#### Team Members:

Priya Mittal

Sai Harshitha Baskar

Rishma Manna

Hari Nair Suresh Chandran

