---
title: 'Kaggle: House Price Prediction'
author: "tiangsinf"
date: "9/23/2018"
output: 
  html_document: 
    keep_md: yes
---


```r
library(tidyverse)
library(ggplot2)

# import data
house_price <- read_csv("dataset/train.csv")
```


```r
head(house_price, n = 10)
str(house_price) # 81 variables including id
```


```r
col_class <- sapply(house_price, class)
table(col_class) # 43 char and 38 int columns
```

```
## col_class
## character   integer 
##        43        38
```

```r
# Check columns with na value:
col_with_na <- sapply(house_price, function(x) any(is.na(x)))
names(house_price[col_with_na]) # list of columns with na values. Total 19 columns with na.
```

```
##  [1] "LotFrontage"  "Alley"        "MasVnrType"   "MasVnrArea"  
##  [5] "BsmtQual"     "BsmtCond"     "BsmtExposure" "BsmtFinType1"
##  [9] "BsmtFinType2" "Electrical"   "FireplaceQu"  "GarageType"  
## [13] "GarageYrBlt"  "GarageFinish" "GarageQual"   "GarageCond"  
## [17] "PoolQC"       "Fence"        "MiscFeature"
```

```r
# Subset numeric columns
int_col <- names(house_price[col_class == "integer"])
int_house_price <- house_price[, int_col][-1] # Subset integer columns and drop id
head(int_house_price)
```

```
## # A tibble: 6 x 37
##   MSSubClass LotFrontage LotArea OverallQual OverallCond YearBuilt
##        <int>       <int>   <int>       <int>       <int>     <int>
## 1         60          65    8450           7           5      2003
## 2         20          80    9600           6           8      1976
## 3         60          68   11250           7           5      2001
## 4         70          60    9550           7           5      1915
## 5         60          84   14260           8           5      2000
## 6         50          85   14115           5           5      1993
## # ... with 31 more variables: YearRemodAdd <int>, MasVnrArea <int>,
## #   BsmtFinSF1 <int>, BsmtFinSF2 <int>, BsmtUnfSF <int>,
## #   TotalBsmtSF <int>, `1stFlrSF` <int>, `2ndFlrSF` <int>,
## #   LowQualFinSF <int>, GrLivArea <int>, BsmtFullBath <int>,
## #   BsmtHalfBath <int>, FullBath <int>, HalfBath <int>,
## #   BedroomAbvGr <int>, KitchenAbvGr <int>, TotRmsAbvGrd <int>,
## #   Fireplaces <int>, GarageYrBlt <int>, GarageCars <int>,
## #   GarageArea <int>, WoodDeckSF <int>, OpenPorchSF <int>,
## #   EnclosedPorch <int>, `3SsnPorch` <int>, ScreenPorch <int>,
## #   PoolArea <int>, MiscVal <int>, MoSold <int>, YrSold <int>,
## #   SalePrice <int>
```

