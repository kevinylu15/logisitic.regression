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

my_logregr <- function(formula, data, tol = 1e-6, max_iter = 100) {
  mf <- model.frame(formula, data) #return a dataframe
  y <- model.response(mf) #response variable y
  X <- model.matrix(attr(mf, "terms"), data = mf) #design matrix
  beta <- rep(0, ncol(X)) #pre allocate beta coefficients vector
  #Update IRLS algorithm
  for (iter in 1:max_iter) {
    eta <- X %*% beta #linear predictor
    p <- 1 / (1 + exp(-eta)) #logistic function
    W <- as.vector(p * (1 - p)) #weight matrix converted to vector
    if (any(W == 0)) { #cannot have 0 weights (division error)
      W[W == 0] <- 1e-6
    }
    #Log-likelihood
    gradient <- t(X) %*% (y - p)
    WX <- X * W #column of X * weights
    Hessian <- t(X) %*% WX
    delta <- solve(Hessian, gradient) #updating coefficients
    beta_new <- beta + delta
    # Check for convergence
    if (sum(abs(beta_new - beta)) < tol) {
      beta <- beta_new 
      break
    }
    beta <- beta_new #update current beta
  }
  eta <- X %*% beta
  fitted_values <- 1 / (1 + exp(-eta)) #final fitted values
  return(list( #return values in list format
    coefficients = beta,
    fitted.values = fitted_values,
    linear.predictors = eta,
    iterations = iter,
    converged = iter < max_iter
  ))
}



## **Algorithm Explanation

Data Parsing: The function starts by parsing the input formula and data to extract the response variable y and the design matrix X.
Pre-Allocation: Pre-allocating a zero vector for large datasets.
Iteration: For each iteration until convergence or reaching the maximum number of iterations.
Linear Predictor (eta): Compute the linear combination of predictors and current coefficients.
Predicted Probabilities (p): Apply the logistic function to eta to get probabilities.
Weights (W): Compute weights of the least squares.
Gradient: Calculate the gradient of the log-likelihood.
Hessian: Compute the Hessian matrix (second order derivatives for optimization)
Update Coefficients: Solve the linear system to find the coefficient updates.
Convergence Check: If the change in coefficients is less than the tolerance, stop iterating.
Results: After convergence, the function returns the estimated coefficients, fitted values, linear predictors, iteration count, and convergence status.

## **Comparison with glm()**

The my_logistic_regression function implements similarly to the glm() function with family = binomial(link = "logit")

Algorithm: Both use the IRLS algorithm for estimation.
Function: glm() handles weights, offsets, complicated formulas and large datasets more efficiently.
Performance: glm() is optimized and may be faster for large or complex datasets
Usage: glm() is part of the base R stats package and can be used for other general statistical modeling

## **Limitations**

Error Handling: The function has basic error checking for formulas and mathematical operations but may not handle all edge cases.
Extensions: Only supports binary response variables.
Performance: Potentially slow for large, complex datasets.
Testing: Does not display significance test results or standard errors.

## **Contributing**

If you'd like to improve the function or add features, please submit a pull request or send me an email.

## **License**

The Logistic Regression Model Funciton is released under the MIT License. See the **[LICENSE](https://www.blackbox.ai/share/LICENSE)** file for details.
