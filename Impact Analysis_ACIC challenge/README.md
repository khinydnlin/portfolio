# Impact Analysis of Cost-Containment Measures in Healthcare Expenditures

#### -- Project Status: [In-progress]

## Project Objective
This project was carried out as an attempt to solve the [2022 data challenge from ACIC](https://acic2022.mathematica.org/). The goal of the analysis was to evaluate the nuanced impacts of policy interventions that aim to lower Medicare expenditure by using causal inference methods.

### Skills Used
* Data Analysis
* Difference-in-Differences Method

### Technologies
* R (plm package)

## Getting Started

1. Clone this repo (for help see this [tutorial](https://help.github.com/articles/cloning-a-repository/)).
2. Raw Data is available [here](https://github.com/khinydnlin/portfolio/blob/main/Car%20Auction%20Price%20Predictions%20(Myanmar)/dataset.csv) within this repo.   
3. Data processing and modelling scripts are documented in a [Jupyter notebook](https://github.com/khinydnlin/portfolio/blob/main/Car%20Auction%20Price%20Predictions%20(Myanmar)/Car%20Auction%20Price%20Predictions.ipynb)
4. The project findings and other details can be found below:

## Project Description

### Data Sources

The data was manually collected from the major car brokers in the market because of the lack of public data on resale prices. The following featuers were collected:

![image](https://github.com/khinydnlin/portfolio/assets/145341635/dbd345d6-43cf-41ad-b31a-db3933e38179)


### Machine Learning Model Development 

#### Insights from Exploratory Data Analysis

- Toyota is likely to dominate the car market which aligns with general observations of Toyota having the largest market share in the country.
- In terms of prices, there is a significant variation based on car brands and car models, with the Toyota brand exhitbiting the highest car price.
- Specifically, Toyota Alphard, Toyota Crown, Toyota Klugers had the highest resale prices after Nissan Quashqai make (this model was not representative due to having considerably smaller samples).
- Black cars tend to have higher resale value compared to other colours.
- SUV body types cars are more likely to have the highest resale prices,followed by vans and sedans.
- Although it was expected that the prices would be determined by age and mileage, correlation results suggest that the resale values have weak direct relationships with these features. Interesingly, data visualization suggests that age seems to be a secondary influential factor after the car brand and model. This indicates the potential non-linear relationship between the car prices and available features.
  

#### Feature Engineering

- The data are right skewed. Hence, a log transformation was used to achieve a normal distribution.
- To reduce the dimensionality of the features, the car brands were regrouped into three groups: high-end brands (Toyota) , mid-range brands (Honda, Nissan and Mitsubishi), and Low-end brands (Suzuki and Daihatsu). Note that this grouping was determined based on the price distributions in the dataset.
- Similarly, I also regrouped the colours into two groups: black and others, as the black colour seems to be the main differentiator. I also combined the 'semi-auto' and 'manual' into one group.

#### Model Exploration

- As a baseline model, a Linear Regression model was chosen for comparison purposes. Since a non-linearity was also detected, a Random Forest model was explored to uncover complex patterns.

- As a primary metric, the goal was to achieve a low Mean Absolute Error (MAE) value of 1,000 - 2,000 USD, which was equivalent to 15 - 30 lakhs MMK at the time.

- For Linear regression, it was found that the model comformed to primary assumptions: linearity, indepedence of residuals (with Durbin Watson test score between 1.5 and 2.5), improved normality after log transformation, and homosdeasticity with randomly scattered residuals. However, some multicollinearity issues were also identified. So, Ridge and Lasso regularisation were explored. Prior to conducting regularisation, it was ensured that the training data and test data were standardised properly.

**Cross-validation Results**

| ML Models        | R2    | MAE (USD) |
|------------------|-------|-----------|
| Linear Regression| 0.829 | 2,520     | 
| Ridge Regression | 0.834 | 2,363     |
| Lasso Regression | 0.749 | 2,714     |
| Random Forest    | 0.892 | 1,624     |

Due to the lowest MAE scores of Random Forest, the Random Forest model was selected as final model to fit on the test data.

The final score on test set is R2 - 0.834, MAE - 1,921

## Challenges and Further Model Improvement

- Data Availability : The dataset comprises only 500 data points, which is insufficient to cover all car models. This limitation constrains the model's ability to generalize across the full spectrum of vehicles.

- Overfitting issues: There is a model performance gap (6%) between the test set and the training set. Despite efforts in parameter tuning to reduce overfitting, this gap persisted, likely due to the small sample size and imbalanced class distribution among car models. Given that Toyota models constitute the majority of the dataset, the model may struggle to generalize effectively to less represented or unseen models.


