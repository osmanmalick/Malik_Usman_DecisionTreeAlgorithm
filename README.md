# Decision Tree Algorithms: ID3, C4.5, and CART

A Python/Jupyter Notebook project that implements and compares three Decision Tree algorithms—**ID3, C4.5, and CART**—using a diabetes prediction dataset. The notebook also includes Random Forest experiments and a scikit-learn baseline.

## Project Overview

The goal of this project is to understand how different decision tree algorithms select features, create splits, and classify records. The target variable is `diabetes` (0 = non-diabetic, 1 = diabetic).

The notebook contains:
- ID3 implemented from scratch using Entropy and Information Gain.
- C4.5 implemented from scratch using Gain Ratio, including numeric threshold splits.
- CART implemented from scratch using Gini impurity and binary splits.
- A scikit-learn Decision Tree baseline.
- Custom and scikit-learn Random Forest experiments.

## Algorithms

### 1. ID3 (Iterative Dichotomiser 3)
- Uses **Entropy** to measure impurity.
- Selects the feature with the highest **Information Gain**.
- Creates a branch for each value of the selected categorical feature.
- In this notebook, numeric columns are converted into categories using bins before ID3 training.

### 2. C4.5
- Uses **Gain Ratio** to select a split.
- Supports categorical features and numeric features through threshold-based binary splits.
- The implementation first filters candidate splits using average information gain, then selects the candidate with the highest gain ratio.
- Uses stopping conditions such as maximum depth and minimum samples.

### 3. CART (Classification and Regression Trees)
- This notebook implements CART for **classification**.
- Uses **Gini impurity** to evaluate splits.
- Produces binary splits for both numeric and categorical features.
- Uses maximum depth and minimum-sample stopping conditions.

## Dataset

The notebook reads a file named:

`diabetes_prediction_dataset.csv`

The dataset should be placed in the same directory as the notebook. The notebook uses fields including age, gender, BMI, hypertension, heart disease, smoking history, HbA1c level, blood glucose level, and the `diabetes` target.

For the from-scratch ID3, C4.5, and CART experiments, the notebook takes a stratified sample of **5,000 rows**, then uses an **80/20 train-test split** (4,000 training rows and 1,000 test rows). ID3 bins selected numeric features into categories; C4.5 and CART work with numeric thresholds.

> The dataset is not included in this repository by this README. Add the dataset only if you have permission to share it, and check its license and source requirements.

## Project Files

```text
decision-tree-algorithms/
├── Id3_c4.5_cart.ipynb
├── diabetes_prediction_dataset.csv   # add this dataset locally
├── requirements.txt
└── README.md
```

Your uploaded notebook currently has the filename `Id3_c4.5_cart.ipynb.ipynb`. You can keep that name or rename it to `Id3_c4.5_cart.ipynb`, then update this file tree to match.

## Requirements

The notebook uses:
- Python 3
- pandas
- NumPy
- scikit-learn
- Jupyter Notebook

Install the packages:

```bash
pip install pandas numpy scikit-learn jupyter
```

Or create a `requirements.txt` containing:

```text
pandas
numpy
scikit-learn
jupyter
```

## How to Run

1. Clone or download this repository.
2. Put `diabetes_prediction_dataset.csv` in the same folder as the notebook.
3. Install the required packages.
4. Start Jupyter:

   ```bash
   jupyter notebook
   ```

5. Open `Id3_c4.5_cart.ipynb` (or the notebook's actual filename).
6. Run the cells from top to bottom.

## Evaluation

The notebook evaluates models using:
- Training accuracy
- Test accuracy
- Confusion matrix
- Precision
- Recall
- F1-score / classification report
- Number of missed diabetic cases

### Recorded comparison from the notebook

The notebook's comparison cell reports the following results on its 1,000-row test set:

| Model | Train accuracy | Test accuracy | Precision (class 1) | Recall (class 1) | Missed diabetic cases |
|---|---:|---:|---:|---:|---:|
| ID3 | 97.50% | 94.60% | 0.804 | 0.482 | 44 |
| C4.5 | 97.48% | 96.10% | 1.000 | 0.541 | 39 |
| CART | 97.50% | 96.10% | 1.000 | 0.541 | 39 |
| scikit-learn Decision Tree (Gini) | 97.50% | 96.10% | 1.000 | 0.541 | 39 |

These are the outputs saved in the notebook, not a guarantee that every run or dataset version will produce identical results.

**Interpretation:** C4.5 and CART have the highest test accuracy in this recorded comparison. However, the positive-class recall is 0.541, meaning the models identify about 54.1% of diabetic cases in this test set. Accuracy alone can be misleading when the classes are imbalanced, so recall and missed cases are important to review.

## Additional Experiments: Random Forest

The final notebook sections extend the experiments to Random Forest:
- A custom forest built from bootstrapped CART trees with random feature selection.
- A scikit-learn `RandomForestClassifier` baseline.
- Experiments with different `max_features` settings, class weighting, and probability cutoffs.

These experiments are additional to the main ID3, C4.5, and CART comparison.

## Learning Outcomes

This project provides practice with:
- Entropy and Information Gain
- Gain Ratio and Split Information
- Gini impurity
- Categorical and numeric feature splitting
- Train-test splitting and stratified sampling
- Confusion matrices and classification metrics
- Class imbalance and the difference between accuracy and recall
- Random Forest and bootstrap sampling

## Limitations

- The implementations are educational versions and do not cover every detail of the full algorithms.
- The ID3 implementation uses binned categorical values for numeric columns.
- The C4.5 implementation uses threshold-based numeric splits and stopping limits; it is not a complete reproduction of every C4.5 feature.
- The CART code is for classification, not regression.
- The diabetes dataset is imbalanced, so a high accuracy score does not necessarily mean diabetic cases are detected reliably.
- This project is for learning and experimentation only. It is **not a medical diagnostic tool**.
