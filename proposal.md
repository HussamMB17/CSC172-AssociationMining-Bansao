# CSC172 Association Mining Project Proposal
**Student:** Hussam M. Bansao, 2022-0484
**Date:** December 12, 2025

## 1. Project Title
**MediMine: Symptom Association Analysis for Disease Prediction**

## 2. Problem Statement
In the Philippines, many individuals resort to self-medication or delay medical consultation due to a lack of immediate diagnostic information. This project addresses the challenge of preliminary medical screening by using data mining to identify statistically significant patterns between reported symptoms and diseases. By uncovering these hidden associations, we can create a rule-based logic to assist in early detection and validate common symptom clusters scientifically.

## 3. Objectives
- Develop and mine an Association Rule model using the Apriori algorithm to discover frequent symptom sets.
- Generate high-confidence "If-Then" rules (e.g., *{Symptom A, Symptom B} -> Disease X*) to assist in prediction.
- Implement a complete data mining pipeline including preprocessing of textual symptom data, one-hot encoding, and metric-based rule filtering (Lift/Confidence).

## 4. Dataset Plan
- **Source:** [Disease Symptom Prediction (Kaggle)](https://www.kaggle.com/datasets/karthikudyawar/disease-symptom-prediction)
- **Size:** 4,920 patient records (Exceeds the 500 records requirement).
- **Classes:** 41 unique diseases (e.g., Malaria, Dengue, Typhoid) and 132 unique symptoms.
- **Acquisition:** Direct download via Kaggle API or manual CSV upload to the repository.

## 5. Technical Approach
- **Architecture:** ETL Pipeline (Extract CSV -> Clean String Data -> TransactionEncoder -> Apriori Engine -> Visualization).
- **Model:** Association Rule Mining (Apriori Algorithm).
- **Framework:** Python (Pandas, NumPy, Mlxtend for mining, Seaborn/NetworkX for visualization).
- **Hardware:** Google Colab (Cloud CPU) or Local Python Environment.

## 6. Expected Challenges & Mitigations
- **Challenge:** High frequency of generic symptoms (e.g., "Fatigue", "Vomiting") creating noisy or obvious rules with low informational value.
- **Solution:** I will use the **Lift** metric (filtering for Lift > 1.2) rather than just Support to ensure the rules represent meaningful correlations, not just coincidences.