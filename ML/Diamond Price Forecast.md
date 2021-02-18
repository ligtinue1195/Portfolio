
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
<br>


 ## Find Missing Values
 > No missing values
```
 sum(is.na(diamond))
```
<br>

<div class='tableauPlaceholder' id='viz1613443840319' style='position: relative'><noscript><a href='#'><img alt=' ' src='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;di&#47;diamonds_1_16134400933900&#47;Diamond_Variable&#47;1_rss.png' style='border: none' /></a></noscript><object class='tableauViz'  style='display:none;'><param name='host_url' value='https%3A%2F%2Fpublic.tableau.com%2F' /> <param name='embed_code_version' value='3' /> <param name='site_root' value='' /><param name='name' value='diamonds_1_16134400933900&#47;Diamond_Variable' /><param name='tabs' value='no' /><param name='toolbar' value='yes' /><param name='static_image' value='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;di&#47;diamonds_1_16134400933900&#47;Diamond_Variable&#47;1.png' /> <param name='animate_transition' value='yes' /><param name='display_static_image' value='yes' /><param name='display_spinner' value='yes' /><param name='display_overlay' value='yes' /><param name='display_count' value='yes' /><param name='language' value='ko' /><param name='filter' value='publish=yes' /></object></div>                <script type='text/javascript'>                    var divElement = document.getElementById('viz1613443840319');                    var vizElement = divElement.getElementsByTagName('object')[0];                    vizElement.style.width='100%';vizElement.style.height=(divElement.offsetWidth*0.75)+'px';                    var scriptElement = document.createElement('script');                    scriptElement.src = 'https://public.tableau.com/javascripts/api/viz_v1.js';                    vizElement.parentNode.insertBefore(scriptElement, vizElement);                </script>
