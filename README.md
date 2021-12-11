# King County House Sales Study

**Author: Kamile Yagci**

## Overview
In this project, I will analyze the King County House Sales. The Windermere Real Estate Agency hired me to develop a model to predict the house sale prices in King County. The agency plans to use the results of this study when advising their customers/homeowners on determining the value of their houses. They believe that the pricing the house correctly will increase the efficiency of sales. The agency also would like to learn about the effect of renovations on house sale prices, so they can advise the customers to do renovation or not. 

### Business Questions
* What are the main predictors for House Sale Price?
* Create a model to predict the House Sale Price.
* Do house renovation affects the Sale Price?

## Method
I will follow the following steps for this study:
1. Data
    * Load
    * Explore
    * clean
    * Check correlation
3. Model - Apply linear regression and do validation
    * Baseline model with one best predictor
    * Second and Third models: Search for the next best predictors
    * Final Model with five best predictors
3. Interpret 
    * Interpret Final Model
    * Check multiple regression assumptions
4. Future work


## Data
I will use the King County House Sales Data for this study. The data file is 'kc_house_data.csv'

### Explore Data 
Data contains 
* information on 21597 houses sold between May 2014 - May 2015.
* 21 columns: 'id', 'date', 'price', 'bedrooms', 'bathrooms', 'sqft_living', 'sqft_lot', 'floors', 'waterfront', 'view', 'condition', 'grade', 'sqft_above', 'sqft_basement', 'yr_built', 'yr_renovated', 'zipcode', 'lat', 'long', 'sqft_living15', 'sqft_lot15'

Since our main goal is predicting sale price, let's look at the distribution of the House Sale Prices. The left plot shows the number of houses in y-axis and sale price on the x-axis. The right plot shows the same distribution on log scale. It will be easier to see the outliers on the log scale.

![Price Distributions](/figures/priceDist.png)

### Clean Data
The Project 2 infomation page recommends to remove these columns to ease the analysis: ['date', 'view', 'sqft_above', 'sqft_basement', 'yr_renovated', 'zipcode', 'lat', 'long', 'sqft_living15', 'sqft_lot15']

I will follow the advise and remove these variables except 'yr_renovated' and maybe 'zipcode'

* 'date' and 'view' are apparently not significant predictors for Sale Price; good to remove
* sqft_above' and 'sqft_basement' will have multicollinearity with 'sqft_living'; so better to remove
* 'lat' and 'long' determine the location; I will use the zipcode for location and so no need for these variables
* 'sqft_living15' and 'sqft_lot15' may have multicollinearity with 'sqft_living' and 'sqft_lot'; OK to remove
One of my business question is about the effect of renovation on sale price; so needs to keep 'yr_renovated'

In general, location is an important factor in house prices. I want to take a closer look at 'zipcode', before making a decision on keeping it or not. 
The below plot shows the sale price vs zipcode and the average price per zipcode.

![Zipcode Distribution](/figures/zipcode.png)

The house prices peak at few zipcodes. How significant is this? I decided to keep 'zipcode' in my data. I have applied hot-encoding to create dummy variables for each zipcode.

#### Remove unneccessary columns
I dropped the columns: 'date', 'view', 'sqft_above', 'sqft_basement', 'lat', 'long', 'sqft_living15', 'sqft_lot15'

#### Handle missing values
* Null values in 'waterfront' is filled with zero.
* A boolean variable created for 'yr_renovated' and the null/zero values in yr-renovated are filled with yr_built.

### Correlation
I drew the correlation heat map to see the correlations between variables.

![Heat Map](/figures/heatMap.png)

There is good correlation between Price and (bedrooms, bathrooms, sqft_living, grade).

There is also correlation among bedrooms, bathrooms, sqft_living, grade. We have to consider multicollinearity effects using them in modeling. I should only use one of them in my model.

There is also high correlation between yr_renovated and yr_built. Again, only one of them can be used in my model.

The variables that have highest correlation with Sale Price are 'sqft_living' and 'grade'. Definition of these variables:
* sqft_living: square footage of the home (continious variable)
* grade: overall grade given to the housing unit, based on King County grading system (categorical varible)


## Model
