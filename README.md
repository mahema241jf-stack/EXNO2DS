# EXNO2DS
# AIM:
      To perform Exploratory Data Analysis on the given data set.
      
# EXPLANATION:
  The primary aim with exploratory analysis is to examine the data for distribution, outliers and anomalies to direct specific testing of your hypothesis.
  
# ALGORITHM:
STEP 1: Import the required packages to perform Data Cleansing,Removing Outliers and Exploratory Data Analysis.

STEP 2: Replace the null value using any one of the method from mode,median and mean based on the dataset available.

STEP 3: Use boxplot method to analyze the outliers of the given dataset.

STEP 4: Remove the outliers using Inter Quantile Range method.

STEP 5: Use Countplot method to analyze in a graphical method for categorical data.

STEP 6: Use displot method to represent the univariate distribution of data.

STEP 7: Use cross tabulation method to quantitatively analyze the relationship between multiple variables.

STEP 8: Use heatmap method of representation to show relationships between two variables, one plotted on each axis.

## CODING AND OUTPUT
````
import pandas as pd
import numpy as np
import seaborn as sns
import matplotlib.pyplot as plt
data = pd.read_csv('titanic_dataset.csv')
print("Initial Data Overview:")
print(data.head())
````
<img width="847" height="467" alt="image" src="https://github.com/user-attachments/assets/8ea7d5ab-dc3f-495a-b64e-53b749a4c137" />
```
print("\nDataset Information:")
print(data.info())
```

<img width="502" height="470" alt="image" src="https://github.com/user-attachments/assets/d16c274c-6c19-4ce1-85bb-6b0da4ebb751" />

```
print("\nMissing Values:")
print(data.isnull().sum())
```
<img width="335" height="308" alt="image" src="https://github.com/user-attachments/assets/89102592-7fb3-40ff-a4bf-80729b548b5b" />

```
for column in data.columns:
    if data[column].dtype == 'object':
        if data[column].isnull().any():
            data[column] = data[column].fillna(data[column].mode()[0])
    else:
        data[column] = data[column].fillna(data[column].mean())

print("Missing values handled.")
print(data.isnull().sum())
```
<img width="358" height="312" alt="image" src="https://github.com/user-attachments/assets/00950c89-8a43-44c1-95ab-8babc529c758" />

```
sns.boxplot(x=data['Fare'])

plt.title("Boxplot - Fare")
plt.xlabel("Fare")
plt.show()
```
<img width="727" height="552" alt="image" src="https://github.com/user-attachments/assets/677c603c-2fa7-47d0-bb51-70c84f7cf3e2" />

```
def remove_outliers_iqr(df, column):
    Q1 = df[column].quantile(0.25)
    Q3 = df[column].quantile(0.75)

    IQR = Q3 - Q1

    lower = Q1 - 1.5 * IQR
    upper = Q3 + 1.5 * IQR

    return df[(df[column] >= lower) & (df[column] <= upper)]

data = remove_outliers_iqr(data, 'Fare')

print("Outliers removed using IQR method.")
```
<img width="460" height="53" alt="image" src="https://github.com/user-attachments/assets/dbbea11e-96ae-479f-b655-e9f2a80732d7" />

```
sns.countplot(x='Sex', data=data)

plt.title("Countplot - Gender Distribution")
plt.show()
```
<img width="772" height="570" alt="image" src="https://github.com/user-attachments/assets/806bd62d-0ebd-4896-92b0-ddb780db5ba7" />

```
sns.displot(data['Age'], kde=True)

plt.title("Displot - Age Distribution")
plt.xlabel("Age")
plt.ylabel("Frequency")
plt.show()
```
<img width="768" height="636" alt="image" src="https://github.com/user-attachments/assets/2bced4ab-828f-4b98-a236-315824104873" />

```
crosstab_result = pd.crosstab(
    data['Sex'],
    data['Pclass']
)

print("\nCross Tabulation Result:")
print(crosstab_result)
```
<img width="327" height="125" alt="image" src="https://github.com/user-attachments/assets/c925544b-6e67-4cb3-b05d-38698754341b" />

```
correlation_matrix = data.corr(numeric_only=True)

sns.heatmap(
    correlation_matrix,
    annot=True,
    cmap='coolwarm'
)

plt.title("Correlation Heatmap")
plt.show()
```
<img width="743" height="626" alt="image" src="https://github.com/user-attachments/assets/b0b857ec-2b12-4484-a637-1d95180137c3" />

# RESULT
       Thus, the Titanic dataset was successfully analyzed and visualized using Python.

