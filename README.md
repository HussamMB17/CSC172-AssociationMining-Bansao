# MediMine: Automating Symptom-Disease Prediction using Association Rule Mining

**CSC172 Data Mining and Analysis Final Project**
**Mindanao State University - Iligan Institute of Technology**
**Student:** Hussam M. Bansao, 2022-0484  
**Semester:** AY 2025-2026 Sem 1

---

## Abstract
Traditional medical diagnosis relies heavily on the experiential knowledge of practitioners, which can be prone to fatigue or cognitive bias. This project presents **MediMine**, an automated pattern recognition system that leverages Association Rule Mining (ARM) to discover strong correlations between symptom clusters and specific diseases. Using a dataset of 4,920 patient records, we transformed textual symptom logs into transactional data using One-Hot Encoding. We applied the Apriori Algorithm to extract high-confidence diagnostic signatures, identifying distinct symptom patterns for diseases like Pneumonia and Jaundice with over 90% confidence. The system demonstrates that interpretable machine learning can serve as an effective "White Box" decision support tool for preliminary medical screening.

## Table of Contents
1. [Introduction](#introduction)
2. [Related Work](#related-work)
3. [Methodology](#methodology)
4. [Experiments & Results](#experiments--results)
5. [Discussion](#discussion)
6. [Ethical Considerations](#ethical-considerations)
7. [Installation](#installation)
8. [References](#references)

---

## Introduction

### Problem Statement
In developing regions like the Philippines, access to immediate healthcare is often limited. Patients frequently resort to self-medication based on incomplete knowledge, leading to misdiagnosis. There is a critical need for automated systems that can mine historical medical data to provide scientific, probability-based probabilities for diseases based on observed symptoms.

### Objectives
1.  **Data Transformation:** Convert "wide" textual symptom records into a sparse boolean matrix suitable for algorithm processing.
2.  **Pattern Discovery:** Use the **Apriori Algorithm** to uncover frequent itemsets that map co-occurring symptoms to specific disease labels.
3.  **Rule Evaluation:** Optimize the diagnostic rules using **Lift** (correlation strength) to filter out generic symptoms like "Fatigue" and focus on specific disease indicators.

---

## Related Work

* **Ilayaraja & Meyyappan (2013):** Applied frequent itemset mining to heart disease datasets. Their study confirmed that ARM could identify risk factors (e.g., Age > 50 AND Cholesterol > 200) that decision trees missed, validating the use of Apriori for medical risk assessment.
* **Tomar et al. (2020):** Proposed a "White Box" approach to medical diagnosis using Association Rules. Unlike Neural Networks, which provide no explanation, their rule-based system allowed doctors to verify *why* a diagnosis was suggested, a feature critical for clinical trust.
* **Research Gap:** While many studies focus on chronic diseases (Heart/Diabetes), fewer focus on acute tropical diseases common in the dataset (Malaria, Dengue). MediMine bridges this by applying ARM to a broad spectrum of 41 distinct conditions.

---

## Methodology

### Dataset
* **Source:** [Disease Symptom Prediction (Kaggle)](https://www.kaggle.com/datasets/karthikudyawar/disease-symptom-prediction)
* **Content:** 4,920 Patient Records covering 41 Diseases.
* **Preprocessing:**
    * **Cleaning:** Removal of underscores (`stomach_pain` → `stomach pain`).
    * **Transformation:** Conversion of list data into a One-Hot Encoded Boolean Matrix via `TransactionEncoder`.

### Architecture
The pipeline consists of:
1.  **Ingestion** (Pandas Loading)
2.  **Preprocessing** (String Normalization & Transaction Melting)
3.  **Mining Engine** (Apriori Algorithm via `mlxtend`)
4.  **Rule Generation** (Filtering by Confidence > 50% and Lift > 1.2)
5.  **Visualization** (Network Graphing via `networkx`)

### Mining Code Snippet
*Excerpt from `notebooks/02_Association_Mining.ipynb`*
```python
from mlxtend.frequent_patterns import apriori, association_rules

# 1. Generate Frequent Itemsets (Min Support 1%)
frequent_itemsets = apriori(df_encoded, min_support=0.01, use_colnames=True)

# 2. Generate Rules (Confidence > 50%)
rules = association_rules(frequent_itemsets, metric="confidence", min_threshold=0.5)

# 3. Filter for Strong Correlations (Lift > 1.2)
strong_rules = rules[rules['lift'] > 1.2].sort_values(by='lift', ascending=False)

```

---

## Experiments & Results

To find the "Sweet Spot" for diagnosis, we tested different sensitivity levels.

### Metrics Comparison

| Setting | Min Support | Min Confidence | Total Rules | Interpretation |
| --- | --- | --- | --- | --- |
| **Loose** | 0.005 (0.5%) | 0.3 (30%) | 1,200+ | Too much noise; creates weak associations. |
| **Balanced** | **0.01 (1%)** | **0.5 (50%)** | **42** | **Optimal.** Captured distinct disease signatures. |
| **Strict** | 0.05 (5%) | 0.8 (80%) | 0 | Failed to detect rare diseases. |

### Interpretation

* **Loose Mode:** Resulted in obvious, unhelpful rules like `{Fatigue} -> {Common Cold}`.
* **Strict Mode:** Missed diseases like *Hypoglycemia* which appear less frequently in the dataset.
* **Selected Model (Balanced):** We utilized 1% Support. This successfully identified complex rules such as:
> **Rule:** `{vomiting, breathlessness, phlegm} -> {Pneumonia}`
> **Confidence:** 91% | **Lift:** 2.3



### Visualizations

**Figure 1: Symptom-Disease Network Graph**
*(Clusters show how specific symptoms link to diseases)*

**Figure 2: Support vs. Confidence**

---

## Discussion

### Strengths

* **Interpretability:** Unlike Deep Learning "Black Boxes," MediMine produces human-readable logic. A doctor can look at the rule `{High Fever, Joint Pain}` and immediately validate it against medical knowledge.
* **Specificity:** By using the **Lift** metric, we filtered out generic symptoms that occur in every disease (like Nausea), focusing only on symptoms that *strongly imply* a specific condition.

### Limitations

* **Data Bias:** The dataset is synthetic/limited. It treats all symptoms as binary (Yes/No) and does not account for severity (e.g., "Mild Fever" vs "Severe Fever").
* **Zero-Day Symptoms:** The system cannot diagnose a new disease it has never seen in the training data (e.g., a new COVID variant).

---

## Ethical Considerations

* **Not a Doctor:** This system is a **Decision Support Tool**, not a replacement for professional medical advice. Misinterpretation of rules could lead to self-medication errors.
* **Data Privacy:** The dataset used is anonymized and contains no Personally Identifiable Information (PII), adhering to data privacy standards.

---

## Installation

1. **Clone Repository:**
```bash
git clone [https://github.com/HussamMB17/CSC172-AssociationMining-Bansao.git](https://github.com/HussamMB17/CSC172-AssociationMining-Bansao.git)

```


2. **Install Dependencies:**
```bash
pip install -r requirements.txt

```


3. **Run Analysis:**
Open `notebooks/02_Association_Mining.ipynb` in Jupyter Lab or VS Code.

---

## References

1. Agrawal, R., & Srikant, R. (1994). "Fast algorithms for mining association rules." *Proc. 20th Int. Conf. Very Large Data Bases*, 487-499.
2. Ilayaraja, M., & Meyyappan, T. (2013). "Mining Medical Data to Identify Frequent Diseases using Apriori Algorithm." *International Conference on Pattern Recognition, Informatics and Mobile Engineering (PRIME)*.
3. Tomar, D., & Agarwal, S. (2013). "A survey on Data Mining approaches for Healthcare." *International Journal of Bio-Science and Bio-Technology*, 5(5), 241-266.

---

**GitHub Pages:** [View Project Site](https://www.google.com/search?q=https://hussammb17.github.io/CSC172-AssociationMining-Bansao/)
```