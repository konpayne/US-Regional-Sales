# US-Regional-Sales

## Introduction

The data used in this exercise is composed of a subset of anonymized sales from a company across the United States. A breakdown of the variables can be found at the bottom of this exercise in the Variables Explained section. There are a total of 7991 observations across 15 variables, which are 8 categorical, 4 numeric and 4 date data types. The CustomerID and CurrencyCode variables were dropped since they provide no significant information in the following analyses. This is the first time I have worked with date data in the format of DD/MM/YY, so it was converted into YYYY-MM-DD for computational ease. No missing values were present, so there was no need for data imputation or removal. The goal of this exercise is to find insights in the trends of sales from this company, in which I will investigate seasonal and yearly changes, sales channel distribution and top selling products. I will also build a regression model to determine the estimated unit price based on the relevant parameters. 

## Sales - Seasonal Changes

To evaluate the seasonal changes in sales I examined the frequency of order dates. As shown below in Figure 1, the overall number of sales in 2018 remains consistent until early to mid winter in which there is a slight drop followed by a peak in Janurary. Followng the sales into 2019 in Figure 2, the number of sales stabilizes, with a very slight decrease throughout the year. Ending in Figure 3 in 2020, the sales are nearly exact across all months. Therefore, excluding the slight drop and bounce back in 2018, there appears to be no consistent seasonal changes in sales for this company. Taking a look at Figure 4, the sales across all 3 years appears nearly constant, however there is a slight consistent decrease since the peak in January of 2019, only about a 1-2 orders per day drop. 

#### Figure 1. 
<img src="https://github.com/konpayne/US-Regional-Sales/blob/main/Images/Order%20Frequency%20in%202018.png" width=700 height=400>

#### Figure 2. 
<img src="https://github.com/konpayne/US-Regional-Sales/blob/main/Images/Order%20Frequency%20in%202019.png" width=700 height=400>

#### Figure 3. 
<img src="https://github.com/konpayne/US-Regional-Sales/blob/main/Images/Oder%20Frequency%20in%202020.png" width=700 height=400>

#### Figure 4. 
<img src="https://github.com/konpayne/US-Regional-Sales/blob/main/Images/Order%20Frequency%20from%202018%20to%202020.png" width=700 height=400>


## Sales - Channels

The channels which products are purchased through were divided into four categories: in-person, online, wholesale, and distributor. As seen in Figure 5, the most number of sales were conducted through in-person stores, followed by online, distributor then wholesale. I wanted to see if this pattern would remain if I changed the the metric from number of sales to revenue (calculated by (Unit.Price X Order.Quantity) X (1-Discount.Applied)), which can be seen in Figure 6. The same order of sales channel is present. I then considered if the metric was changed to profit (calculated by revenue - (Unit.Cost*Order.Quantity)), if there would be an significant changes. Looking at Figure 7 the same order appears and in the same relative proportions to one another. Therefore by looking at all of these metrics, the most sales and money are produced through in-store purchases. 

#### Figure 5. 
<img src="https://github.com/konpayne/US-Regional-Sales/blob/main/Images/Sales%20Channel%20%23%20of%20Sales.png" width=700 height=400>

#### Figure 6. 
<img src="https://github.com/konpayne/US-Regional-Sales/blob/main/Images/Sales%20Channel%20Total%20Revenue.png" width=700 height=400>

#### Figure 7. 
<img src="https://github.com/konpayne/US-Regional-Sales/blob/main/Images/Sales%20Channel%20Total%20Profit.png" width=700 height=400>

## Sales - Products

The top selling product refers to the product with highest number of sales, which as observed in Figure 8 is a tie between products #4 and #37 at 200 sales between 2018 and 2020. Looking at the breakdown of the sales channels, the products appear to sell in equal proportions across all product types. The order of which most sales occur is consistent with the previous findings of in-store, online, distributor and wholesale. I decided to see if the most profitable products would also be the most sold products, which was not the case as seen in Figure 9. By far the most profitable product is #23 and unsurprisingly the distribution of sales channels in profits from the products follows the same order previously seen. Therefore, the products #4, #23 and #37 must be the most significant items for this company. 

#### Figure 8. 
<img src="https://github.com/konpayne/US-Regional-Sales/blob/main/Images/Product%20%23%20of%20Sales.png" width=700 height=400>

