# NSL-KDD Dataset

## Abstract

NSL-KDD is a dataset suggested to solve some of the inherent problems of the KDD'99 dataset, which are discussed in Tavallaee et al. [1]. Although this version of the KDD dataset still suffers from some of the issues raised by McHugh [2] and may not fully represent existing real-world networks, the lack of public datasets for network-based Intrusion Detection Systems (IDS) makes it an effective benchmark dataset for comparing different intrusion detection methods.

Additionally, the number of records in the NSL-KDD train and test sets is reasonable. This efficiency allows researchers to run experiments on the complete dataset without needing to randomly sample small portions, ensuring consistent and directly comparable evaluation results across different research efforts.

---

## Data Files

| File Name | Description |
| --- | --- |
| `KDDTrain+.ARFF` | The full NSL-KDD train set with binary labels in ARFF format |
| `KDDTrain+.TXT` | The full NSL-KDD train set including attack-type labels and difficulty level in CSV format |
| `KDDTrain+_20Percent.ARFF` | A 20% subset of the `KDDTrain+.ARFF` file |
| `KDDTrain+_20Percent.TXT` | A 20% subset of the `KDDTrain+.TXT` file |
| `KDDTest+.ARFF` | The full NSL-KDD test set with binary labels in ARFF format |
| `KDDTest+.TXT` | The full NSL-KDD test set including attack-type labels and difficulty level in CSV format |
| `KDDTest-21.ARFF` | A subset of the `KDDTest+.ARFF` file which excludes records with a difficulty level of 21 out of 21 |
| `KDDTest-21.TXT` | A subset of the `KDDTest+.TXT` file which excludes records with a difficulty level of 21 out of 21 |

---

## Improvements Over the KDD'99 Dataset

The NSL-KDD dataset introduces several key improvements over the original KDD'99 dataset:

* **Elimination of Redundant Training Records:** The training set contains no redundant records, preventing classifiers from becoming biased toward frequently occurring patterns.
* **Elimination of Duplicate Test Records:** Test sets do not contain duplicate entries, ensuring evaluation metrics are not skewed by algorithms that perform disproportionately well on frequent records.
* **Balanced Difficulty Selection:** The proportion of selected records from each difficulty level group is inversely proportional to their percentage in the original KDD dataset. This spreads classification performance across a broader range, enabling more accurate differentiation between learning techniques.
* **Manageable Dataset Size:** The total record counts in both training and test sets are computationally affordable for full-set experiments, eliminating the need for random sub-sampling and standardizing research benchmarks.

---

## Statistical Observations

### Redundant Record Statistics

One of the primary deficiencies of the original KDD dataset is the vast volume of duplicate records. These force learning algorithms to favor frequent patterns while neglecting infrequent, high-severity attacks such as User to Root (U2R) and Remote to Local (R2L). Furthermore, test set duplicates distort performance evaluations.

#### KDD Train Set Redundancy

| Record Type | Original Records | Distinct Records | Reduction Rate |
| --- | --- | --- | --- |
| **Attacks** | 3,925,650 | 262,178 | 93.32% |
| **Normal** | 972,781 | 812,814 | 16.44% |
| **Total** | **4,898,431** | **1,074,992** | **78.05%** |

#### KDD Test Set Redundancy

| Record Type | Original Records | Distinct Records | Reduction Rate |
| --- | --- | --- | --- |
| **Attacks** | 250,436 | 29,378 | 88.26% |
| **Normal** | 60,591 | 47,911 | 20.92% |
| **Total** | **311,027** | **77,289** | **75.15%** |

---

### Record Difficulty Analysis

An analysis of record difficulty revealed that approximately **98% of training set records** and **86% of test set records** were correctly classified across all 21 evaluated learners.

#### Methodology

1. **Subset Creation:** Three random subsets of 50,000 records each were sampled from the KDD train set.
2. **Model Training:** Seven distinct machine learning algorithms were each trained on the three subsets, yielding 21 trained classifiers ($7 \text{ learners} \times 3 \text{ runs}$).
3. **Evaluation & Scoring:** All 21 classifiers predicted labels for every record in the full KDD train and test sets.
4. **`#successfulPrediction` Metric:** Each record was annotated with a score ranging from `0` to `21`, corresponding to the number of learners that correctly identified its label. A score of `21` indicates that every trained classifier correctly predicted the record.

---

## References

1. M. Tavallaee, E. Bagheri, W. Lu, and A. Ghorbani, "A Detailed Analysis of the KDD CUP 99 Data Set," *Submitted to Second IEEE Symposium on Computational Intelligence for Security and Defense Applications (CISDA)*, 2009.
2. J. McHugh, "Testing intrusion detection systems: a critique of the 1998 and 1999 DARPA intrusion detection system evaluations as performed by Lincoln Laboratory," *ACM Transactions on Information and System Security*, vol. 3, no. 4, pp. 262–294, 2000.
