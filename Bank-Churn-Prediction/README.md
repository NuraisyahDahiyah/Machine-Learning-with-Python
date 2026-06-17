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

The churn dataset is highly imbalanced because there are far fewer churned customers than existing ones, which can cause the predictive model to be biased toward the majority class. To fix this and improve accuracy, two balancing techniques were used: SMOTE, which creates fake samples of the minority class only within the training folds to prevent data leakage, and class weighting for Random Forest and Logistic Regression, which penalizes the models more heavily for misclassifying churn cases.

For the model selection phase, three specific classification algorithms were chosen to compare and find the best fit for predicting credit card churn:
1. **Logistic Regression (LR):** Chosen because it is simple, fast, and easy to interpret.
2. **Random Forest (RF):** Chosen because it handles non-linear relationships well, offers higher accuracy, and prevents overfitting by using multiple decision trees.
3. **XGBoost:** Chosen for its high accuracy and ability to handle complex patterns and class imbalances when properly tuned.

*Model Validation*

While a standard train-test split was used initially, it can break the balance of class labels in the test set, leading to biased and unreliable performance estimates. To fix this, Stratified K-Fold Cross-Validation was implemented to break the dataset into *k* equal parts, making sure the ratio of major and minor classes stays the same in every single fold.

## Model Testing

To handle class imbalance, three variations of each classifier were tested using *imblearn.Pipeline* to prevent data leakage: 1) no balancing 2) SMOTE oversampling 3) class weight balancing. Hyperparameter tuning was performed inside the pipeline using *GridSearchCV* with a stratified 5-fold cross-validation to find the best settings for key parameters, and the results were evaluated using ROC curves and confusion matrices. 

Separately from the grid search, the final models were checked using a 5-fold Stratified K-Fold cross-validation to keep class distributions consistent across data splits. Ultimately, the models were evaluated and compared using accuracy, F1-scores, and class-specific recall, focusing heavily on class 0 (churners) to meet the project's main objective.

**Feature Importance**

Here is how feature importance is extracted for each specific model:
1. **Random Forest:** Uses a feature importance plot that calculates how much each feature helps reduce "Gini impurity" (essentially measuring how much cleaner the data splits get) across all the decision trees.
2. **Logistic Regression:** Uses the model's learned coefficients. A positive number means a feature makes a customer more likely to churn, a negative number means less likely, and the actual size of the number shows how powerful that feature's influence is.
3. **XGBoost:** Uses an importance plot set to measure "gain" instead of "weight." Gain calculates the average improvement in accuracy whenever a feature is used to split data, giving a much truer look at which features the model actually relies on most.

<img width="468" height="277" alt="image" src="https://github.com/user-attachments/assets/30f3a897-531c-48bf-a238-cc78fa4168fe" />
<img width="468" height="278" alt="image" src="https://github.com/user-attachments/assets/cb8d412e-f645-4c31-936d-55becf58e0a3" />
<img width="468" height="279" alt="image" src="https://github.com/user-attachments/assets/aa5e4307-f960-40e9-8be6-504ba5de9f11" />

Across all model runs using XGBoost and Random Forest, the same core features consistently ranked as the most important indicators of customer churn. Other frequent indicators include Utilization Ratio, Count Change from Q4 to Q1, and Months Inactive in the last 12 Months, all of which point to behavioral patterns of declining bank usage. Ultimately, these features tie back to a drop in financial interactions, showing that churning happens when a customer's transactional activity and engagement slow down, giving banks a clear warning sign to monitor.

The most important data features identified by the models are:
1. Total Transaction Count: Ranked number 1 across all models.
2. Total Transaction Amount: Consistently ranked in the top 3.
3. Total Revolving Balance: Consistently ranked in the top 3.

**ROC Curve**

ROC curve was also prepared but it shows minimal differences between each variation of the model across the 3 model that we have tested Although there are no significant differences from the variations of the same model, XGBoost and Random Forest perform better than Logistic Regression with a difference of 0.07 in AUC. 

