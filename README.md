## North Point Software Listing Company

### North Point Software Listing Company Dataset File: [Click Here:](https://github.com/Priya07A/Analytics-Practicum/blob/main/North-Point%20List.csv)
```
library(dplyr)
library(ggplot2)
library(caret)
library(corrplot)
library(tidyr)
library(rpart)
library(C50)
library(readr)
library(car)
library(psych)
library(forecast)
library(rpart.plot)
library(plotly)
library(rattle)
library(coefplot)
library(gains)
library(e1071)
```
## Table of Contents
- [Introduction](#introduction)	
- [1.0 Business Problem](#10-business-problems-and-goals)	
  - [1.1 Business Problems:](#business-problem)	
  - [1.2 Analytics Goals:](#12-analytics-goals)
- [2.0 Data Exploration and Preprocessing](#20-data-exploration-and-preprocessing)
  - [2.1 Attributes Definition](#21-attributes-definition)
  - [2.2 Data Exploration](#22-data-exploration)
  - [2.3 Distribution of Variables](#23-distribution-of-variables)
- [3.0 Predictors Analysis and Relevancy](#30-predictors-analysis-and-relevancy)
- [4.0 Dimension Reduction](#40-dimension-reduction)
   - [PCA Analysis:](#pca-analysis)
- [5.0 Data partitioning method](#50-data-partitioning-method)
- [6.0 Classifier Models Selection and Model Performance](#60-classifier-models-selection-and-model-performance)
  - [6.1 Logistic regression model](#61-logistic-regression-model)
  - [6.2 Evaluating the logistic regression model Performance](#62-evaluating-the-logistic-regression-model-performance)
  - [6.3 Stepwise Regression Model](#63-stepwise-regression-model)
  - [6.4 Evaluating the Stepwise Backward model Performance](#64-evaluating-the-stepwise-backward-model-performance)
  - [6.5 Evaluating the Stepwise Forward model Performance](#65-evaluating-the-stepwise-forward-model-performance)
  - [6.6 K-NN Model](#66-k-nn-model)
  - [6.7 Evaluating K-NN model performance](#67-evaluating-k-nn-model-performance)
  - [6.8 Tree Model](#68-tree-model)
  - [6.9 Evaluating Tree model Performance](#69-evaluating-tree-model-performance)
  - [6.10 Naïve Bayes Model](#610-naïve-bayes-model)
  - [6.11 Evaluating Naïve Model Performance](#611-evaluating-naïve-model-performance)
- [7.0 Best Classifier Model Selection](#70-best-classifier-model-selection)
- [8.0 Regression Model Selection](#80-regression-model-selection)
  - [8.1 Linear Regression Model](#81-linear-regression-model)
  - [8.2 Evaluating Regression Model Performance](#82-evaluating-regression-model-performance)
  - [8.3 Stepwise- backward Regression](#83-stepwise--backward-regression)
  - [8.4 Evaluating Stepwise Backward Regression Model Performance](#84-evaluating-stepwise-backward-regression-model-performance)
  - [8.5 Regression tree](#85-regression-tree)
  - [8.6 Evaluating Regression tree model Performance](#86-evaluating-regression-tree-model-performance)
- [9.0 Best Regression Model Selection](#90-best-regression-model-selection)
- [10.0 Profit analysis](#100-profit-analysis)
  - [10.1 Gross profit](#101-gross-profit)
- [11.0 Conclusion](#110-conclusion)

### Introduction
North-point is a software company that sells games and educational software. In the beginning they manufactured their own software but currently they include other products apart from their own products. Additionally, North- point just joined a consortium by adding a 200,000-customer list. This is to pick out another 200,000 customers from the pool which has 500,000 customer list.
	North-Point selected 20,000 people and ran a test by mailing all the customers. This is to see how many customers are purchasing. Out of these 20,000 only 5.3%, that is 1,060 customers bought the products. For further analysis they took a list of 1000 purchasers and 1000 non- purchasers. Using this data, they want to predict estimated gross profit by adjusting the rate back by multiplying 0.106 with each case for the expected spending.

<div align="center">
 <img  alt="Picture1" style="max-width:100%;" src="https://github.com/Priya07A/Analytics-Practicum/assets/170826083/8d85fe8e-da82-4a4c-8126-4b631a003808">
    <p><b>Figure 2.2.1:</b> First Six Rows and dimension of the data</p>
</div>


#### Business Problem:
Optimize the process of customer classification to get the probability to identify the potential customers and enhance customer targeting strategy for North Point Software Company. This is achieved by developing models for customer classification as purchasers (1) or non-purchasers (0) and then predicting how much each purchaser spends. Then comparing the performances of different machine learning models and evaluating them. Also attempt to answer a few business questions that arise in further stages. Finally, providing some recommendations to North-Point on their customer classification and targeting methods. Also, to estimate the gross profit that the firm could expect from the remaining 180,000 observations (customers) if it selects them randomly from the pool. This involves calculating the potential revenue generated from purchases made by these customers and comparing it to the cost of mailing, which is $2 per customer, to determine the net profit.

##### Business Goal:
Identifying the potential customers. Ranking the customers. Even if the customer is not a purchaser there is still probability for that customer to purchase. So, finding potential customers is the business goal. Acknowledging that not all customers immediately make purchases, North-Point recognizes the importance of accurately pinpointing potential purchasers, as they represent valuable opportunities for future revenue growth. North-Point aspires to not only identify the likelihood of making purchases but also to anticipate their spending behavior. North-Point aims to refine its customer classification and targeting methods, thereby enhancing its competitive edge, and driving sustained growth in the dynamic software market landscape.

#### Analytics Goals:

The primary analytics goal is to develop two predictive models.
Purchase Classification Model: Identify potential customers likely to make a purchase based on historical data. Pinpoints the potential customers by giving probability.
Spending Prediction Model: For customers identified as potential purchasers, predict the amount they are likely to spend. This will enable North-Point to tailor its marketing strategies and promotions for better revenue generation.

###  Data Exploration and Preprocessing
#### Attributes Definition:
- **Sequence_number:** Unique number for each record.
- **US**: If customer location is in USA if yes 1 or else 0.
- **Source_a, source_b, source_c, source_d, source_e, source_m, source_o, source_h, source_r, source_s, source_t, source_u, source_p, source_x, source_w**:List of sources through which the customer is obtained. If yes 1 or else 0..
- **Freq**: Number of purchases made by customer. Customer loyalty can be predicted.
- **last_update_days_ago**: Recent interaction of the customer.
-	**1st_update_days_ago**: First interaction of the customer.
-	**Web order**: Helps in distinguishing normal and online purchases.
-	**Gender=male**: 0 for Female and 1 for male.
-	**Address_is_res**: Address type.
-	**Purchase**: If 1 then customer responded to the mail and bought. If 0 no response to mail.
-	**Spending**: Represents the amount of dollars spent if the customer purchased.
•	2000 rows with 25 columns. The dataset has a 2000 number of customer lists and the data from which they are sourced from. The dataset contains information such as, if the customer is male or female, is from US or not, how many days ago they were active, has made purchases from the web, how many dollars spent etc.
 
Table 6.2 Dimension of dataset
•	First 6 rows of the data: US, source(a-w), web order, gender= male, Address_is_res, Purchase are all categorical variables with binary representation (0/1). The remaining are numerical variables which represent values.
 
Table 6.3 Head of the dataset
Structure of data: There are 4 numeric variables. Those are Freq, last_update_days_ago, last_update_days_ago, Spending.
•	Remaining are categorical variables in binary. US, source a-w, Web order, Gender Male, Address is res, Purchase.
 
Table 6.4 Structure of the data.
•	Viewing Frequency for the Address_is_res.
The table indicates that very few customers have the residential address. So, we can assume that few customers order from outside the USA, few customers who don’t have residential address and there is chance that customer might be purchasing for people in different locations. 
 
Table 6.5 Count of Address_is_res.
6.b. IDENTIFYING MISSING VALUES: 
There are no missing values.
 
Table 6.6 Identifying missing values.
Zero values: If zero spending is possible for this case, then we can keep those rows, else we need to impute those rows with some values (maybe median, or mean (but mean is highly sensitive to outliers))
 
Table 6.7 Zero values
•	Dropping the sequence column since it is unique and represents the number of customers.
 
Table 6.8 Dropping the sequence_number.
6.c. IDENTIFYING OUTLIERS: 
•	Box plot for Frequency:
 
Figure 6.1 Boxplot of frequency
•	Box plot for Last update days ago: The median here is slightly lower when compared to the first updated days ago. 
 
Figure 6.2 Boxplot for Last update days ago
•	Box plot for First update days ago: The median is high compared to the last update days ago.
 
Figure 6.3 Box plot for First update days ago
•	Boxplot for spending: Most of the observations fall under Quartile 3. Line represents median. No observations in quartile 1.
 
Figure 6.4 Boxplot for spending
Boxplot of Purchase status
 
            Figure 6.5 Boxplot of purchase status
There are outliers in the data. But it seems irrelevant to remove the outliers. To keep the data balanced. Important information might get lost if we remove the outliers.

#### Data Exploration:


###  Predictors Analysis and Relevancy


### 4.0 Dimension Reduction


#### PCA analysis:


### Data partitioning

#### Data Partition:


### Predictive model Selection
# 1. Classification


#### Logistic regression model:

####  Evaluation:

###### Step AIC Logistic Regression:
####  Evaluation:

##### Decision tree using C5.0
####  Evaluation:

#### Decision tree using C5.0 (Trials = 7)
####  Evaluation:

#### Decision tree using C5.0 (Trials = 10)
####  Evaluation:

#### K-NN Model (K = 29)
####  Evaluation:

#### K-NN Model (K = 35)
####  Evaluation:

#### K-NN Model (K = 45)
####  Evaluation:



### Best Classifier Model Selection


# 1. Regression

#### Multi Linear Regression Model
####  Evaluation:

#### Stepwise- backward Regression
####  Evaluation:

#### Stepwise- forward Regression
####  Evaluation:

#### Regression tree
####  Evaluation:

### Best Regression Model Selection

#### Holdout data predictions
.

#### Cummulative gains chart

# Decile-wise lift chart

### Profit analysis


### Conclusion

