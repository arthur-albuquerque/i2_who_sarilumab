
### Confidence intervals of heterogeneity parameters in the “Association Between Administration of IL-6 Antagonists and Mortality Among Patients Hospitalized for COVID-19” article

#### Arthur M. Albuquerque, Donald R. Williams and James M. Brophy

#### July 23, 2021

## Introduction

In this document, we present the estimated confidence intervals of
*I*<sup>2</sup> estimates derived from the article [“Association Between
Administration of IL-6 Antagonists and Mortality Among Patients
Hospitalized for
COVID-19”](https://jamanetwork.com/journals/jama/fullarticle/2781880).

We fitted random-effect meta-analyses to estimate heterogeneity
parameters with three different estimators:

-   Restricted maximum-likelihood estimator
-   DerSimonian-Laird estimator
-   Hedges estimator

All models were fitted using the R package
[metafor](https://wviechtb.github.io/metafor/reference/confint.rma.html).

#### Load data

``` r
# Ensures the package "pacman" is installed
if (!require("pacman")) install.packages("pacman")

pacman::p_load(rio, # import data
               here, # reproducible file paths
               dplyr, # to use %>%
               metafor) # fit meta-analyses

d = import(here("figure1_data.xlsx"))

# Calculate effect sizes for each study
d_or = escalc(measure = "OR",
              ai = trt_events, n1i = trt_total,
              ci = control_events, n2i = control_total,
              slab= study,
              data = d)
```

## Restricted maximum-likelihood estimator

#### Pooled tocilizumab and sarilumab

``` r
rma(yi, vi, data=d_or, method = "REML") %>% 
  confint(digits = 1)
```

    ## 
    ##        estimate ci.lb ci.ub 
    ## tau^2       0.0   0.0   0.1 
    ## tau         0.1   0.0   0.4 
    ## I^2(%)     16.6   0.0  58.5 
    ## H^2         1.2   1.0   2.4

The estimated *I*<sup>2</sup> was 16.6% (95% confidence interval \[CI\]
0 - 58.5).

#### Tocilizumab

``` r
rma(yi, vi, data=d_or, subset=(treatment=="tocilizumab"),
    method = "REML") %>% 
  confint(digits = 1)
```

    ## 
    ##        estimate ci.lb ci.ub 
    ## tau^2       0.0   0.0   0.2 
    ## tau         0.0   0.0   0.5 
    ## I^2(%)      0.0   0.0  71.2 
    ## H^2         1.0   1.0   3.5

The estimated *I*<sup>2</sup> was 0% (95% CI 0 - 71.2).

#### Sarilumab

``` r
rma(yi, vi, data=d_or, subset=(treatment=="sarilumab"),
    method = "REML") %>% 
  confint(digits = 1)
```

    ## 
    ##        estimate ci.lb ci.ub 
    ## tau^2       0.0   0.0   0.7 
    ## tau         0.0   0.0   0.8 
    ## I^2(%)      0.0   0.0  80.1 
    ## H^2         1.0   1.0   5.0

The estimated *I*<sup>2</sup> was 0% (95% CI 0 - 80.1).

## DerSimonian-Laird estimator

#### Pooled tocilizumab and sarilumab

``` r
rma(yi, vi, data=d_or, method = "DL") %>% 
  confint(digits = 1)
```

    ## 
    ##        estimate ci.lb ci.ub 
    ## tau^2       0.0   0.0   0.1 
    ## tau         0.0   0.0   0.4 
    ## I^2(%)      1.2   0.0  58.5 
    ## H^2         1.0   1.0   2.4

The estimated *I*<sup>2</sup> was 1.2% (95% CI 0 - 58.5).

#### Tocilizumab

``` r
rma(yi, vi, data=d_or, subset=(treatment=="tocilizumab"),
    method = "DL") %>% 
  confint(digits = 1)
```

    ## 
    ##        estimate ci.lb ci.ub 
    ## tau^2       0.0   0.0   0.2 
    ## tau         0.0   0.0   0.5 
    ## I^2(%)      0.0   0.0  71.2 
    ## H^2         1.0   1.0   3.5

The estimated *I*<sup>2</sup> was 0% (95% CI 0 - 71.2).

#### Sarilumab

``` r
rma(yi, vi, data=d_or, subset=(treatment=="sarilumab"),
    method = "DL") %>% 
  confint(digits = 1)
```

    ## 
    ##        estimate ci.lb ci.ub 
    ## tau^2       0.0   0.0   0.7 
    ## tau         0.0   0.0   0.8 
    ## I^2(%)      0.0   0.0  80.1 
    ## H^2         1.0   1.0   5.0

The estimated *I*<sup>2</sup> was 0% (95% CI 0 - 80.1).

## Hedges estimator

#### Pooled tocilizumab and sarilumab

``` r
rma(yi, vi, data=d_or, method = "HE") %>% 
  confint(digits = 1)
```

    ## 
    ##        estimate ci.lb ci.ub 
    ## tau^2       0.0   0.0   0.1 
    ## tau         0.0   0.0   0.4 
    ## I^2(%)      0.0   0.0  58.5 
    ## H^2         1.0   1.0   2.4

The estimated *I*<sup>2</sup> was 0% (95% CI 0 - 58.5).

#### Tocilizumab

``` r
rma(yi, vi, data=d_or, subset=(treatment=="tocilizumab"),
    method = "HE") %>% 
  confint(digits = 1)
```

    ## 
    ##        estimate ci.lb ci.ub 
    ## tau^2       0.0   0.0   0.2 
    ## tau         0.0   0.0   0.5 
    ## I^2(%)      0.0   0.0  71.2 
    ## H^2         1.0   1.0   3.5

The estimated *I*<sup>2</sup> was 0% (95% CI 0 - 71.2).

#### Sarilumab

``` r
rma(yi, vi, data=d_or, subset=(treatment=="sarilumab"),
    method = "HE") %>% 
  confint(digits = 1)
```

    ## 
    ##        estimate ci.lb ci.ub 
    ## tau^2       0.0   0.0   0.7 
    ## tau         0.0   0.0   0.8 
    ## I^2(%)      0.0   0.0  80.1 
    ## H^2         1.0   1.0   5.0

The estimated *I*<sup>2</sup> was 0% (95% CI 0 - 80.1).
