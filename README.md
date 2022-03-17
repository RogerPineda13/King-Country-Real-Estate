# King County Real Estate Advice
## Overview
This project uses statistical analysis, simple linear regression and  multivariate linear regression modeling to analyze housing data in King County, Washington. The purpose of this project is to provide an accurate model for Seattle based, Every Door Real Estate Company, that can be used to advise their clients on both sales and purchases of residential real estate in King County.
## Business Problem & Key Questions
As a real estate agency firm, their primary role is to connect potential buyers and sellers of real estate properties. It is therefore imperative that they provide an accurate information and services to their clients and ensure both parties consent on a fair property price. Every Door Real Estate Company needs a model that provides statistically significant information on features that impact housing value and predicts a fair price based on those features and will make ssure the client is content on their decision of choosing Every Door Real Estate Company. 

* Which specific features significantly influence the overall value of the house?
* How significant are the locations of the house within King County?
* Is it possible to predict the housing price based on its features?
* How can Every Door Real Estate Company utilize this model to increase their profit? 
## Data Understanding
The following dataset was given and used to build the model.
* data/kc_house_data.csv

The dataset was provided to allow for deep exploration into King County's housing data. The dataset included specs for over 21,000 homes with giving their square footage, rating of construction quality, number of bedrooms and bathrooms and most importantly their price.

After some exploratory data analysis it was deemed the data wasn't in a state the would give out proper models instantly with some columns not being in a managable numeric value and others missing data. Also was determined many columns would not be useful in future model creation they were not included in our working dataframe.

Heavy use of the efficient tools within scikit-learn's library allowed us to manage the data to allow for model creation down the  line. 
SimpleImputer to deal with missing values in our waterfront amd view columns.
OneHotEncoder to deal with non continous categorical features and creating columns for each category of that feature that was represented in the column as a value of 0 or 1 in reference on whther that house had that spcific feature column or not.




## Modeling
The modeling is divided into two parts: inferential and predictive. 
1) Predictive modeling
2) Inferential modeling


### Predictive Models
* The goal of our prediction model is to achieve the 'best' model to predict our target price with high accuracy and low error. Pretty much getting to the idea of predicting price given certain parameters such as number of floors or whether it's view is avergae or excellent.
As to deal with heteroscesdsitdy we made the decision to log transform our target variable, price.

Now with our dataframe fully sorted we created our dummy regressor with price and the log of price. 
#### Simple Regressor
Seeing that our target is our log_price column we tried to see which columns had a positive and substantial correlation to it. 
* sqft_living 
* bathrooms 
* grade_num
* bedrooms

These features had a strong individual correlation to our target, log_price, but sqft_living had the highest value that was not a categorical so it was deemed as the right feature to be the one to be put into our simple model.

![Screenshot 2021-11-19 125446](https://user-images.githubusercontent.com/92402366/142669110-8c6ea1f0-68ff-4607-a833-511232f608d6.png)




With Y as our target and X our housing feature.(Y=price, X =sqft_living).

After spliting up our variables into two subsets(Train and Test data) we performed proper scaling to sqft_living as to prepare it for simple linear regression.

Finally we calculated the value for our predicted model and determined our regression scores as well as mean squared error for train and test.

This simple model gave us values for our Train data of (~.38147061) and our Test data of (~.37977233). These low values show that there is much improvement that can be done to the model.

#### Multi-Feature Model
With the simple model we just saw how our target, price, was impacted by just sqft_living. But you can you apply multiple features to our models to get a more accurate model. 
##### Multi-Feature-Model 1 Price with Sqft_living and View
After repeating the steps for the regression like in the simple regression but with two features being apllied we get values for our Train data of (~.41453618) and for our Test data of (~.41423440). So we see that our model has improved over our simple so it shows adding more features to our model improves it.
##### Multi-Feature-Model 8
After many iterations (7 more in total) we get to our final model(8) where in our model we included the following features
* sqft_living
* zipcode(encoded)
* Basement
* floors(encoded)
* waterfront
* view(encoded)
* condition(encoded)
* grade_num(encoded)
* bathrooms(encoded)
* bedrooms(encoded)

The model produced scores for our Train data of (~.85896066) and for our Test data of (~.85536786). This was the best model that we were able to produce it gives a fair amount of accuracy with reference to price

![Screenshot 2021-11-19 114436](https://user-images.githubusercontent.com/92402366/142659982-4a4f847a-6810-40bb-9ff0-2cbb4bccb00b.png)
We achieved a root-mean-square-error(RSME) of 105,546.
![Screenshot 2021-11-19 121343](https://user-images.githubusercontent.com/92402366/142663697-23b84621-3681-4d3b-9d59-1a73013c0f32.png)

### Inferential Model

* The goal of our inferential model is to estimate an association between the price and other features and understand their relationship.

The features that were included in our inferential model were as follows

* sqft_living (179.4199)
* waterfront (379,400)
* view
* * Excellent (269,600)
* * Good (93,090)
* * Fair (-5143)
* * Average (our reference therefore no coef)
* * None (-91,010)
* zipcode
* * 98039 'top zipcode' (1,400,000)
* * 98004 '2nd best zipcode' (830,000)

(next to each of the features are their coefficient numbers)

Since grade_num was highly correlated to sqft_living we deemed it to be correct to exclude it from the inferential model.

Our adjusted R-sqaured value from the inferential model came to be (.78)
The coefficient numbers relates to

## Recommendations and Conclusions
Through exhausted data cleaning and model creation we deem that the data set given to not have enough within it to allow a proper model to be built that can accurately predict our target, price. With our best predicting model having a mean square error of 105,546 dollars it give way too much unncertainty on price. We have notice that as the price of the homes increase that the amount of error increases therefore limiting the amount of homes our model would be functional. Withour inferential model we violated a number of assumptions of linear regressions therefore making it as well a poor model. But with this in mind our model expresses that to focus more on the square footage of the home, whether it has a basment or not, which zipcode it falls in, amount of floors of the home, whther it has a waterfront or not, its view rating, the condition of the home, the amount of bathrooms, the amount of bedrooms and the overall building grade of the home. 


