# Bottling Process Statistical Analysis

## Overview
This project involves statistical analysis of a vineyard's bottling process. The vineyard provided two datasets, and the goal is to perform various statistical tests and analyses to assess the performance of new and existing bottling machines.

### Datasets:
- `Bottle_New_6.csv`: Contains data for the new bottling machine.
- `Bottle_Check_6.csv`: Contains data for the existing bottling machines.

## 1. New Bottling Machine Analysis

### a. Mean and Variance of Wine Dispensed
The mean and variance of the quantity of wine dispensed by the new bottling machine were calculated.

```r
new_bottle <- data$x
mean_bottle <- mean(new_bottle)
variance_bottle <- var(new_bottle)
print(paste("mean :", mean_bottle))
print(paste("variance :", variance_bottle))
```
**Results:**
- Mean: 752.6 ml
- Variance: 13.28 ml²

### b. 95% Confidence Interval for the Mean
We constructed a 95% confidence interval for the mean quantity of wine dispensed.

```r
t_test_value <- t.test(new_bottle)
print(paste("95% confidence interval is [", t_test_value$conf.int[1], " , ", t_test_value$conf.int[2], "]"))
```
**Result:**
- 95% Confidence Interval: [750.50, 754.70] ml

### c. Hypothesis Test for Overfilling
We tested the hypothesis that the new bottling machine systematically overfills bottles (H0: μ = 750 ml, H1: μ > 750 ml) at a 10% significance level.

```r
ans <- t.test(new_bottle, mu=750, alternative ="greater", conf.level = 0.90)
p_value <- ans$p.value
```
**Result:**
- p-value: 0.0096
- The hypothesis was rejected, indicating that the machine overfills bottles.

## 2. Existing Bottling Machines Analysis

### a. P-Value for Each Machine
For each existing bottling machine, we calculated the p-value under the null hypothesis H0: μ = 750 ml using the known standard deviation of 2.1 ml.

```r
s_d <- 2.1
sample_size <- 10
mu <- 750
pAA <- rep(NA, 14)
for(i in 1:14){
  machineRow <- data2[[paste("Machine.", i, sep = "")]]
  sample_mean <- mean(machineRow)
  standard_dev_mean <- s_d / sqrt(sample_size)
  z_score <- abs((sample_mean - mu) / standard_dev_mean)
  pAA[i] <- 2 * pnorm(q = z_score, lower.tail = FALSE)
  print(paste("Probability values for machine", i, " :", pAA[i]))
}
```
**Results:**
- Machines with p-values less than 0.04 indicate a statistically significant difference from the target 750 ml.

### b. Hypothesis Rejection with Benjamini-Hochberg Correction
Using a significance level of α = 0.04 and the Benjamini-Hochberg correction, we identified the machines where the null hypothesis is rejected.

```r
N <- 14
alpha <- 0.04
sorted_p <- sort(pAA)
q_value <- rep(NA, N)
dit <- c()
for(i in 1:N){
  q_value[i] <- (i / N) * alpha
  if(sorted_p[i] < q_value[i]){
    dit <- append(dit, sorted_p[i])
  }
}
```
**Rejected Machines:**
- Machine 2, Machine 3, Machine 5, Machine 7, Machine 8, Machine 11, Machine 14

![Probability Values Plot](https://github.com/lokeshwaran97/probability_and_statistics/blob/main/Bottling_process/result_image/probability_values.png?raw=true)

## Conclusion
The analysis helped identify bottling machines that deviate from the target wine quantity and demonstrated systematic overfilling by the new bottling machine. The Benjamini-Hochberg correction method allowed us to adjust for multiple comparisons and control the false discovery rate when identifying faulty machines.
