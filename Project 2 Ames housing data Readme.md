# Project 2 - Ames Housing Data and Kaggle Challenge


**Kaggle Submission Score**
[DSI-US-11 Regression Challenge](https://www.kaggle.com/c/dsi-us-11-project-2-regression-challenge) score is provided as per below,
![Kaggle score](https://github.com/crystalmunyee/Project_2_Ames_Housing_Challenge/blob/main/kaggle%20challenge%20submission%20score.JPG)


**Executive summary**

These are the models that we have tested to understand the correlation on the Ames Iowa data set features and its sale price.

| Model            | Penalty     | Value of a | Training Acuracy | Testing Acuracy | RMSE   | Interpretation/Conclusion                                                                                                                           |
|:------------------|:-------------|:------------:|:------------------|:-----------------|:--------|:-----------------------------------------------------------------------------------------------------------------------------------------------------|
| linear regession | NA          | NA         | -1696222         | -1600552        | 0.1561 | 15 features. train and test score is negative which is a poor fit to the model.                                                                     |
| pipe1_ridge      | RIDGE       | 18.31      | 0.8750           | 0.8594          | 0.1559 | 15 features. train and test score better than linear reg, RMSE on the lower side which is better as well.                                           |
| pipe1_lasso      | LASSO       | 0.01       | 0.8722           | 0.8543          | 0.1587 | 15 features. train and test score slightly lower than ridge. RMSE also higher than ridge. Ridge has better fit and accuracy.                        |
| pipe1_elasticnet | ELASTIC NET | 0.5        | 0.8310           | 0.8102          | 0.1811 | 15 features. train and test score lower than both ridge and lasso. RMSE also higher than ridge and lasso. Ridge has better fit and accuracy.        |
| pipe2_ridge      | RIDGE       | 11.50         | 0.8776            | 0.8633          | 0.1538 | 14 features+ skewness correction. Combined features give better R2 score for train and test. RMSE is also lower in the reduced feature ridge model. |

**Problem Statement**
- We are real estate agents which are using the Ames housing data to create a regression model that predicts the price of houses in Ames, IA. 
- Understanding what features have strong correlation to houses prices in Ames.
- Update housing estate investors and potential homeowners in Ames.
- Build machine learning models to describe the local housing market and to use these models to predict house prices in that market

**Data Cleaning and EDA**
- In this portion we found a number of null data for certain features in the train data set.
    *PoolQC,Misc Feature and Alley has more than 50% data missing. We decide to drop these features to prevent incorrect impute on the data.
-In the next step we realize that some of the features can be categorized under the same characteristics.
    *Number of rooms, Area, Quality and Misc.
-Looking into each data by similar characteristics such as garage set ('Garage Type', 'Garage Yr Blt','Garage Finish', 'Garage Cars', 'Garage Area', 'Garage Qual','Garage Cond'),we can see that some input is not standardized. So we imputed 0 to the garage cars and area for those that do not have a garage.
-Similary for the basement set, we imputed unfinished for bsmt finish type 2 for the row that clearly shows there is unfinished SF.
-We also imputed all the bsmt sf related features to 0 for those that have no garage because its Na for all the bsmt conditions and total bsmt sf.
-For fireplace quality we will leave the NaN as it is since it represents no fireplace.
- The distribution on the sales price shows that its skewed to the right. To prevent bias on the data, we will use the logarithm of the sales price to give it a normal distribution.
- Outliers identified in this project includes the garage year built which is in year 2207 (not possible). This will be imputed with reference to year built since we see a positive propertional relationship in the line plot.
-Besides this, outliers from gr living area above 4000 gives does not add value to the mode. Thus, we dropped these values from the dataset.
- For the summary statistics for train/test data,overall mean and std is quite high for some features such as lot area which is why we need to use standard scalar later on to ensure all the features are on a uniform scale.
-Salesprice std or variation lower since its converted to log sales price.
-Based on the heatmap for all the features, we can identify the features with highest pearson coefficient to be impacting salesprice the most.
-Factors with positive influence on salesprice are identified with the ridge coefficient:('Exter Qual','Gr Liv Area','Kitchen Qual','Overall Qual','Garage Area','Garage Cars','Total Bsmt SF','1st Flr SF','Bsmt Qual','Year Built','Year Remod/Add','Fireplace Qu','Full Bath','Garage Yr Blt','Foundation_PConc','SalePrice')
-Plotting each of these features with a line plot or boxplot shows a clear correlation to salesprice. 
-For every 1k SF increase in Gr living area, we expect $160,921 increase in sale price!

**Preprocessing and Modeling**
- For the Nominal and discrete categorical variables, it will be one-hot encoded.
- For the Ordinal data with different scales, we will map and encode them on a fixed 1 to 5 scale.
- We have identified top features with linear relationships to the salesprice previously using the heatmap and individual EDA plots.
- The data been scaled using standard scalar before running the regression analysis to prevent uniform data values from impacting the final result.
- We then proceed to do a train test split to validate the accuracy of the train model.
- Utilize feature selection such as lasso, ridge, elantic net and the pearson coefficient we are able to identify and remove noisy features. 
- We tested and evaluated a variety of models such as linear regression, lasso, ridge,elastic net to identify a production algorithm that has better R2 score and lower RMSE.
- Does the student defend their choice of production model relevant to the data at hand and the problem?
- The model that we selected is the ridge regularization due to better overall R2 score for train and test and lower RMSE. We also did an alpha test run to find the most optimum alpha value.
- Some multi-collinear features were also identified and combined to form 1 feature to further improve the model. In the end we concluded that ridge regression with reduced features gives the best score and RMSE.

**Evaluation and Conceptual Understanding**
- The data we got from the train/test ridge score with combined features gives us confidence that it will be able to predict the test split sales price with lower overfitting and higher accuracy compared to linear regression.

**Conclusion and Recommendations**
In conclusion, from the models that we have tested it shows ridge and lasso to have the best r2 score and lower RMSE. But in this context we will use ridge to build the model. The features with the highest ridge coefficient tells us that area, quality and built year has the most influence on the sales price in Ames Iowa housing. We use this knowledge that we learn to predict the salesprice for the test set which helps us as real estate agents to position ourselfs in a more market competitive edge to recommend to clients on suitable housings. 

The recommendations we have for buyers that wish to upscale their property to fetch better pricing is to buy houses with bigger living area and renovate it with better quality finishings and a fireplace to get better investment returns.



**References**

*https://nycdatascience.com/blog/student-works/house-price-prediction-in-ames-iowa/
*http://jse.amstat.org/v19n3/decock/DataDocumentation.txt


