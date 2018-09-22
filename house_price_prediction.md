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
table(sapply(house_price, class)) # 43 char and 38 int columns
```

```
## 
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