#### Figure 9. 
<img src="https://github.com/konpayne/US-Regional-Sales/blob/main/Images/Product%20Profit.png" width=700 height=400>


## Predicting Unit Price

In order to best predict the unit price of this company I utilized a neural network regression model in order to capture the nonlinear trends between the response and predictors variables. A linear regression model with stepwise selection based on minimum Bayesian Information Criterion (BIC) was also included as a comparison of the model performance with the neural network regression model. A train and test split of 80/20 on the original dataset was used for later computation of the root squared mean error to compare model predictive power. The R-squared value was also calculated to compare the percentage of variance present in the data explained by the respective model. All assumptions from the neural network and linear regression mdoels were assessed with diagnostic plots. The dataset was modifed from its original form, as the CustomerID and manmade variables of revenue and profit were removed. To account for any possible monthly or seasonal trends I did not observe previously, a new variable was made with the month of each order date (OrderDate_Month). I also created a variable for the amount of days shipping took to deliver the product (ShippingTime = DeliveryDate - ShippingDate), in case the unit price included shipping costs. Then all date related variables were removed (ProcuredDate, OrderDate, ShippingDate, DeliveryDate). The final datset for the regression analysis consisted of 10 predicotrs with 6 factors and 4 numeric data types. 

### Response Variable 

As observed in Figure 10, the unit price is not normally distributed due to the lack of a typical normal bell curve, which is confirmed in the QQ plot of Figure 11, in which the blue line represents a normal distribution so the trend line is severely nonlinear. This indicates that the relationship between the repsonse and predictor variables will be nonlinear. Typically the response variable and predictors can be coerced to be more normally distributed through transformations, however in order to conduct a nueral network regression all variables must be standardized, which was conducted with the standardize function from the datawizard package. To remain consisten with the later comparisons of model metrics (RMSE and R-squared), no more transformations were done. 

#### Figure 10. 
<img src="https://github.com/konpayne/US-Regional-Sales/blob/main/Images/Histogram%20of%20Unit%20Price.png" width=700 height=400>

#### Figure 11. 
<img src="https://github.com/konpayne/US-Regional-Sales/blob/main/Images/QQ%20Plot%20of%20Unit%20Price.png" width=700 height=400>

### Linear Regression Model 

Two linear regression models were tested in this exercise, the full model including all predictors, and the reduced model containing all the predictors selected during the stepwise selection process based on the minimum BIC. The linear regression models were fit using the lm() function in the stats package of R. The results from the stepwise selection process indicated that the optimal model only has one predictor: unit cost. Comparing the RMSE of both models, the full model had a value of 0.00246 and the reduced model had an RMSE of 0.00489. The R-squared for the full and reduced model were 0.8934 and 0.8863, respectively. Considering how close the two models were in model comparison metrics I performed an ANOVA to determine if they were significantly different. The results from the ANOVA had a p-value of 0.9874, much larger than the desired alpha level of 0.05 so the full and reduced models were not signficantly different. Therefore, the reduced linear regression model can be used to capture as much information in the dataset as the full regression model with a far smaller dimensionality. 

Looking at the diagnostic plots in Figure 12, some problems arise for the assumptions of a linear regression model. Looking at the posterior predictive check and linearity plots, the distributions do not resemble normality, indicating that the reduced linear regression model is not capturing nonlinear trends in the data. Another issue is the variance, as observed in the Homogeneity of Variance plot, which shows a spread of points in a rough funnel shape, starting tighly pacted in the lower values and slowly spreading across as the values increase. This funnel shaped pattern is a strong sign of heteroscedacity in the model. However, the influential observations plot shows no signs of outliers that would negatively impact the performance of the model. The Normality of Residuals plot has some curves within it, but they are tolerable as majority of the points fall along or near the normal reference line. Overall, the assumptions of the linear model are not met due to intrinsic nonlinear trends in the data that cannot be fitted by this model. 

