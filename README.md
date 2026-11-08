

<!-- README.md is generated from README.qmd via: quarto render README.qmd --to gfm -->

# Truncated Gaussian Regression Models in R

## Overview

The R package [truncreg](https://zeileis.codeberg.page/truncreg/)
provides estimation of regression with a truncated Gaussian response via
maximum likelihood.

In short, a linear model with homoscedastic Gaussian (normally
distributed) errors is assumed for a latent untruncated response
$y_i^*$:

$$ y_i^* = x_i^\top \beta + \varepsilon_i \qquad \varepsilon_i \sim \mathcal{N}(0, \sigma^2) $$

The observed outcome variable $y_i$ is then the truncated version of the
latent variable $y_i^*$, restricted to be positive: $y_i^* | y_i^* > 0$.
Instead of $0$ other truncation points could also be used.

The function `truncreg()` estimates the regression coefficients via
maximum likelihood and returns an object of class `"truncreg"`. Standard
methods are provided for extracting information: `print()`, `summary()`,
`predict()`, `coef()`, `vcov()`, `model.matrix`(), `model.frame()`,
`residuals()`, `fitted()`, `logLik()`. Furthermore, there is a
`prodist()` method, enabling the workflow provided by the
[distributions3](https://zeileis.github.io/distributions3/) and
[topmodels](https://zeileis.codeberg.page/topmodels/) packages.

A more flexible implementation of truncated regression with more
features is available in the [crch](https://zeileis.codeberg.page/crch/)
package. In particular, this provides more response distributions,
heteroscedastic errors, interval truncation, and also censoring in
addition to truncation.

## Installation

The stable version of `truncreg` is available from
[CRAN](https://CRAN.R-project.org/package=truncreg):

``` r
install.packages("truncreg")
```

The latest development version can be installed from
[R-universe](https://zeileis.R-universe.dev/truncreg):

``` r
install.packages("truncreg", repos = "https://zeileis.R-universe.dev")
```

## License

The package is available under the [General Public License version
3](https://www.gnu.org/licenses/gpl-3.0.html) or [version
2](https://www.gnu.org/licenses/old-licenses/gpl-2.0.html)

## Get started

Simulation of a simple artificial sample from a truncated normal
distribution.

``` r
set.seed(1071)
n <- 1000
x <- runif(n, -5, 5)
y <- 1 + 1 * x + rnorm(n, sd = 3)
y[y <= 0] <- NA
d <- data.frame(x = x, y = y)
```

Estimate the unknown coefficients and error variance via maximum
likelihood.

``` r
library("truncreg")
m <- truncreg(y ~ x, data = d)
summary(m)
## 
## Call:
## truncreg(formula = y ~ x, data = d)
## 
## BFGS maximization method
## 39 iterations, 0h:0m:0s 
## g'(-H)^-1g = 4.39E-11 
##  
## 
## 
## Coefficients :
##             Estimate Std. Error t-value Pr(>|t|)    
## (Intercept) 0.733149   0.386431  1.8972   0.0578 .  
## x           1.099983   0.098068 11.2166   <2e-16 ***
## sigma       2.999813   0.154238 19.4493   <2e-16 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Log-Likelihood: -1218.4 on 3 Df
```

Estimated coefficients, variance-covariance matrix, confidence
intervals, number of observations, log-likelihood, and information
criteria.

``` r
coef(m)
## (Intercept)           x       sigma 
##   0.7331488   1.0999830   2.9998128
vcov(m)
##             (Intercept)            x        sigma
## (Intercept)  0.14932880 -0.031668241 -0.046290620
## x           -0.03166824  0.009617287  0.008963986
## sigma       -0.04629062  0.008963986  0.023789280
confint(m)
##                   2.5 %   97.5 %
## (Intercept) -0.02424175 1.490539
## x            0.90777371 1.292192
## sigma        2.69751234 3.302113
nobs(m)
## [1] 587
logLik(m)
## 'log Lik.' -1218.385 (df=3)
AIC(m)
## numeric(0)
BIC(m)
## [1] 2455.895
```
