# Traffic Accident Severity Prediction in Addis Ababa

Traffic accidents cause roughly 1.3 million annual deaths globally, heavily impacting developing urban areas like Addis Ababa, Ethiopia, where rapid growth and weak infrastructure lead to frequent collisions. Predicting accident severity is vital for improving city safety and allocating emergency resources effectively. Because traditional awareness campaigns and manual reporting cannot handle the unpredictable complexity of modern traffic, leveraging data mining and machine learning to analyze data patterns offers a much more powerful solution.

## Project Objective 

Road traffic accidents are a growing safety challenge in Addis Ababa, but the lack of an analytical framework means existing data is underutilized, forcing safety and emergency interventions to be reactive rather than proactive.

1.	Develop an ML model to classify Addis Ababa accident severity as slight, serious, or fatal.
2.	Identify critical risk factors linked to severe accidents using data analysis and feature importance.
3.	Provide actionable recommendations for emergency services and urban planners to implement accident countermeasures.

## Dataset Overview

Includes 32,000+ records and represents a single traffic accident case and contains both categorical and numerical attributes. The dataset was originally published to support research in road safety, policy development, and urban transportation planning. Understanding the factors most strongly associated with fatal, serious, or slight accidents can help authorities implement more effective preventive strategies. 

<img width="476" height="175" alt="image" src="https://github.com/user-attachments/assets/e8aacfe3-bbf2-4929-b238-ae4456582d7f" />

<img width="304" height="149" alt="image" src="https://github.com/user-attachments/assets/024f4187-6a12-4736-a02a-055bf0fc7596" />

## Exploratory Data Analysis (EDA)
**Severity Distribution**

<img width="299" height="284" alt="image" src="https://github.com/user-attachments/assets/8065cb9f-277e-46d4-8fe8-36adcddf0496" />

**Number of Vehicles Involved by Accident Severity**

<img width="456" height="213" alt="image" src="https://github.com/user-attachments/assets/d20c2e77-c3c2-4d33-825f-94c5fae57294" />

**Cause of Accident vs Severity**

<img width="465" height="236" alt="image" src="https://github.com/user-attachments/assets/061f5b06-5e51-4a11-a582-6adc8d8d373d" />

**Vehicle Type vs Severity**

<img width="420" height="218" alt="image" src="https://github.com/user-attachments/assets/3ac9b6e5-f8ea-4e40-8ccd-85f145e32a5f" />

## Pre-Processing Techniques 

The dataset required complex cleaning due to structural flaws like missing data, "Unknown" labels, high cardinality, inconsistent column naming, and a target variable heavily skewed toward "Slight" accidents. Systematically resolving these issues was essential to reduce noise, eliminate bias, and improve overall model performance.

**Handling Missing Values**

Missing data was handled strategically based on importance to ensure unbiased model training. Low-importance columns with substantial missing entries were deleted entirely. For critical features, missing gaps were filled using mode imputation (the most common value) to maintain data quality without distorting the data distribution.

<img width="489" height="258" alt="image" src="https://github.com/user-attachments/assets/b102f0bd-0af5-4fb1-8730-95108ef4aac0" />

**Standardising Time Features**

To diminish noise and eliminate potential bias, time-related fields required systematic transformation into their corresponding standard datetime formats.

1. Time (Lighting Condition): Changed from "Day" or "Night" into numbers, where Day is 0 and Night is 1.
2. Driver's Age: Grouped into ranked numbers based on how old the driver is: 0 (<18), 1 (18-30), 2 (31-50), 3 (>51)
3. Driving Experience: Ranked from 0 to 5 based on years of experience, starting at 0 for "No License" and going up to 5 for "Above 10 years" to show progression in driving skill.
4. Accident Severity (Target Variable): 0 (Slight Injury), 1 (Serious Injury), 2 (Fatal Injury)
   
<img width="468" height="104" alt="image" src="https://github.com/user-attachments/assets/9cae9ef4-7b7b-495e-b91f-40026a4448a8" />

**Feature Engineering**

New features were engineered from domain knowledge and available attributes to add more power and context to the dataset

1. Is_Weekend: Whether accident took place Saturday or Sunday as driver behavioura nd traffic patterns are likely to be different on weekdays vs weekends
2. Night_Condition: Appended using Time column where accidents during night (1) and accidents during daylight (0) to account for impact of visibility and lighting
3. Traffic_Complexity: Combination of Type_of_collision, Types_of_Junction, and Vehicle_movement then converted into numbers using Label Encoder

<img width="476" height="87" alt="image" src="https://github.com/user-attachments/assets/763e5bb9-00a1-4eee-990f-789fd188666b" />

# Data Mining Techniques 

The data was split into an 80% training set and a 20% testing set using stratified sampling, which keeps the mix of accident types even across both groups. Finally, the features were normalized using StandardScaler so that models sensitive to number sizes could make fair and steady predictions.

