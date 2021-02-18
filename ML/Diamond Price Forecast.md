
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


