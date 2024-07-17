Import Necessary Libraries
You've correctly imported essential Python libraries for data manipulation (pandas), statistical analysis (numpy), visualization (seaborn, matplotlib), and handling missing values (sklearn.impute). Suppressing warnings is a good practice for cleaner output, though it's important to review these warnings during development to catch potential issues early.

import numpy as np
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt
import warnings
from sklearn.impute import KNNImputer
warnings.filterwarnings("ignore")
Read DataFrame
Reading the dataset using pd.read_csv is straightforward. It's good practice to immediately check the first few rows (df.head()) and the last few rows (df.tail()) to ensure the dataset was loaded correctly.

df = pd.read_csv("life expectancy data.csv")
print(df.head())
print(df.tail())
Sanity Check of the Data
Performing a sanity check involves understanding the dataset's shape, checking for missing values, duplicates, and getting a sense of the unique values in categorical columns. These steps are crucial for identifying potential issues early on.

print(df.shape)
print(df.info())
print(df["Country"].unique())
print(df.isnull().sum())
print(df.isnull().sum() / df.shape[0] * 100)
print(df.duplicated().sum())
for i in df.select_dtypes(include="object").columns:
    print(df[i].value_counts())
Exploratory Data Analysis (EDA)
EDA is vital for understanding the distribution of numerical variables, identifying outliers, and exploring relationships between features. Using Seaborn for visualizations like boxplots, histograms, and scatter plots helps in gaining insights into the data.

print(df.describe())
print(df.describe(include="object"))
for i in df.select_dtypes(include="number").columns:
    sns.boxplot(data=df, y=i)
    plt.show()

for i in df.select_dtypes(include="number").columns:
    sns.histplot(data=df, x=i)
    plt.show()

for i in ['Year', 'Adult Mortality', 'infant deaths', 'Alcohol', 'percentage expenditure', 'Hepatitis B', 'Measles ', ' BMI ', 'under-five deaths ', 'Polio', 'Total expenditure', 'Diphtheria ', ' HIV/AIDS', 'GDP', 'Population', ' thinness  1-19 years', ' thinness 5-9 years', 'Income composition of resources', 'Schooling']:
    sns.scatterplot(data=df, x=i, y='Life expectancy ')
    plt.show()
Missing Value Treatment
Using KNNImputer for missing value imputation is a sophisticated choice, especially for datasets where missing values may not be random. It's important to apply imputation carefully to avoid introducing bias.

impute = KNNImputer()
for i in df.select_dtypes(include="number").columns:
    df[i] = impute.fit_transform(df[[i]])
print(df.isnull().sum())
Encoding Data
Encoding categorical variables using pd.get_dummies is a common practice for preparing data for machine learning models. Dropping the first category helps avoid multicollinearity.

dummy = pd.get_dummies(data=df, columns=["Country", "Status"], drop_first=True)
print(dummy)
