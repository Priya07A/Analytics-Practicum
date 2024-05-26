## North Point Software Listing Company

### North Point Software Listing Company Dataset File: [Click Here:](https://github.com/Mahendra710/Analytical-Practicum/blob/main/North-Point%20List.csv)
```
# Load the necessary packages
library(readr)
library(ggplot2)
library(reshape2)
#install.packages("corrplot")
library(corrplot)
# install.packages("GGally")
library(GGally)
library(dplyr)
library(factoextra)
library(caret)
#install.packages("rpart")
library(rpart)
library(rpart.plot)
library(e1071)
library(forecast)
library(gains)
library(gridExtra)
```
## Table of Contents
- [Introduction](#introduction)	
- [1.0 Business Problems and Goals](#10-business-problems-and-goals)	
  - [1.1 Business Problems:](#11-business-problems)	
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
The North Point Software Company is a firm that sells games and educational software. The company wants to expand its customer base, so they join the group name consortium. This group specializes in computer hardware and software products. Every member of the group shares their customer list in a pool, and they receive the same number of customers from the pool. The North Point Software Company shared 200,000 names in the pool, for a total of 5,000,000 names in the pool. The company picked 20,000 names and did a test mailing. Out of the 20,000 customers listed, 1065 purchased after receiving mail, with a response rate of 0.053, or 5.3%. So, the company made a list of 1000 purchasers and 1000 non-purchasers (a response rate of 0.5 or 50%) to build the best prediction model. While using the prediction model in the pool, the purchase rate needs to be adjusted back down by multiplying each “case’s probability of purchase” by 5.3/50, or 0.106. The company is allowed to use a prediction model in the pool (5,000,000), so they can select the top 180,000 customers from the pool. The study will use the models to identify the purchasers and predict their spending behaviours to maximize gross profit and the customer base.

### 1.0 Business Problems and Goals
#### 1.1 Business Problems:
The company's primary objectives are to expand its customer base and enhance profit. After paying $2 for mail, the company wants to know if the customer will make a purchase or not. The business also wants to know if the customers are purchasers and how much they are going to spend on software or games. The company believes that they can apply the models to the pool of 5,000,000 customers. The company needs to rank those customers from the pool based on the original purchase rate (adjusted probability: 0.106) and adjusted probabilities.
The aim of maximizing gross profit while maintaining cost-effectiveness led to the decision to focus on the top customers rather than all customers. This target is based on the knowledge that the greatest returns on investment will come from concentrating on the top customers who are most likely to make purchases.
The business can maximize profit and expand its customer base by focusing its efforts on the most promising customers.
#### 1.2 Analytics Goals:
The main goal of the North Point Software Company is to select all the potential customers from the pool to expand their business. The company aims to build prediction models that classify the customer as a purchaser or non-purchaser after receiving mail and their spending behaviors. Based on what the remaining 180,000 customers might spend on games and software, the company hopes to estimate the gross profit from them. By ranking all the customers from the pool, the company wants to use higher probabilities of spending customers to maximize their gross profit and the remaining average or lower probabilities of spending customers to make more cost-effective strategies.
### 2.0 Data Exploration and Preprocessing
#### 2.1 Attributes Definition:
- **Sequence_number:** It shows the distinct number or index associated with every record in the dataset.
- **US**: This column indicates whether the customer is located in the United States or not. It is likely a binary variable, with 1 representing customers from the US and 0 representing customers from other countries.
- **Source_a, source_b, source_c, source_d, source_e, source_m, source_o, source_h, source_r, source_s, source_t, source_u, source_p, source_x, source_w**: These columns likely represent different sources or channels through which customers were acquired. Each column may contain binary values (0 or 1) indicating whether a particular source was used to acquire the customer.
- **Freq**: This column represents the frequency or number of purchases made by the customer. It is likely a numeric variable that indicates the count of purchases.
- **last_update_days_ago**: This column may indicate the number of days that have passed since the last update or interaction with the customer's data.
-	**1st_update_days_ago**: It may represent the number of days that have passed since the first update or interaction with the customer's data.
-	**Web order**: This column may indicate whether the purchase was made through a web order or not. It could be a binary variable with 1 representing a web order and 0 representing other types of orders.
-	**Gender=male**: This column may indicate the gender of the customer, with a binary value of 1 representing male and 0 representing female or other genders.
-	**Address_is_res**: This column may indicate whether the customer's address is residential or not. It could be a binary variable with 1 representing a residential address and 0 representing a non-residential address.
-	**Purchase**: This variable indicates whether a prospect responded to the test mailing and made a purchase. It is likely a binary variable with values like 0 or 1, where 0 represents no purchase and 1 represents a purchase.
-	**Spending**: For those prospects who made a purchase (Purchase = 1), this variable represents the amount they spent. It is likely a numeric variable that indicates the monetary value of the purchase.

#### 2.2 Data Exploration:
- Data exploration helps to get the value inside of the dataset. First, the dataset is typically loaded using the 'read_csv' function. With the “head ()” function, which shows the first six rows and dimension of the dataset (Figure 2.2.1). In the dataset, there are 2000 rows (records) and 25 columns (attributes) stored as ‘North_Point_List’. The target variables are “Purchase” and “Spending” which show whether a customer made a purchase or not after receiving mail and how much amount (in dollars) a customer spent.
``` R Code:
#Load the dataset
North_Point_List <- read_csv("G:/Webster/Analytical Practicum/Final/North-Point List.csv")
North_Point_List <- data.frame(North_Point_List)

#First Six rows 
head(North_Point_List)
#the dimension of the data
dim(North_Point_List)
```
<div align="center">
    <img src="https://github.com/Mahendra710/Analytical-Practicum/assets/83266654/9e940f13-f4cd-4f56-82a2-c94a7634ef6d" alt="Summary" style="max-width:100%;">
    <p><b>Figure 2.2.1:</b> First Six Rows and dimension of the data</p>
</div>

- Figure 2.2.2 displays the column names of the dataset which includes sequence number, US, different sources, freq (frequency), last update days ago and 1st update days ago, web order, Gender=male, Address is res (US), Purchase, and Spending.
```
#colnames of the dataset
colnames(North_Point_List)
```
<div align="center">
    <img src="https://github.com/Mahendra710/Analytical-Practicum/assets/83266654/b636279c-f9a7-4f27-bc86-008c2544171c"
 alt="Summary" style="max-width:100%;">
    <p><b>Figure 2.2.2:</b> Columns names of the dataset</p>
</div>

- Summary statistics provide an overview of the dataset including mean, median, minimum, maximum,1st Quartile, and 3rd Quartile. In the summary of the dataset (figure: 2.2.3), the company got customers from various sources and the majority of the customers are from the US. However, there are very few customers whose addresses are residential (mean: 0.221). From all the sources, the company got the highest number of customers from source_e (mean: 0.151) and the lowest number of customers from source_p (mean:0.006). The average spending amount by the customers is $102.6 with minimum spending $0 and maximum spending $1500. Also, some variables are related to customer behaviors like frequency (the number of purchases), last_update_days_ago, and spending.
```
#Summary of the data
summary(North_Point_List)
```
<div align="center">
    <img src="https://github.com/Mahendra710/Analytical-Practicum/assets/83266654/8c471399-6958-4fcf-8a92-5ab88c749479"
 alt="Summary" style="max-width:100%;">
    <p><b>Figure 2.2.3:</b> Summary of the data </p>
</div>

- Figure 2.2.4 shows that the data types for all the variables are numeric. In the dataset, the Sources, US, Web Order, Gender=male, Address_is_res, and Purchase columns have categorical data where 0 represents ‘no’ and 1 represents ‘yes’.
```
#the data types of the variables
str(North_Point_List)
```
<div align="center">
    <img src="https://github.com/Mahendra710/Analytical-Practicum/assets/83266654/0a22932c-77d3-40aa-bff5-c38504868934"
 alt="Summary" style="max-width:100%;">
    <p><b>Figure 2.2.4:</b> Data Types of the Variables </p>
</div>

- Missing values in the dataset give information about fake transactions or other information. However, checking the missing values in the dataset, figure 2.2.5 shows that there is no missing value in the dataset. This means all the transaction data and other information (e.g., sources, gender=male, address) are correctly collected.
```
#seeing the missing values
colSums(is.na(North_Point_List))
```
<div align="center">
    <img src="https://github.com/Mahendra710/Analytical-Practicum/assets/83266654/4468ec0e-4abe-4dd3-a59b-7ecf0a8c49e0"
 alt="Summary" style="max-width:100%;">
    <p><b>Figure 2.2.5:</b> Checking the missing Values </p>
</div>

- When it comes to checking the zeros in the dataset (Figure 2.2.6), there are 999 zeros in spending, which means there are 1001 customers who spent money, but there are only 1000 customers who purchased after receiving a mail. This might be happening due to a web order or a customer making an offline transaction. Also, 951 zeros in gender columns show that 951 customers are females and 1049 are males.
```
#check for zero
colSums(North_Point_List==0)
```
<div align="center">
    <img src="https://github.com/Mahendra710/Analytical-Practicum/assets/83266654/2c048367-b766-4d9d-8037-7e097562752c"
 alt="Summary" style="max-width:100%;">
    <p><b>Figure 2.2.6:</b> Check for the Zero’s </p>
</div>

#### 2.3 Distribution of Variables
- The Distribution of Purchase graph (Figure 2.3.1) shows that 1000 customers made purchases and 1000 customers didn't make any purchases after receiving a mail from the company. The distribution of gender (Figure 2.3.1) shows that male customers are more than female customers.
```
# Distribution of 'Purchase'
ggplot(North_Point_List, aes(x = Purchase)) +
  geom_bar(fill = "grey", color = "black") +
  theme_minimal() +
  labs(title = "Distribution of Purchase",
       x = "Purchase",
       y = "Frequency")

#Distribution of Gender
barplot(table(North_Point_List$Gender.male), main = "Distribution of Gender= Male", xlab = "Gender", col = "grey", border = "black")
```
<div align="center">
    <img src="https://github.com/Mahendra710/Analytical-Practicum/assets/83266654/d62c5206-a0a6-4771-bbc5-155d2c435235"
 alt="Summary" style="max-width:100%;">
    <p><b>Figure 2.3.1 :</b> Distribution of Purchase and Gender=Male</p>
</div>

- The distribution of the number of transactions graph (Figure 2.3.2) shows that approximately 375 customers didn’t make any transactions, and around 875 customers made one transaction. There are very few customers who have made more than five transactions.
```
  #Distribution of the no of transaction
ggplot(North_Point_List, aes(x = Freq)) +
  geom_bar(fill = "grey", color = "black") +
  theme_minimal() +
  labs(title = "Distribution of the No of transactions",
       x = "No of transactions",
       y = "Frequency")
```
<div align="center">
    <img src="https://github.com/Mahendra710/Analytical-Practicum/assets/83266654/53db4449-7110-4ed0-af59-c5f5089a2461"
 alt="Summary" style="max-width:100%;">
    <p><b>Figure 2.3.2 :</b> Distribution of the No of transactions </p>
</div>

- Figure 2.3.3  shows many of the customers who made a purchase through the mail and spent between 0 and 500 dollars. There are very few customers who have purchased more than $500. So, the company should know that many new customers would spend between 0 and 500 dollars. Some of the customers who spend $0 show that the company might give them free games or software.
```
#Distribution of Spending
hist(North_Point_List$Spending, main = "Distribution of Spending amount", xlab = "Spending", col = "grey", border = "black")
```
<div align="center">
    <img src="https://github.com/Mahendra710/Analytical-Practicum/assets/83266654/7875f5a3-d3e0-4b9e-9b2d-6c8e952479da"
 alt="Summary" style="max-width:100%;">
    <p><b>Figure 2.3.3 :</b> Distribution of Spending amount </p>
</div>

- The distribution of the web order (Figure 2.3.4) shows that around 800 customers made a purchase through the web order, and around 1200 customers didn’t make a purchase through the web order. This shows that the majority of the company’s purchases come through other types (e.g. offline).
```
#Distribution of Web order
barplot(table(North_Point_List$Web.order), main = "Distribution of Web Order", xlab = "Web Order", col = "grey", border = "black")
```
<div align="center">
    <img src="https://github.com/Mahendra710/Analytical-Practicum/assets/83266654/ea98a8e2-d29b-426a-ad3f-29acf64ca212"
 alt="Summary" style="max-width:100%;">
    <p><b>Figure 2.3.4 :</b> Distribution of Web Order </p>
</div>

- Figure 2.3.5 shows the distribution of US addresses and residences. Most of the customers are from the US, but not their residence. So, if a few of the customers are from outside of the US, they might purchase through the web order.
```
#Distribution of US
barplot(table(North_Point_List$US), main = "Distribution of US address", xlab = "US address", col = "grey", border = "black")

#Distribution of US Residence
barplot(table(North_Point_List$Address_is_res), main = "Distribution of US Residence", xlab = "US Residence", col = "grey", border = "black")
```
<div align="center">
    <img src="https://github.com/Mahendra710/Analytical-Practicum/assets/83266654/96271a61-2382-457b-9a53-95bfd7ae0893"
 alt="Summary" style="max-width:100%;">
    <p><b>Figure 2.3.5 :</b> Distribution of US addresses and US Residence </p>
</div>

### 3.0 Predictors Analysis and Relevancy
- The correlation matrix gives an analysis of the relationship between predictors and target variables. From the correlation plot (Figure 3.0.1), spending and frequency have a strong positive relationship, which suggests a customer who makes more transactions spends more. The target variable spending and the predictors last_update_days_ago and Xst_update_days_ago have a weak relationship, which means they are not strongly correlated. The target variables ‘Purchase’ and ‘Spending’ have a negative relationship with ‘last_update_days_ago’, which shows that the higher number in 'last_update_days_ago' has less chance or no purchase and spending. Last_update_days_ago and X1st_Update_days_ago have highly strong relationship with each other which may affect on modelling.
```
#correlation matrix
correlation_matrix <- cor(North_Point_List[, c("Freq", "last_update_days_ago", "X1st_update_days_ago","Purchase", "Spending")])
corrplot(correlation_matrix, method="number")
```
<div align="center">
    <img src="https://github.com/Mahendra710/Analytical-Practicum/assets/83266654/0bc396d3-c2e3-4e56-9de9-662c6857724a"
 alt="Summary" style="max-width:100%;">
    <p><b>Figure 3.0.1 :</b> Correlation matrix plot  </p>
</div>

- From the matrix and pairwise plots (Figure 3.0.2), for the predictors, more than 10 frequencies (10-time transactions) show more than $1,000 in spending, which shows a strong correlation between spending and frequency. Also, more than 5 frequencies show that customers purchased after receiving mail, and frequencies between 0 and 5 show that some customers made transactions but did not purchase through mail. These transactions might be offline.
```
#Matrix and pairwise plots
ggpairs(North_Point_List[, c("Freq", "last_update_days_ago", "X1st_update_days_ago","Purchase","Spending")])
```
<div align="center">
    <img src="https://github.com/Mahendra710/Analytical-Practicum/assets/83266654/f992cc80-c070-45b7-9ab5-f324232d2c16"
 alt="Summary" style="max-width:100%;">
    <p><b>Figure 3.0.2 :</b> Pairwise Plot  </p>
</div>

- The scatter plot of 1st update days ago and last update days ago vs. spending (figure 3.0.3) shows that the majority of customers who spent more than $1000 made the first update or interaction between 3000 and 4000 days ago, and the last interaction or update happened between 0 and 1000 days ago, which means they might like the game or software and again make purchases.
```
#Scatter plot of  Spending vs Last update days ago
plot(x = North_Point_List$last_update_days_ago,
     y = North_Point_List$Spending,
     main = "Last_update_days_ago vs. Spending",
     xlab = "Last_update_days_ago",
     ylab = "Spending",
     col = "black")

#Scatter plot of Spending vs first update days ago
plot(x = North_Point_List$X1st_update_days_ago,
     y = North_Point_List$Spending,
     main = "1st_update_days_ago vs. Spending",
     xlab = "1st_update_days_ago",
     ylab = "Spending",
     col = "black")
```
<div align="center">
    <img src="https://github.com/Mahendra710/Analytical-Practicum/assets/83266654/4207c79c-edc9-4e43-8c40-53da77f13038"
 alt="Summary" style="max-width:100%;">
    <p><b>Figure 3.0.3 :</b> Last Update Days Ago & X1st Update Days Ago Vs Spending  </p>
</div>

- The scatter plot of spending vs. frequency (Figure 3.0.4) shows that less frequency means less spending, except for some customers. Customers who purchase more than 10 times spend more than $1000 on games and software.
```
#Scatter plot of spending vs frequency
plot(x = North_Point_List$Freq,
     y = North_Point_List$Spending,
     main = "Frequency vs. Spending",
     xlab = "Frequency",
     ylab = "Spending",
     col = "black")
```
<div align="center">
    <img src="https://github.com/Mahendra710/Analytical-Practicum/assets/83266654/9cfecbf3-cdd4-45a5-8088-18ed81d0993a"
 alt="Summary" style="max-width:100%;">
    <p><b>Figure 3.0.4 :</b> Frequency Vs Spending   </p>
</div>

- The box plot of spending by web order (figure 3.0.5) shows less spending by the customers through the web order than the amount of spending by the customers through the other type (e.g., offline).
```
#boxplot of Spending by Web order
boxplot(North_Point_List$Spending ~ North_Point_List$Web.order,
        main = "Spending by Web Order",
        xlab = "Web Order",
        ylab = "Spending",
        col = "grey")
```
<div align="center">
    <img src="https://github.com/Mahendra710/Analytical-Practicum/assets/83266654/a15419f2-b666-49e7-a2f6-63f91afa7c6c"
 alt="Summary" style="max-width:100%;">
    <p><b>Figure 3.0.5 :</b> Spending By Web Order </p>
</div>

- The boxplot of spending by the purchaser (Figure 3.0.6) shows that there is one customer who didn’t make any purchases but spent an amount, which might be anomalies or offline transaction. The boxplot of spending by gender (male) shows that males spend more money than females.
```
#boxplot of Spending by Purchaser
boxplot(North_Point_List$Spending ~ North_Point_List$Purchase,
        main = "Spending by Purchaser",
        xlab = "Purchase",
        ylab = "Spending",
        col = "grey")

#boxplot of Spending by Gender
boxplot(North_Point_List$Spending ~ North_Point_List$Gender.male,
        main = "Spending by Gender= Male",
        xlab = "Gender= Male",
        ylab = "Spending",
        col = "grey")
```
<div align="center">
    <img src="https://github.com/Mahendra710/Analytical-Practicum/assets/83266654/35f401ca-0538-45b0-ac06-05118d3047da"
 alt="Summary" style="max-width:100%;">
    <p><b>Figure 3.0.6 :</b> Spending By Purchaser & Gender= Male </p>
</div>

- Figure 3.0.7 shows the boxplots of spending by US address and US residence, which display the highest amount of money spent by customers who live in the US and who are not residents of the US.
```
#boxplot of spending by US address
boxplot(North_Point_List$Spending ~ North_Point_List$US,
        main = "Spending by US address",
        xlab = "US address",
        ylab = "Spending",
        col = "grey")

#boxplot of spending by US residence
boxplot(North_Point_List$Spending ~ North_Point_List$Address_is_res,
        main = "Spending by US residence",
        xlab = "US residence",
        ylab = "Spending",
        col = "grey")
```
<div align="center">
    <img src="https://github.com/Mahendra710/Analytical-Practicum/assets/83266654/f1bf8634-26a7-456f-add0-46d74dbcc880"
 alt="Summary" style="max-width:100%;">
    <p><b>Figure 3.0.7 :</b> Spending By US Address and US residence</p>
</div>

### 4.0 Dimension Reduction
- In the dataset, all the predictors are important for the classification and regression models. However, there is a predictor named sequence_number, which is removed from the data frame using df<-df[,-1] ( Figure: 4.0.1) because this is a unique identifier, which is not useful for the prediction model. All the sources are relevant to the customer’s purchases. This dataset is a balanced dataset with 1000 purchasers and 1000 non-purchasers.
```
df <- North_Point_List
#remove the sequence column
df<-df[,-1]
names(df)
```
<div align="center">
    <img src="https://github.com/Mahendra710/Analytical-Practicum/assets/83266654/819275f0-f319-4a64-a821-0a813319eeb2"
 alt="Summary" style="max-width:100%;">
    <p><b>Figure 4.0.1 :</b> Removing the Sequence Column </p>
</div>

#### PCA analysis:
- Figure 4.0.2 shows the PCA plot, which shows how much variance is captured by the dimension. Dimension 1 shows the highest variance captured, which accounts for 11.1% of the cumulative variance.
```
#PCA analysis
pca_result <- prcomp(df, scale. = T)
names(pca_result)
#PCA Plot
plot(pca_result)
fviz_eig(pca_result, 
         addlabels = TRUE,
         ylim = c(0, 20),
         main="PCA plot")
```
<div align="center">
    <img src="https://github.com/Mahendra710/Analytical-Practicum/assets/83266654/5ca4ea83-7a99-4579-a657-ce723a884cce"
 alt="Summary" style="max-width:100%;">
    <p><b>Figure 4.0.2 :</b> Variance Captured by Dimensions </p>
</div>

- Figure 4.0.3 shows the standard deviation, proportion of variance, and cumulative proportion. The first two PCs (PC1 and PC2) together account for 20.94% of the variance, the first three PCs account for 27.22%, and so on, according to the cumulative proportion. Principal component (PC23 and PC24) doesn't do much to explain the variance in the data, based on its incredibly small standard deviation and proportion of variance.
```
# Summary
summary(pca_result)
```
<div align="center">
    <img src="https://github.com/Mahendra710/Analytical-Practicum/assets/83266654/0cbfe314-8177-42eb-b3ff-d5adc4ab70df"
 alt="Summary" style="max-width:100%;">
    <p><b>Figure 4.0.3 :</b> Summary of PCA result </p>
</div>

- The biplot (Figure: 4.0.4) shows the variability of the predictors, all the variables look in a similar space which shows that there are no clusters in the data set.
```
#Biplot
biplot(pca_result)
```
<div align="center">
    <img src="https://github.com/Mahendra710/Analytical-Practicum/assets/83266654/5f9b0bbf-c879-4845-bec7-0445ac2c91b3"
 alt="Summary" style="max-width:100%;">
    <p><b>Figure 4.0.4 :</b> Variability of the predictors </p>
</div>

### 5.0 Data partitioning method
- In the data partitioning, the data is divided into training (40%), validation (35%), and holdout (25%). In the training data, there are 800 random observations, which are going to be used to train the model. In the validation data, 700 random observations are not included in the training data used to evaluate model performance. In holdout data, 500 observations are not in training data, and validation data is used to evaluate the performance of new unseen data. Holdout data is fresh data or new data for the model and never seen or used by the model, which will use as how the model will works on the pool data.
- So, the company can target customers who are classified as “purchaser” to send a mail.
#### Data Partition:
- First, the target variable “Purchase” is converted into a factor, with 0 as non-purchaser and 1 as purchaser. For the classification, the spending column is removed as per business purpose to select a customer who is a “purchaser” or “non-purchaser”.
- First six raw of training, validation, and holdout data:
```
df<-df[,-24]
dim(df)
df <- df %>%
  mutate(
    Purchase = factor(Purchase, levels=c(0,1), labels=c("Non-Purchaser","Purchaser"))
  )


# data Partitioning
set.seed(1)
## partitioning into training (40%), validation (35%), holdout (25%)
train.rows <- sample(rownames(df), nrow(df)*0.4)
valid.rows <- sample(setdiff(rownames(df), train.rows),nrow(df)*0.35)
holdout.rows <- setdiff(rownames(df), union(train.rows, valid.rows))
# create the 3 data frames by collecting all columns from the appropriate rows
train.df <- df[train.rows, ]
valid.df <- df[valid.rows, ]
holdout.df <-df[holdout.rows, ]

head(train.df)
head(valid.df)
head(holdout.df)

dim(train.df)
dim(valid.df)
dim(holdout.df)
```
<div align="center">
    <img src="https://github.com/Mahendra710/Analytical-Practicum/assets/83266654/6620cfcd-73cf-49b1-955a-c3c5dbaaff02"
 alt="Summary" style="max-width:100%;">
    <p><b>Figure 5.0.1 :</b> Data Partition </p>
</div>

### 6.0 Classifier Models Selection and Model Performance
For the model selection, the below model will be used to predict class, whether customers make a purchase or not.
- Logistic regression model
-	Stepwise regression model 
-	K-NN model
-	Tree model (default tree and deep tree)
-	Naïve Bayes model

#### 6.1 Logistic regression model:
- The logistic regression model is a supervised algorithm used for classification. In the dataset, target variable is “Purchase”, the logistic regression model gives the probability of customer purchase or not. First, the model is build using the ‘glm’ function on the training dataset.
- From the below model (Figure : 6.1.1) , logistic regression equations:
- logit=β_0+β_1 x_1+β_2 x_2+…+β_q x_q
- Logit(Purchase=1)= -4.1790531 + 0.2263908 *{US} + 1.7689511 *{source_a} - 0.0324075 *{source_c} - 0.1947970 *{source_b} - 0.7524404 *{source_d} + 0.9862691 *{source_e} + 0.8812215 *{source_m} + 0.3637817 *{source_o} - 2.9005290 *{source_h} + 0.7551389 *{source_r} + 1.2815347 *{source_s} + 0.6816827 *{source_t} + 2.2084900 *{source_u} + 2.3429232 *{source_p} + 1.7157863 *{source_x} + 1.2327250 *{source_w} + 2.3463503*{Freq} + 0.0001486 *{last_update_days_ago} - 0.0001993 *{X1st_update_days_ago} + 1.1026641 *{Web.order} - 0.1718877 *{Gender.male} - 0.8235130 *{Address_is_res}
- p=1/(1+e^(-(logit)) )
- If the logit value is greater than 0 then success is more likely to happen. The positive coefficient shows the higher predictor value is related to a high chance of getting a purchase. In the dataset, higher frequency means a high chance of purchase. The model output in figure 6.1.1 shows the intercept and coefficient values for the predictors in the model. Also, star marked variable shows the importance of predictors in the model.

```
##-----------------------Logistic Regression------------------------------------
#Training the model
# build model

trControl <- caret::trainControl(method="cv", number=5, allowParallel=TRUE)
lgmodel <- caret::train(Purchase ~ ., data=train.df, trControl=trControl,
                        method="glm", family="binomial")
lgmodel
summary(lgmodel$finalModel)
```
<div align="center">
    <img src="https://github.com/Mahendra710/Analytical-Practicum/assets/83266654/608ccdc8-8dda-4d18-bdda-1f6651035ba3"
 alt="Summary" style="max-width:100%;">
    <p><b>Figure 6.1.1 :</b> Summary of the model</p>
</div>

#### 6.2 Evaluating the logistic regression model Performance:
- When it comes to model performance, the logistic regression model gives an 82.5% accuracy rate with a sensitivity of 0.8207 and a specificity of 0.8292 for the training model. While testing this model on new unseen data (validation data), it correctly identified the class with an accuracy of 79.29%. For business purposes, a logistic regression model can classify around 73.83% of the positive class (Purchaser) through this predictor information and select top customers among them who are more likely to purchase and send them mail. Figure 6.2.1 shows the logistic regression model performance on training and validation data.

```
options(scrippen = 999)

#evaluating performance of training data
confusionMatrix(predict(lgmodel, train.df), train.df$Purchase, positive = "Purchaser")
#evaluating performance of Validation data
confusionMatrix(predict(lgmodel, valid.df), valid.df$Purchase, positive = "Purchaser")
```
<div align="center">
    <img src="https://github.com/Mahendra710/Analytical-Practicum/assets/83266654/8df99a72-6a7d-4f63-bd28-0d544ed2c50a"
 alt="Summary" style="max-width:100%;">
    <p><b>Figure 6.2.1 :</b> Confusion Matrix of Logistic Regression Model</p>
</div>

#### 6.3 Stepwise Regression Model:
- The figure 6.3.1 shows the summary of the stepwise backward and figure 6.3.2 shows the  summary of forward models, the AIC (Akaike Information Criterion) of the backward model is **651.28** and the forward model is **649.46**. The summary also shows the coefficient values for all the predictors, which shows the importance of the predictors in the model. Also, it gives information about the changes in the model; for example, a high frequency shows a high chance of getting a positive class (purchaser). Stars indicate significant predictors in the model. Here, the low AIC shows the better performance of the model.

```
lg.full <- glm(Purchase ~ ., data = train.df, family = "binomial")

# Stepwise backward
step_backward <- step(lg.full, direction = "backward")
summary(step_backward)

# Stepwise forward
lg.null <- glm(Purchase ~ 1, data = train.df, family = "binomial")  # Null model
step_forward <- step(lg.null, scope = list(lower = lg.null, upper = lg.full), direction = "forward")
summary(step_forward)
```
<div align="center">
    <img src="https://github.com/Mahendra710/Analytical-Practicum/assets/83266654/43b25d95-7ca3-449f-a46a-c369474cdaf5"
 alt="Summary" style="max-width:100%;">
    <p><b>Figure 6.3.1 :</b>Summary of Stepwise Backward Regression Model</p>
</div>

<div align="center">
    <img src="https://github.com/Mahendra710/Analytical-Practicum/assets/83266654/f1a20cb7-04db-44fe-914b-149608c36fe7"
 alt="Summary" style="max-width:100%;">
    <p><b>Figure 6.3.2 :</b> Summary of Stepwise Forward Regression Model</p>
</div>

#### 6.4 Evaluating the Stepwise Backward model Performance.
- With regards to backward regression, the confusion matrix (Figure: 6.4.1) shows that the model performs 82.12% accurately on training data and 78.43% on validation data (Figure: 6.4.2). For validation data, 284 non-purchasers and 265 purchasers were correctly classified, whereas 98 non-purchasers and 53 purchasers were misclassified. As for business purposes, the backward regression model correctly identifies around 73% of the positive class from pool data, which helps the business owner decide which top customers from the pool to send mail to.

```
# Confusion matrix for backward stepwise model
backward_pred_train <- predict(step_backward, newdata = train.df, type = "response")
backward_pred_valid <- predict(step_backward, newdata = valid.df, type = "response")
# Convert probabilities to binary predictions for backward stepwise model
backward_pred_train_binary <- ifelse(backward_pred_train > 0.5, "Purchaser", "Non-Purchaser")
backward_pred_valid_binary <- ifelse(backward_pred_valid > 0.5, "Purchaser", "Non-Purchaser")
# Confusion matrix for training data
confusionMatrix(table(backward_pred_train_binary, train.df$Purchase), positive = "Purchaser")
# Confusion matrix for validation data
confusionMatrix(table(backward_pred_valid_binary, valid.df$Purchase), positive = "Purchaser")
```
<div align="center">
    <img src="https://github.com/Mahendra710/Analytical-Practicum/assets/83266654/03bc4483-0b20-4eb7-8c84-ef583c6cf818"
 alt="Summary" style="max-width:100%;">
    <p><b>Figure 6.4.1 :</b>Confusion matrix for Training data</p>
</div>

<div align="center">
    <img src="https://github.com/Mahendra710/Analytical-Practicum/assets/83266654/28db405a-aec5-4454-aa1e-d399ad0b50ae"
 alt="Summary" style="max-width:100%;">
    <p><b>Figure 6.4.2 :</b> Confusion Matrix for Validation Data</p>
</div>

#### 6.5 Evaluating the Stepwise Forward model Performance
- With regards to forward regression, the below confusion matrix gives the accuracy of training data (Figure: 6.5.1) as 82.38% and validation data (Figure: 6.5.2) as 78.71%. Looking on the validation data, the model identified 281 non-purchasers and 270 purchasers correctly classified. However, 56 purchasers and 93 non-purchasers were misclassified. Businesses can use this model to classify the purchaser, which performs around 74.38% accurately classify positive class on new data.

```
# Confusion matrix for forward stepwise model
forward_pred_train <- predict(step_forward, newdata = train.df, type = "response")
forward_pred_valid <- predict(step_forward, newdata = valid.df, type = "response")
# Convert probabilities to binary predictions
forward_pred_train_binary <- ifelse(forward_pred_train > 0.5, "Purchaser", "Non-Purchaser")
forward_pred_valid_binary <- ifelse(forward_pred_valid > 0.5, "Purchaser", "Non-Purchaser")
# Confusion matrix for training data
confusionMatrix(table(forward_pred_train_binary, train.df$Purchase), positive = "Purchaser")
# Confusion matrix for validation data
confusionMatrix(table(forward_pred_valid_binary, valid.df$Purchase), positive="Purchaser")
```
<div align="center">
    <img src="https://github.com/Mahendra710/Analytical-Practicum/assets/83266654/18285ea5-058b-4fa3-9af3-b0f85eed303a"
 alt="Summary" style="max-width:100%;">
    <p><b>Figure 6.5.1 :</b>Confusion matrix for Training data</p>
</div>

<div align="center">
    <img src="https://github.com/Mahendra710/Analytical-Practicum/assets/83266654/6e2777a4-dbea-4424-a2f2-4ac220c12153"
 alt="Summary" style="max-width:100%;">
    <p><b>Figure 6.5.2 :</b> Confusion Matrix for Validation Data</p>
</div>

#### 6.6 K-NN Model 
- The K-NN model is used for both classification and regression. In classification, the K-NN model predicts the new class based on the majority of its neighbour’s class. First, check the best k value for the model using the cross-validation method. From figure 29, k = 3 gives a more accurate model than others.

```
##-----------K-NN Model---------------------------------------------------------
# use leave-one-out cross-validation
trControl <- trainControl(method="loocv", number=5, allowParallel=TRUE)
knn_model <- train(Purchase ~ ., data=train.df,
                   method="knn",
                   preProcess=c("center", "scale"),
                   tuneGrid=expand.grid(k=seq(1, 13, 2)),
                   trControl=trControl)

knn_model
#knn model with k =3.
knn.model <- train(Purchase ~ ., data=train.df,
                   method="knn",
                   preProcess=c("center", "scale"),
                   tuneGrid=expand.grid(k=3),
                   trControl=trainControl(method="none"))
knn.model
```
<div align="center">
    <img src="https://github.com/Mahendra710/Analytical-Practicum/assets/83266654/4a752b7b-521f-4bb1-b87c-348b250fdfce"
 alt="Summary" style="max-width:100%;">
    <p><b>Figure 6.6.1 :</b> Best K Values in K-NN model</p>
</div>

#### 6.7 Evaluating K-NN model performance.
- Using k = 3, the k-nn model classified accuracy of 85.38 on training data (Figure 6.7.1) and 72.29% on validation data (Figure 6.7.1). For validation data, 267 non-purchasers and 239 purchasers were correctly classified, whereas 124 non-purchasers and 70 purchasers were misclassified. A sensitivity for validation shows that 65.84% of the positive class ‘Purchaser’ were correctly identified, and a specificity for validation data shows that 79.23% of the negative class “Non-Purchaser” were correctly identified.
```
#evaluating performance of training data
confusionMatrix(predict(knn.model, train.df), train.df$Purchase, positive = "Purchaser")
#evaluating performance of Validation data
confusionMatrix(predict(knn.model, valid.df), valid.df$Purchase, positive = "Purchaser")


#predict(knn.model, valid.df)
```
<div align="center">
    <img src="https://github.com/Mahendra710/Analytical-Practicum/assets/83266654/97e098b0-300f-46e2-8042-38f1a1ae349e"
 alt="Summary" style="max-width:100%;">
    <p><b>Figure 6.7.1 :</b>Confusion Matrix for K-NN model on training and Validation data</p>
</div>

#### 6.8 Tree Model
- From the default classification tree, if the frequency is less than 1, then it will be classified as a non-purchaser. Also, there are other predictors from tree shows about the class chances.
```
# # Classification tree
#install.packages("rpart")
library(rpart)
library(rpart.plot)
# classification tree

#Default tree
default.ct <- rpart(Purchase ~ ., data=train.df, method="class")
#count number of leaves
sum(default.ct$frame$var=='<leaf>')
# plot tree
rpart.plot(default.ct, extra=1, fallen.leaves=FALSE)
```
<div align="center">
    <img src="https://github.com/Mahendra710/Analytical-Practicum/assets/83266654/2614e2ab-0869-4983-ad91-9c6a3eef80c9"
 alt="Summary" style="max-width:100%;">
    <p><b>Figure 6.8.1 :</b>Default Classification Tree</p>
</div>

#### 6.9 Evaluating Tree model Performance:
- About the default tree model, it is 84.38% accurate on training data (Figure: 6.9.1) and 77% accurate on validation data (Figure: 6.9.2). To classify new data, the default tree classified  75.48% correctly identifies the new class.
```
default.ct.pred.train <- predict(default.ct, train.df, type='class')
#training confusion matrix
confusionMatrix(default.ct.pred.train,train.df$Purchase,positive = "Purchaser")
#validation confusion matrix
default.ct.pred.valid <- predict(default.ct, valid.df, type='class')
confusionMatrix(default.ct.pred.valid ,valid.df$Purchase,positive = "Purchaser")
```
<div align="center">
    <img src="https://github.com/Mahendra710/Analytical-Practicum/assets/83266654/e0e68f86-d7d8-4a19-9f06-15df76e8ddbf"
 alt="Summary" style="max-width:100%;">
    <p><b>Figure 6.9.1 :</b>Confusion matrix for Training data</p>
</div>

<div align="center">
    <img src="https://github.com/Mahendra710/Analytical-Practicum/assets/83266654/ad7334f4-ca6d-4f30-a8c5-79cb16ca44be"
 alt="Summary" style="max-width:100%;">
    <p><b>Figure 6.9.2 :</b> Confusion Matrix for Validation Data</p>
</div>

#### 6.10 Naïve Bayes Model 
- A Naïve Bayes model is used for classification when there are more predictors. For the dataset, the Naïve Bayes model is built by loading the library library (e1071), which is used for statistical analysis. Then train the model using a training dataset, and it gives an output as a conditional probability for each predictor. Also, Figure 6.10.1 shows the output of a priori probabilities: there is a 50.5% chance of getting a non-purchaser and a 49.5% chance of getting a purchaser. The conditional probabilities for each predictor show the probability that the predictor belongs to a particular class. Then the model predicts the results using these probabilities and gives an output for the chance of the target variable.
```
library(e1071)
options(scipen=999, digits = 7)

purchase.nb <- naiveBayes(Purchase~ ., data = train.df)
purchase.nb
```
<div align="center">
    <img src="https://github.com/Mahendra710/Analytical-Practicum/assets/83266654/9fb926f1-7996-409f-a2b1-6541bc1f43bb"
 alt="Summary" style="max-width:100%;">
    <p><b>Figure 6.10.1 :</b> Summary of Naïve Model</p>
</div>

#### 6.11 Evaluating Naïve Model Performance.
- The model gives 73.12% accuracy on training data (Figure: 6.11.1) and 72.86% accuracy on new validation data (Figure: 6.11.2). 270 non-purchasers were correctly identified as non-purchasers, and 240 purchasers were correctly identified as purchasers in the validation data.
```
#training confusion matrix
confusionMatrix(predict(purchase.nb, newdata = train.df), train.df$Purchase, positive = "Purchaser")

#validation confusion matrix
confusionMatrix(predict(purchase.nb, newdata = valid.df), valid.df$Purchase, positive = "Purchaser")
```
<div align="center">
    <img src="https://github.com/Mahendra710/Analytical-Practicum/assets/83266654/d622446e-08c7-4cac-9567-cd294216fba0"
 alt="Summary" style="max-width:100%;">
    <p><b>Figure 6.11.1 :</b>Confusion matrix for Training data</p>
</div>

<div align="center">
    <img src="https://github.com/Mahendra710/Analytical-Practicum/assets/83266654/e6f14aa4-9f3e-4e0d-bf22-538a1f1628c8"
 alt="Summary" style="max-width:100%;">
    <p><b>Figure 6.11.2 :</b> Confusion Matrix for Validation Data</p>
</div>

### 7.0 Best Classifier Model Selection
<div align="center">
    <img src="https://github.com/Mahendra710/Analytical-Practicum/assets/83266654/dda5d6e6-4753-4146-91ef-fdc0a8db6c60"
 alt="Summary" style="max-width:100%;">
    <p><b>Figure 7.0.1:</b> Comparison of Classification Models </p>
</div>

- Among all the classification models, logistic regression performance is better than that of other models on the validation dataset with an accuracy of 79.29% and Sensitivity of 0.7383. Using this model, the probability of purchaser will be calculated, which gives the probability of customer likely to be a purchaser after receiving mail.

### 8.0 Regression Model Selection
For the model selection, the below model will be used to predict the spending amount for the customer who made a purchase after receiving a mail. 
- Linear Regression model
-	Stepwise- Backward model
-	Regression tree

Before the modelling process, only purchaser-based partitions will be used for the training and validation datasets. The “sequence” and “purchase” will be removed for modelling. So, there are 396 records and 23 columns in the training dataset, and the validation data set has 363 records and 23 columns.
```
df1=data.frame(North_Point_List)
df1<-df1[,-1]

df1 <- df1 %>%
  mutate(
    Purchase = factor(Purchase, levels=c(0,1), labels=c("Non-Purchaser","Purchaser"))
  )
head(df1)
# data Partitioning
set.seed(1)
## partitioning into training (40%), validation (35%), holdout (25%)
train.rows <- sample(rownames(df1), nrow(df1)*0.4)
valid.rows <- sample(setdiff(rownames(df1), train.rows),nrow(df1)*0.35)
holdout.rows <- setdiff(rownames(df1), union(train.rows, valid.rows))
# create the 3 data frames by collecting all columns from the appropriate rows
train.df <- df1[train.rows, ]
valid.df <- df1[valid.rows, ]
holdout.df <-df1[holdout.rows, ]

train.p <- subset(train.df, Purchase == "Purchaser")
valid.p <- subset(valid.df, Purchase=="Purchaser")
train.p<-train.p[,-23]
valid.p <- valid.p[,-23]
dim(train.p)
dim(valid.p)

```
#### 8.1 Linear Regression Model
- Using the regression function lm, the model is trained using a training dataset. The targeted variable, spending, can be predicted using the intercept and coefficient values for the predictors. The model output (Figure: 8.1.1) marked the stars as the important predictors. The minimum residual is -425.52, and the maximum residual is 1062.70. The positive coefficient of the predictors shows the more amount of spending on games and software. The negative coefficient shows the less amount of spending on games and software.
```
sr.model <- lm(Spending ~. , data = train.p)
summary(sr.model)
```
<div align="center">
    <img src="https://github.com/Mahendra710/Analytical-Practicum/assets/83266654/b13a7449-8c77-451c-8726-b047ddff7318"
 alt="Summary" style="max-width:100%;">
    <p><b>Figure 8.1.1:</b> Summary of the Regression Model </p>
</div>

#### 8.2 Evaluating Regression Model Performance
- From figure 8.2.1, the model gave the RMSE (Root Mean Square Error) of 167.2498. which shows the predictor deviates from the actual value is around 167 units.
```
pred<- predict(sr.model,valid.p)
#Accuracy for validation
accuracy(pred,valid.p$Spending)
```
<div align="center">
    <img src="https://github.com/Mahendra710/Analytical-Practicum/assets/83266654/02ee8fd5-5aff-49b2-b189-a1fdfb3138a2"
 alt="Summary" style="max-width:100%;">
    <p><b>Figure 8.2.1:</b> Accuracy for Validation </p>
</div>

#### 8.3 Stepwise- backward Regression
- In the stepwise-backward regression model, check for all the important predictors by removing less effective predictors and training the model using the training dataset. The stepwise-backward model summary (Figure: 8.3.1) shows that five variables give better performance on the training dataset. The model marked stars as the important predictors.
```
stepwise_backward <- step(sr.model,direction = "backward")
summary(stepwise_backward)
```
<div align="center">
    <img src="https://github.com/Mahendra710/Analytical-Practicum/assets/83266654/c36fdaae-7496-4894-a879-bcc033805add"
 alt="Summary" style="max-width:100%;">
    <p><b>Figure 8.3.1:</b> Summary of Stepwise Backward Regression Model </p>
</div>

#### 8.4 Evaluating Stepwise Backward Regression Model Performance
- With regards to accuracy for validation data (Figure 8.4.1), the model gave 165.6397 RMSE on new unseen data. Also, accuracy parameters ME (mean error) shows the mean average value (-1.618712) for the validation dataset.
```
p <- predict(stepwise_backward, valid.p)
#Accuracy for Validation
accuracy(p,valid.p$Spending)
```
<div align="center">
    <img src="https://github.com/Mahendra710/Analytical-Practicum/assets/83266654/52926b76-6013-4b6e-9dd8-96f64cc007c5"
 alt="Summary" style="max-width:100%;">
    <p><b>Figure 8.4.1:</b> Accuracy for Validation </p>
</div>

#### 8.5 Regression tree
- The regression tree model is built by using rpart() function on the training dataset. The tree plot (Figure: 8.5.1) shows tree rules for the model. For example, if frequency is less than 3 than the average spending is 148 which 70% accurate.
```
tree.model <- rpart(Spending ~ ., data=train.p)
rpart.plot(tree.model)
```
<div align="center">
    <img src="https://github.com/Mahendra710/Analytical-Practicum/assets/83266654/3e2c02c9-0798-4938-8d65-fb78881a16f5"
 alt="Summary" style="max-width:100%;">
    <p><b>Figure 8.5.1:</b> Regression tree plot </p>
</div>

#### 8.6 Evaluating Regression tree model Performance.
- RMSE vale of regression tree model for validation data (Figure: 8.6.1) is 181.0081, which shows the predictor deviates from the actual value is around 181 units.
```
tree.test.pred <- predict(tree.model, valid.p, type='vector')
#Accuracy for Validation
accuracy(tree.test.pred,valid.p$Spending)
```
<div align="center">
    <img src="https://github.com/Mahendra710/Analytical-Practicum/assets/83266654/b5e06926-77fa-41c7-9e33-d6345fecc6b8"
 alt="Summary" style="max-width:100%;">
    <p><b>Figure 8.6.1:</b> Accuracy for Validation </p>
</div>

### 9.0 Best Regression Model Selection
<div align="center">
    <img src="https://github.com/Mahendra710/Analytical-Practicum/assets/83266654/12f2d223-0ff4-4bf9-bc63-d13b1a4e7a4e"
 alt="Summary" style="max-width:100%;">
    <p><b>Figure 9.0.1:</b> Comparison of regression Models  </p>
</div>

Among all the linear models, stepwise backward regression performs better on the validation dataset, with an RMSE of 165.6397. Using this model, the predicted spending value will be by the customers. It provides the estimated spending amount that customers are going to spend on software and games.

### 10.0 Profit analysis
- For modeling and performance, logistic regression model will be used for classification and stepwise backward regression for prediction. These models will be used for the holdout data, which was not used before by these models. For the modelling, the dataset has 2000 customer details, which includes 1000 purchasers and 1000 non-purchasers, which means the response rate is 50%. However, the actual response rate is 0.1065. So, by adjusting the probability of the purchaser and their expected spending amount with an actual response rate of 0.1065.
- First, the column of the probability of the purchaser is added using a linear regression model, which shows the chance that the customer is likely to make purchases after receiving the mail. Also, another column with the predicted spending value of the customer is added using a stepwise backward model. The probability of a purchaser is adjusted by multiplying it by the original purchase rate of 0.1065. For the adjusted spending value, multiply the predicted spending values by the adjusted probabilities of purchase. Figure 10.0.1 shows the output of these processes, which includes the first six rows of the holdout data.
```
### Add a column to the data frame with the predicted probability of purchase 
holdout.df$predicted_probability_Purchaser <- predict(lgmodel,holdout.df,type= "prob")[,"Purchaser"]

### Add another column with predicted spending value 
holdout.df$predicted_spending_value <- predict(stepwise_backward,holdout.df)

### Add a column for “adjusted probability of purchase” to adjust for oversampling the purchaser 
original_purchase_rate <- 0.1065
holdout.df$adjusted_probability_of_purchase <- holdout.df$predicted_probability_Purchaser*original_purchase_rate

### Add another column for expected spending
holdout.df$expected_spending <- holdout.df$predicted_spending_value*holdout.df$adjusted_probability_of_purchase
head(holdout.df)
```
<div align="center">
    <img src="https://github.com/Mahendra710/Analytical-Practicum/assets/83266654/01e78b1d-889f-4df4-8272-ebd86597f393"
 alt="Summary" style="max-width:100%;">
    <p><b>Figure 10.0.1:</b> Model Performance on Holdout data  </p>
</div>

- A cumulative gain chart and a decile-wise lift chart are used to see the model's performance on new, unseen data. These models are compared with the random model, which showed a baseline. The cumulative gain chart (Figure 10.0.2) shows the expected spending by the top customers. For example, here it shows that the North Point company could expect around $2000 in spending from the top 50 customers out of 500 customers. Also, a decile-wise lift chart shows how much a predictive model performs as compared to a random model. From figure 10.0.2, a lift of around 4 shows that the predictive model can identify the top 10% of 500 customers four times better than randomly selected customers.
```
gain <- gains(holdout.df$expected_spending, holdout.df$adjusted_probability_of_purchase, groups=10)
df2 <- data.frame(
  ncases=c(0, gain$cume.obs),
  cumulative=sum(holdout.df$expected_spending)*c(0, gain$cume.pct.of.total)
)
df2
g1<-ggplot(df2, aes(x=ncases, y=cumulative)) +
  geom_line() +
  geom_segment(aes(x=0, y=0, xend=nrow(holdout.df), yend=sum(holdout.df$expected_spending)),
               color="gray", linetype=2) + # adds baseline
  labs(x="# Cases", y="# Expected Spending", title="Cumulative gains chart")

g1

barplot(gain$mean.resp / mean(holdout.df$expected_spending), names.arg=seq(10, 100, by=10),
        xlab="Percentile", ylab="Decile mean / global mean")

# Decile-wise lift chart
df3 <- data.frame(
  decile=gain$depth,
  meanResponse=gain$mean.resp /mean(holdout.df$expected_spending))

g2 <- ggplot(df3, aes(x=decile, y=meanResponse)) +
  geom_bar(stat="identity") +
  labs(x="decile", y=" ", title="Decile-wise lift chart")
grid.arrange(g1,g2,ncol=2)
```
<div align="center">
    <img src="https://github.com/Mahendra710/Analytical-Practicum/assets/83266654/4bc62b3b-1a24-4d5c-a909-118361a4a06a"
 alt="Summary" style="max-width:100%;">
    <p><b>Figure 10.0.2:</b> Cumulative Gains Chart and Decile wise lift chart</p>
</div>

#### 10.1 Gross profit
- So, Holdout data is used to calculate the expected spending value for new customers. The sum of the expected spending for 500 customers is $4815.239. Each list booklet costs approximately $2 to mail, which includes printing, postage, and mailing other mailing costs. The company need to spend $360,000 to send the mail to 180,000 customers. The company could expect the spending amount of $1,733,486 from remaining180,000 customers. So, the gross profit is $1,373,486 that firm could expect from the remaining 180,000 customers.
Figure 10.1.1 shows the calculation of this process.
```
#sum of total expected spending form 500 customers
sum(holdout.df$expected_spending)
#sum of total expectd spending form 180,000 customers
(180000*sum(holdout.df$expected_spending))/500

#expected gross profit from 180,000 customers
((180000*sum(holdout.df$expected_spending))/500)- (2*180000)

#expected gross profit from one customer
(((180000*sum(holdout.df$expected_spending))/500)- (2*180000))/180000
```
<div align="center">
    <img src="https://github.com/Mahendra710/Analytical-Practicum/assets/83266654/d93b1fc0-43ea-4b4d-a4c2-902fc1eb35e1"
 alt="Summary" style="max-width:100%;">
    <p><b>Figure 10.1.1:</b> Gross Profit Calculation </p>
</div>

### 11.0 Conclusion
In conclusion, the company’s main customers come from the US, and male customers are more frequent than female customers. When customers buy more software or games again, the company generates more revenue from those customers. For the classification, logistic regression performs better on new data with an accuracy of 0.7929 and sensitivity of 0.7383, while the stepwise backward model performs well on new data with an RMSE of 165.6397. Using these models, the company could expect $1,373,486 in gross profit from the remaining 180,000 customers. In the recommendation, if the company can select the customers from the 5,000,000, then they should select or ask for contact details of the top-ranked customers by the expected spending, then use them partially, like first using 20,000 customers from the top 180,000 customers, and so on. Also, the company can use first the high probability of purchasers like top 10% and the high expected spending of customers to send the mail. Then, the company can use other marketing strategies for those customers with a lower probability and a lower spending amount. For example, the company can provide some additional discounts on games or some free games or software.
