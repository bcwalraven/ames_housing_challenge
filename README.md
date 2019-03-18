
# Problem Statement:



To develop a predictive model for home sale prices in Ames, Iowa based on sales from 2006 to 2010, that will accurately predict the market price for as many home owners as possible. 

# Executive Summary:



Our goal is to build a model that will accurately predict the market price for as many home owners as possible. 

Preperation of the data included removing null values or imputing them based on the data dictiornary or other features in the data. The dataframe also incuded both categorical and numeric data that needed to be parsed through to determine how they can best be included included in the final model. Multiple features that rated the quality of certain house features were changed to ordinal values on a scale of 1-5. 

The EDA process revealed the following insights:
- The skew of the saleprices was 1.558, however taking the LN reduced the skew to 0.443. This was identified as a likely way to increase the performance of the model
- There was a significant amount of mulitcolinearity between the features.
- There were two obvious outliers that had high square footage but sold for low sale price, these were removed. Taking the LN of this feature imporved its correlation with saleprice almost as much as removing the outliers.
- Overall quality was highly coordinated as a set ordinal values. The feature was left as is without changing to dummy variables.
 - Overall condition had an unusual number of 5 ratings which reversed the underlying positive correlation. This feature was not used. 

The following featuers were engineered from the data:
- Calculating the total finished floor area significantly improves the correlation compared to above ground living area.
- Calculating the total number of bathrooms significantly increases its correlation
- Year built was converted to age which reflected the age of the house at time is was sold
- Positive features totaled the number of positive featurs in the house
- Negative features totaled the number of negative features in the house 


Results and Conclusions:
- The lasso model was chosen as the best linear regression model
- You can build a strong predictive model for home sale prices with feature engineering and a few strong predictors
- If more features are added I expect taking the LN of saleprice and features will be more effective
- For future submissions, incorporating a wider variety of features despite lower correlation and multicolinarity may boost performance if incorporated with regularization through Ridge, Lasso, ElasticNet

# Data Dictionary:

---

**Engineered Features**

|Feature|Name|Type|Description|
|---|---|---|---|
|**total_fin_sf**|Total Finished sf|*int*|The sum of above ground living area and total basement sf minus unfinish basement sf.|
|**total_baths**|total number of baths|*float*|The total number of bathrooms in the house (half baths count as 0.5).|
|**age**|House Age|*int*|Age of the house when it was sold.|
|**positive_features**|Positive Features|*float*|The count of positive features in the house.|
|**negative_features**|Negative Features|*float*|The count of negative features in the house.|

---

**Original Features**
The data dictionary for the original features can be found here:

https://www.kaggle.com/c/house-prices-advanced-regression-techniques/data



# Results and Conclusions:


Results and Conclusions:

The final model used the following numeric features: 

- overall_qual
- total_fin_area
- garage_area
- total_bath 
- age 
- kitchen_abvgr 
- enclosed_porch
- positive_features
- negative_features

And the following features as dummy variables:
- neighborhood
- ms_zoning
- house_style 
- bldg_type
- lot_shape
- ms_subclass 
- mo_sold
- functional 
- sale_type
- central_air
- foundation

The lasso model was found to perform significantly better than ridge or an unregularized liner regression when testing on the kaggle data set.

With these features the mean cross validation score was 0.9162 and the root mean square was 22,095. This resulted in a Kaggle rmse of approximately 23,000 on the 30% kaggle test and approximately 30,000 on the 70% kaggle test. A model with the same featuers but trained on data with the outliers perfromed better on the 70% kaggle test but worse on the 30% kaggle test.

There still appears to be some overfitting between the training data and kaggle test data. To address this next steps would be to score a model on the full kaggle test data with all features, and then remove features as necessary to reduce overfitting. In order to optomize the rmse score, outliers should likely be kept in the data, and calculating the log of saleprice and certain features such as total finished area should be considered as well.

Finally, using an ensamble approach with XGBoost or RandomForest should be considered as well. 
