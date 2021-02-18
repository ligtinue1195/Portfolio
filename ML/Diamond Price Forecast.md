
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
```
 sum(is.na(diamond))
```
