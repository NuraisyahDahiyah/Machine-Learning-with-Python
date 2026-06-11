# Telco Customer Churn Modeling 
With the rise of artificial intelligence and the rapid advancements made by technologies today, data has become even more crucial in this data-driven world. Organizations today produce and collect enormous amounts of data. This makes data mining a vital tool in revealing hidden patterns and trends in these vast amount of data available. Companies from all sectors like healthcare to banking are adopting data mining techniques to transform raw data into actionable insights. For instance, economists in banks leverage data mining processes to predict market trends and other macroeconomic changes that often have vast amounts of data. In this case study, the author will investigate the use of data mining, looking at how it might be applied to better decision-making in actual case scenarios. This case study demonstrates how the data mining method can reveal hidden patterns, providing a deeper comprehension of the issue and assisting in the process of making better decisions.

## Project Objective 
1.	The rapidly evolving nature of customer preferences and usage patterns, which makes behavioral prediction difficult.
2.	The complex interplay between service-related attributes that directly influences customer decisions and drive brand loyalty. 
3.	The absence of a clear, data-driven framework to identify and proactively target high-risk customer segments.

## Pre-processing 
Data pre-processing is described as the process of cleaning, transforming and preparing raw data into a usable format for data mining processing, machine learning or other data science related tasks. In this case study, I used data pre-processing techniques of label encoding and one-hot encoding to prepare the dataset for data mining. 

**Cleaning Data Types and Handling Missing Values**
Before implementing these data pre-processing techniques, running quick summary to check for correct data types displayed and if there any missing values. The summary shows that monthly charges is recognised as an object (string) instead of a float (numeric). It is most likely stored as a string due to some missing or blank values. We will convert it to numeric using pd.to_numeric and set errors='coerce' to mark errors as NaN and then we will drop NaN values.The feature ‘customerID’ is dropped as it provides no useful predictive value for this case study. The author runs a summary of the first fiver rows to check if feature ‘customerID’ is dropped. 

<img width="210" height="266" alt="image" src="https://github.com/user-attachments/assets/b78c8642-c7c4-485b-97d8-ab46e8725cca" />

<img width="468" height="120" alt="image" src="https://github.com/user-attachments/assets/8382b68f-4d13-42f1-8053-c74747836ff4" />

**Label Encoding**
Majority of the features in this dataset are categorical features, which makes it difficult later when applying data mining techniques to the dataset as most machine learning models cannot directly process categorial data like “Yes” and “No” and instead require the data to be numerical. To do this, we will encode these categorical features into numerical values using label encoding for further analysis and modelling purposes. Label encoding assigns a unique numerical label to each category in the feature which allows algorithms to process the data effectively. 

**One-Hot Encoding**
Many of the features, especially service-related ones like Internet Service, Device Protection, and Online Security, are categorical variables with more than two possible values (e.g., “No internet service”, “DSL”, “Fiber optic”). These types of variables cannot be directly used in machine learning models, which typically require numerical input. To address this, we apply one-hot encoding,  a pre-processing technique that converts each unique category into a new binary (0 or 1) column. For instance, the Internet Service feature is split into multiple columns such as InternetService_DSL, InternetService_Fiber optic, and InternetService_No, where each row has a “1” in the column corresponding to its category and “0” elsewhere. This allows the model to interpret the presence or absence of each category explicitly without assuming any ordinal relationship between them. This transformation is crucial for ensuring that our machine learning models interpret the categorical information correctly during training and prediction

<img width="468" height="99" alt="image" src="https://github.com/user-attachments/assets/31442b34-e64c-4181-b638-ed0f290e2623" />

## Data Mining Technique 
Based on the findings on related works, data mining techniques that was commonly brought up were tree-based methods such Decision Trees, Random Forests as they often provide the best balance of accuracy and interpretability. 

### Random Forest Classification Model
Random Forest Classification (RF) is a supervised machine learning technique that builds numerous decision trees using different subsets of the training data. The algorithm would then aggregate the results from each tree to determine the final output, reducing the likelihood of overfitting and boosting overall accuracy. The Random Forest Classification Model's capacity to manage huge datasets well while remaining resilient to noise and missing values is one of its main features. In the context of this dataset, which focuses on predicting customer churn based on various customer and service attributes (such as monthly charges, contract type, and tenure group), RF is especially useful. This algorithm not only performs well with high-dimensional data but also allows us to rank the features based on how strongly they influence the prediction outcome. By training the Random Forest model on this dataset, we are able to gain insights into which factors are most associated with customer churn.

<img width="423" height="151" alt="image" src="https://github.com/user-attachments/assets/3919e0ff-5562-4ad8-b82f-438202c89653" />

<img width="391" height="233" alt="image" src="https://github.com/user-attachments/assets/4c714a51-4416-4a2c-99fd-e836d8083007" />

From the model's output, the most important predictor of churn is the Total Charges a customer has incurred, followed closely by Monthly Charges and whether the customer is on a Month-to-Month Contract. These findings provide a strong indication of which customers may be more at risk of leaving and help guide targeted retention strategy.

### Decision Tree Model Classification 
Decision Tree is a commonly-used data mining method that is ideal for examining consumer behavior due to its ease of use, transparency, and compatibility with both numerical and categorical data.  Because business stakeholders can easily observe and grasp the decision flow, its unambiguous decision rules make it particularly helpful for churn analysis. This level of interpretability is important for companies looking to not only predict churn but also understand the "why" behind it. In this dataset, we focus specifically on service-related features, such as internet service type, contract type, and support-related options, because these are the attributes that most directly influence a customer’s experience and, by extension, their likelihood to remain loyal to the brand. These variables are operational touchpoints that businesses can actively improve, making them valuable for targeted churn prevention strategies.

<img width="468" height="248" alt="image" src="https://github.com/user-attachments/assets/ca70e41d-3ff3-4cc9-b3e8-dc39e9c291f8" />

To validate the insights derived from the Decision Tree model, a feature importance analysis and a segment analysis were conducted. 

<img width="162" height="121" alt="image" src="https://github.com/user-attachments/assets/88206b78-d75f-484b-8f7f-f1e8eb4d2ee0" />

<img width="296" height="121" alt="image" src="https://github.com/user-attachments/assets/045df697-80f5-49d9-ace6-7fb7ed1f9c15" />

By training a Decision Tree model using key service-related features, we find that Contract_Month-to-Month is the most important factor driving customer churn, followed by Internet Service: Fiber Optic. When further combined with customers who lack Online Security and Tech Support, the model uncovers a high-risk segment with a churn probability of 61%. This means that customers on month-to-month contracts who use fiber optic internet but do not have access to online security or technical support are significantly more likely to leave.

## Customer Segmentation
Although Objective 3 aimed to segment customers by churn risk using key features, no advanced data mining or clustering techniques (e.g., k-means or decision trees) were applied, instead segments were created through basic groupings and manual rule-based classification.

<img width="468" height="226" alt="image" src="https://github.com/user-attachments/assets/1404e304-8896-415f-99dd-a5144fdbc72c" />

# Conclusion 
This study shows how effective data mining methods can be in identifying and resolving client attrition.  Through the methodical use of techniques like rule-based segmentation, decision tree modeling, and feature importance analysis, we were able to glean valuable insights from what would otherwise be unprocessed consumer data.  These methods were essential for both determining the factors that contribute to churn and converting those discoveries into workable retention tactics.

Ultimately, this case study illustrates that data mining is not only a valuable analytical tool but also a practical one. It enabled us to move from raw customer records to strategic, insight-led decision-making. The techniques applied in this study provided clarity, direction, and evidence-based prioritization for churn reduction efforts.























