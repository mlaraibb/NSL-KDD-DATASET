# NSL-KDD Network Intrusion Detection

## Project Overview

This project uses the NSL-KDD dataset to classify network connections as either normal traffic or network attacks.

* `0` represents normal traffic.
* `1` represents a network attack.

I used pandas for data preprocessing, scikit-learn for a baseline logistic regression model, and PyTorch for a simple binary classifier.

## Dataset

The following NSL-KDD files were used:

* `KDDTrain+.txt` — 125,973 training rows
* `KDDTest+.txt` — 22,544 testing rows

The testing dataset was kept separate from the training dataset so the models could be evaluated on unseen data.

## Data Preprocessing

I completed the following preprocessing steps using pandas:

1. Loaded and viewed the training and testing datasets.
2. Renamed the protocol, service, flag, and result columns.
3. Combined the datasets temporarily to produce identical encoded columns.
4. Applied one-hot encoding to:

   * Protocol type
   * Service
   * Flag
5. Converted the target into binary labels:

   * Normal = `0`
   * Attack = `1`
6. Removed the original attack-name and difficulty-score columns.
7. Separated the input features (`X`) from the target labels (`y`).
8. Checked the datasets for missing values.
9. Standardized the features using `StandardScaler`.

After preprocessing, each connection contained 122 numerical input features.

## Scikit-Learn Model

Logistic regression was used as the baseline scikit-learn classifier.

The model was trained using the scaled training features and their correct labels. It then predicted the classes of the testing connections.

The model used `class_weight="balanced"` to help handle class imbalance.

## PyTorch Model

I created a beginner-friendly PyTorch binary classifier using one linear layer.

The PyTorch workflow included:

1. Converting the scaled data into tensors.
2. Creating a linear binary classifier.
3. Using `BCEWithLogitsLoss` to calculate prediction errors.
4. Using the Adam optimizer to update the model.
5. Training the model for 20 epochs.
6. Predicting the testing results.
7. Evaluating the predictions.

## PyTorch Results

The model’s training loss decreased from approximately `0.7139` to `0.1735`, showing that it learned from the training data.

| Metric             | Result |
| ------------------ | -----: |
| Accuracy           | 75.63% |
| ROC-AUC            |   0.78 |
| Average Precision  |   0.86 |
| Attack Precision   |   0.92 |
| Attack Recall      |   0.63 |
| Attack F1-score    |   0.74 |
| Weighted Precision |   0.80 |
| Weighted Recall    |   0.75 |
| Weighted F1-score  |   0.75 |

The complete classification report, confusion matrix, precision-recall curve, and ROC curve are displayed in the notebook.

## Findings

The simple PyTorch model achieved approximately 76% testing accuracy. Its attack precision of 0.92 means that most connections identified as attacks were actually attacks.

However, its attack recall was 0.63, meaning the model did not detect every attack. This shows that the simple linear model learned useful patterns but still had limitations in detecting attack traffic.

A more advanced neural network, additional tuning, or stronger class-imbalance handling could potentially improve attack recall.

## Evaluation Methods

The models were evaluated using:

* Accuracy
* Confusion matrix
* Precision
* Recall
* F1-score
* Precision-recall curve
* Average precision
* ROC curve
* ROC-AUC score

## Project Files

```text
KDDTrain+.txt
KDDTest+.txt
nsl_kdd_intrusion_detection.ipynb
requirements.txt
README.md
```

## Installation

Install the required Python libraries with:

```bash
python3 -m pip install -r requirements.txt
```

The required libraries are:

* pandas
* NumPy
* scikit-learn
* Matplotlib
* PyTorch

## Running the Project

1. Download or clone this repository.
2. Keep the dataset files and notebook in the same folder.
3. Install the libraries listed in `requirements.txt`.
4. Open `nsl_kdd_intrusion_detection.ipynb`.
5. Run all notebook cells from top to bottom.

## AI Assistance

I began this project with little knowledge of machine learning and no previous experience using pandas, scikit-learn, or PyTorch. I used AI assistance and educational videos to learn unfamiliar concepts and support parts of the implementation, particularly the PyTorch portion. I ran, reviewed, and tested the code, using this project as an opportunity to develop my understanding of the machine-learning workflow.