<img width="234" height="185" alt="image" src="https://github.com/user-attachments/assets/9bf5b57b-35fb-4d2c-bcc5-9c3265f4e97a" />
<img width="234" height="185" alt="image" src="https://github.com/user-attachments/assets/e2331a67-4417-411a-992c-df38cf53962e" />
<img width="234" height="185" alt="image" src="https://github.com/user-attachments/assets/a70e3b2b-d9cd-4b0c-bdc3-ccc98dbafc7b" />

**Confusion Matrices**

Confusion matrices are used to easily evaluate model performance, focusing heavily on minimizing false positives (wrongly flagging loyal customers) and false negatives (missing actual churners). Because banks generally prioritize catching as many churners as possible over keeping false positives low, the ideal setup varies by algorithm.

The performance breakdowns for each algorithm are as follows:
1. **Random Forest:** The SMOTE version is the most effective overall because it catches the most churners (188), though it yields 31 false positives. In contrast, the Class Weighted version minimizes false positives to 12 but misses 45 churners, while the Plain version catches 173 churners with 14 false positives.

<img width="638" height="265" alt="image" src="https://github.com/user-attachments/assets/d4b1ae15-9f1c-45d9-bcc4-10ef86872765" />

3. **Logistic Regression:** Class Weighting provides the most balanced performance here by catching 167 churners with only 12 false positives. SMOTE catches the most churners (178) but is unacceptable because it flags more loyal customers (185) than actual churners, while the Plain version performs the worst by missing 106 churners.

<img width="638" height="265" alt="image" src="https://github.com/user-attachments/assets/214033ba-fd58-4a66-b502-0004ae1c8970" />

5. **XGBoost:** The SMOTE version delivers the highest recall across all configurations, catching 190 out of 212 churners with 26 false positives. The Plain version achieves the highest overall accuracy and best generalization by catching 180 churners with only 9 false positives, while the Class Weighted version performs the worst of the three XGBoost variations.

<img width="638" height="265" alt="image" src="https://github.com/user-attachments/assets/6f9b8355-b7bf-4484-a117-e734b001d33b" />

**Results from from Stratified K Fold with Cross Validation**

Stratified K-Fold cross-validation confirmed that the models are reliable and not overfitted. Among the three Random Forest configurations, the SMOTE-trained version achieved the highest recall and F1-score for identifying churners (Class 0). For Logistic Regression, Class Weighting proved to be the best option to catch the greatest number of churners, as SMOTE provided no significant improvement. For XGBoost, Weighted XGB performed best because it delivered a 4.7% increase in recall over the plain version, whereas SMOTE suffered performance drops in almost every category. Ultimately, when ranking all models by their specific ability to recall churners, Weighted XGBoost ranks first (0.916), followed by Random Forest with SMOTE (0.876), and lastly Logistic Regression with Class Weighting (0.825).

<img width="480" height="182" alt="image" src="https://github.com/user-attachments/assets/55fbbaea-fb19-42db-be08-7e1eda7ccfe2" />
<img width="478" height="170" alt="image" src="https://github.com/user-attachments/assets/93396c7d-fea8-4828-83c5-50e83250df7b" />
<img width="478" height="170" alt="image" src="https://github.com/user-attachments/assets/c2801af4-4c01-47be-8266-58ca42bfa82c" />

## Ending Remarks

The primary goal of this project was to identify customer churn indicators and build machine learning models with at least 80% accuracy. The results confirmed that churn is driven by a combination of factors rather than a single feature, with total revolving balance, transaction amount, and transaction count emerging as the most significant common indicators. 

Across the three tested algorithms (Logistic Regression, Random Forest, and XGBoost), XGBoost with class weighting was selected as the most reliable, balanced, and stable model, consistently achieving low false positive counts and over 80% accuracy across data splits.

To help banks translate these insights into practice, three key strategies are recommended: setting up real-time monitoring dashboards with early warning alerts, launching tailored retention campaigns designed specifically to re-engage inactive or younger customer segments, and deploying automated, personalized engagement nudges via SMS or email to intercept customers who have been inactive for two months or show declining financial behavior.


