# King County House Sales Study

**Author: Kamile Yagci**

## Overview
In this project, I will analyze the King County House Sales. The Windermere Real Estate Agency hired me to develop a model to predict the house sale prices in King County. The agency plans to use the results of this study when advising their customers/homeowners on determining the value of their houses. They believe that the pricing the house correctly will increase the efficiency of sales. The agency also would like to learn about the effect of renovations on house sale prices, so they can advise the customers to do renovation or not. 

### Business Questions
* What are the main predictors for House Sale Price?
* Create a model to predict the House Sale Price.
* Do house renovation affects the Sale Price?

## Data
I will use the King County House Sales Data for this study. The data file is 'kc_house_data.csv'

### Explore Data 
Data contains 
* information on 21597 houses sold between May 2014 - May 2015.
* 21 columns: 'id', 'date', 'price', 'bedrooms', 'bathrooms', 'sqft_living', 'sqft_lot', 'floors', 'waterfront', 'view', 'condition', 'grade', 'sqft_above', 'sqft_basement', 'yr_built', 'yr_renovated', 'zipcode', 'lat', 'long', 'sqft_living15', 'sqft_lot15'

Since our main goal is predicting sale price, let's look at the distribution of the House Sale Prices. The left plot shows the number of houses in y axis and sale price on the x-axis. The right plot shows the same distribution on log scale. It will be easier to see the outliers on the log scale.

![Price Distribution](/figures/priceDist.png)




