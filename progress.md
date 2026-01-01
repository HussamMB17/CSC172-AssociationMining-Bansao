# CSC172 Association Mining Project Progress Report
**Student:** Hussam M. Bansao, 2022-0484
**Date:** December 17, 2025
**Repository:** [https://github.com/HussamMB17/CSC172-AssociationMining-Bansao](https://github.com/HussamMB17/CSC172-AssociationMining-Bansao)

## 📊 Current Status
| Milestone | Status | Notes |
|-----------|--------|-------|
| Dataset Preparation | ✅ Completed | 4,920 transactions cleaned & encoded |
| Initial Mining | ✅ Completed | Apriori algorithm execution successful |
| Rule Evaluation | ✅ Completed | Filtering rules by Lift metric |
| Visualization | ✅ Completed | Network Graph generated |

## 1. Dataset Progress
- **Total Transactions:** 4,920 Patient Records
- **Items/Symptoms:** 132 unique items (e.g., "chills", "vomiting", "fatigue")
- **Preprocessing applied:** String standardization (removed underscores), List transformation, One-Hot Encoding (`TransactionEncoder`).

**Sample data preview:**
> *See `results/dataset_preview.png` in the repo.*

## 2. Mining Progress
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

## 4. Next Steps (Final Submission)
- [x] Finalize the Network Graph visualization.
- [ ] Record 5-min demo video (Due Dec 19).