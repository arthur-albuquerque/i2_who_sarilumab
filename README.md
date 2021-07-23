Estimating confidence intervals
================

#### Arthur M. Albuquerque, Donald R. Williams and James M. Brophy

#### July 23, 2021

Load packages

``` r
# Ensures the package "pacman" is installed
if (!require("pacman")) install.packages("pacman")

pacman::p_load(rio, # import data
               here, # reproducible file paths
               tidyverse, # data wrangle
               metafor) # fit meta-analyses
```

Load data

``` r
d = import(here("figure1_data.xlsx"))
```

Calculate effect sizes for each study

``` r
# Calculate log odds ratio
d_or = escalc(measure = "OR",
              ai = trt_events, n1i = trt_total,
              ci = control_events, n2i = control_total,
              slab= study,
              data = d)

 
### fit random-effects model in the each treatment
fit_toci_reml = rma(yi, vi, subset=(treatment=="tocilizumab"), data=d_or, method = "REML")
fit_sari_reml = rma(yi, vi, subset=(treatment=="sarilumab"),  data=d_or, method = "REML")
```

## Restricted maximum-likelihood estimator

#### Pooled tocilizumab and sarilumab

``` r
rma(yi, vi, data=d_or, method = "REML") %>% 
  confint()
```

    ## 
    ##        estimate  ci.lb   ci.ub 
    ## tau^2    0.0189 0.0000  0.1336 
    ## tau      0.1375 0.0000  0.3655 
    ## I^2(%)  16.6385 0.0000 58.5215 
    ## H^2      1.1996 1.0000  2.4109

The estimated *I*<sup>2</sup> was 16.6% (95% confidence interval \[CI\]
0 - 58.5).

#### Tocilizumab

``` r
rma(yi, vi, data=d_or, subset=(treatment=="tocilizumab"),
    method = "REML") %>% 
  confint()
```

    ## 
    ##        estimate  ci.lb   ci.ub 
    ## tau^2    0.0000 0.0000  0.2362 
    ## tau      0.0000 0.0000  0.4860 
    ## I^2(%)   0.0000 0.0000 71.2179 
    ## H^2      1.0000 1.0000  3.4744

The estimated *I*<sup>2</sup> was 0% (95% confidence interval \[CI\] 0 -
71.2).

#### Sarilumab

``` r
rma(yi, vi, data=d_or, subset=(treatment=="sarilumab"),
    method = "REML") %>% 
  confint()
```

    ## 
    ##        estimate  ci.lb   ci.ub 
    ## tau^2    0.0000 0.0000  0.6614 
    ## tau      0.0000 0.0000  0.8133 
    ## I^2(%)   0.0000 0.0000 80.1350 
    ## H^2      1.0000 1.0000  5.0340

The estimated *I*<sup>2</sup> was 0% (95% confidence interval \[CI\] 0 -
80).

## DerSimonian-Laird estimator

#### Pooled tocilizumab and sarilumab

``` r
rma(yi, vi, data=d_or, method = "DL") %>% 
  confint()
```

    ## 
    ##        estimate  ci.lb   ci.ub 
    ## tau^2    0.0012 0.0000  0.1336 
    ## tau      0.0345 0.0000  0.3655 
    ## I^2(%)   1.2420 0.0000 58.5215 
    ## H^2      1.0126 1.0000  2.4109

The estimated *I*<sup>2</sup> was 1.2% (95% confidence interval \[CI\] 0
- 58.5).

#### Tocilizumab

``` r
rma(yi, vi, data=d_or, subset=(treatment=="tocilizumab"),
    method = "DL") %>% 
  confint()
```

    ## 
    ##        estimate  ci.lb   ci.ub 
    ## tau^2    0.0000 0.0000  0.2362 
    ## tau      0.0000 0.0000  0.4860 
    ## I^2(%)   0.0000 0.0000 71.2179 
    ## H^2      1.0000 1.0000  3.4744

The estimated *I*<sup>2</sup> was 0% (95% confidence interval \[CI\] 0 -
71.2).

#### Sarilumab

``` r
rma(yi, vi, data=d_or, subset=(treatment=="sarilumab"),
    method = "DL") %>% 
  confint()
```

    ## 
    ##        estimate  ci.lb   ci.ub 
    ## tau^2    0.0000 0.0000  0.6614 
    ## tau      0.0000 0.0000  0.8133 
    ## I^2(%)   0.0000 0.0000 80.1350 
    ## H^2      1.0000 1.0000  5.0340

The estimated *I*<sup>2</sup> was 0% (95% confidence interval \[CI\] 0 -
80).
