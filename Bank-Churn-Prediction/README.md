# Bank Churn Modelling 

## Project Background
In the credit card industry, keeping customers loyal is a major challenge because customer churn hurts bank profits, and keeping existing clients is much cheaper than finding new ones. Fortunately, banks can use data science to spot early warning signs of churn by looking at factors like age, income, card usage, and credit limits, allowing them to step in early with special deals or better services. This project will analyze credit card user data to pinpoint exactly what drives customers away and build a prediction model. By using this model, banks can stop customers from leaving and offer personalized services that improve overall satisfaction and loyalty.

## Project Goal 

1. To identify key churn indicators from both financial and nonfinancial behaviours
2. To identify which variables have the biggest impact on customer churn
3. To build and test several machine learning models to accurately predict churn with at least 80% accuracy
4. To suggest strateegies for banks to retain at-risk customers

## Dataset Overview

**Dataset Description**
The dataset consists of 10 000 rows and 23 columns, with one target variables.

<img width="550" height="605" alt="image" src="https://github.com/user-attachments/assets/fe682a82-afa4-457a-a30c-6ec82266e1fc" />

**Statistics**

High level statistics were done to understand the structure of the data, recognise trends, and identify anomalies before starting modelling. This was done on both numerical and categorical data tp check for possible relationships between churn and the other columns.

<img width="314" height="272" alt="image" src="https://github.com/user-attachments/assets/51ebf17c-ddc6-4771-a85f-fea6a12aa4d9" />

<img width="359" height="186" alt="image" src="https://github.com/user-attachments/assets/8a7bfadc-ae86-4ba3-85b0-2d962204c5f8" />


**Exploratory Data Analysis (EDA)**

EDA methods that were applied: histograms, attrition flag counts, boxplots, and correlation heatmaps. This allowed for a more detailed analysis in identifying important patterns, possible relationships, and underlying data quality issues. 

**Distribution of All Features**

<img width="435" height="605" alt="image" src="https://github.com/user-attachments/assets/494c2428-e819-400f-847b-c8ed37fae64e" />

Analysis of the 21 histograms showed a heavy imbalance in the 'Attrition Flag' column, with far more existing customers than churned ones. Demographically, most customers are aged 40–50, have 0–3 dependents, are married or single, hold a graduate-level education, fall into the lower-middle-income bracket, and primarily hold 'Blue' cards. Behaviorally, most users have been with the bank for 30–40 months, showing low scores in inactive months and contact counts, which points to regular account usage. Finally, financial metrics like credit limit, revolving balance, open to buy, and total transaction amounts are skewed to the left, meaning most customers have lower values, while a double peak in transaction counts reveals distinct groups of users based on how frequently they use their cards.

**Box Plots for Numerical Features**

<img width="293" height="510" alt="image" src="https://github.com/user-attachments/assets/d4b8ff4f-2ed4-424d-ad90-972cc7e65a54" />

The boxplots were used to examine the distribution of each numerical feature and  identify any outliers. Numerous variables such as ‘Credit Limit’, ‘Total Transaction Amount’, ‘Avg Open To Buy’, and ‘Total Count Change Q4 to Q1’ all displayed a large number of outliers, indicating longtailed distributions, or perhaps the presence of a low number of customers with extreme values. Other features such as ‘Customer Age’, ‘Dependent Count’, and ‘Months on Book’ showcased more close and symmetric distributions. 

**Correlation Heatmap of All Features**

<img width="459" height="407" alt="image" src="https://github.com/user-attachments/assets/50a94a9b-2595-4527-9e9e-ff7ac92be2de" />

The correlation heatmap showed several logical, strong positive relationships among the numerical data. For instance, there is a high correlation (0.81) between total transaction counts and transaction amounts, as well as a strong link (0.63) between credit limits and average open-to-buy credit. Another strong positive relationship exists between customer age and months on book, meaning older customers naturally tend to keep their accounts open longer. Crucially, the churn indicator ('Attrition Flag') showed only weak correlations with most numerical columns, proving that customer churn isn't triggered by a single factor alone but is instead driven by a combination of multiple features.

