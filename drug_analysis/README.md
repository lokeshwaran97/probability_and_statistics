
# Statistical Analysis of Drug Treatments

## Overview
This project involves a statistical analysis of two new drugs, A and B, compared to an existing drug X. The goal is to determine the effectiveness of these drugs through hypothesis testing, regression modeling, and various statistical computations based on provided datasets.

### Datasets:
- `Drug_new_7.csv`: Contains data for drugs A, B, and X with corresponding response data (Yes/No).
- `Drug_A_7.csv`: Contains before and after treatment well-being scores for drug A.

## 1. Analysis of Drugs A, B, and X

### a. Data Tabulation
The dataset was tabulated to show the number of positive (Yes) and negative (No) responses for each drug.

```r
print(table(drug_data))
```
|   | No | Yes |
|---|----|-----|
| A | 21 |  20 |
| B | 25 |  19 |
| X | 15 |  20 |

### b. Probability of a Positive Response for Drug X
We calculated the probability that an individual who responded "Yes" was given Drug X.

```r
N_X_Y <- sum(drug_data$Drug == 'X' & drug_data$Response == 'Yes')
N_X <- sum(drug_data$Drug == 'X')
prob_Y_X <- N_X_Y / N_X
```
**Result:**  
- Probability of "Yes" response for Drug X: **0.571** (57.14%)

### c. Expected Number of No Responses for Drug A
We computed the expected number of "No" responses for Drug A, assuming independence between the drug and the response.

```r
Exp_A_No <- (A_total * No_total) / N
print(paste("The expected number of No responses for Drug A is:", Exp_A_No))
```
**Result:**  
- Expected "No" responses for Drug A: **20.84**

### d. Chi-Square Test for Independence
We performed a chi-squared test to check if drug type and response are independent.

```r
chi_test <- chisq.test(drug_data$Drug, drug_data$Response, correct = FALSE)
```
**Result:**
- p-value: **0.467**
- Conclusion: We **accept** the null hypothesis, indicating independence between the drug type and the response.

## 2. Analysis of Drug A's Effect on Well-Being Scores

### a. Scatter Plot of Well-Being Scores (Before vs. After Treatment)
A scatter plot was created to visualize the relationship between the well-being scores before and after taking Drug A.

```r
plot(before, after, xlab = "Before Drug", ylab = "After Drug", main="Well-Being Score")
```

![Well-Being Score Scatter Plot](https://github.com/lokeshwaran97/probability_and_statistics/blob/main/drug_analysis/images/drug_correlation.png?raw=true)

### b. Linear Regression Model for Well-Being Scores
We fitted a linear regression model to estimate the relationship between the well-being score before (x) and after (y) treatment.

```r
model_drug <- lm(after ~ before)
alpha <- model_drug$coef[1]
beta <- model_drug$coef[2]
```
**Result:**
- α (Intercept): **4.69**
- β (Slope): **1.08**

### c. Plotting the Least Squares Regression Line
The least squares regression line was added to the scatter plot of the data.

```r
abline(a = alpha, b = beta)
```

![Regression Line](https://github.com/lokeshwaran97/probability_and_statistics/blob/main/drug_analysis/images/drug_prediction.png?raw=true)

### d. Assessing the Reasonableness of the Linear Regression Model
The residuals of the model were examined to check if the linear regression model is appropriate.

```r
hist(model_drug$residuals, main = "Residuals of Well-Being Scores", xlab = "Residuals")
plot(model_drug$fitted.values, model_drug$residuals, xlab = "Fitted values", ylab = "Residuals")
```

![Residual Plot](https://github.com/lokeshwaran97/probability_and_statistics/blob/main/drug_analysis/images/well_being_drug_A.png?raw=true)
![Residual Histogram](https://github.com/lokeshwaran97/probability_and_statistics/blob/main/drug_analysis/images/well_being_score.png?raw=true)

**Conclusion:**  
- The residuals are normally distributed, and there is no pattern in the residual vs. fitted values plot. Therefore, the linear model is a **reasonable fit** for the data.

### e. 95% Confidence Interval for After Treatment Well-Being Score
A 95% confidence interval was constructed for a patient who had a well-being score of 50 prior to treatment.

```r
before_wellbeing <- 50
confidence_interval <- predict(model_drug, newdata = data.frame(before = before_wellbeing), interval = "prediction")
```

**Result:**  
- Predicted well-being score after treatment: **58.48**
- 95% Confidence Interval: **[51.42, 65.54]**

![Confidence Interval Plot](https://github.com/lokeshwaran97/probability_and_statistics/blob/main/drug_analysis/images/pred_conf_interval.png?raw=true)

## Conclusion
This analysis explored the relationship between drug treatment and patient responses, demonstrating the independence of drugs A, B, and X with health outcomes. For Drug A, the linear regression model was found to be a reasonable predictor of well-being improvement after treatment. The analysis supports further investigation of the drugs' effectiveness in clinical settings.
