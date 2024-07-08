#This README document guides users through the preparation of a dataset for machine learning modeling,
focusing on the "life expectancy data.csv" dataset. The process encompasses several critical steps, including library imports, data reading, initial checks, exploratory data analysis (EDA), handling missing values, and encoding categorical data. This structured approach ensures that the dataset is clean, well-understood, and ready for further analysis or model training.

Author & Date
Author: Ibrahim Mohamed Shedoh
Date: 13/02/2024

#Steps in the Script

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
print(df.head())
print(df.tail())
Sanity Check of the Data
print(df.shape)
print(df.info())
print(df["Country"].unique())
print(df.isnull().sum())
print(df.isnull().sum() / df.shape[0] * 100)
print(df.duplicated().sum())
for i in df.select_dtypes(include="object").columns:
    print(df[i].value_counts())
Exploratory Data Analysis (EDA)
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

print(df.select_dtypes(include='number').corr())
Missing Value Treatment
impute = KNNImputer()
for i in df.select_dtypes(include="number").columns:
    df[i] = impute.fit_transform(df[[i]])

print(df.isnull().sum())
Encoding Data
dummy = pd.get_dummies(data=df, columns=["Country", "Status"], drop_first=True)
print(dummy)

#Notes
Ensure all required libraries are installed before running the script.
The dataset "life expectancy data.csv" should be in the same directory as the script or provide the correct path to the file.
Warnings are suppressed in the script for cleaner output, but it's recommended to review them in a real-world scenario.
Conclusion
This script offers a comprehensive method for preparing a dataset for machine learning modeling, encompassing crucial steps from data ingestion to preprocessing. It serves as a foundational guide that can be customized according to specific project needs and the characteristics of the dataset being worked with.
