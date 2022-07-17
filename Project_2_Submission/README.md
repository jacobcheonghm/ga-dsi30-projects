# Project 2 - Ames Housing Data and Kaggle Challenge



## Problem Statement

AgentAmes.com is a popular property website that connects buyers and sellers in the Ames property market. A recent focus group conducted
by the marketing team surfaced the top pain-point experienced by users is that they have no idea how to price their property on the platform.
This has resulted in sellers not getting bids for their property listings and many have resulted in shunning the platform altogether.
Therefore, the management team has tasked the tech team to leverage this consumer insight by creating a regression model that can be
built into the platform to help users gauge the sale price of their properties to reduce the gap between seller's and buyer's price expectations.



## Data Dictionary

For detailed information on the dataset, please review the [data description](http://jse.amstat.org/v19n3/decock/DataDocumentation.txt).

## Data Cleaning

Data cleaning is first conducted on the train.csv dataset. Outliers (oversized properties) indicated in the data description have been removed. A quick check also revealed 3 columns with very high count of null value, namely the "Alley", "Pool QC" and "Misc Feature" columns which have been dropped from the train dataset.

After dropping the 3 aboved-mentioned columns, there are still 23 features that still contained null values. Upon furter investigation, majority of the null values were wrongly classified as null due to the use of terms such as "NA" and "None". Appropriate imputation are then carried out and check done to ensure all null values are addressed accordingly.

There are multiple ordinal features in the dataset that are recorded as strings, therefore we have mapped the rankings to equal scales to facilitate processing them as numerical features during the features filtering phase.

3 features that were recorded as years have also been converted to age (by taking the difference between 2022 and the year recorded) for more intuitive intepretation should they end up as important predictive features.

## Feature Selection

### Selecting Numeric (Continuous and Discrete) Features

We first derived the correlation of all the numeric features with sale price and identified those with correlation more than or equals to 0.5. After which we plot a heatmap to identify any occurences of correlation among the predictive features.

INSERT HEAT MAP PICTURE

We identified 6 numeric features ("1st Flr SF", "TotRms AbvGrd", "Garage Cars", "Bsmt Qual",c"Exter Qual", "Kitchen Qual") to be dropped as including them in the model will not add much additional information for the model.

### Selecting Categorical Features

We will attempt to get an overview of the catergorical features by plotting the count plots and box plots to help narrow down features we want to keep in our regression model.

Insert BOXPLOT COUNTPLOT COMPARISON

From the above comparisons, we observe that the five features above have very high occurence in only 1 or 2 categories within the feature. The boxplot also show limited variations among the catergories when plotted against the Sale price, therefore these may not add more predictive powers to our model and will be dropped from the model.

## Preprocessing and Modeling

After narrowing down the categorical features to keep, we performed one-hot encoding for all the remaining categorical features. A quick check on the summary statistics shows that we do have at least 1 feature in the model that will help predict the sale price.

INSERT OLS REGRESSION RESULT

Before modeling, we applied the same imputation for null values and dropped the same columns in test.csv dataset.

A train test split (with test size at 20%) is then performed on the train dataset before scaling all the data based on X_train.

Four models are then constructed and a summmary of their performance can be found in the table below:

|        Model Type | Cross Val Score | Train |  Test |      RMSE |      α |
|------------------:|----------------:|------:|------:|----------:|-------:|
| Base Model (Mean) | NA              | NA    | NA    | 77296.53  | NA     |
| Linear Regression |      -4.028e+22 | 0.900 | 0.882 | 1.461e+16 |     NA |
|       Ridge Model |           0.870 | 0.897 | 0.881 |  28339.55 |  52.14 |
|       Lasso Model |           0.872 | 0.892 | 0.879 |  28173.42 | 394.12 |

## Evaluation

When we look at the train and test R² score for our linear regression model, it may seem we have a winner as it achieved a relatively high train score of 90% and a slightly lower 88% test score. However after conducting a 5 fold cross validation it reveals it weakness by returning a RMSE of 1.461e+16 which is significantly higher than that from our baseline model. This shows the Linear Regression model grossly oversimplifies the data and has a very high bias.

Both Ridge and Lasso model score very similarly across the various metric with the Lasso model acheiving slightly better RMSE result of 28173.42. When consulting the top 10 features (by highest absolute coefficient value) of both model, we see that they share 9 common features in their top 10 list, in fact the top 3 features and ranking are exactly the same for both model. The commonality in features used and their weightage may help to explain the similarity in their performance.

Thus having considered the above, we will select the **lasso model** as our model of choice as the lasso model helps to reduce the number of features used from 146 to 86 which reduced complexity with little compromise on performance.

|    | **Ridge Model Features** | **Absolute coef** | **Lasso Model Features** | **Absolute coef** |
|---:|-------------------------:|------------------:|-------------------------:|------------------:|
|  1 |              Gr Liv Area |      24235.069243 |              Gr Liv Area |      27075.970103 |
|  2 |             Overall Qual |      14692.860819 |             Overall Qual |      16421.239136 |
|  3 |            Total Bsmt SF |      13255.270896 |            Total Bsmt SF |      11744.972113 |
|  4 |           MS SubClass_20 |       8805.940788 |     Neighborhood_NridgHt |       8086.166642 |
|  5 |              Garage Area |       8325.112076 |              Garage Area |       7164.533261 |
|  6 |             Mas Vnr Area |       7463.643542 |             Mas Vnr Area |       6991.376686 |
|  7 |     Neighborhood_NridgHt |       7228.967847 |                Remod Age |       6205.456312 |
|  8 |                 Prop Age |       6506.338406 |                 Prop Age |       5784.698415 |
|  9 |                Remod Age |       6417.992318 |     Neighborhood_StoneBr |       5698.449658 |
| 10 |            Sale Type_New |       6337.496198 |           MS SubClass_20 |       5629.266237 |

Insert Lasso Feature diagram

**Intepretation of top 5 features in Lasso Model**

1. Gr Liv Area - A 1 square feet increase in above ground living area can increase the sale price by $27076.
2. Overall Qual - A 1 grade increase in overall quality rating can increase the sale price by \$16421.
3. Total Bsmt SF - A 1 square feet increase in total basement are can increase the sale price by \$11745.
4. Neighborhood_NridgHt - If the property is located in the Northridge Heights neighborhood, the sale price can increase by \$8086.
5. Garage Area - A 1 square feet increase in garage are can increase the sale price by \$7165.

## Conclusion and Recommendations

In conclusion, the tech team will recommend to build a **price recommender function** for AgentAmes.com website and app based on the **lasso regression model**. Since it requires less features compared to the other models, it translates to **ease of use** for our users as it also means they need to provide us with less information in order to get a reasonably good price prediction.

When seller's list their property with a price that is not too far off the market rate, it is more likely to attract bidders and in turn increases the chance of a successful sale. With more sales conducted through our platform, it will solidify AgentAmes.com's reputation as a effective platform for sellers and buyer of properties.

## Future Developments and Improvements

AgentAmes should continue collecting data from the property transactions and try to discover more features that will help to predict final sale price. While the current model does a good job, it is still quite heavily dependant on features related to size of the property.

We can also work toward further reducing the complexity of the model to make it even easier for our users to take advantage of our price prediction model. With lesser required data to furnish, it also increases the chance of the model making good price prediction. 