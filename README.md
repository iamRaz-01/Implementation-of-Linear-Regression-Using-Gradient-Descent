# Implementation-of-Linear-Regression-Using-Gradient-Descent

## AIM:
To write a program to predict the profit of a city using the linear regression model with gradient descent.

## Equipments Required:
1. Hardware – PCs
2. Anaconda – Python 3.7 Installation / Jupyter notebook

## Algorithm
1. Import the required library and read the dataframe.
2. Write a function computeCost to generate the cost function.
3. Perform iterations og gradient steps with learning rate.
4. Plot the Cost function using Gradient Descent and generate the required graph.

## Program:
```python
/*
Program to implement the linear regression using gradient descent.
Developed by: Abdul Rasak . N 
RegisterNumber:  24002896
*/
import numpy as np
import pandas as pd
from sklearn.preprocessing import StandardScaler


# Define the linear regression function using gradient descent
def linear_regression(X1, y, learning_rate=0.01, num_iters=1000):
    X = np.c_[np.ones(len(X1)), X1]  # Add a column of ones for the intercept
    theta = np.zeros(X.shape[1]).reshape(-1, 1)  # Initialize theta with zeros

    for _ in range(num_iters):
        predictions = X.dot(theta).reshape(-1, 1)  # Compute predictions
        errors = (predictions - y).reshape(-1, 1)  # Compute errors
        theta -= learning_rate * (1 / len(X1)) * X.T.dot(errors)  # Update theta

    return theta


# Load the data
data = pd.read_csv('datasets/50_Startups.csv', header=None)

# Extract the feature and target variable from the dataset
X = data.iloc[1:, :-2].values.astype(float)
y = data.iloc[1:, -1].values.reshape(-1, 1)

# Standardize the data
scaler = StandardScaler()
X1_Scaled = scaler.fit_transform(X)
y_Scaled = scaler.fit_transform(y)

# Perform linear regression using the function
theta = linear_regression(X1_Scaled, y_Scaled)

# Prepare new data for prediction and standardize it
new_data = np.array([165349.2, 136897.8, 471784.1]).reshape(-1, 1)
new_Scaled = scaler.fit_transform(new_data)

# Predict using the model
prediction = np.dot(np.append(1, new_Scaled), theta)
prediction = prediction.reshape(-1, 1)

# Inverse transform the prediction to original scale
pre = scaler.inverse_transform(prediction)
print(data.head())
# Print the predicted value
print(f"Predicted value: {pre}")
```

## Output:
![image](https://github.com/user-attachments/assets/4e253f2e-45cd-4341-a93f-f5bfd8c980b1)


## Result:
Thus the program to implement the linear regression using gradient descent is written and verified using python programming.
