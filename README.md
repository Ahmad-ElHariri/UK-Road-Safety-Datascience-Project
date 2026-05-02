# UK Road Safety Accident Severity Prediction

## Project Idea

This project analyzes the UK Road Safety dataset to understand the main factors related to road accident severity and to build machine learning models that predict whether a collision is **Fatal**, **Serious**, or **Slight**.

The goal is not only to get high accuracy, but also to handle the class imbalance problem and identify which road, vehicle, driver, time, and location factors contribute most to severe accidents.

---

## Dataset

The project uses UK road safety collision data, including features related to:

- Accident location and administrative area
- Road type and speed limit
- Weather, light, and road surface conditions
- Vehicle and driver information
- Casualty information
- Time-based information such as hour, month, and weekday
- Collision severity as the target variable

The target variable is:

- `Fatal`
- `Serious`
- `Slight`

---

## Main Techniques Used

### 1. Exploratory Data Analysis

EDA was used to understand the structure of the data, including:

- Target class distribution
- Missing values
- Numerical feature distributions
- Skewness
- Correlation between numerical variables
- Early signs of redundancy and multicollinearity

A clear class imbalance was observed, where slight accidents were much more common than serious and fatal accidents.

---

### 2. Data Cleaning

Several cleaning steps were applied:

- Removed unnecessary identifier/reference columns
- Converted sentinel missing codes such as `-1`, `9`, and `99` into proper missing values
- Handled missing values based on the meaning of each feature
- Inspected outliers using the IQR method
- Kept meaningful outliers when they represented real accident cases

---

### 3. Feature Engineering

New features were created to improve model performance and interpretability, including:

- Time-based features such as `hour`, `month`, and weekend indicators
- Log transformations for skewed numerical variables
- Binned variables such as driver age groups and speed groups
- Interaction features such as:
  - Vehicles × casualties
  - Speed × urban context

These features helped represent accident patterns more clearly.

---

### 4. Feature Selection

Multiple feature selection methods were used:

- Correlation analysis
- Variance Inflation Factor (VIF)
- Chi-squared test for categorical features
- Recursive Feature Elimination as a reference method
- PCA analysis to check dimensionality reduction potential

Highly redundant features were removed when they created multicollinearity or repeated information already captured by stronger engineered features.

---

### 5. Preprocessing

The final preprocessing pipeline included:

- Train/test split
- Encoding categorical variables
- Scaling where needed
- Handling class imbalance using SMOTE
- Preparing the data for multiple classification models

---

## Models Used

The following models were trained and compared:

- Logistic Regression
- Random Forest
- XGBoost
- Balanced Random Forest
- Tuned Random Forest with threshold tuning

The models were evaluated using:

- Accuracy
- Balanced Accuracy
- Macro-F1 Score
- Weighted-F1 Score
- Confusion Matrix
- Bootstrap Confidence Intervals
- Pairwise Bootstrap Comparisons
- Holm Correction for multiple comparisons

Because the dataset is imbalanced, **balanced accuracy** and **macro-F1** were more important than simple accuracy.

---

## Main Results

The default Random Forest achieved the highest accuracy, but it was biased toward the majority class.

After threshold tuning, the Random Forest became better at detecting minority classes, especially fatal and serious accidents. The tuned model reduced overall accuracy slightly but improved balanced accuracy, which is more important for this problem.

The final tuned Random Forest achieved a better balance between the three severity classes.

---

## Conclusion

This project shows that road accident severity prediction is strongly affected by class imbalance. A model can appear strong if it predicts the majority class well, but this is not enough when the goal is to detect serious and fatal accidents.

The best practical model was the tuned Random Forest because it improved balanced accuracy and gave more useful predictions across all accident severity levels.

The most important factors were related to accident scale, road context, speed, time, and location. Based on the results, road safety efforts should not be distributed equally everywhere. Instead, they should target high-risk combinations of road type, speed context, time patterns, and accident conditions.

---

## Technologies Used

- Python
- Pandas
- NumPy
- Matplotlib
- Scikit-learn
- Imbalanced-learn
- XGBoost
- Joblib
- Jupyter Notebook

---

## Repository Structure

```text
.
├── uk-road-safety-accident-severity-prediction.ipynb
├── README.md
└── data/