2. Decision Tree Model
3. Random Forest Classification Model
4. Logistic Regression Model 

# Results & Model Validation 

The dataset was highly imbalanced, with 83% slight, 14% serious, and only 1.3% fatal cases. Such imbalance causes models to favour the majority class, resulting in high accuracy but poor detection of minority classes. 

To mitigate this issue, SMOTE was applied to generate synthetic minority class samples, while class weighting increased the importance of minority classes during training. Model performance was evaluated using macro-averaged F1-score and recall instead of accuracy alone, as these metrics provide a fairer assessment for imbalanced classification problems. Feature importance analysis was also performed to identify the variables contributing most to each model's predictions.

**Decision Tree Model**

A Decision Tree Classifier was implemented as the baseline model to predict accident severity. The tree primarily split on the number of vehicles involved, followed by factors such as light conditions, number of casualties, and weather conditions. Due to the class imbalance, the model predominantly predicted the "Slight" class, with very few branches classifying fatal cases.

<img width="482" height="264" alt="image" src="https://github.com/user-attachments/assets/307c9308-2fa6-4d0f-95f3-a5018f447198" />

The model achieved an accuracy of 78.50%, with a Class 0 Recall of 13.00% and F1-score of 13.00%. Although it classified the majority class reasonably well, the confusion matrix showed that many serious and fatal cases were misclassified as slight, indicating poor performance in detecting minority classes.

<img width="452" height="342" alt="image" src="https://github.com/user-attachments/assets/ac757b56-6e93-4688-8690-a6e81558a499" />

**Random Forest Classification Model**

The Random Forest Classifier was implemented to improve prediction performance by combining multiple decision trees. Feature importance analysis identified Cause of Accident, Type of Vehicle, and Day of Week as the most influential predictors, followed by driver demographics, vehicle movement, and road layout, highlighting the complex factors affecting accident severity.

<img width="490" height="180" alt="image" src="https://github.com/user-attachments/assets/9d88e84b-9517-47d8-8f89-52e85dd487d2" />

<img width="394" height="308" alt="image" src="https://github.com/user-attachments/assets/bb140a6e-3822-4a15-83a0-b1dcd5e628dc" />

The model achieved an accuracy of 84.60%, with a Class 0 Recall of 65.00% and F1-score of 68.00%. Compared to the Decision Tree, Random Forest substantially improved the detection of minority class cases while maintaining high accuracy, demonstrating better generalization and greater robustness to class imbalance.

<img width="452" height="342" alt="image" src="https://github.com/user-attachments/assets/3f39608d-669c-4627-99a7-0f60882970c5" />

**Logistic Regression Model**

A Logistic Regression model was implemented using the same standardized dataset to classify accident severity. Feature importance based on coefficient magnitude showed that Number of Vehicles Involved and Number of Casualties were the strongest predictors, followed by incident time, age bands, and collision type. Environmental factors such as weather and light conditions had relatively lower influence.

<img width="495" height="155" alt="image" src="https://github.com/user-attachments/assets/068d55d2-4ca8-4dd8-b8c6-5da18dd633bd" />

<img width="346" height="206" alt="image" src="https://github.com/user-attachments/assets/c8f423be-1e65-49fd-bafd-a2b914f88043" />

The model achieved the highest overall accuracy of 84.65% but performed poorly on the minority class, with a Class 0 Recall of 6.38% and F1-score of 11.54%. The confusion matrix showed that most serious and fatal cases were classified as slight, reflecting the model's bias toward the majority class and its limited ability to capture the non-linear relationships present in the data.

<img width="452" height="342" alt="image" src="https://github.com/user-attachments/assets/02034b0d-2c52-4783-adb0-25f901df6bd2" />

## Limitiations and Improvements

**Limitations**

1. The models achieved 78–85% accuracy, but multiclass classification is inherently more difficult than binary classification
2. Although SMOTE and class weighting were applied, the severe class imbalance limited model performance, as synthetic samples may not fully capture real-world data distributions

**Improvements**

1. Implement XGBoost, which has demonstrated 88–91% accuracy in similar accident severity prediction studies
2. Apply class-weighted XGBoost to assign greater importance to minority classes, particularly fatal accidents
3. Use feature-guided SMOTE to generate synthetic samples based on the most important features identified by XGBoost
4. Perform strategic undersampling of the majority class after SMOTE to further reduce class imbalance while preserving meaningful data patterns

# Ending Remarks

This study demonstrated the effectiveness of supervised machine learning models in predicting road traffic accident severity in Addis Ababa. Among the three models evaluated, Random Forest achieved the best overall performance by balancing high accuracy with improved detection of minority classes. The findings show that proper data preprocessing, feature engineering, and model selection can significantly enhance accident severity prediction, providing valuable insights for emergency response planning and road safety initiatives. Future work should focus on implementing advanced models such as XGBoost, improving class imbalance handling, and incorporating real-time spatial and weather data to further strengthen prediction performance.






