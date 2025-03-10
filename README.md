# Calories Burnt Prediction using XGBoost Regressor

This project demonstrates the prediction of calories burnt based on various physical characteristics of an individual such as age, height, weight, and gender using machine learning. The model is trained using the XGBoost Regressor, a popular machine learning algorithm known for its efficiency and performance.

## Prerequisites

To run this project, you need the following Python libraries installed:

- `numpy`
- `pandas`
- `matplotlib`
- `seaborn`
- `sklearn`
- `xgboost`

You can install these dependencies using pip:
```bash
pip install numpy pandas matplotlib seaborn scikit-learn xgboost
```

## Dataset

The dataset used in this project can be found on Kaggle: [Calories Burnt Prediction Dataset](https://www.kaggle.com/datasets/fmendes/fmendesdat263xdemos?select=exercise.csv). 

The dataset consists of two CSV files:

1. **exercise.csv**: Contains features like gender, age, height, weight, and exercise hours.
2. **calories.csv**: Contains the target variable, which is the calories burnt by the individual based on the features from `exercise.csv`.

The features in the dataset include:
- **User_ID**: Unique identifier for each user.
- **Gender**: Gender of the user (Male/Female).
- **Age**: Age of the user.
- **Height**: Height of the user (in centimeters).
- **Weight**: Weight of the user (in kilograms).
- **Exercise Hours**: Hours of exercise per day.
- **Calories**: The target variable representing the calories burnt.

## Project Description

The goal of this project is to predict the number of calories burnt by an individual based on their physical characteristics and exercise hours using the XGBoost Regressor model. 

### Steps

1. **Importing Dependencies**: 
   - Libraries such as `numpy`, `pandas`, `matplotlib`, `seaborn`, `sklearn`, and `xgboost` are imported for data manipulation, visualization, and modeling.

2. **Data Loading & Processing**:
   - The exercise and calories data are loaded from CSV files into Pandas DataFrames.
   - Both datasets are merged based on common information, and basic information about the data (like shape and missing values) is analyzed.

3. **Data Exploration & Visualization**:
   - Statistical summaries are calculated, and distributions of key features such as age, height, weight, and gender are visualized using histograms and count plots.
   - The correlation between various features and the target variable is assessed using a heatmap.

4. **Feature Engineering & Preprocessing**:
   - Categorical data (gender) is converted into numerical format (0 for male, 1 for female).
   - Features (X) are separated from the target variable (Y).

5. **Model Training**:
   - The data is split into training and testing sets.
   - The XGBoost Regressor model is trained on the training set.

6. **Evaluation**:
   - The trained model is used to make predictions on the test set.
   - The performance of the model is evaluated using Mean Absolute Error (MAE).

### Code Implementation

```python
# Importing the Dependencies
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
from sklearn.model_selection import train_test_split
from xgboost import XGBRegressor
from sklearn import metrics

# Data Collection & Processing
calories = pd.read_csv('/content/calories.csv')
calories.head()

exercise_data = pd.read_csv('/content/exercise.csv')
exercise_data.head()

# Combining the two Dataframes
calories_data = pd.concat([exercise_data, calories['Calories']], axis=1)
calories_data.head()

# Data Exploration
calories_data.info()
calories_data.isnull().sum()

# Statistical Measures
calories_data.describe()

# Data Visualization
sns.set()
sns.countplot(calories_data['Gender'])
sns.distplot(calories_data['Age'])
sns.distplot(calories_data['Height'])
sns.distplot(calories_data['Weight'])

# Correlation Heatmap
calories_data.replace({"Gender": {'male': 0, 'female': 1}}, inplace=True)
correlation = calories_data.corr()
plt.figure(figsize=(10, 10))
sns.heatmap(correlation, cbar=True, square=True, fmt='.1f', annot=True, annot_kws={'size': 8}, cmap='Blues')

# Feature Selection
X = calories_data.drop(columns=['User_ID', 'Calories'], axis=1)
Y = calories_data['Calories']

# Splitting the data into training and test sets
X_train, X_test, Y_train, Y_test = train_test_split(X, Y, test_size=0.2, random_state=2)

# Model Training with XGBoost
model = XGBRegressor()
model.fit(X_train, Y_train)

# Model Evaluation
test_data_prediction = model.predict(X_test)

# Mean Absolute Error
mae = metrics.mean_absolute_error(Y_test, test_data_prediction)
print("Mean Absolute Error = ", mae)
```

### Output

- **Visualizations**: 
  - Count plots for gender distribution.
  - Distribution plots for age, height, and weight.
  - Correlation heatmap to visualize the relationships between features and target variable.

- **Evaluation Metrics**: 
  - Mean Absolute Error (MAE) to assess the accuracy of the predictions.

### Results

The model predicts the calories burnt by an individual based on their age, height, weight, gender, and exercise hours. The Mean Absolute Error (MAE) provides an indication of the model's accuracy, with lower values representing better performance.

## Conclusion

This project demonstrates how to predict calories burnt using a machine learning model (XGBoost Regressor). The model takes into account the physical characteristics of an individual and their exercise habits to make predictions. The use of the XGBoost algorithm ensures high performance in terms of prediction accuracy.

## Future Work

- **Hyperparameter Tuning**: Use techniques like GridSearchCV to fine-tune the model for better performance.
- **Model Comparison**: Compare XGBoost with other regression algorithms such as Linear Regression, Random Forest, etc.
- **Real-time Prediction**: Implement the model in a web or mobile application for real-time calories burnt prediction.
- **Additional Features**: Integrate other features like sleep patterns, diet, or activity types for more accurate predictions.

## License

This project is open-source and available under the MIT License.

---

Feel free to adapt, extend, and improve this project for your own use cases!