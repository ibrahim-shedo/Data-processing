README for Machine Learning Model Preparation Script
Overview
This document outlines the steps involved in preparing a dataset for machine learning modeling, specifically focusing on the "life expectancy data.csv" dataset. The process includes importing necessary libraries, reading the dataset, performing a sanity check, conducting exploratory data analysis (EDA), handling missing values, and encoding categorical data.

Author: Ibrahim Mohamed Shedoh
Date: 13/02/2024

Steps in the Script
Import Necessary Libraries
import numpy as np
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt
import warnings
from sklearn.impute import KNNImputer
warnings.filterwarnings("ignore")
Read DataFrame
df = pd.read_csv("life expectancy data.csv")
Display the first few and last few rows of the DataFrame:
df.head()
df.tail()
Sanity Check of the Data
Get the shape (number of rows and columns):
df.shape
Get detailed information about the DataFrame, including data types and null values:
df.info()
Get unique values in the "Country" column:
df["Country"].unique()
Check for missing values and their percentages:
df.isnull().sum()
df.isnull().sum() / df.shape[0] * 100
Check for duplicate rows:
df.duplicated().sum()
Identify potential garbage values in object-type columns:
for i in df.select_dtypes(include="object").columns:
    print(df[i].value_counts())
Exploratory Data Analysis (EDA)
Generate descriptive statistics:
df.describe()
df.describe(include="object")
Visualize data distributions and detect outliers using box plots and histograms:
for i in df.select_dtypes(include="number").columns:
    sns.boxplot(data=df, y=i)
    plt.show()

for i in df.select_dtypes(include="number").columns:
    sns.histplot(data=df, x=i)
    plt.show()
Scatter plots to examine relationships between dependent and independent variables:
for i in ['Year', 'Adult Mortality', 'infant deaths', 'Alcohol', 'percentage expenditure', 'Hepatitis B', 'Measles ', ' BMI ', 'under-five deaths ', 'Polio', 'Total expenditure', 'Diphtheria ', ' HIV/AIDS', 'GDP', 'Population', ' thinness  1-19 years', ' thinness 5-9 years', 'Income composition of resources', 'Schooling']:
    sns.scatterplot(data=df, x=i, y='Life expectancy ')
    plt.show()
Correlation matrix to identify relationships between numerical variables:
df.select_dtypes(include='number').corr()
Missing Value Treatment
Impute missing values using KNN Imputer:
impute = KNNImputer()
for i in df.select_dtypes(include="number").columns:
    df[i] = impute.fit_transform(df[[i]])
Check for remaining null values:
df.isnull().sum()
Encoding Data
Convert categorical data into numerical data using one-hot encoding:
dummy = pd.get_dummies(data=df, columns=["Country", "Status"], drop_first=True)
dummy
Notes
Ensure all required libraries are installed before running the script.
The dataset "life expectancy data.csv" should be in the same directory as the script or provide the correct path to the file.
Warnings are suppressed in the script for cleaner output, but it's recommended to review them in a real-world scenario.
Conclusion
This script provides a structured approach to preparing a dataset for machine learning modeling, covering essential steps from data loading to pre-processing. Use this as a foundation and extend it based on specific requirements and the nature of your dataset.
