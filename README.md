# Assignment
## A model based on the S&P Case-Schiller home price index
In this project, we have developed a data science model to analyze and understand the relationship between key supply-demand factors and the S&P Case-Schiller Home Price Index in the United States. The model utilizes publicly available datasets to examine how these factors have influenced home prices over the past two decades, specifically from 2000 to 2020. By examining the data and building the model, we aim to provide insights into the factors that have impacted home prices during this period[2000-2020]
## Features which can impact US home prices 
[image]

## Data points collected
### Demographic
* population

### Income-age distribution (average annual expenditure by people in a particular age group)
* average expenditure 25-34
* average expenditure 35-44
* average expenditure 45-54
* average-expenditure-55-64

![demographic](https://github.com/yasirali09/task.llc/blob/master/images/demographic.JPG)


## Mortgage
[HCAI - Housing Credit availibility index](https://www.urban.org/policy-centers/housing-finance-policy-center/projects/housing-credit-availability-index)
* HCAI_GOVT
* HCAI_GSE - Government sponsorship enterprises
* HCAI_PP - Portfolio and private label securities loan
* MORTGAGE30US

![Mortgage](https://github.com/yasirali09/task.llc/blob/master/images/mortgage.png)

## Health of the economy
* GDP
* CPI - Consumer price index (expressed in terms of %)
* private_job_gains (Number of new private job gains in a month)
* personal_saving_rate (expressed in terms of %)
* UNRATE - Unemployment rate
* unrate_construction - Unemployment rate in construction industry

![economic](https://github.com/yasirali09/task.llc/blob/master/images/economic.png)

## Construction Industry
* employees_construction - Number of employees in construction industry
* industrial_production_cement
* residential_const_val - Total value of residential construction(monthly)
* producer_price_index_concrete_brick

![Construction](https://github.com/yasirali09/task.llc/blob/master/images/construction.png)

## Housing industry
* houses-for-sale-to-sold - Number of houses for sale vs number of houses that got sold
* home-ownership-rate - Percentage of U.S. homes that are owner-occupied
* house_units_completed - Number of new house units completed in a given month
* retail_sales_home_furnishing_stores - Sales of home furnishing stores

![Housing](https://github.com/yasirali09/task.llc/blob/master/images/housing.png)

## Infrastructure and permits
* nonresidential_const_val - Total value of residential construction(monthly)
* permits - Building permits

![infrastructure](https://github.com/yasirali09/task.llc/blob/master/images/infrastructure.png)

### Some of the features are in annual and quaterly frequency, we have converted them into monthly frequency by assuming equal distribution of change of feature value during that period.

## Capturing rate of change and trend

* Some of the features are not linearly correlated with the target, but derivative of these features are influencing the prices.
* To capture such derivates, we have taken cumulative sum, rolling sum (mostly 12 months), rate of change (past 12 months) and trend (introduced a categorical variable, "UP" for uptrend and "DOWN" for downtrend )

![infrastructure](https://github.com/yasirali09/task.llc/blob/master/images/infrastructure.png)

The variable permits is not linearly correlated with the target variable, but its derivate, (cumulative sum) has a correlation coefficient of 0.66 **-- Average length of time from start to completion of new privately owned residential buildings in the U.S is roungly 8 - 12 months , hence we have taken window size of 12 months**


## Feature selection

We have used Lasso regression, with alpha = 0.014 for feature selection

![featimp](https://github.com/yasirali09/task.llc/blob/master/images/featimp.png)

#### Features with zero coefficients (eliminated)

* avg_expenditure_45_54
* avg_expenditure_55_64
* GDP
* private_job_gains
* MORTGAGE30US
* permits
* producer_price_index_concrete_brick
* UNRATE
* unrate_construction
* avg_expenditure_35_54
* HCAI
* cpi_cum
* houses_for_sale_to_sold_cum
* private_job_gains_cum
* house_units_completed_cum
* industrial_production_cement_rate
* pvt_owned_house_under_const_rate
* permits_rate
* house_units_completed_rate
* HOUSES_S2S_TREND_UP
* PERMITS_TREND_UP
* private_job_gains_trend_UP
* pvt_owned_house_under_const_trend_UP
* house_units_completed_trend_UP

#### Features with non-zero coefficients (influential factors)

* residential_const_val 8.522123
* employees_construction 7.202071
* gdp_per_capita 7.075599
* industrial_production_cement_cum 4.421657
* HCAI_GSE 4.366235
* permits_cum 4.031410
* pvt_owned_house_under_const_cum 2.859470
* home_ownership_rate 2.373083
* HCAI_PP 2.350209
* house_units_completed 2.175655
* houses_for_sale_to_sold_rate 1.015123
* population 0.859498
* GDP_RATE 0.495746
* pvt_owned_house_under_const 0.286402
* retail_sales_home_furnishing_stores 0.284348
* avg_expenditure_35_44 0.275713
* houses_for_sale_to_sold 0.224290
* CPI_TREND_UP 0.179261
* GDP_TREND_UP 0.036036
* industrial_production_cement -0.076664
* CPI -0.076826
* private_job_gains_rate -0.339181
* EMP_CONST_TREND_UP -0.436380
* avg_expenditure_25_34 -0.461559
* personal_saving_rate -0.971455
* nonresidential_const_val -1.144469
* EMP_CONST_RATE -3.735800
* HCAI_GOVT -4.522580

A Lasso regression with a alpha 0.014 is used to model the S&P Case-Schiller Home Price Index with the above features

![prediction](https://github.com/yasirali09/task.llc/blob/master/images/prediction.png)

#### Metrics 
* MSE = 35.23196017633148
* RMSE = 5.935651621880404
* R2 = 0.84


## Sources
* [Worldbank](https://data.worldbank.org/)
* [Stlouisfed](https://fred.stlouisfed.org/)
* [Urban](https://www.urban.org/)
