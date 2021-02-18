
# R) Multiple Linear Regression
![다운로드](https://static.wixstatic.com/media/nsplsh_356b48576a595a42343555~mv2_d_5472_3648_s_4_2.jpg/v1/fill/w_740,h_493,al_c,q_90,usm_0.66_1.00_0.01/nsplsh_356b48576a595a42343555~mv2_d_5472_3648_s_4_2.webp)
```
다중 선형 회귀 (Multiple Linear Regression) 를 사용하여 모델을 개발하여 분석한다
```
 - - -
 <br>
 
   
   
 ## Load Data
> Use Cagle Diamond csv file
```
 diamond <- read.csv("data/diamonds.csv", stringsAsFactors = F)
```
 - - -
 <br>

 ## Find Missing Values
 > No missing values
```
 sum(is.na(diamond))
```
 - - -
<br>

 ## Data Correlation
![Diamond_Variable](https://user-images.githubusercontent.com/79243911/108318552-5d41e500-7203-11eb-959e-af175c8365c5.png)
 - - -
<br>

 ## Multicollinearity
 > Exclude Null Hypotheses
```
 multiple.reg <- lm.beta(lm(price ~ carat + cut + color + clarity + table , diamond))

 vif(multiple.reg)
```
 - - -
<br>

 ## DataPartition
 > Categorize data and use it for learning and validation
```
 set.seed(42)
 
 inTrain <- caret::createDataPartition(y = diamond$price, p = 0.1, list = F)
 sample.data <- diamond[-inTrain,]
 test.data <- diamond[inTrain,]
```
 - - -
<br>

 ## Recommended Variables
 > Using forward
```
 model.pre0 <- lm(price ~ 1, sample.data)

 model.pre0 <- step(model.pre0,
                    direction = "forward",
                    scope = (price ~ carat + cut + color + clarity + depth + table + x + y + z),
                    trace = T)
```
 - - -
<br>

 ## Modeling
 > Dependent variable : Price <br>
 > Independent variable: Carat, Cut, Color, Clarity, Table

```
 model.pre1 <- lm(price ~ carat + cut + color + clarity + table, sample.data)
```
 - - -
<br>

 ## T - Statistics
 > The Overall T-value Except For The Table Is 2e-16 Table T-value is 9.31e-12 <br>
 > Adjusted R-squared:  0.9164  P-Value : 2.2e-16<br>

```
 summary(model.pre1)
```
 - - -
<br>

 ## Design Matrix
 > Note When Modeling

```
 model.matrix(price ~ carat + cut + color + clarity + table , sample.data)
```
 - - -
<br>

 ## Regression diagnostics
 ![Rplot](https://user-images.githubusercontent.com/79243911/108323984-b06b6600-720a-11eb-954a-eb4fbb7f42af.png)
```
 par(mfrow = c(2,2))
 plot(model.pre1)
```
 - - -
<br>

 ## Diamond Price Prediction Function
> Predict using test data
```
 model.test <- function(data, model_){
  num <- list(1)
  for(i in 1:data){
    num[i] <-  predict(model_, test.data[i,])
  }
  return(num)
 }
```
 - - -
<br>

 ## Differences between actual and predicted values (residuals)
> The reason for creating a function separately is because of the implementation of the add-ons
```
 model.res <- function(data, su){
  pri <- test.data$price
  result <- list(1)
  
  for(i in 1:su){
    number1 <- data[i]
    number2 <- pri[i] 
    number1 <- as.numeric(as.character(number1))
    if(number1 < 0){
      number1 <- (number1 * -1)
      result[i] <- as.numeric(number1) + as.numeric(number2)
    }else{
      result[i] <- as.numeric(number1) - as.numeric(number2) 
    }
    if(result[i] < 0){
      result[i] <- as.numeric(result[i]) * -1
    }
  }
  return(result)
 }
```
 - - -
<br>

 ## Total interval between actual and forecast values
 > The mean was calculated by dividing it by the return value after the function runs
```
 model.sum <- function(data, su){
  num <- 0
  
  for(i in 1:su){
    number1 <- data[i]
    number1 <- as.numeric(number1)
    
    if(number1 < 0){
      number1 <- number1 * -1
    }
    num <- num + number1
  }
  return(num)
 }
```
 - - -
<br>

 ## Model Verification
 > On average, 802.6185$ error
```
 for_su <- nrow(test.data)
 dia.pre <- model.test(for_su, model.pre1)
 
 dia.res <- model.res(dia.pre, for_su)
 
 model.sum(dia.res, for_su)/for_su
```
 - - -
<br>

 ## Second modeling
 > Dependent variable : Price <br>
 > All independent variables <br>
 > <br>
 > On average, 739.7546$ error
```
 model.pre2 <- lm(price ~ . , sample.data)

 summary(model.pre2)

 for_su <- nrow(test.data)
 dia.pre <- model.test(as.numeric(for_su), model.pre2)

 dia.res <- model.res(dia.pre, for_su)

 model.sum(dia.res, for_su)/for_su
```
 - - -
<br>

 ## Third modeling
 > Dependent variable : Price <br>
 > Use Optimization Independent Variables (forward) <br>
 > <br>
 > On average, 739.7512$ error
```
 model.pre3 <- lm(price ~ carat + clarity + color + cut + table + x + depth + z, sample.data)

 summary(model.pre3)

 for_su <- nrow(test.data)
 dia.pre <- model.test(as.numeric(for_su), model.pre3)

 dia.res <- model.res(dia.pre, for_su)

 model.sum(dia.res, for_su)/for_su
```
 - - -
<br>

 ## Fourth modeling
 > Dependent variable : Price <br>
 > Independent variable: Carat Clarity Color Cut Table X Depth <br>
 > <br>
 > On average, 739.8397$ error
```
model.pre4 <- lm(price ~ carat + clarity + color + cut + table + x + depth, sample.data)

summary(model.pre4)

for_su <- nrow(test.data)
dia.pre <- model.test(as.numeric(for_su), model.pre4)

dia.res <- model.res(dia.pre, for_su)

model.sum(dia.res, for_su)/for_su
```
 - - -
<br>

 ## Fifth modeling
 > Dependent variable : Price <br>
 > Independent variable: Carat Cut Color <br>
 > <br>
 > On average, 960.2413$ error
```
model.pre5 <- lm(price ~ carat + cut + color, sample.data)

summary(model.pre5)

for_su <- nrow(test.data)
dia.pre <- model.test(as.numeric(for_su), model.pre5)

dia.res <- model.res(dia.pre, for_su)

model.sum(dia.res, for_su)/for_su
```
 - - -
<br>
