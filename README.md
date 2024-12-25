# 1. Introduction
A bike sharing system is a service which bikes made available for the shared use to individuals on a short term basis. For a price or free.
US bike sharing provider Boom Bikes has recently suffered considerable dips in their revenue due to Corona Pandemic. 
Plan to accelerate revenue once ongoing lockdown ends and economy restores to healthy state.

They planned to prepare themselves to cater to the people needs once the situations gets better all around and stand out from other service providers and make huge profits


# 2. Business Goal
- Model the demand for the shared bikes with available independent variables
- It will be used by management how exactly the demand variables with different features
- So business strategy to meet the demand levels and meet customers expectations
- The model will be a good way for management to understand demand dynamics of a new market

They want to understand the factors affecting the demand for these shared bikes in the American market
Company wants to know 
1. Which variables are significant in predicting the demand for shared bikes
2. How well those variables describe the bike demand


# 3. Reading, Understanding Data and EDA

We will use Python for reading and understanding the data sets. Also do EDA to get more insights using visualization

### 3.1 Setup Python modules and Basic understanding of data

Python Modules and version used from conda list

```
matplotlib                3.9.2
numpy                     1.26.4
pandas                    2.2.2
plotly                    5.24.1
scikit-learn              1.5.1
scipy                     1.13.1
seaborn                   0.13.2
statsmodels               0.14.2
```

### 3.2 Data Cleaning

#### 3.2.1 Check for Missing Values

- No Null values or missing values
- But might need to change the dteday to datetime

#### 3.2.2 Drop Unwanted Columns

- Drop the unnecessary columns: casual and registered, which already which captured by target column cnt
- Drop the unwanted column: instant, this is column used for row indentification, no use for linear regression
- Drop the dteday after post EDA, as this will not be more useful since mnth and yr columns are already present


#### 3.2.3 Check for uniqueness and drop duplicates

- No Duplicates were identified

#### 3.2.4 Rename and Map the category columns for EDA 

**date** There are 730 day entries
- There are 2 years 2018 and 2019 as described in the data dict as 0 and 1
- Will temporaily map for EDA and will revert back during Model building
  
**month** 12 is correct
- **Need to map** the respective months to category
  
**holiday** 2 is correct it will be 0 or 1

**weekday** 7 is correct 
- **Need to map** the data to weekdays
  
**weathersit** 3 Verify if the data is correct since there are only 3 unique values identified instead of 4
- **Need to map** the data to the respective weather category
  
**season**: 4 is correct. There are 4 Seasons as described in the data dict (1:spring, 2:summer, 3:fall, 4:winter)
- **Need to map** the four seasons as they should be avoided to be numerically represented and of any order


### 3.3 EDA Analysis

##### 3.3.1 Check for Outliers

- No Outliers found on target variable cnt

#### 3.3.2 Univariate Analysis

- Using histplot on the cnt

##### 3.3.2.1 Grouped Univariate Analysis

- Using boxplot and barchart grouped based on category variables and target variable cnt

#### 3.3.3 Bivariate Analysis

- Using pairplot of all continuous variable

#### 3.3.4 Mulivariate Analysis

- Using Heatmap of all continuous variable


### 4. Data Preparation for linear Regression model

#### 4.1 Create dummy variables

Following are the categories greater than 2
- season
- month
- weekday
- weather

### 5. Linear Regression Model building

#### 5.1 Split to Train and Test

- Split data sets as 70% train and 30% test data

#### 5.2 Scale the train data sets

- Transform the numerical values using MinMaxScaler
- Check correlation of numerical values with Heatmap
- Verify the correlation holds good with temp and cnt

#### 5.3 Model Building

- Create the Linear regression model
- Split the x independent vavriable and y dependent variable
- fit the train data sets x and y

##### 5.3.1 Feature Selection using RFE

- Fits model lr and recursively remote least important feature
- Provide the required RFE features with ranking
- 
##### 5.3.2 Feature Selection using VIF

- Provide inflation factor to determine multicollinearity
- Eliminate the features having higher VIF values
- Threshold of VIF > 5 should be considered for removal, VIF > 10 must be removed unless there is business use case recommended to do otherwise

##### 5.3.3 Final LR Model

- Check the P Values which are insignificant and remove them recursively one by one
- Check the F-statistics and Prob F-Statistics and validate the model for multicollinearity and probability of model is not by chance

##### 5.3.4 Prediction using Train and Test Datasets

- Run the prediction on the train data sets
- Run the prediction on the test data sets

### 6. Model Evaluation

#### 6.1 Error Term Distribution Analysis

- Using distplot on train data sets and verify if its normally distributed
- Using distplot on test  data sets and verify if its normally distributed

#### 6.2 Residual Analysis

- Residual analysis evaluates the differences between observed values (actual data) and predicted values (from a linear regression model).
- Using scatter plot, it helps validate the assumptions of a linear regression model.

#### 6.3 R-Square and Adjusted R-Square Analysis

- Using regplot on train data sets and verify R-Square and Adjusted holds good
- Using regplot on test  data sets and verify R-Square and Adjusted holds good

#### 6.4 Model Evaluation Observation
- Error terms are normally distributed
- Residual anaylsis holds good git of the model since there is no pattern found
- The model performing well with training and test data sets with small drop in R-Square value
- The model explains 84% of the variance in the training data, indicating a solid fit to the training set.
- The slight drop in R-squared from 0.84 (train) to 0.82 (test) suggests minimal overfitting and good generalization.
- The Adjusted R-squared values of 0.83 on training data and 0.81 on test data suggest that the model is generalizing well to unseen data.

