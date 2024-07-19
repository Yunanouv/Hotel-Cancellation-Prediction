# Hotel Cancellation Prediction
-------------------------------

## **Business Background**

According to the [Hospitality Net](https://www.hospitalitynet.org/opinion/4082318.html), there are four segments of the hospitality industry: Food and Beverages, Travel and Tourism, Lodging, and Recreation. **The hotel industry**, a key part of the lodging sector is highly competitive, with hotels striving to maintain high occupancy rates and maximize revenue frequently encounters the issue of booking cancellations by customers. Cancellations can disrupt operations, lead to revenue loss, create inefficiencies in resource allocation, and marketing cost. Casting a broad umbrella, it encompasses all economic and business activities that rely upon or contribute to travel and tourism.

The **Ruby Hotel**, a renowned four-star destination based in Portugal, **is currently grappling with a high rate of booking cancellations**. This challenge **impacts multiple facets of our operations and overall business strategy**. Cancellations disrupt operations, lead to significant revenue loss, create inefficiencies in resource allocation, and increase marketing costs.

To address these issues, Ruby Hotel’s management and various departments are seeking a data-driven solution. By understanding the factors leading to cancellations and predicting them accurately, we can mitigate these issues. Leveraging machine learning models to forecast cancellations will allow us to adopt proactive measures, optimize revenue management strategies, and manage hotel budgets more effectively.

This approach will help us maintain high occupancy rates, reduce financial impacts, and enhance the overall guest experience, ensuring that Ruby Hotel continues to set the standard for excellence in the hospitality industry.

 ----------------------------------
## **Business Problem**

**1. How to differentiate between customers likely to cancel their bookings and those who will proceed with their stay?**   
**2. How to predict which customers are more likely to cancel their bookings in advance?**   
**3. Which factors contribute the most to a customer deciding to cancel their booking?**   

* **Revenue Loss**   
Each cancellation represents a potential revenue loss, as the likelihood of rebooking the canceled room on short notice is low. This impacts the hotel's financial performance and overall revenue goals.   
* **Marketing Cost**   
Costs are incurred when a room is predicted to be canceled but is not, leading to potential additional marketing costs to re-engage customers who were predicted to cancel but actually did not need to be re-engaged. This unnecessary expenditure impacts the hotel's marketing budget efficiency and profitability.

## **Objectives**
**Mitigate Revenue Loss and Reduced Potential of Extra Marketing Cost**   
Proactively manage cancellations to reduce the financial impact because each cancellation represents a potential revenue loss.

**1. Revenue Loss due to Cancellations (Main Objective)**   
Booking cancellations directly impact a hotel's revenue stream. When a booking is canceled, especially on short notice, the likelihood of rebooking the same room decreases significantly. This leads to a direct loss in potential revenue that the hotel could have earned from that booking. The revenue loss due to cancellations is calculated based on the room rate and the number of canceled bookings.

**2. Extra Marketing Cost**
Additional marketing costs refer to the expenses incurred when a booking is predicted to be canceled but the customer ultimately does not cancel. In such cases, the hotel may initiate marketing efforts to retain the booking or re-engage the customer. These marketing activities could include personalized offers, discounts, or other incentives to persuade the customer not to cancel or to rebook if they have already canceled.

------------
## Problem Solving

### **Analytical Approach**
To address the business problem, we will use a machine learning model to predict booking cancellations (Classification). The analytical approach includes:

* **Data Collection and Preprocessing:** Collect historical data and preprocess it to handle missing values, outliers, and categorical variables.
* **Model Development:** Develop and train machine learning models to predict the probability of customers canceling their hotel booking.
* **Model Evaluation:** Evaluate the models using appropriate metrics to ensure they accurately predict cancellations and minimize false positives and false negatives.
* **Optimization:** Optimize the model to balance the trade-off between revenue loss and additional marketing costs. Identify key factors underlie the cancelation of hotel bookings as well.

### **Evaluation Metrics**

To evaluate the machine learning model, we will use **Recall** where our main target is to minimize the highest cost between revenue loss due to cancellation and marketing budget.

* Room price: $99 per night  
* Marketing budget comprised roughly 13.6% of a company’s total budget  

As per definition above, we will minimize the revenue loss due to cancellation (False Negative) which costs $99 per canceled booking.

### **Business Metrics**
To measure the success of the model, we will use **Revenue Loss** metrics as the **additional metrics** that will calculate:

* **Revenue Loss due to Cancellations**  
This metric calculates the financial impact of cancellations that were not predicted by the model, leading to potential revenue loss.
* **Extra Marketing Cost**  
This metric calculates the cost incurred from incorrectly predicting cancellations, leading to unnecessary marketing expenses.

A dataset containing historical hotel booking records, including information such as customer demographics, booking channels, room types, and reservation details will be utilized to build a predictive model.

*Note : The room price and marketing budget are based on assumption. Please refer to the reference on the last section*  

------------------
## Data Understanding and EDA

**Data Overview**

| Feature Name | Description |
| --- | --- |
|**country** | Country of origin |
|**market_segment** | Market segment designation. In categories, the term “TA” means “Travel Agents” and “TO” means “Tour Operators”  |
|**previous_cancellations** | Number of previous bookings that were cancelled by the customer prior to the current booking |
|**booking_changes** | Number of changes/amendments made to the booking from the moment the booking was entered on the PMS until the moment of check-in or cancellation |
|**deposit_type** |  Indication on if the customer made a deposit to guarantee the booking.  |
|**days_in_waiting_list** | Number of days the booking was in the waiting list before it was confirmed to the customer  |
|**customer_type** | Type of booking |
|**reserved_room_type** | Code of room type reserved. Code is presented instead of designation for anonymity reasons|
|**required_car_parking_spaces** | Number of car parking spaces required by the customer |
|**total_of_special_requests** | Number of special requests made by the customer (e.g. twin bed or high floor) |
|**is_canceled** | Value indicating if the booking was canceled (1) or not (0)|  

1. This hotel business has a large amount of customers, 83,573 records with 11 features. But 73,371 (87.79%) are duplicated. So, we have 10202 rows of data to be analyzed.
2. There are 1 columns containing null values, which is `country` features  
3. After exploring, the null and abnormal values will be analyzed more deeply to ensure our assumptions. We also need to check the unique value for categorical columns and other analysis
4. Overall, the charts show a heavy reliance on online travel agencies, a preference for certain room types (especially room type A), a significant majority opting for no deposit, and a predominant transient customer base.
5. Based on the normality test results and the skewness and kurtosis values, it's clear that none of the numerical features follow a normal distribution (all p-values are 0.0, indicating significant deviations from normality). Additionally, many features exhibit high skewness and kurtosis, suggesting they have extreme values or outliers.
6. This data is imbalanced.
  * Not Canceled Bookings: 7,788 bookings were not canceled (make up 76.34% of total bookings).   
  * Canceled Bookings: 2,414 bookings were canceled (constitute 23.66% of total bookings).

## Data Cleaning and Preparation   
1. Impute Missing values in Country
2. 
