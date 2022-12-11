# Price Prediction for Vacation Houses in King County, WA 
Author: Vickie Yang
Pic: Mountains in King County
![king-county-mountain](https://user-images.githubusercontent.com/117051182/206802107-e8870cc3-7edf-4cdf-827e-a0ef0710cfc6.jpeg)

## Business Problem
As a result of the increasing demand for purchasing vacation homes following the pandemic, the FS Real Estate data analytics team conducted a data analysis over the vacation house sales for the King County area. The analysis aims to answer the following questions for vacation home buyers:
* What kind of house should they buy？
* What renovations are needed to increase the estimated value of their vacation homes
* What is a best price to purchase?

Below are the filters used for selecting vacation homes in the dataset:
*Scenic view, close to waterfront, or greenbelt
*Decent house grade and condition that doesn't require lots of maintenance.

## Stakeholder
All vacation home buyers who are interested in the King County Area.

## Dataset
The dataset was provided by the FS Real Estate research department that covers all the sales of houses in the King County area for the period of 2021 and 2022. The houses that were above 5 million, below 200k dollars, and less than one bathroom were identified as outliers. After the outliers were removed, there were a total 3925 of sales records that satisfied the vacation home criteria. Details of the dataset can be found in the “data” folder.

## Variables and Metrics
The **Dependent Variable** is **Vacation Housing Sale Price**.
The **Independent Variables** are **housing grade, condition, waterfront, view, greenbelt, sqft living**. 
The prediction model is expected to use independent variables to predict the dependent variable. 
**Metrics:** Price, House Ranking scores (Grade and Condition), External Environment scores (waterfront, greenbelt, view). 

## First-look of Data Analysis
Before we jump to the prediction model, the FS Real Estate data team conducted an initial analysis to examine the correlations between three key factors (grade, sqft living, zipcode) and the sales price to establish an overview of the housing market. 

#### Overview of Price distribution for vacation homes
The average price of vacation homes in King County is around $1.4 million. This distribution shows a right-skewed trend towards the pricey range, therefore there are more houses for sale in the middle to lower range of price.

![barplot price count distribution](https://user-images.githubusercontent.com/117051182/206803464-135a7906-1577-4c0d-a2e5-8ddb58e715f5.png)

#### Price vs Grade
Price and housing grade have a positive correlation the higher grade of the house, the more expensive it is. Home buyers may use this information to search for a house in the grade that aligns with their budget. 

![Pricevs Grade](https://user-images.githubusercontent.com/117051182/206803538-3382d225-ccb3-40a0-af8e-9301ad2979f3.png)

#### Sqft. Living /Environment vs Price
Environment feature is created for houses that meet with one of these three criteria: waterfront, greenbelt, view. Based on the information shown in the graph below: large houses are more expensive and more likely to have a view or to be close to nature.
![Sqft living vs price final](https://user-images.githubusercontent.com/117051182/206803654-7d118fa0-1fd7-4f76-bd45-7cd5bada902b.png)

#### ZipCode with best view vs Price 
Below are the top 15 zip codes that have the best average ranked vacation grading score. Vacation Grade Score is calculated by view rating (0 for no view to 4 for excellent) + waterfront(0 for no and 1 for yes)  + greenbelt(0 for no and 1 for yes).
![vacationgrade](https://user-images.githubusercontent.com/117051182/206803865-a9998e0e-6f16-47f7-832c-dcedb7f67c64.png)

## Data Cleaning
To ensure the consistency of data for further analysis, the sales team cleaned up the dataset through the following steps:
1. Separated zipcode from “Address” column
2. Changed data format to either string, integer, float, or datetime
3. Converted ordinal values to numerical values for view, waterfront, greenbelt, nuisance, condition, grade columns.
4. Created a new feature ‘VacationGrade’ to calculate the overall score of each house by adding the scores of view, waterfront, greenbelt

## Modeling & Regression Results
The sales team has conducted six modeling and returned different results, see below for a summary:

First run:
Training data R^2 score: 0.7174740500353162
Testing data R^2 score：0.7232473897055692

Second run:
Training data R^2 score: 0.8340156143269408
Testing data R^2 score：0.825259265260174

Third run - adding city and persqft :
Training data R^2 score: 0.6942728715224923
Testing data R^2 score：0.6145195694112986

Fourth run - remove yr_built, condition, city, persqft
Training data R^2 score: 0.6929362351498297
Testing data R^2 score：0.6540055381345878

Fifth run - add new engineering feature - Environment Rank 
Training data R^2 score: 0.6780789848810684
Testing data R^2 score：0.6646713605192298

**Sixth run - add back all columns except id, date, price and log price**
**Training data R^2 score: 0.8318420740595907**
**Testing data R^2 score：0.834621013913642**

Regression Model line

![yelowregression ](https://user-images.githubusercontent.com/117051182/206884502-78033498-10cd-41bd-97ec-1748832647f4.png)

The best score from the model testing was achieved in the sixth run, 83% accuracy. 
However, the model predicts better result for houses under 2.5 m, as accuracy faded due to less data points in the high end market. 

## RESULTS: Data Insights

#### Insight 1 - General features impact on Vacation House Price (No. of Bedrooms and bathrooms, waterfront, greenbelt, nuisance, view, grade, yr built):
* Every unit increase in bedrooms, bathrooms, waterfront, housing grade, nuisance has a significant positive influence on the price. In other words, the houses with these features are more expensive than the rest. 
* As opposed, greenbelt, view and yr built do not have much positive impact on house value.

![features price](https://user-images.githubusercontent.com/117051182/206804705-b03486c9-b034-41d9-bcb8-8da1be2952f7.png)

#### Insight 2 - Top 5 | Bottom 5 Cities’ Impact on Vacation Housing Values (Note: housing values are not equivalent to housing price)
* Vacation homes in Burien, Auburn, Bothell, North Bend, Normandy Park are shown to have better value compared to other regions. The room for price increase of the vacation homes in these regions are higher than the bottom five cities.
* The bottom cities for housing values are Lake Forest Park, Kirkland, Mercer Island, Medina, Ravendale. Although housing prices in these cities are high (according to external research) , the data shows housing values in these regions are very low due to smaller room for growth. 

![city price](https://user-images.githubusercontent.com/117051182/206804872-62e5e8e9-6ee0-47f3-ac8b-9aa6ec8bb5fe.png)

#### Insight 3 - Heat Source | Sewer System Impact on PRICE
* The houses that have oil/solar heat source systems and private systems are shown to increase the value of vacation homes. 

![final heat](https://user-images.githubusercontent.com/117051182/206804963-0376d2d0-b8ad-4762-b908-088b8e58f97c.png)

## SUMMARY AND RECOMMENDATION
* Sixth model was chosen because of the highest R^2 result and its high accuracy for houses below 2.5 million dollars. 
* Features that are recommended to look for when buying vacation homes: near waterfront, grade, # of bedrooms & bathrooms, oil/solar heat source system, private sewer systems.
* For investors, I recommend starting a housing search in Burien, Auburn, Bothell, North Bend, Normandy Park as the potential for growth is higher than the other regions.

## NEXT STEP
As the dataset only covers the sales record for the year of 2021 and 2022, more data would be needed prior to 2021 to finalize the prediction model for the high end market (above 2.5 million dollars). In order to provide better recommendations, income distribution and demographic (ie population distribution) are also recommended to be added to the prediction model.

