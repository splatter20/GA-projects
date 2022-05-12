# Capstone Project: Can COE Premiums be predicted?

## Background  

Certificate of Entitlement (COE) represents a right own a vehicle and use it on Singapore roads for 10 years.  
COEs are separated into 5 different vehicle categories (A - E). [Source](https://onemotoring.lta.gov.sg/content/onemotoring/home/buying/upfront-vehicle-costs/certificate-of-entitlement--coe-.html)

- **Cat A**: Car, except fully electric car, with engine capacity up to 1,600cc and Maximum Power Output up to 97kW (130bhp); and fully electric car with Maximum Power Output up to 110kW (147bhp)
- **Cat B**: Car, except fully electric car, with engine capacity above 1,600cc or Maximum Power Output above 97kW (130bhp); and fully electric car with Maximum Power Output above 110kW (147bhp)
- **Cat C**: Goods vehicle and bus
- **Cat D**: Motorcycle
- **Cat E**: Open – all except motorcycle


Quotas allocated by government and is calculated by:
1) Number of vehicles taken off the roads (number of vehicles deregistered).  
2) Allowable growth in vehicle population.  
3) Adjustments to account for changes in taxi population, replacements under Early Turnover Scheme , past over-projections and expired or cancelled temporary COEs, etc.

The current allowable growth in vehicle population from 2022 to 2025 is at 0% for all categories except Cat C which allowed a 0.25% growth.

COE are obtained via bidding exercises which are held on the 1st and 3rd week of each month and each bidding will last for 3 working days. The quota for each category will be announced before the start of each bidding exercise. The COE premium will keep increasing until the number of bidders who are prepared to pay more than or at bidding price equals the quota at the close of the exercise. At the end of each bidding exercise, bidders whose bids are above or equal to the CCP will get a COE. All successful bidders in the same vehicle category will pay the same quota premium for that particular category

When purchasing a car in Singapore, the price of the COE is usually factored together with the overall price of the car. There are also several car packages which car dealers offer. [Source](https://www.sgcarmart.com/news/writeup.php?AID=5)  

For simplicity of this project, I will be talking about 1 type of COE package: 
- Guaranteed COE

Under this scheme, the dealer will get the COE within a fixed period of time, usually three months. The car dealer would have to ensure that they successfully bid for a COE anytime within the three months. The price of this package is fixed and the dealer will be able to earn the difference if they are able to successfully bid for a lower COE than they had priced on the package.


## Problem Statement

As a car dealer in Singapore, I have been tasked to create a model which will be able to accurately predict COE premiums. This will allow the company to maximise profits by accurately bidding when the COE premiums are lower and at the same time set prices that are competitive in the market.

On the other hand, being able to predict the COE premiums accurately would also allow for more successful bids in a shorter time period and this would help to increase the reputation of the company.

**Goal:** To create an accurate model to predict COE premiums, I will be focusing on reducing the Mean Squared Error (MSE) of the predictions made by the model. Additionally, since successful bids are also important, I will create a success metric to ensure that the prediction will be more than or equal to the premium price.

## Dataset

The datasets were extracted from statistics given by LTA:  
https://www.lta.gov.sg/content/ltagov/en/who_we_are/statistics_and_publications/statistics.html (COE PDF)

However, as the LTA statistics were given in a PDF format, they were hard to extract. Another website which has uploaded the statistics had been used instead:  
https://docs.google.com/spreadsheets/d/1Ma8dm_rdtdfNp8ONUG5ykFHwrEg1GFC3ObOMualMVBM/edit#gid=0 (Compiled COE)

I had performed cross checking with the statistics with LTA ensure that the data compiled was correct.

Other datasets were extracted from singstat:  
https://tablebuilder.singstat.gov.sg/

Straits Times Index Pricing chart was extracted from Wall Stree Journal:  
https://www.wsj.com/market-data/quotes/index/SG/STI/historical-prices (STI prices)


## Method 

**1) Data Cleaning and Exploratory Data Analysis**  
- Perform data cleaning and extract essential features for further analysis
- Understanding the data in the various datasets

**2) Feature Engineering and selection**
- Separating data for different vehicle categories
- Engineer features(Scarcity, lags for time sensitive data)

**3) Modelling**
- Analyse data and create predictive modelling with ARIMA / SARIMA models, linear regression and neural network models.
- Tune model hyperparameters to improve on the model performance.

**4) Error Analysis**
- Checking on where the model fails and to further improve on the model.

**5) Predictions**
- Utilising the predictive model to predict the prices of upcoming COE premium.

**6) Extending the model**
- Extending the model created for cat A to other predicted COE premiums of other vehicle categories.

## Summary of Findings and Recommendations

While COE lasts for 10 years, it is easy to assume that there will be some seasonality in this timeseries modelling. However, as there are only 20 years of data, the model was not able to pick up on the seasonality.

Below is the summary of the models created.

|**Model**|**Univariate / Multivariate**|**MSE**|**Success %**|
|---|---|---|---|
|ARIMA|Univariate|170,766,416|43.3|
|Linear Regression|Univariate| 86,105,841|83.5|
|Linear Regression|Multivariate|627,776,111|100.0|
|Linear Regression w Lasso|Multivariate|629,132,479|100.0|
|Linear Regression w Ridge|Multivariate|629,122,991|100.0|
|SARIMA| Univariate|151,149,668|50.5|
|RNN - LSTM|Univariate|15,133,745|40.5|
|RNN - GRU|Univariate|7,453,959|75.9|
|RNN - GRU 1|Multivariate|8,823,055|20.3|
|RNN - GRU 2|Multivariate|19,145,021|5.1|
|RNN - GRU 3|Multivariate|10,139,610|19.0|

According to our goal, I want a model with a low MSE and a high success rate. However, as success rates can be adjusted, I include a new metric which was the average difference and std of the difference to actual premiums. 

Having a low average difference to the actual coe premiums would allow for us to be competitive in the market while having a low standard deviate would allow us to have consistent earnings.

## Conclusion

The model that was eventually selected was the Univariate GRU model as it has the lowest MSE and after adjusting the success rates to be the same across all models, it  has the lowest difference and std to the actual premiums.

## Other areas for future exploration

As a add on to the model, I would like to be able to predict for more than just the next bidding exercise. If the model is able to predict for 2 - 3 months ahead, the company will be able to price the COE packages accordingly and advice customers if there is an upward or downward trend in the COE premiums.

While extending the model to predict for both category B and E, the model used had its hyperparameters tuned to the dataset of category A values. In order to make the models even more accurate to each of their own categories, the models should retune their hyperparameters in order to get the best MSE.
