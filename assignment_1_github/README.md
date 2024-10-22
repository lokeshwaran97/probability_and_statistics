# Car Garage Statistical Analysis

## Overview

A car garage has tasked us with conducting statistical analysis on two datasets they provided: car sales data and car battery data. The analysis is aimed at answering several queries related to car sales and battery lifetime. This repository contains the analysis results, including statistical summaries, probability calculations, and distribution fitting.

## Datasets

- **Car Sales Data**: Data on the weekly sales of Brand X cars.
- **Car Battery Data**: Data on the lifetimes (in months) of two types of car batteries (Type A and Type B).

## Queries and Analysis

### 1. Car Sales Data Analysis

#### a) Summarize the Sales of Brand X Cars

We begin by summarizing the sales data for Brand X cars. This includes calculating numerical summaries, such as quartiles and standard deviation, and visualizing the data using a boxplot.

```r
sales <- car_sales_data$x
summary(sales)
boxplot(sales, horizontal = TRUE, xlab = "sales of car")
```

Summary of Sales:
```
Min. 1st Qu. Median Mean 3rd Qu. Max.
0.000 1.000 2.000 1.692 3.000 3.000
```
The sales data is left-skewed with a low standard deviation, indicating little variance.

![Boxplot of Car Sales](https://github.com/lokeshwaran97/probability_and_statistics/blob/main/assignment_1_github/result_images/box_plot_car.png?raw=true)

#### b) Probability of Selling 1 Car in a Week

We estimated the probability that exactly 1 Brand X car would be sold in a given week based on the sales data.

```r
no_of_cars_sold <- length(sales)
no_of_brand_1_cars_sold <- sum(sales == 1, na.rm = TRUE)
prob_brand_1_sales <- no_of_brand_1_cars_sold / no_of_cars_sold
```

**Probability of selling 1 car in a week**: `0.2115`

#### c) Mean and Variance of Sales Over 8 Weeks

The mean and variance of Brand X car sales over a rolling period of 8 weeks were calculated.

```r
mean_avg_8_weeks <- median(mean_8_weeks)
variance_avg_8_weeks <- median(variance_8_weeks)
```

- **Mean**: `1.75`
- **Variance**: `1.071`

#### d) Probability of 23 Weeks With 0 Sales in 2023

We calculated the probability that there will be 23 weeks in 2023 where 0 Brand X cars will be sold, using binomial distribution.

```r
prob_cdf_23weeks <- dbinom(23, size = no_of_cars_sold, prob = probability_per_week_0)
```

**Probability**: `0.00002`

---

### 2. Car Battery Data Analysis

#### a) Statistical Comparison of Battery Lifetimes

We compared the lifetimes of Battery Type A and Battery Type B. The lifetimes of both battery types are right-skewed, with Battery B having a slightly higher mean lifetime.

```r
mean(batteryA_lifetime)
mean(batteryB_lifetime)
```

- **Mean Lifetime of Battery A**: `42.98 months`
- **Mean Lifetime of Battery B**: `45.10 months`
- **Standard Deviation of Battery A**: `27.37`
- **Standard Deviation of Battery B**: `20.30`

![Battery A Lifetime](https://github.com/lokeshwaran97/probability_and_statistics/blob/main/assignment_1_github/result_images/hist_battery_a.png?raw=true)
![Battery B Lifetime](https://github.com/lokeshwaran97/probability_and_statistics/blob/main/assignment_1_github/result_images/hist_battery_b.png?raw=true)

#### b) Fit a Distribution to Battery B Data

A gamma distribution was fitted to the Battery B data. The shape and rate parameters of the gamma distribution were estimated.

```r
shape <- 5.338
rate <- 0.118
```

![Gamma Distribution for Battery B](https://github.com/lokeshwaran97/probability_and_statistics/blob/main/assignment_1_github/result_images/gamma_batteryb_lifetime.png?raw=true)

#### c) Free Replacement Probability for Battery B

We calculated the value of `M` (in months) such that the probability of replacing a Battery B for free is 0.03.

```r
pgamma(value, shape, rate)
```

**M**: `16.08 months`

---

## Conclusion

The analysis provided detailed insights into car sales trends and battery lifetimes, addressing each of the garage's queries with statistical rigor. For further details, please refer to the code provided in the repository.

