# NSL-KDD Network Intrusion Detection

## Project Overview

This project uses the NSL-KDD dataset to classify network connections as normal traffic or network attacks.

 `0` represents normal traffic.
`1` represents an attack.

I used pandas for data preprocessing, scikit-learn for a baseline classifier, and PyTorch for a simple binary classification model.

## Dataset

The project uses:

`KDDTrain+.txt` for training
`KDDTest+.txt` for testing

The training dataset contains 125,973 rows, and the testing dataset contains 22,544 rows.

## Data Preprocessing

I completed the following steps using pandas:

1. Loaded and viewed the training and testing datasets.
2. Renamed the protocol, service, flag, and result columns.
3. Combined both datasets temporarily to create matching encoded columns.
4. Applied one-hot encoding to the protocol, service, and flag columns.
5. Converted the result into a binary target:

    Normal = `0`
   Attack = `1`
6. Removed the original attack-name and difficulty-score columns.
7. Separated the input features (`X`) from the target answers (`y`).
8. Checked the datasets for missing values.
9. Standardized the features using `StandardScaler`.

After preprocessing, each connection contained 122 numerical input features.

## Scikit-Learn Model

I used logistic regression as my baseline scikit-learn classifier.

The model was trained using `X_train` and `y_train`. It then predicted the classes for `X_test`, and the predictions were compared with `y_test`.

The model used `class_weight="balanced"` to help handle class imbalance.

## PyTorch Model

I created a beginner-friendly PyTorch binary classifier using one linear layer.

The PyTorch process included:

1. Converting the data into tensors.
2. Creating the model.
3. Selecting a loss function and optimizer.
4. Training the model for 20 epochs.
5. Predicting the testing results.
6. Evaluating the predictions.

## PyTorch Results

The training loss decreased from approximately `0.7047` to `0.1665`, showing that the model learned from the training data.

Accuracy: `75.98%`
 Correctly classified normal connections: `9,383`
Correctly classified attacks: `7,746`
Normal connections incorrectly classified as attacks: `328`
Attacks incorrectly classified as normal: `5,087`

### Confusion Matrix

```text
[[9383  328]
 [5087 7746]]
```

## Findings

The simple PyTorch model achieved approximately 76% accuracy. It classified most normal connections correctly but missed a considerable number of attacks.

The results show that a simple model can learn meaningful patterns from the NSL-KDD dataset. However, class-imbalance handling, additional training, or a more advanced neural network could improve attack detection.

## Evaluation

The models were evaluated using:

Accuracy
Confusion matrix
Precision
Recall
F1-score
Precision-recall curve
ROC curve
ROC-AUC score

## Requirements

Install the required libraries using:

```bash
python3 -m pip install -r requirements.txt
```

The project requires:

* pandas
* NumPy
* scikit-learn
* Matplotlib
* PyTorch

## Running the Project

1. Download or clone this repository.
2. Keep `KDDTrain+.txt` and `KDDTest+.txt` in the project folder.
3. Install the libraries from `requirements.txt`.
4. Open `nsl_kdd_intrusion_detection.ipynb`.
5. Run all notebook cells from top to bottom.

## AI Assistance
I began this project with little knowledge of machine learning and no previous experience using pandas, scikit-learn, or PyTorch. I used AI assistance and educational videos to learn unfamiliar concepts and support parts of the implementation, particularly the PyTorch portion. I ran, reviewed, and tested the code, using this project as an opportunity to develop my understanding of the machine-learning workflow.