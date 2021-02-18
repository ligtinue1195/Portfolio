# R) Neural Network
```
다중 선형 회귀 (Multiple Linear Regression) 를 사용하여 모델을 개발하여 분석한다
```
 - - -
 <br>
 
 ## Load Data
> Use Cagle Diamond csv file
```
 library(nnet)
 library(caret)
 library(ROCR)
 library(psych)
```
 - - -
 <br>

 ## 데이터 불러오기 및 탐색
```
 cb <- read.delim("Hshopping.txt", stringsAsFactors = FALSE)
 head(cb)
```
