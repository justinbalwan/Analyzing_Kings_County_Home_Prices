# Analyzing Kings County Home Sale Prices

![Kings County](https://res.cloudinary.com/sagacity/image/upload/c_crop,h_667,w_1000,x_0,y_0/c_limit,dpr_auto,f_auto,fl_lossy,q_80,w_1080/bellevue_fall_lnb6qm.jpg)


## Project Overview

This project analyzes home, real-estate elements in Kings County, Washington. The elements are imported, manipulated, and modeled to help predict home prices in Kings County.

### Business Problem

As an employee for a real estate agency, I am analyzing information from the Kings County House Sales dataset. Given several factors from the dataset, I aim to provide advice to my agency on how home renovations will increase the values of homes in Kings County; more specifically, I aim to determine which home renovation factors are the most lucrative. By understanding which factors increase a home's value, my agency will be able to successfully help homeowners sell their homes for a maximized profit.

### The Data
#### Data Understanding
The data from the Kings County House Sales dataset contains a variety of home-related factors, such as the year the home was built, the square footage of the living area or lot, the number of bedrooms or bathrooms, or several related factors regarding the condition of the home itself. In this stage of the project, I chose to understand how my target variable, "price", was represented throughout the dataset.
#### Data Cleaning
Next, I chose to clean my data by dropping unnecessary columns that would not help me achieve the result I was aiming for. These columns included:

- id
- date
- waterfront
- view
- grade
- sqft_above
- sqft_basement
- yr_renovated
- zipcode
- lat
- long
- sqft_living15
- sqft_lot15

After dropping these columns, the remaining columns I was experimenting with were:
- price
- bedrooms
- bathrooms
- sqft_living
- sqft_lot
- floors
- condition

I checked the data type of each column and discovered the only non-numeric column: condition. I then transformed the condition column by converting it from a non-numeric data type to a numeric data type by using one hot encoder. This broke down condition into it's subsections: cond_avg, cond_fair, cond_good, cond_poor, cond_verygood. Each subsection became data type float.

After this, I separated my remaining columns into distinctive 'continuous' and 'categorical' arrays. I then modeled each array to analyze it further; I created histograms for my categorical variables and a scatter matrix for my continuous variables.
![categorical histograms](data/categorical%20histograms.jpg)
![continuous scatter matrix](file:///Users/justin/Desktop/Flatiron/continuous%20scatter%20matrix.jpg)

#### Data Preparation
Since my target variable is 'price' I had to ensure there were nothing wrong with it since it is my target variable. I attempted to use the train v. test method to normalize the target variable. It dropped the target variable from the original dataframe and set it as "y". All other variables were "X". This process made me realize the power of logging; it can be a useful tool to help normalize features.

Right after normalizing price, I chose to build a heatmap that displays the correlation of all the columns in relation to my target variable, price.
![heatmap](file:///Users/justin/Desktop/Flatiron/heatmap.png)
From the heatmap, I discovered that my most correlated variable was sqft_living. I checked how strongly correlated this variable was to my target variable by using cross validation. My train score and validation score were about .01 off, indicating that it was a very strong model.

Lastly in the preparation stage, I wanted to create two models; one that shows the most to least strongly correlated variables, and another that shows a scatter matrix of all the variables, intending to highlight the non-normal distributions that exist. This would allow me to determine which variables I would need to normalize during my modeling stage.
![heatmap2](file:///Users/justin/Desktop/Flatiron/heatmap2.png)
![scattermatrix2](file:///Users/justin/Desktop/Flatiron/scattermatrix2.png)

## Modeling
First, I checked for multicollinerarity and heteroscedacity for my most correlated predictor variable: sqft_living.
![sqft_living_regression_plots](file:///Users/justin/Desktop/Flatiron/sqft_living_regression_plots.png)
To resolve the heteroscedacity, I performed a log transformation on sqft_living.
![sqft_living_log_regression_plots](file:///Users/justin/Desktop/Flatiron/sqft_living_log_regression_plots.png)
As you can see, the funnel-like shape transformed into a more scattered, normalized plot.

#### Baseline Model
Baseline Score R²: 0.0
#### Simple Linear Regression Model
Simple Linear Regression R²: 0.49268789904035093
#### First Multiple Linear Regression Model
First Multiple Linear Regression R²: 0.34665470419864375
#### Second Multiple Linear Regression Model
Second Multiple Linear Regression Model R²: 0.45535727584899854
#### Third Multiple Linear Regression Model
Third Multiple Linear Regression Model R²: 0.5343447212266113

[models_rsquared_values](file:///Users/justin/Desktop/Flatiron/models_rsquared_values.png)
[model_regression_coefficients](file:///Users/justin/Desktop/Flatiron/model_regression_coefficients.png)

## Conclusion
After comparing each model to one another, it was determined that my third/final multiple regression model had the highest adjusted R-squared value. What does this mean? Since my third model had the highest adjusted R-squared value, it better fits my observation. It will be the model we will use to make predictions going forward since most of the scattered data points are centered/normalized around the line of best fit; there are smaller differences between observed data and fitted values (fitted values are on the line of best fit).

In addition, it was found that the strongest home price predictor was sqft_living, which is what we expected.

In the future, I think it would be useful to include more predicitive factors besides sqft_living and sqft_lot. This will help to get a better understanding of what other types of home renovation factors would be useful in increasing the values of homes.
