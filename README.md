# Kaggle_House_Price_Solution


## Table Of Content
[Project Descriptiom](https://www.kaggle.com/competitions/house-prices-advanced-regression-techniques)<br>
1. Project background analysis<br>
    1.1. Market and social factors affecting house prices<br>
    1.2. House price data<br>
    1.3. Model building and evaluation metrics<br>
2. load and view data<br>
3. [EDA](https://github.com/kklsy109/Kaggle_House_Price_Solution/blob/main/House_Price_EDA_Python.ipynb)<br>
    3.1 View price distribution<br>
    3.2 Significant numerical predictors<br>
    3.2.1 Correlation between numeric variables and house prices<br>
    3.2.2 Overall Quality<br>
    3.2.3 GrLivArea<br>
4. [Default value padding and variable type conversion](https://github.com/kklsy109/Kaggle_House_Price_Solution/blob/main/House_Price_EDA_Python.ipynb)<br>
    4.1 View default and 0 values<br>
    4.2 Imputing missing data<br>
    4.3 Transform some numerical variables into categorical variables<br>
    4.4 Label Encoding for Categorical Variables<br>
5. [Visualization](https://github.com/kklsy109/Kaggle_House_Price_Solution/blob/main/House_Price_EDA_Python.ipynb)<br>
    5.1 Correlations again<br>
    5.2 Visual analysis of GrLivArea and other surface-related variables<br>
    5.3 Overall Quality, and other Quality variables<br>
    5.4 Garage variables<br>
    5.5 Basement variables<br>
    5.6 Neighborhood<br>
    5.7 MSSubClass<br>
    5.8 Delete irrelevant columns<br>
6. [Data cleaning](https://github.com/kklsy109/Kaggle_House_Price_Solution/blob/main/House_Price_EDA_Python.ipynb)<br>
    6.1 Data Standardization<br>
    6.2 Process data for model preparation<br>
7.  [Model linear fit](https://github.com/kklsy109/Kaggle_House_Price_Solution/blob/main/%20House_Price_Modeling.ipynb)<br>
    7.1 Ridge Regression<br>
    7.2 Random Forest<br>
    7.3 Lasso<br>
    7.4 XGBoost<br>


### 1. Project background analysis
#### 1.1 Market and social factors affecting house prices
The purpose of conducting house price prediction is to estimate the cost of a property using specific details related to the property. This can greatly assist both buyers and sellers in making the wisest choices when buying or selling a house. It also provides valuable information about market trends and forecasts for investors and individuals involved in the real estate market.

Currently, there are many factors that can influence the price of a house, so we need to consider different features. These features include the size of the house, its location, accessibility to transportation, nearby amenities, age of the property, number of floors, style, and more. To predict the price, I will use a linear regression model to train these features and find their relationship with the price.

#### 1.2 House price data
Dataset: The dataset I have chosen is sourced from the Kaggle housing price prediction competition. This dataset includes the feature values for each transaction and the corresponding property prices.

#### 1.3 Model building and evaluation metrics
This project utilized Ridge, Random Forest, Lasso and XGBoost models as target models for predicting housing prices, and validated the model's performance using mean squared error (MSE).

### 2. load and view data

First load the required libraries

![](https://github.com/kklsy109/Kaggle_House_Price_Solution/blob/main/pictures/1.png)

load and view data

![](https://github.com/kklsy109/Kaggle_House_Price_Solution/blob/main/pictures/2.png)

Merge datasets for subsequent processing

![](https://github.com/kklsy109/Kaggle_House_Price_Solution/blob/main/pictures/3.png)


### 3. EDA
#### 3.1 View price distribution
First, draw a histogram of the price distribution to see which price range has the most houses. From the graph, it can be observed that the distribution of property prices closely resembles a normal distribution. This indicates that selecting the appropriate fitting parameters can lead to better predictions of price trends.

![](https://github.com/kklsy109/Kaggle_House_Price_Solution/blob/main/pictures/4.png)

#### 3.2 Significant numerical predictors

#### 3.2.1 Correlation between numeric variables and house prices

I start by looking at which numeric variables have a high correlation with sales price.

![](https://github.com/kklsy109/Kaggle_House_Price_Solution/blob/main/pictures/5.png)
![](https://github.com/kklsy109/Kaggle_House_Price_Solution/blob/main/pictures/6.png)

It can be seen that a total of 10 numeric variables have a correlation of at least 0.5 with SalePrice. All these correlations are positive.Besides,there is multicollinearity between GarageCars and GarageArea, with a high correlation of 0.89.

I will visualize the relationship between SalePrice and the two predictors most correlated with SalePrice; 'OverallQual' and 'GrLivArea'.

#### 3.2.2 Overall Quality

The correlation between overall quality and sales price is as high as 0.79. It rates the overall material and finish of the house on a scale of 1 (very poor) to 10 (excellent).

![](https://github.com/kklsy109/Kaggle_House_Price_Solution/blob/main/pictures/7.png)

#### 3.2.3 GrLivArea

The second highest numerical variable in correlation with SalesPrice is Above Grade Living Area (0.71). After all, larger houses are generally more expensive.

![](https://github.com/kklsy109/Kaggle_House_Price_Solution/blob/main/pictures/8.png)

From the graph, it can be observed that there are two outliers, which are the two houses with significantly larger living areas but lower SalePrices. I will remove these two outliers.

### 4.Default value padding and variable type conversion

#### 4.1 View default and 0 values

![](https://github.com/kklsy109/Kaggle_House_Price_Solution/blob/main/pictures/9.png)
![](https://github.com/kklsy109/Kaggle_House_Price_Solution/blob/main/pictures/10.png)

"PoolQC" "MiscFeature"
"Alley"
"Fence"
"FireplaceQu"

These 5 columns have missing values over 50%, so it has to be done with droping them.

"PoolArea"
"3SsnPorch"
"LowQualFinSF" "MiscVal"
"BsmtHalfBath"
"ScreenPorch"
"BsmtFinSF2"
"EnclosedPorch" "HalfBath"
"MasVnrArea"
"BsmtFullBath"
"2ndFlrSF"
"WoodDeckSF"
"Fireplaces"

These 14 columns have zero values over 50%, so it has to be done with droping them.

![](https://github.com/kklsy109/Kaggle_House_Price_Solution/blob/main/pictures/11.png)

#### 4.2 Imputing missing data

I choose three ways to fill missing values:

1.I will fill the rest of the attribute default values with 'modes'

2.For the default value in the classification column I will fill it with 'None'

3.Fill the 'LotFrontage' default with the 'median'

3.For the 'GarageYrBlt' variable, I will fill it with the value of 'YearBuilt'

4.Finally delete the 'Utilities' column

![](https://github.com/kklsy109/Kaggle_House_Price_Solution/blob/main/pictures/12.png)

"KitchenQual" 1

"MSZoning" 4

"Functional" 2

"Exterior2nd" 1

"Exterior1st" 1

"SaleType" 1

"Electrical" 1

"GarageArea" 1

"GarageCars" 1

"BsmtFinSF1" 1

"BsmtUnfSF" 1

"TotalBsmtSF" 1

These fitures contain very little missing values, thus, we can fill them with their modes.

![](https://github.com/kklsy109/Kaggle_House_Price_Solution/blob/main/pictures/13.png)

"GarageCond" 

"GarageQual"

"GarageFinish" 

"GarageType" 

"BsmtExposure"

"BsmtFinType2"

"BsmtFinType1" 

"MasVnrType" 
"BsmtCond" 

"BsmtQual" 

These four columns have too many missing values, which are also catogerical values. Thus, we can fill them with "None" catogery.

![](https://github.com/kklsy109/Kaggle_House_Price_Solution/blob/main/pictures/14.png)


For the 'GarageYrBlt' variable, I will fill it with the value of 'YearBuilt'

![](https://github.com/kklsy109/Kaggle_House_Price_Solution/blob/main/pictures/15.png)

Fill the 'LotFrontage' default with the 'median'

![](https://github.com/kklsy109/Kaggle_House_Price_Solution/blob/main/pictures/16.png)

#### 4.3 Transform some numerical variables into categorical variables
"YrSold", "MoSold" and "MSSubClass" are three variable types that are numeric, but they are actually categorical variables. Therefore, I converted their categories into categorical variables.

![](https://github.com/kklsy109/Kaggle_House_Price_Solution/blob/main/pictures/17.png)

#### 4.4 Label Encoding for Categorical Variables
I am performing label encoding on some categorical variables because the values are ordered, which allows for better observation of linear correlations.

![](https://github.com/kklsy109/Kaggle_House_Price_Solution/blob/main/pictures/18.png)

### 5.Visualization
#### 5.1 Correlations again

![](https://github.com/kklsy109/Kaggle_House_Price_Solution/blob/main/pictures/19.png)

I have rechecked the correlations. It can be observed that the number of variables with a correlation of at least 0.5 with SalePrice has increased from 10 to 16 after data processing.

#### 5.2 Visual analysis of GrLivArea and other surface-related variables


![](https://github.com/kklsy109/Kaggle_House_Price_Solution/blob/main/pictures/20.png)

It can be seen that there is a high degree of linear correlation between them.

#### 5.3 Overall Quality, and other Quality variables

![](https://github.com/kklsy109/Kaggle_House_Price_Solution/blob/main/pictures/21.png)
![](https://github.com/kklsy109/Kaggle_House_Price_Solution/blob/main/pictures/22.png)

It can be seen that there is a high degree of linear correlation between them.

#### 5.4 Garage variables

![](https://github.com/kklsy109/Kaggle_House_Price_Solution/blob/main/pictures/23.png)
![](https://github.com/kklsy109/Kaggle_House_Price_Solution/blob/main/pictures/24.png)


#### 5.5 Basement variables

![](https://github.com/kklsy109/Kaggle_House_Price_Solution/blob/main/pictures/25.png)
![](https://github.com/kklsy109/Kaggle_House_Price_Solution/blob/main/pictures/26.png)


From the analysis, it can be observed that there seems to be no linear relationship between 'BsmtFinSF2' and 'BsmtFinType2' variables with housing prices. Therefore, I have decided to drop them.

Delete irrelevant data

Next, I will analyze the correlation between the category attribute and the house price in a visual way

#### 5.6 Neighborhood

![](https://github.com/kklsy109/Kaggle_House_Price_Solution/blob/main/pictures/27.png)

It can be seen that 'NoRidge' has the highest house price, followed by 'NridgHt' and 'StoneBr'


#### 5.7 MSSubClass

![](https://github.com/kklsy109/Kaggle_House_Price_Solution/blob/main/pictures/28.png)

#### 5.8 Delete irrelevant columns

![](https://github.com/kklsy109/Kaggle_House_Price_Solution/blob/main/pictures/29.png)

### 6.Data cleaning

#### 6.1 Data Standardization

![](https://github.com/kklsy109/Kaggle_House_Price_Solution/blob/main/pictures/30.png)
![](https://github.com/kklsy109/Kaggle_House_Price_Solution/blob/main/pictures/31.png)

Uniformly perform one-hot processing on all the string data in the data to facilitate fitting.

![](https://github.com/kklsy109/Kaggle_House_Price_Solution/blob/main/pictures/32.png)

#### 6.2 Process data for model preparation
Displaying the distribution of the target data, it can be seen that it conforms to the characteristics of a normal distribution, but the variance of the data is too large.

It is processed by log1p to make its distribution closer to the standard normal distribution, as shown in the right figure.

![](https://github.com/kklsy109/Kaggle_House_Price_Solution/blob/main/pictures/33.png)

### 7.Model linear fit

First, I compared the Ridge, Random Forest, Lasso and XGBoost models as target models and fitted the processed data separately.

Within the three models, I iterated through the corresponding hyperparameters to adjust the model parameters for the best results. During the iteration process, I chose cross-validation as a method to evaluate the model's scores and error rates. By plotting the curves of hyperparameters and cross-validation scores, it can be observed that the model fitting results can be locally optimized to the best.

#### 7.1 Ridge Regression

![](https://github.com/kklsy109/Kaggle_House_Price_Solution/blob/main/pictures/34.png)

#### 7.2 Random Forest

![](https://github.com/kklsy109/Kaggle_House_Price_Solution/blob/main/pictures/35.png)

#### 7.3 Lasso

![](https://github.com/kklsy109/Kaggle_House_Price_Solution/blob/main/pictures/36.png)

#### 7.4 XGBoost

![](https://github.com/kklsy109/Kaggle_House_Price_Solution/blob/main/pictures/37.png)
![](https://github.com/kklsy109/Kaggle_House_Price_Solution/blob/main/pictures/38.png)

XGBoost works best with a score of 0.0389










