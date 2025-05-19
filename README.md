# US-Regional-Sales

## Introduction



## Sales - Seasonal Changes


#### Figure 1. 
<img src="https://github.com/konpayne/US-Regional-Sales/blob/main/Images/Order%20Frequency%20in%202018.png" width=700 height=400>

#### Figure 2. 
<img src="https://github.com/konpayne/US-Regional-Sales/blob/main/Images/Order%20Frequency%20in%202019.png" width=700 height=400>

#### Figure 3. 
<img src="https://github.com/konpayne/US-Regional-Sales/blob/main/Images/Oder%20Frequency%20in%202020.png" width=700 height=400>

#### Figure 4. 
<img src="https://github.com/konpayne/US-Regional-Sales/blob/main/Images/Order%20Frequency%20from%202018%20to%202020.png" width=700 height=400>


## Sales - Channels

#### Figure 5. 
<img src="https://github.com/konpayne/US-Regional-Sales/blob/main/Images/Sales%20Channel%20%23%20of%20Sales.png" width=700 height=400>

#### Figure 6. 
<img src="https://github.com/konpayne/US-Regional-Sales/blob/main/Images/Sales%20Channel%20Total%20Revenue.png" width=700 height=400>

#### Figure 7. 
<img src="https://github.com/konpayne/US-Regional-Sales/blob/main/Images/Sales%20Channel%20Total%20Profit.png" width=700 height=400>

## Sales - Products

#### Figure 8. 
<img src="https://github.com/konpayne/US-Regional-Sales/blob/main/Images/Product%20%23%20of%20Sales.png" width=700 height=400>

#### Figure 9. 
<img src="https://github.com/konpayne/US-Regional-Sales/blob/main/Images/Product%20Profit.png" width=700 height=400>


## Predicting Unit Price
### Response Variable 


#### Figure 10. 
<img src="https://github.com/konpayne/US-Regional-Sales/blob/main/Images/Histogram%20of%20Unit%20Price.png" width=700 height=400>

#### Figure 11. 
<img src="https://github.com/konpayne/US-Regional-Sales/blob/main/Images/QQ%20Plot%20of%20Unit%20Price.png" width=700 height=400>

### Linear Regression Model 


#### Figure 12. 
![Diagnostic Plots of Linear Regression Model](https://github.com/konpayne/US-Regional-Sales/blob/main/Images/Diagnostic%20Plots%20of%20Linear%20Regression%20Model%20-%20Reduced.png)

### Neural Network Regression Model


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

Only install into Rstudio and ensure that all packages included in the code are properly nstalled. 

Data was obtained from Kaggle.com at the link below, but the Kaggle page originally obtained the data from data.world

https://www.kaggle.com/datasets/talhabu/us-regional-sales-data
