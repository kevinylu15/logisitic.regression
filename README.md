## **Logistic Regression Model Function**

An alternate implementation of logistic regression in R using the Iteratively Reweighted Least Squares (IRLS) algorithm, serving as a replacement for the built-in glm() function with binary predictor variable(s).

<!-- badges: start -->
[![R-CMD-check](https://github.com/kevinylu15/logistic.regression/actions/workflows/R-CMD-check.yaml/badge.svg)](https://github.com/kevinylu15/logistic.regression/actions/workflows/R-CMD-check.yaml)
[![Codecov test coverage](https://codecov.io/gh/kevinylu15/logistic.regression/graph/badge.svg)](https://app.codecov.io/gh/kevinylu15/logistic.regression)
<!-- badges: end -->

## Table of Contents

- [Introduction](#introduction)
- [Features](#features)
- [Installation](#installation)
- [Usage](#usage)
- [Function Details](#function-details)
- [Example](#example)
- [Algorithm Explanation](#algorithm-explanation)
- [Comparison with `glm()`](#comparison-with-glm)
- [Limitations](#limitations)
- [Contributing](#contributing)
- [License](#license)


## **Introduction**

The my_logregr function is a custom R function that fits a logistic regression model without directly using R's built-in glm() function. It uses the Iteratively Reweighted Least Squares (IRLS) algorithm to estimate the model coefficients and manually calculates fitted values, linear predictors, the design matrix, and checks for convergence.


## **Features**

Fits a binary logistic regression model.
Can handle single or multiple predictors, including interactions.
Returns coefficients, fitted values, linear predictors, iteration count, and convergence status.
Allows manual input of convergence tolerance and maximum iterations.


## **Installation**

To install the my_logregr function, you can source/download the function into your R environment or directly copy&paste the function into your R script.

## **Usage**

my_logistic_regression(formula, data, tol = 1e-6, max_iter = 100)

formula: An object of class "formula" (or one that can be coerced to that class): a symbolic description of the model to be fitted.
data: A data frame containing the variables in the model.
tol: Convergence tolerance. The algorithm stops when the change in coefficients is less than this value. Default is 1e-6.
max_iter: Maximum number of iterations allowed. Default is 100

## **Function Details**



## **Example**

## **Algorithm Explanation

## **Comparison with glm()**

## **Limitations**

## **Contributing**

If you'd like to contribute to Project Title, here are some guidelines:

1. Fork the repository.
2. Create a new branch for your changes.
3. Make your changes.
4. Write tests to cover your changes.
5. Run the tests to ensure they pass.
6. Commit your changes.
7. Push your changes to your forked repository.
8. Submit a pull request.

## **License**

Project Title is released under the MIT License. See the **[LICENSE](https://www.blackbox.ai/share/LICENSE)** file for details.