## Pre-Processing 

A number of issues have been identified that have the potential to interfere with the data efficiency, accuracy, or clarity. Among those issues are column names, missing values not easily detected through code, outliers and categorical variables. Data set issues:

1. **Fixing column names:** 
Some column names were inconsistent, illegible, and difficult to understand. For example, some column names have underscores, such as 'Dependant_Count,' while others have abbreviated words, such as 'Total_Revolving_Bal.'

2. **Hidden missing values:**
Some missing values are written as "unknown" rather than NaN or left blank which is detected as a strong instead of a missing value.

3. **Extreme outliers in “Credit Limit”, “Average Open to Buy”, “Total Amount Change Q4 to Q1”, “Total Transaction Amount”, and “Total Count Change Q4 to Q1” columns:**
Boxplots revealed that several columns contain extreme outliers. These outliers lie far outside the typical rang and can negatively affect the accuracy of the model.

5. **Categorial Data Encoding:**
The dataset includes categorical data which must be converted into numerical data for predictive modelling.

Pre-processing was done to ensure that the dataset can be used efficiently with the most accurate predictive model. 

**Handling Missing Values**

Because "unknown" is a valid string, functions like isnull() or dropna() would not be able to identify or drop strings as they are not NaN values. So, we can replace cells with the string "unknown" with NaN and then properly drop the rows using dropna(). 

<img width="360" height="367" alt="image" src="https://github.com/user-attachments/assets/62de7d8f-a670-4e70-8961-13a903bb01e8" />

**Handling Outliers**

To handle extreme outliers, we applied a capping method using the 1st and 99th percentiles. This was done on columns like Credit Limit, Avg Open To Buy, Total Amount Change Q4 to Q1, Total Transaction Amount, and Total Count Change Q4 to Q1 to lessen the impact of unusually high or low values. 

<img width="197" height="212" alt="image" src="https://github.com/user-attachments/assets/32de181b-00ac-4111-8ee7-f1591a9e2b73" />

**Renaming Columns**

Column names were renamed as some were abbreviated and all contained ‘_’. This improves the readability and avoid misunderstanding. 

<img width="162" height="200" alt="image" src="https://github.com/user-attachments/assets/41d946b9-1e7b-442a-b11e-e3ae98d4f61c" />

**Data Transformation**

LabelEncoder was used to encode the values in the "Attrition Flag" column with 0 (Attrited customers) and 1 (existing customers). Also, applied MinMax scaling on all numerical columns (excluding the target) to prepare and make them within a numerical range of 0 to 1 to to keep features with larger scales from overwhelming that those with smaller ranges. 

<img width="259" height="171" alt="image" src="https://github.com/user-attachments/assets/6272eb96-30f8-43ea-b395-b0a8cec8650f" />

<img width="268" height="149" alt="image" src="https://github.com/user-attachments/assets/2bd3f12b-87d6-46c3-828c-8b84d8d647d2" />

**Feature Selection**

Dropped columns like “Client Number”, “Education Level”, “Marital Status”, “Card Category”, “Dependent Count”, and “Avg Open To Buy” due to low correlation with attrition and low correlation with other features. 

Used SelectKBest to double-check the top 5 features most related to the target. However, we didn’t rely only on these five, as our EDA showed that no single feature dominates, attrition is likely influenced by a combination of factors, so we kept other relevant features for modeling. 

<img width="507" height="52" alt="image" src="https://github.com/user-attachments/assets/57ee7075-7b5e-4efd-8876-faeebd5ca976" />

## Model Testing and Comparison 
**Resampling and Imbalance Handling**

*Model Validation*

## Model Testing

**Feature Importance**

**ROC Curve**

**Confusion Matrices**

**Results from from Stratified K Fold with Cross Validation**

## Ending Remarks


