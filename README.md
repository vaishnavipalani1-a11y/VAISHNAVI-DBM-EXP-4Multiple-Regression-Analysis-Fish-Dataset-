# Experiment 4: Multiple Regression Analysis (Fish Dataset)

## Aim
To perform Multiple Linear Regression on a dataset imported from a CSV file to analyze how multiple features together predict a dependent variable.

## Dataset
The dataset used for this experiment is `fish.csv` which contains real-world physical measurements of various fish species:
* **Independent Variables ($X$):**
  * `L`: Mean length derived from `Length1`, `Length2`, and `Length3`
  * `Height`: Vertical height of the fish
  * `Width`: Diagonal width of the fish
* **Dependent Variable ($Y$):**
  * `Weight`: Weight of the fish (in grams)

## Algorithm / Steps Followed
1. Import the required Python libraries (`numpy`, `pandas`, `matplotlib`, `scikit-learn`).
2. Load the fish dataset into a Pandas DataFrame using `pd.read_csv()`.
3. Display the dataset and inspect its columns.
4. Define the dependent ($Y$) and independent ($X$) variables.
5. Train the Multiple Linear Regression model using `LinearRegression()`.
6. Display the model coefficients (`model.coef_`), intercept (`model.intercept_`), and regression equation.
7. Predict target variable (`Weight`) values using `model.predict()`.
8. Evaluate model accuracy using the $R^2$ score (`r2_score()`).
9. Plot actual vs. predicted values for visual comparison.

## Functions and Methods Used

| Category | Function / Method | Purpose / Description |
| :--- | :--- | :--- |
| **Data Creation / Handling** | `pd.read_csv()` | Load the CSV dataset into a Pandas DataFrame |
| | `np.array()` / `pd.DataFrame()` | Create and manage numerical arrays and tabular data for regression |
| **Model Building (Scikit-learn)** | `LinearRegression()` | Initialize the Multiple Linear Regression model |
| | `model.fit()` | Train the regression model using multiple independent variables ($X$) and target ($Y$) |
| | `model.predict()` | Predict dependent variable values ($Y$) using the trained model |
| | `r2_score()` | Evaluate the accuracy of the regression model using the $R^2$ score |
| **Model Attributes** | `model.intercept_` | Retrieve the intercept (constant term) of the regression equation |
| | `model.coef_` | Retrieve the coefficients (slopes) for each independent variable |
| **Visualization (Matplotlib)** | `plt.plot()` | Plot actual and predicted weight values for comparison |
| | `plt.title()`, `plt.xlabel()`, `plt.ylabel()`, `plt.legend()`, `plt.show()` | Configure titles, axis labels, legend, and display the plotted figure |

## Program & Output
## Input 1
```

# Multiple Regression Using CSV File (Fish Dataset)

# Step 1: Import Required Libraries
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
from sklearn.linear_model import LinearRegression
from sklearn.metrics import r2_score

# Step 2: Load Dataset
df = pd.read_csv('/content/Fish_length.csv')

# Step 3: Display Dataset
print(df.head())
print(df.columns)
```
## Output 1
```
  Species  Weight  Length1  Length2  Length3   Height   Width
0   Roach   259.1     25.1     27.2     29.9   8.8210  4.6136
1   Bream   423.2     29.0     30.9     33.5  13.4218  5.6620
2   Roach   151.1     21.4     23.2     25.2   7.2479  3.9580
3   Perch   523.2     31.5     34.2     37.6   9.9794  5.5136
4   Perch   355.7     27.3     29.9     32.9   8.7762  4.7713
Index(['Species', 'Weight', 'Length1', 'Length2', 'Length3', 'Height',
       'Width'],
      dtype='object')
```
## Input 2
```
# Step 4: Select Independent (X) and Dependent (Y) Variables

# Calculate average length
L = df[['Length1', 'Length2', 'Length3']].mean(axis=1)

# Independent variables
X = pd.DataFrame({
    'L': L,
    'Height': df['Height'],
    'Width': df['Width']
})

# Dependent variable
Y = df['Weight']

# Step 5: Build and Train the Multiple Regression Model
model = LinearRegression()
model.fit(X, Y)

# Step 6: Display Model Coefficients and Intercept
print("Intercept:", model.intercept_)
print("Coefficients:", model.coef_)
```
## Output 2
```
Intercept: -495.38038500886614
Coefficients: [  38.44144067   25.80398645 -107.6604105 ]

```
## Input 3
```
# Regression Equation
print("\nRegression Equation:")
print("Weight =", model.intercept_,
      "+", model.coef_[0], "* L",
      "+", model.coef_[1], "* Height",
      "+", model.coef_[2], "* Width")
```
## Output 3
```
Regression Equation:
Weight = -495.38038500886614 + 38.441440670641356 * L + 25.803986449763947 * Height + -107.66041049560657 * Width

```
## Input 4
```
# Step 7: Predict Target Variable Values
Y_pred = model.predict(X)

print("\nPredicted Values:")
print(Y_pred)
```
## Output 4
```
Predicted Values:
[ 288.82998398  438.19250231  159.92860991  492.19841849  371.92504575
   25.27356172 -111.1782049   233.01936222  -81.7527203   538.78563123
  325.99588442  575.02180527  215.28602323 1503.04128115  301.47481017
  225.57602786  397.34540489  754.01370124   88.14922326  391.26866704
   56.22741025  186.5913662   289.48635608  586.76542651  555.09324726
  329.23846602  266.18099288  154.36299483  682.56098996  372.33259089
  393.53694876  590.54158244  171.69644744  841.32245857  231.66327135
  -64.93498541  532.00327008  337.76229326  410.33233346   83.55578122
  693.12627611 1058.64463492  289.69287515  -64.54923009  271.70509414
  361.99025962  501.5869448   582.76931523  358.77826301  482.41447159
 -142.06041779  446.3109905    64.94927522  434.0283514  1107.99863523]
```
## Input 5
```
# Step 8: Evaluate Model Accuracy
accuracy = r2_score(Y, Y_pred)
print("\nR2 Score:", accuracy)
```
## Output 5
```
R2 Score: 0.9139876519274813
```
## Input 6
```
# Step 9: Visualize Actual vs Predicted Values
plt.plot(Y.values, label='Actual Weight')
plt.plot(Y_pred, label='Predicted Weight')

plt.title('Actual vs Predicted Fish Weight')
plt.xlabel('Fish Index')
plt.ylabel('Weight')
plt.legend()
plt.show()
```
## Output 6

<img width="580" height="455" alt="image" src="https://github.com/user-attachments/assets/6b684812-1198-4c72-8ab5-5176621bc757" />


## Result

Thus, Multiple Linear Regression was performed on a dataset imported from a CSV file using Python. The relationship between multiple independent variables and the dependent variable was analysed, and the objective was successfully achieved.
