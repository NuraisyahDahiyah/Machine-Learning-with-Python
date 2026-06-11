# Online Retail Purchasing Pattern
In this project, I used market basket analysis to identify purchasing patterns in an online retail dataset.

## Problem Statement 
Retailers who leverage customer purchasing behaviour data can potentially increase sales by up to 25%, yet many still struggle to optimize product placement and inventory management in the store. The root issues lie in retailers insufficient understanding in customer’s buying patterns leading to generic product displays and a one-size-fits-all approach that fails to personalize the customer’s shopping experience. To address this gap, this study employs the Association Rule Mining technique to identify frequent product combinations. This will help retailers optimise inventory, enhance cross-selling, and improve digital product layout.

By using Association Rule Mining, we will investigate customer’s purchasing patterns of an online retail store to identify frequent itemset and the presence of strong association rules. Findings from the analysis will be utilised to apply customer-centric strategies in marketing, optimised inventory management, and strengthen product recommendations.

## Objectives 
1. To apply the Apriori algorithm to identify frequent itemsets and uncover meaningful associations between products based on support, confidence, and lift.
2. To generate actionable insights from purchase patterns that support more effective product placement, inventory decisions, and marketing strategies.

## Data Pre-processing 
Data preprocessing is done to identify present issues in the dataset such as missing values and duplicate data. This is done by removing these missing and redundant data points to ensure data quality for better outcome and accuracy of the Apriori algorithm and Associate Rule Mining Technique implemented. Items are standardized (converted to lowercase and spaces are removed) to reduce inconsistencies because of formatting differences. Then, the data is transformed into a list of lists, each of which represents the goods a consumer has purchased in a single online transaction. This is so that the frequency of itemsets can be as accurately as possible determined by the Apriori algorithm.

<img width="509" height="95" alt="image" src="https://github.com/user-attachments/assets/f1ec4687-f9fc-47d8-94f7-f7e33c4f3154" />

## Frequent Itemsets Generation with Apriori Algorithm

To generate frequent itemsets for this online retail transaction, we will implement data transformation to convert the transaction data into one-hot encoded format and apply Apriori algorithm. This is then followed by visualisation of the distribution of the itemsets and the top frequent items. The Apriori algorithm is applied to on-hot encoded transactional data in which each column represents an item and each row a transaction. Setting a low support threshold is also crucial in capturing a wider range of item combinations, even the ones that are less common but still relevant to purchasing patterns. The distribution of itemset sizes depicts the plausible combinations items can be grouped together in purchases. These insights form the foundation for identifying popular product combinations and the customer's purchasing behaviours.

<img width="278" height="288" alt="image" src="https://github.com/user-attachments/assets/3dfca284-8e27-4a8c-9f7c-00f37d895a9f" />

<img width="280" height="295" alt="image" src="https://github.com/user-attachments/assets/5bc20499-e1a1-4a3f-aa47-9d043b744c6e" />

<img width="330" height="131" alt="image" src="https://github.com/user-attachments/assets/898db368-9016-412a-b61f-9ab1dd948802" />

## Associate Rules Based on Frequent Itemsets

Frequent Itemsets is used to create association rules and filter them depending on the support confidence and lift. Support is a measure of an item's default popularity that may be computed by dividing the total number of transactions by the number of transactions that contain a specific item. Suppose we want to find support for item B, this can be calculated as:

<img width="468" height="41" alt="image" src="https://github.com/user-attachments/assets/93b82a18-3b49-4a63-9338-22c16e1aad90" />

Confidence is the probability that, for instance, if item A is purchased, item B will also be purchased. It can be computed as the number of transactions in which A and B are purchased together, divided by the total number of transactions in which A is purchased. Mathematically, it can be represented as:

<img width="468" height="43" alt="image" src="https://github.com/user-attachments/assets/0f95ed92-0a7c-40e8-8ea4-c097c6c11008" />

Lastly, Lift refers to the increase in the ratio of, for example, sale of item B when item A is sold. It tells us that the likelihood of buying item B and item A together is XXX times more than the likelihood of just buying item B. Lift of greater than 1 means products A and B are more likely to be purchased together whereas a Lift of less than 1 indicates the two products are unlikely to be bought together. Lift can be computed  by dividing Confidence(A -> B) divided by Support(B). Mathematically it can be represented as:

<img width="468" height="43" alt="image" src="https://github.com/user-attachments/assets/ee7815f5-c6b0-47fc-aff7-5f58c06e2446" />

We examine these rules and visualise to spot insightful patterns and trends in the customer’s purchasing behaviour. To ensure that only the most dependable and practical rules are left, association rules a created by setting minimum tresholds for confidence and lift. Sorting by confidence and lift shows us the most valuable associations, and a scatter plot visually shows the relationship between support, confidence, and lift. High-lift, high-confidence rules are especially useful as they display strong connections between items. This can support retail strategies like personalised product recommendations. 

<img width="264" height="251" alt="image" src="https://github.com/user-attachments/assets/401ef3b7-a2c8-4cf9-bd9f-20b75665dd7e" />

<img width="286" height="93" alt="image" src="https://github.com/user-attachments/assets/03c7cc73-66b8-454b-b193-dd0f85d7a8fd" />

