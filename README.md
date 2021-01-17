# DigiHack 2021 - Credit Default Prediction
Organised by the Analytics Cell of NMIMS SDSOS, Digihack 2021 was a 3-stage hackathon comprising an Aptitude Test, 24 Hour Hackathon and Final Presentations to a panel of experts. 

**Problem Statement:**
Make a decision regarding whether to grant a loan to the customers that have approached banks, based on the dataset provided by the credit bureau. The expected solution to which will be building an appropriate model for customer defaulting.

## Dataset Description
* **ID** - Customer ID
* **Age** -	Age of the Customer
* **Customer_type**	- Salaried / Self Employed
* **Gross_income** - Gross income declared by Customer
* **Net_income** - Net income declared by Customer
* **SEX**	- Gender
* **Type_of_industry** - Type of industry
* **Marital_Status** - Marital Status declared by Customer
* **Months_in_city** - Months in city 
* **Months_in_current_job** - Months in current job
* **Org_Type** - Org Type declared by Customer
* **Bank_balance** - Bank balance declared by Customer
* **Debt_ratio** - Debt ratio declared by Customer
* **Target** - Default or not.
* **ENQ_1** - Days since last enquiry was made with any other bank
* **ENQ_2** - Days since last Home loan enquiry made with any other bank
* **ENQ_3** - Total enquiries in last 3 months
* **ENQ_4**	- Total home loan enquiries in last 3 months
* **ENQ_5**	- Total enquiries in last 12 months
* **ENQ_6**	- Total home loan enquiries in last 12 months
* **ENQ_7**	- Total enquiries
* **ENQ_8**	- Total home loan enquires
* **ACCOUNT_9**	- Number of defaults in last 3 months
* **ACCOUNT_10** - Number of default in last 12 months
* **ACCOUNT_11** - Days since last account was open
* **ACCOUNT_12** - Total number of loans with other bank ( live + closed )
* **ACCOUNT_13** - Total number of home loans with other bank ( live + closed )
* **ACCOUNT_14** - Total number of unsecured loans with other bank ( live + closed )
* **ACCOUNT_15** - Total number of live loans
* **ACCOUNT_16** - Total number of live home loans
* **ACCOUNT_17** - Total number of live unsecured loans
* **ACCOUNT_18** - Total outstanding amount
* **ACCOUNT_19** - Total secured outstanding amount
* **ACCOUNT_20** - Total unsecured outstanding amount
* **ACCOUNT_21** - Average number of days the individual is in debt

## Exploratory Data Analysis and Data Pre-processing
**1. Repeated Data Points** - Out of the 3980 data points, the number of unique IDs were 3894. Thus the 86 repeated data points were dropped.

**2. Multicollinearity** - The correlation between the Gross Income and Net Income variables was very high (0.93). Hence Gross Income variable was dropped to prevent multicollinearity.

**3. Redundant Information** - The Type of Industry variable contained majority of data points (close to 3200) as ‘OTHER’ category while the remaining datapoints were distributed among 78 categories. Since this would not add any valuable insights, the variable Type of Industry was dropped.

**4. Outlier Detection** - Boxplots of numeric variables were plotted to detect outliers. The Months in Current Job variable showed 2 outliers, with values greater than 1,80,000 months which did not make sense and were therefore removed. The vraible Bank Balance had 4 negative values which were also removed.

**5. Missing Value Imputation** - On null value analysis of the dataset, it was noticed that there were a few missing values in some of the variables, and 636 missing values (16%) in the variable Bank Balance. To impute missing values, the Iterative Imputation technique was used where each feature is modeled as a function of the other features and missing values are predicted. Each feature is imputed sequentially, one after the other, allowing prior imputed values to be used as part of a model in predicting subsequent features.

**6. Dummy Variable Creation** - Since most algorithms cannot work with categorical variables directly, they were converted into dummy variables.

**7. Weight of Evidence** - The weight of evidence (WOE), which tells the predictive power of an independent variable with respect to a dependent variable, was used to combine categories of categorical variables that behaved in a similar manner to classify the dependent variable. Since the categorical variable Organization Type had multiple categories, categories were combined based on the WOE values. The variable Net Income was highly positively skewed, so the values were binned after a log transformation and categories with similar WOE values were combined.

**8. Unbalanced Target Variable** - The Target variable in the dataset was highly unbalanced. 92% of the target values were 0, and the rest 1. To avoid poor perfomance on an imbalanced dataset, Synthetic Minority Oversampling Technique (SMOTE) was used. SMOTE works by selecting examples that are close in the feature space, drawing a line between the examples in the feature space, and drawing a new sample along that line. Post oversampling, the data had 7182 data points and the proportion of each value in the target variable was 0.5.

## Approach
To predict default, four classifiers were used and accuracies before and after feature selection were compared.

**1. Logistic Regression:** The most popular classifier for predicting loan defaults is the Binary Logistic Regression model which gave an accuracy of 58% on our data. 
**Final accuracy post feature selection: 71%**

**2. Random Forest Classifier:** An ensemble model created by bagging decision trees, the Random Forest Classifier with 100 decision trees gave an accuracy of 95% on our data.
**Final accuracy post feature selection: 96.6%**

**3. XG Boost Classifier:** A boosting algorithm that builds decision trees sequentially to minimize error, the XG Boost Classifier gave an accuracy of 94.9% on our data.
**Final accuracy post feature selection: 95.3%**

**4. Light GBM Classifier:** Another boosting algorithm that increases efficiency through leaf-wise growth, the Light GBM classifier gave an accuracy of 95.7% on our data.
**Final accuracy post feature selection: 96.4%**

## Conclusion and Results
Recommending the Random Forest Classifier (post feature selection) to predict defaults and providing additional functionalities such as loss estimation and micro-financing, my team stood **1st** in DigiHack 2021.