#### Figure 12. 
![Diagnostic Plots of Linear Regression Model](https://github.com/konpayne/US-Regional-Sales/blob/main/Images/Diagnostic%20Plots%20of%20Linear%20Regression%20Model%20-%20Reduced.png)

### Neural Network Regression Model

The architecture of the neural network regression model in this exercise is 2 hidden layers comprised of 15 and 10 neurons respectively. The dataset had to be modified from its original form for the neuralnet() function of the neuralnet package to handle factor type data. The factor variables were manually converted into dummy varaibles using the model.matrix() function. With this modified dataset the neural network regression model was determined to have an RMSE value of 0.02189 and an R-squared value of 0.6882. 

The assumptions for a neural network regression model are less constrictive than the linear regression model due to no assumptions of normality, multicollinearity and homoscedascity. However, examining these aspects of the model are stll useful in determining how well the model fits the data. First looking at Figure 13, the trend line is following a near perfect line indicating that the model is accurately predicting the unit price, however there is quite a large spread along this trend line. In Figure 14, the residuals are spread relatively evenly across the line, but follow a curved line that suggests the architecture of this neural network is not fully capturing the nonlinear trends in the data. Both Figure 15 and 16 show the residuals having a relatively normal distribution, though Figure 16 shows some trailing of the tails, but majority of the points fall along the normal reference line. In figure 17, the variances show a curved trend indicating heteroscedascity, which the model does not assume but if prevalent enough may be causing issues in prediction capabilites. Overall, the neural network model shows signs that the architecture needs further testing to better fit the nonlinear trends within the data. 

#### Figure 13. 
<img src="https://github.com/konpayne/US-Regional-Sales/blob/main/Images/Predicted%20vs.%20Actual%20(NN).png" width=700 height=400>

#### Figure 14. 
<img src="https://github.com/konpayne/US-Regional-Sales/blob/main/Images/Residuals%20vs.%20Predicted%20(NN).png" width=700 height=400>

#### Figure 15. 
<img src="https://github.com/konpayne/US-Regional-Sales/blob/main/Images/Histogram%20of%20Residuals%20(NN).png" width=700 height=400>

#### Figure 16. 
<img src="https://github.com/konpayne/US-Regional-Sales/blob/main/Images/QQ%20Plot%20of%20Residuals%20(NN).png" width=700 height=400>

#### Figure 17. 
<img src="https://github.com/konpayne/US-Regional-Sales/blob/main/Images/Scale-Location%20(NN).png" width=700 height=400>

### Model Comparisons

As mentioned previously, the reduced linear regression model is an inappropriate fit for this dataset due to the nonlinear trends within the data resulting in most assumptions not being met. The linear model was supposed to represent a baseline comparison for the neural network regression model, so these breaks in assumptions were expected. However, the RMSE of the reduced model is 0.00489 compared to the larger RMSE of the neural network model at 0.02189. As well as the reduced model having an R-sqaured value of 0.8863 with the neural network model having a smaller value of 0.6882. This was an unexpected outcome, but the architecture of the neural network model is not optimal as I did not have the time or computing power to use cross-validation to find the best number of hidden layers and then test different variations of neurons. In order to present the findings in this exercise, the nerual network code has to run for multiple hours, so only a few neuron choices were tested. Given more time and computational power I would optimize the arhcitecture of the neural network model to find the best number of hidden layers and neurons that minimize RMSE. Also, it is possible that the training dataset was insufficient and did not contain enough data to properly train the neural network. Given additional time and resources I hypothesize that the neural network regression model would perform significantly better than the reduced linear regression model in predicting unit price due to its innate capability to capture nonlinear trends between the response and predictor variables. 

## Variables Explained

OrderNumber = code for each order

SalesChannel = the channel the sale was made through (online, in-person, distributor, wholesale)

WharehouseCode = code for the warehouse involved in the sale

ProcuredDate = date when products were procured (DD/MM/YY)

OrderDate = date when order placed (DD/MM/YY)

ShipDate = date when order shipped (DD/MM/YY)

DeliveryDate = date when order arrived to customer (DD/MM/YY)

CurrencyCode = code for currency used (all USD)

SalesTeamID = a unique number for each sales team 

CustomerID = a unique number for each customer

StoreID = a unique number for each store

ProductID = a unique number for each product 

OrderQuantity = number of product ordered in sale

DiscountApplied = discount applied to the order 

UnitCost = the cost of a single unit of the product

UnitPrice = the price of a single unit of the product sold 

## Dependencies

Only install Rstudio and ensure that all packages included in the code are properly nstalled. 

Data was obtained from Kaggle.com at the link below, but the Kaggle page originally obtained the data from data.world

https://www.kaggle.com/datasets/talhabu/us-regional-sales-data
