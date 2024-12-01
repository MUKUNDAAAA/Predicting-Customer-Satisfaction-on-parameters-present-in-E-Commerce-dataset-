# Predicting-Customer-Satisfaction-on-parameters-present-in-E-Commerce-dataset

Project Overview
This project aims to analyze various aspects of an e-commerce dataset to predict customer satisfaction and derive actionable insights. The analysis covers revenue trends, order patterns, product reviews, and customer satisfaction prediction using machine learning models. The insights gained from this analysis can help optimize business strategies, improve customer satisfaction, and enhance operational efficiency.

Revenue Analysis
From the metrics, we observe that revenue generally increases over time, albeit with some fluctuations. Notably, there was a sudden spike in revenue from October to November 2017, followed by a significant dip in the subsequent month. This pattern suggests a potential seasonal or promotional influence on sales during this period.

Upon further analysis, it appears that there was a significant spike in revenue on 24 November 2017, which aligns with Black Friday, a significant shopping event. This indicates a strong correlation between the holiday season and increased customer activity.

To optimize resource allocation for future peak seasons, a strategic approach can be implemented to dynamically scale computing resources. By scaling instances during periods of high demand, such as Black Friday, the system can handle increased traffic and prevent performance degradation. This proactive measure ensures a seamless customer experience and maximizes revenue potential.

Order Analysis
The analysis suggests that the majority of orders are placed during the evening hours (4 PM to 12 AM), indicating a preference for late-night shopping.
While there is a noticeable difference in order volume between weekdays and weekends, a definitive pattern is not evident.
A comparison of 2017 and 2018 reveals a significant increase in orders, demonstrating the company's year-over-year growth.
Certain states exhibit a higher percentage of delayed orders compared to others, necessitating a deeper investigation into the underlying causes of delays in these specific regions.
It is recommended that the company conducts a comprehensive review of its logistics and delivery operations in the states with significant delays. By identifying bottlenecks and inefficiencies, the company can optimize delivery times, ensuring timely fulfillment and enhancing operational efficiency in these regions.

The analysis has revealed a strong correlation between delayed orders and reduced customer satisfaction, as evidenced by lower satisfaction scores in customer reviews from these states. Addressing these delays is crucial to improving customer satisfaction and fostering positive customer relationships.

Product Reviews
The analysis enables the derivation of valuable insights into product categories by taking the state as an input parameter. This method effectively identifies the top five best-selling products and the top five products with the highest review scores within a given region.

Top 5 Sold Products in State (SP)
Top 5 Reviewed Products with Average Rating
Bottom 5 Reviewed Products

Based on these insights, the company can provide targeted product suggestions to customers, highlighting products that are popular in their specific region. This approach enhances customer engagement by aligning recommendations with local buying trends.

Additionally, the analysis highlights products with lower average review scores. The company can focus on these products to understand the underlying causes of dissatisfaction. By investigating and addressing these issues, the company can enhance product quality and customer satisfaction, ultimately strengthening the brand's reputation.

Predicting Customer Satisfaction
Data Cleaning and Preprocessing
Removed Missing Values: Used .dropna() to remove rows with missing values in the orders_df.
Removed Duplicates: Used .dropDuplicates() on order_id in order_items_df to ensure each order ID has unique entries.
Filled Missing Values: Replaced null values in the review_comment_message column with an empty string '' using .fillna().
Converted Date Columns: Transformed order_purchase_timestamp, order_delivered_customer_date, order_delivered_carrier_date, and order_estimated_delivery_date columns to a uniform date format for consistency using to_date.
Created Positive Review Indicator: Added a column is_positive_review to identify reviews with a score of 5 and a non-empty review comment.
Encoded Customer Satisfaction: Introduced a binary target column customer_satisfaction to label scores above 4 as satisfied (1), otherwise not satisfied (0).
Feature Engineering
Delivery Time Calculation: Added a delivery_time column to compute the difference (in days) between order_delivered_customer_date and order_purchase_timestamp using datediff.
On-Time Delivery Indicator: Created a binary feature delivered_on_time to indicate whether the delivery occurred on or before the order_estimated_delivery_date.
Shipped on Time: Added a column shipped_on_time to check if the order_delivered_carrier_date was before or equal to the shipping_limit_date.
Joined DataFrames: Combined order_reviews_df, orders_df, order_items_df, and order_payments_df using successive .join() operations on the order_id.
Dropped Rows with Missing Values: Ensured all rows in the final dataset had complete data using .dropna().
Feature Transformation
Excluded Target Variable: Excluded customer_satisfaction (the target) from the feature set.
Vector Assembler: Combined the selected features into a single feature vector using VectorAssembler with inputCols as the selected features and outputCol as "features".
Model Building and Evaluation
Random Forest Classifier: Used a RandomForestClassifier with 100 trees (numTrees=100) to predict customer_satisfaction based on the engineered features.
Train-Test Split: Split the dataset into 80% training and 20% testing using .randomSplit().
Accuracy: Used MulticlassClassificationEvaluator with the accuracy metric to evaluate overall prediction accuracy.
Precision: Evaluated the weighted precision score across all classes.
Recall: Computed the weighted recall score, measuring the proportion of correctly identified instances of each class.
F1 Score: Calculated the F1 Score, which balances precision and recall.
Customer Retention Strategy Based on Previous Analysis
Based on our predictive modeling, we have identified customers who are likely to discontinue their engagement with our company. To mitigate this risk and enhance customer retention, we propose the following strategic initiatives:

Targeted Promotions: Focus on providing personalized promotions to at-risk customers. By offering tailored incentives, we can improve customer loyalty and reduce churn.
Product Recommendations: Utilize data analytics to identify trending products with high review scores in the customer's state or region. These products should be highlighted and recommended to customers, leveraging their proven popularity and satisfaction metrics.
Optimized Communication: Based on previous analyses, the evening is the most effective time for customer engagement. Therefore, we recommend scheduling notifications and promotions through our app to reach customers during this peak period, maximizing the likelihood of interaction and purchase.
Enhanced Delivery Strategy: Develop a comprehensive strategy to ensure timely delivery of products to these customers. By focusing on improving delivery times, we can significantly boost customer satisfaction, leading to increased revenue and customer retention.
Implementing these strategies will not only help retain customers but also strengthen our market position by building trust and loyalty among our customer base.

Scalability Considerations for Data Analytics and Modeling
As our dataset spans approximately 20 months and continues to grow, it is crucial to ensure our data analytics and modeling processes remain efficient and scalable. By leveraging Apache Spark, we can maintain robust data analysis capabilities with minimal impact on processing time, even as the dataset expands over several years. Spark's distributed computing framework allows us to employ distributed modeling techniques, significantly enhancing model performance and scalability.

Furthermore, all raw data is securely stored in a data lake. This architecture is inherently scalable, accommodating increasing volumes of data seamlessly. The data lake's flexible storage capacity ensures that as our data grows, it can be efficiently managed and accessed for analytics.

Data ingestion is facilitated by Apache Kafka, a scalable messaging system designed to handle high-throughput data streams. Kafka's ability to efficiently manage large volumes of real-time data ensures that our data pipeline remains robust and responsive, supporting our analytics infrastructure.

By integrating these technologies, we ensure that our data analytics and modeling processes are well-equipped to scale alongside our expanding dataset, maintaining performance and accuracy.
