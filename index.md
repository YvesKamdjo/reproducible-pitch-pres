---
title       : Default credit card payments in Taiwan.
subtitle    : 
author      : Yves Ef
job         : 
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : []            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
---


## Introduction

This research employed a binary variable, default payment (Yes = 1, No = 0), as the response variable. This study reviewed the literature and used the following 23 variables as explanatory variables: 

* X1: Amount of the given credit (NT dollar): it includes both the individual consumer credit and his/her family (supplementary) credit.
* X2: Gender (1 = male; 2 = female).
* X3: Education (1 = graduate school; 2 = university; 3 = high school; 4 = others).
* X4: Marital status (1 = married; 2 = single; 3 = others).
* X5: Age (year).
* X6 - X23: Click here: http://archive.ics.uci.edu/ml/datasets/default+of+credit+card+clients

For this project we have choosed the logistic regression to predict default payment variable and only 5 variables as predictor: X1(LIM_BAL), X2(Gender), X3(Education), X4(Marital status) and X5(Age).

---

## Analysis

### 1. Reading data and processing



```r
filename <- 'CreditCard.xls'
  
  if(file.exists(filename)==FALSE){
    download.file('http://archive.ics.uci.edu/ml/machine-learning-databases/00350/default%20of%20credit%20card%20clients.xls',filename,mode = 'w', quiet = TRUE)
  }
    Cdata <- read.xls(filename,pattern = 'ID')
  okData <- data.frame(EDUCATION=factor(Cdata$EDUCATION),SEX=factor(Cdata$SEX),
                       MARRIAGE=factor(Cdata$MARRIAGE),AGE=Cdata$AGE,
                       LIMIT_BAL= Cdata$LIMIT_BAL,
                       default.payment.next.month=factor(Cdata$default.payment.next.month)
  )
```

---

### 2. Fit the prediction model

```
##                  Estimate   Std. Error     z value      Pr(>|z|)
## (Intercept) -1.290962e+01 9.649952e+01  -0.1337792  8.935772e-01
## EDUCATION1   1.111044e+01 9.649802e+01   0.1151365  9.083369e-01
## EDUCATION2   1.117350e+01 9.649802e+01   0.1157899  9.078191e-01
## EDUCATION3   1.114142e+01 9.649802e+01   0.1154575  9.080825e-01
## EDUCATION4   1.003463e+01 9.649895e+01   0.1039870  9.171797e-01
## EDUCATION5   9.698620e+00 9.649841e+01   0.1005055  9.199430e-01
## EDUCATION6   1.049213e+01 9.649904e+01   0.1087278  9.134184e-01
## SEX2        -1.628529e-01 3.338021e-02  -4.8787259  1.067734e-06
## MARRIAGE1    1.118478e+00 5.316712e-01   2.1037025  3.540440e-02
## MARRIAGE2    9.205236e-01 5.318850e-01   1.7306816  8.350856e-02
## MARRIAGE3    9.059341e-01 5.536029e-01   1.6364332  1.017490e-01
## AGE          3.180645e-03 2.032914e-03   1.5645744  1.176827e-01
## LIMIT_BAL   -3.344832e-06 1.549348e-07 -21.5886432 2.296563e-103
```

---
### 3.  Test and validation

```
## Confusion Matrix and Statistics
## 
##           Reference
## Prediction    0    1
##          0 5841 1659
##          1    0    0
##                                           
##                Accuracy : 0.7788          
##                  95% CI : (0.7692, 0.7882)
##     No Information Rate : 0.7788          
##     P-Value [Acc > NIR] : 0.5066          
##                                           
##                   Kappa : 0               
##  Mcnemar's Test P-Value : <2e-16          
##                                           
##             Sensitivity : 1.0000          
##             Specificity : 0.0000          
##          Pos Pred Value : 0.7788          
##          Neg Pred Value :    NaN          
##              Prevalence : 0.7788          
##          Detection Rate : 0.7788          
##    Detection Prevalence : 1.0000          
##       Balanced Accuracy : 0.5000          
##                                           
##        'Positive' Class : 0               
## 
```


