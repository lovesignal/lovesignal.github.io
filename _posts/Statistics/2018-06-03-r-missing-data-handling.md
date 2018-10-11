---
key: 201806-03
title: "[R] 결측값 데이터 다루기"
excerpt: "결측값 데이터 다루기:  "
categories: Statistics
comments: true
tags: [R, data structure]
---

## 1. 결측값 단순 삭제

## na.omit()

결측값이 있는 행을 삭제하는 함수

<br>

**example**

```R
> dat <- data.frame( a = c(1, 2, 3, 4),
+                    b = c(5, 6, 7, NA),
+                    c = c('a', 'b', 'c', NA),
+                    d = c('e', NA, 'f', 'g'))
> dat
  a  b    c    d
1 1  5    a    e
2 2  6    b <NA>
3 3  7    c    f
4 4 NA <NA>    g
> dat <- na.omit(dat)
> dat
  a b c d
1 1 5 a e
3 3 7 c f
```

2행, 4행이 삭제된 것을 확인할 수 있다.

<br>

<br>

## 2. Multiple Imputation 다중대체법

m번의 대치를 통해 m개의 가상 자료를 만들어서 대체하는 방법이다.

> Multiple imputation is a statistical technique for analyzing incomplete data sets, that is, data sets for which some entries are missing. Application of the technique requires three steps: imputation, analysis and pooling. The figure illustrates these steps. [1]

<br>

다중 대체법은 결측값을 처리하는 방법 중 하나인데 대체, 분석, 풀링 3단계로 이루어져있다.

![img](https://image.slidesharecdn.com/20151215apresentation-151216031138/95/multiple-imputation-joint-and-conditional-modeling-of-missing-data-13-638.jpg?cb=1450236425)

### mice()

> The mice package implements a method to deal with missing data. The package creates multiple imputations (replacement values) for multivariate missing data. The method is based on Fully Conditional Specification, where each incomplete variable is imputed by a separate model. The MICE algorithm can impute mixes of continuous, binary, unordered categorical and ordered categorical data. In addition, MICE can impute continuous two-level data, and maintain consistency between imputations by means of passive imputation. Many diagnostic plots are implemented to inspect the quality of the imputations.

 <br>

통계기법을 이용한 예측방정식을 이용해서 결측값이 대체된다. 대체할 값이 수렴될 때까지 반복한다.

```R
> library(mice)
> data(nhanes)
> str(nhanes)
## 'data.frame':    25 obs. of  4 variables:
##  $ age: num  1 2 1 3 1 3 1 1 2 2 ...
##  $ bmi: num  NA 22.7 NA NA 20.4 NA 22.5 30.1 22 NA ...
##  $ hyp: num  NA 1 1 NA 1 NA 1 1 1 NA ...
##  $ chl: num  NA 187 187 NA 113 184 118 187 238 NA ...
```

 <br>

#### 참고문헌

[1] <http://www.stefvanbuuren.nl/mi/mi.html>

[2] <https://www.rdocumentation.org/packages/mice/versions/2.46.0/topics/mice>

[3] <https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3074241>/

[4] <https://statkclee.github.io/data-science/ds-missing.html>

[5] <https://www.analyticsvidhya.com/blog/2016/03/tutorial-powerful-packages-imputing-missing-values>/

[6] <http://web.maths.unsw.edu.au/~dwarton/missingDataLab.html>

