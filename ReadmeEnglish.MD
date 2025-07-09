# Project Viability Application

This simple application uses logistic regression to evaluate the viability of projects based on three key features: investment amount, expected return, and impact score. You can train the model on historical project data and predict the viability and probability of success for new project proposals.

## Features

* **Model Training & Evaluation**: Train a logistic regression model using scikit-learn and evaluate its performance with classification metrics.
* **Feature Scaling**: Standardize input features (`investment`, `expected_return`, `impact_score`) using `StandardScaler`.
* **Persistence**: Save and load the trained model, scaler, and evaluation metrics using `joblib`.
* **Prediction API**: Use the `train_or_predict()` function to either train the model or predict viability for new projects.

## Installation

1. **Clone the repository**:

   ```bash
   git clone https://github.com/SamuelLucasVieira/ProjectViabilityApplication.git
   cd ProjectViabilityApplication
   ```
2. **Create a virtual environment and install dependencies**:

   ```bash
   python3 -m venv venv
   source venv/bin/activate    # On Windows: venv\Scripts\activate
   pip install -r requirements.txt
   ```

## Usage

### 1. Training the Model

Run the training step (no new projects to predict):

```python
from viability import train_or_predict

# Train the model and retrieve evaluation metrics
default_predictions, metrics = train_or_predict(new_projects=None)
print("Model Evaluation Metrics:")
print(metrics)
```

### 2. Predicting New Projects

Provide a list of new project dictionaries to receive viability predictions and probabilities:

```python
from viability import train_or_predict

new_projects = [
    {"investment": 40000, "expected_return": 60000, "impact_score": 6},
    {"investment": 25000, "expected_return": 50000, "impact_score": 8},
]
predictions, metrics = train_or_predict(new_projects)
print("Predictions for New Projects:")
print(predictions)
print("Model Evaluation Metrics:")
print(metrics)
```

## Data

* **`projects_data.csv`**: Historical dataset containing:

  * `investment` (numeric)
  * `expected_return` (numeric)
  * `impact_score` (numeric)
  * `viability` (0 for non-viable, 1 for viable)

Make sure this file is placed in the project root before running the training.

## Methodology

1. **Load Data**: Read `projects_data.csv` into a pandas DataFrame.
2. **Feature Selection**: Extract the numeric features and target variable.
3. **Preprocessing**: Standardize features with `StandardScaler`.
4. **Model Training**:

   * Split data into training and test sets using `train_test_split`.
   * Train a `LogisticRegression` classifier.
5. **Evaluation**: Generate a classification report with precision, recall, and F1-score.
6. **Persistence**: Save the trained model, scaler, and metrics for later use.
7. **Prediction**: Load saved artifacts to predict new project viability and probability.

## Requirements

* Python 3.7 or higher
* pandas
* scikit-learn
* joblib

Install all Python dependencies via:

```bash
pip install -r requirements.txt
```

## Future Improvements

* Add cross-validation and hyperparameter tuning (e.g., `GridSearchCV`).
* Implement a web or CLI interface for easier interaction.
* Expand feature set with additional project characteristics (e.g., duration, team size).
* Provide visualization of ROC curves and performance metrics.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
