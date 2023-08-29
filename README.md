# Used_Car_Price_Neural_Network
Exploration and cleaning of Craigslist used car dataset

# Data Cleaning & Preperation
This dataset required extensive cleaning as it is taken directly from Craigslist on a quarterly basis - it can be found here: https://www.kaggle.com/datasets/austinreese/craigslist-carstrucks-data

Due to the propensity of some people to spam the same listing repetitivly, which anyone who has browsed auto listings on craigslist has seen, there were hundreds of thousands of duplicate listings.  118,246 unique vins out of a dataset of over 420,000.  

I droped all duplicate VIN listings, keeping the first occurance, then dropped the collumns id, size, VIN, cylinders, and paint_color to reduce the dimensionality of the dataset for one hot encoding, and becuase those columns contained many nulls and seemed to be amount the least important based on my experience. 

I replaced nulls in the drive column with rwd for the sake of simplicity, and dropped nulls in the type column due to their not being many and its high relative importance.  I then investigated nulls in the condition column and decided to drop a few manufacturers who had such a small number of listings that it would not be possible to train the model effectivly and added a column for current year.  To remove erronious listings and rare collectors cars which would be irrelevant for the business purpose of these models, I dropped vehicles older than 1980 and priced higher than 250,000. I preformed string matching to consolidate model names into groupings, then ordinally encoded the columns I thought were appropirate, and hot encoded the rest.

# Modeling

I created a linear regression model 
Linear Regression Metrics:
Mean Squared Error (MSE): 71650204.98086838
Mean Absolute Error (MAE): 4036.4780770523016
R^2 Score: 0.5580593081098308
Root Mean Squared Error (RMSE): 8464.644409593848

A lasso model
Lasso Regression Metrics:
Mean Squared Error (MSE): 226054719.89175013
Mean Absolute Error (MAE): 8226.178904497372
R^2 Score: -0.39431254021776896
Root Mean Squared Error (RMSE): 15035.116224750314

An optimized Random Forest regression
Random Forest Metrics:
Mean Squared Error (MSE): 28748816.022772335
Mean Absolute Error (MAE): 3065.0940752772754
R^2 Score: 0.8226764042344913
Root Mean Squared Error (RMSE): 5361.792239799332

And an optimized Neural Network
Neural Network Metrics:
Mean Squared Error (MSE): 24856168.0
Mean Absolute Error (MAE): 2878.360595703125
R^2 Score: 0.8466863789627694
Root Mean Squared Error (RMSE): 4985.59619140625

The most noteworthy is the Neural Network which can be used to help predict used car prices with an accuracy of R2 = 0.847 
These models can help you make informed decisions about inventory and pricing.

# Key Findings
High Accuracy: The Neural Network model has an 
R2 score of 0.847, making it the best preformer in this metric.  It also outperforms all the other models in every other metric, having a lower MSE, MAE, and RMSE.

Neural Network Feature Importance:

Odometer: The number of miles a car has traveled significantly influences its price.
Year/Car Age: The age of the car is another major determinant.
Drive (4WD): Cars with 4-wheel drive generally hold higher value.
Transmission: A preference for automatic transmission affects car prices.
Regional Impact: The value of a car appears to vary by region.

# Residuals Analysis: 
While the residuals are generally well-distributed, there is a small but noticeable linear downward line present, indicating that the models tend to overestimate car prices as they increase. This suggests there may be additional factors or non-linear relationships not yet accounted for.

# Recommendations
Further Analysis: Investigate other potential factors or features that may capture the nonlinear aspects of car pricing. These could include interaction terms, polynomial features, or other domain-specific variables.

Segmentation: Consider building different models for different price ranges or car types to better capture these nuances.

Complex Models: To capture non-linearity, more complex models or ensembles can be explored.
