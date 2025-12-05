# CAP5510-Final-Project
##  Gene Expression-Based Classification of Leukemia Using Machine Learning and Neural Network Methods

### Dataset and Preprocessing
The dataset consists of microarray gene-expression profiles from 72 leukemia patients, split into 38 training samples and 34 independent test samples, labeled as either ALL (0) or AML (1). Each sample originally contains thousands of gene-expression measurements, along with metadata fields such as Gene Description, Gene Accession Number, and probe “call” values. During preprocessing, all non-expression metadata and “call” columns were removed, and the gene matrices were aligned and transposed so that each row represents a patient and each column represents a gene feature. After cleaning and feature ranking, the dataset was reduced to the top 40 most informative genes, which form the final feature set used for model training and evaluation.

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

<img width="3570" height="1466" alt="top40_features (1)" src="https://github.com/user-attachments/assets/74f07caa-9e51-4cf0-be92-ee847c6be6ee" />


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

