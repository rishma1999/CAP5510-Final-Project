
# **Gene Expression-Based Classification of Leukemia Using Machine Learning and Neural Network Methods**

## **CAP 5510 – Bioinformatics Project**

---

## **Team Members**

- **Priya Mittal (UFID: 98536535)**
- **Sai Harshitha Baskar (UFID: 49831986)**
- **Rishma Manna (UFID: 55360448)**
- **Hari Nair Suresh Chandran (UFID: 24745989)**

---

## **Project Overview**

This project explores the classification of leukemia subtypes (ALL vs AML) using the Golub gene expression dataset, which contains:

- **72 samples**
- **7,129 gene expression values per sample**
- A highly high-dimensional, small-sample challenge typical in bioinformatics

Our goal is to examine how feature selection and dimensionality reduction techniques impact classical ML models and neural network performance.

We implement:

- **Feature selection:** ANOVA, correlation-based selection  
- **Dimensionality reduction:** PCA  
- **Classical ML classifiers:** SVM, k-NN, Decision Trees  
- **Neural models:** Multilayer Perceptron (MLP), Committee Neural Networks  

We evaluate models on accuracy, F1-score, ROC-AUC, confusion matrices, and statistical tests, and observe how performance changes when reducing gene dimensionality.

---

## **Dataset Used**

### **Golub ALL/AML Dataset**

- Affymetrix microarray data  
- **72 samples, 7,129 genes**  
- Pre-labeled as **ALL or AML**  

Source: CMA Golub dataset – https://www.kaggle.com/datasets/crawford/gene-expression

---

## **Project Workflow**

### **1. Preprocessing**
The original data includes thousands of gene features and additional metadata, all non-expression fields were removed during preprocessing. The gene matrices were then aligned and transposed so that each row corresponds to a patient and each column to a gene. Following data cleaning and feature-ranking procedures, the dimensionality was reduced to the 50, 100 and 250 most informative genes, which were used as the final input set for model training and analysis.

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

From this ranked list, we extract the **Top 50, 100, 250 genes**, which form the final reduced feature set used for training ML classifiers.

## Visualization

The bar chart below displays the combined importance score for the top 50 genes.
Higher bars indicate genes with stronger overall predictive value.

**Figure: Top 50 Most Informative Genes**

<img width="3570" height="1466" alt="top50_features" src="https://github.com/user-attachments/assets/ccc24d89-3233-4f92-92ef-2a7244cf68e0" />

## Why This Matters

* Reduces dimensionality from thousands of genes → 50, 100, 250 key biomarkers
* Improves model performance and generalization
* Removes noisy or redundant features
* Ensures selected genes are supported by multiple statistical perspectives

**This feature-selection pipeline forms a critical step in building robust leukemia-classification models.**

---

### **2. Feature Selection & Dimensionality Reduction**

**Techniques implemented:**

| **Method** | **Purpose** |
|-----------|-------------|
| **ANOVA** | Multi-class variance-based selection |
| **Correlation-based** | Remove redundant genes |
| **PCA** | Reduce dimensionality while preserving variance |

We evaluate top **50, 100, 250 genes** as subsets.

---

### **3. Classification Models**

#### **Classical ML Models**
- Support Vector Machines (SVM)  
- k-Nearest Neighbors (k-NN)  
- Decision Trees  

#### **Neural Network Models**
- Multilayer Perceptron (MLP)  
- Committee Neural Networks (Majority voting ensemble)  

---

## **Experiments Conducted**

### **A. Full vs Reduced Gene Sets**

We compare models trained on:
- Full 7,129-gene dataset  
- Selected subsets of **50, 100, 250** top genes  

### **B. Performance Metrics**

- Accuracy  
- F1-score  
- ROC-AUC  
- Confusion matrix analysis  
- p-values for statistical testing  

### **C. Overfitting Behavior**

We analyze:
- How accuracy changes with gene selection  
- Whether dimensionality reduction reduces overfitting  
- Model sensitivity to sample size  

---

## **Results Summary**

### **Key Observations**

- Dimensionality reduction improved stability and reduced overfitting across most models.  
- SVM performed best among classical ML models on reduced feature sets.  
- MLP and Committee Neural Networks benefited significantly from moderate dimensionality reduction (top 100–250 genes).  
- PCA sometimes reduced interpretability but provided strong performance for neural networks.  
- Statistical validation (p-values) confirmed significance of differences between model configurations.  

---

## **Workload Distribution**

| **Team Member** | **Responsibilities** |
|-----------------|-----------------------|
| **Priya** | Preprocessing, statistical feature selection (ANOVA, PCA, Pearson Correlation), dataset preparation |
| **Harshitha** | Neural models (MLP, Committee NN), hyperparameter tuning |
| **Rishma** | Classical ML models (SVM, k-NN, Decision Trees), performance comparisons |
| **Hari** | Cross-validation, statistical testing, results visualization, documentation |

---

## **References**

- Golub et al. *Molecular Classification of Cancer Using Gene Expression Monitoring.*  
- Sevak et al. *Gene Expression-Based Leukemia Sub-Classification Using Committee Neural Networks.*  
- Toure & Basu. *Application of Neural Networks to Gene Expression Data for Cancer Classification.*  
- Cho. *Exploring Features and Classifiers to Classify Gene Expression Profiles of Acute Leukemia.*  
- Fathi et al. *Efficient Cancer Classification Model Using Microarray and High-Dimensional Data.*


