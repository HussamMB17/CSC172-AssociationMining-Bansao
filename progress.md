# CSC172 Association Mining Project Progress Report
**Student:** JJ Montemayor, [Your ID]
**Date:** December 16, 2025
**Repository:** [https://github.com/jjmmontemayor/CSC172-AssociationMining-Montemayor](https://github.com/jjmmontemayor/CSC172-AssociationMining-Montemayor)


## 📊 Current Status
| Milestone | Status | Notes |
|-----------|--------|-------|
| Dataset Preparation | ✅ Completed | 4,920 transactions cleaned & encoded |
| Initial Mining | ✅ Completed | Apriori algorithm execution successful |
| Rule Evaluation | ✅ In Progress | Filtering rules by Lift metric |
| Visualization | ⏳ Pending | Generating Network Graph for final report |

## 1. Dataset Progress
- **Total Transactions:** 4,920 Patient Records
- **Matrix Dimensions:** 4,920 rows × 132 columns (Symptoms)
- **Items/Symptoms:** 132 unique items (e.g., "chills", "vomiting", "fatigue")
- **Preprocessing applied:** String standardization (removed underscores), List transformation, One-Hot Encoding (`TransactionEncoder`).

**Sample data preview:**
> *Note: Screenshot of the dataframe head (df.head())*
![Dataset Sample](results/dataset_preview.png)

## 2. Mining Progress

**Visualizations (so far)**
> *Scatterplot of Support vs. Confidence*
![Support vs Confidence](results/visualization.png)

**Current Metrics:**
| Metric | Value | Meaning |
|--------|-------|---------|
| Min Support | 0.01 | Items must appear in >1% of cases |
| Min Confidence | 0.50 | Rules must be true >50% of the time |
| Avg Lift | 2.4 | Strong positive correlation detected |
| Total Rules Found | 42 | (After filtering for Lift > 1.2) |

## 3. Challenges Encountered & Solutions
| Issue | Status | Resolution |
|-------|--------|------------|
| Generic Symptoms | ✅ Fixed | Symptoms like "Fatigue" appeared in every rule. Increased `min_lift` threshold to 1.2 to filter noise. |
| Redundant Rules | ✅ Fixed | Removed duplicate inverse rules (If A->B, ignore B->A). |
| Data Formatting | ✅ Fixed | Raw CSV was in "Wide" format; wrote a script to melt it into Transactional format. |

## 4. Next Steps (Before Final Submission)
- [ ] Finalize the Network Graph visualization (Symptom Clusters).
- [ ] Export final `rules.csv` for the repository.
- [ ] Write interpretation of the top 3 strongest rules in `README.md`.
- [ ] Record 5-min demo video.