## Results
### Visualising Frequent Itemsets
The data is visualized using a histogram and barplot. The distribution of frequent itemset lengths as seen in Figure 10 reveals that most transactions consist of single-item purchases. In some cases, a half of the transactions included purchase of two items together, while longer combinations of itemset (3 or more) are less common within the online retail customers. This pattern suggests that customers primarily make focused purchases, likely buying individual needs or complementary items rather than collecting multiple unrelated products in a single order. 

The top 15 most frequent item combinations, illustrated in Figure 11 shows the specific items and groups of items that are purchased together often; these include ‘white hanging heart t-light holder’, ‘regency cake stand 3-tier’ and ‘baking set 9 piece retrospot’. ‘White hanging heart t-light holder’ is most popular as it is in 26% of all purchases with ‘regency cake stand 3-tier’ trailing closely behind as the second most popular item in 23% of all purchases. Overall, this bar chart gives a detailed view of online retail store’s best-selling products.

<img width="337" height="184" alt="image" src="https://github.com/user-attachments/assets/8cc02a3b-a4ba-48c2-a21f-79c432199979" />

<img width="334" height="170" alt="image" src="https://github.com/user-attachments/assets/9419b0b2-f1e9-4ab7-9d70-4238b7c420a4" />

### Visualising Association Rules
To visualise the association rules, we will focus on the relationships between support, confidence and lift. The relationship between the three is visualised using a scatterplot and heatmap. 

Figure 13 displays support on the x-axis and confidence on the y-axis, with point size and color representing lift. The plot shows that while rules with moderate to low support can show high confidence, those with strong support frequently show lower confidence. Interestingly, low support and confidence levels are where high-lift rules cluster, suggesting that while these item combinations are less often, they do show strong connections when they do occur.

A heatmap of the top 10 rules by lift as seen in Figure 14 gives a detailed view of the strongest rules. For example, the rule ‘poppy’s playhouse kitchen’ leading to ‘poppy’s playhouse bedroom’ produces the highest lift (13.0), indicating a strong association. The rule ‘regency cakestand 3 tier, roses regency teacup and saucer’ leading to ‘green regency teacup and saucer’ has a relatively lower lift (11.0), but still indicates a strong association. The color gradient shows lift values, darker colors represent lower lift and lights colors represent higher lift. 

<img width="297" height="187" alt="image" src="https://github.com/user-attachments/assets/3e93e903-3704-457e-85bf-729854c53a08" />

<img width="258" height="203" alt="image" src="https://github.com/user-attachments/assets/29d356ea-aa60-4c8c-bc34-8cc2c3af4f6f" /> 

## Results and Interpretation
The analysis revealed that most frequent itemsets consisted of single items, with 358 itemsets of length 1 and only a small number of larger itemsets. The top 5 items by support (frequency of occurrence in transactions) are:
•	White hanging heart T-light holder (Support: 26%)
•	Regency cakestand 3 tier (Support: 23%)
•	Baking set 9 piece retrospot (Support: 19%)
•	Assorted colour bird ornament (Support: 18%)
•	Heart of wicker small (Support: 16%)

Although the frequent itemset analysis revealed a large number of single-item purchases, the presence of multi-item sets—though limited in number—provided key insights into how customers make purchasing decisions. Among the top items by support, the White hanging heart T-light holder appeared in approximately 26% of transactions, making it a clear bestseller. Similarly, the Regency cakestand 3 tier, Baking set 9 piece retrospot, and Assorted colour bird ornament each appeared in roughly 18–23% of transactions. These numbers, though calculated from a reduced dataset (half the original due to size constraints), still indicate strong product appeal and repeated customer interest. The high support levels suggest that these products either meet a consistent functional or aesthetic need or benefit from prominent placement in the store, both physically and digitally.

Moving into association rules, what stands out is the exceptionally high confidence and lift values among specific product pairs. For example, customers who bought the Candleholder pink hanging heart also bought the White hanging heart T-light holder with 94.7% confidence and a lift of 3.59. This indicates not just a tendency, but a strong likelihood that these products are bought together intentionally. The lift value of 3.59 tells us that this purchase pattern happens 3.6 times more often than if the two items were bought independently. This strongly suggests a complementary relationship between the items, likely driven by matching themes or visual aesthetics.

In a similar vein, the Green regency teacup and saucer and the Pink regency teacup and saucer have a confidence of over 92% and a lift of 12.16, suggesting that when a customer chooses one, they very often want the other. This insight reflects consumer behavior that values completeness and coordination. From the customer’s perspective, this pattern hints at a desire for curated or harmonious designs, possibly for gifts, home décor, or personal use where style consistency is important.

It’s worth noting that these insights are drawn from only half of the original dataset, a necessary compromise due to data volume. As a result, there may be additional frequent patterns or rule structures in the full dataset that were not captured. 

## Ending Remarks
In this project, we used association rule mining to analyze transactional data from an online retail store and uncover patterns in how customers shop and what products they tend to buy together. The implementation of the Apriori algorithm revealed significant associations between products, such as the frequent co-purchase of Poppy’s Playhouse sets and Regency teacups. These patterns illuminate how customers naturally combine items, providing actionable opportunities for retailers to refine recommendations, curate targeted bundles, and optimize marketing strategies. Bundling often co-purchased products or displaying high-lift item pairings, for example, might increase average order values while simplifying the buying process.










































