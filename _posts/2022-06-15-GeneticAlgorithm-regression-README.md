# 최적화 알고리즘을 이용한 회귀식 추정

## 유전 알고리즘
* 실제 생물 진화를 모방해서 문제를 해결하는 진화 연산의 대표적인 방법.  
* 병렬적이고 전역적인 탐색 알고리즘. 

## 회귀분석
* 둘 이상의 변수 간의 관계를 보여주는 통계적 방법.  
* 일반적으로 독립변수는 종속변수에 따라 변경되며 해당 변경에서 가장 중요한 요소에 대한 답을 찾으려 시도함.


## 최적화 알고리즘 구현
최종 단계 : 가장 적합한 숫자를 찾아내는 것  

회귀분석은 상관 분석이랑 비슷하다.  

<상관분석과의 차이점>  
상관 분석은 두 변수가 서로 상관관계가 있는지 파악하는 분석이라면 회귀분석은 두 변수가 서로 상관이 있을때 점점 펴져있는 모습들을 보고 일정한 패턴을 이용하여 예측하는 것이다.   

![](https://postfiles.pstatic.net/MjAyMjA2MTdfNzAg/MDAxNjU1NDQyNDg1MjA3.8vul97tAbWajPV3wYqyXlfhZTukkUlbESclGCMGA4xcg.h_xCGv_yle4-IqV7j1O7y8Aqbj8EqXviNUwz5IaJbjQg.PNG.kimsanga0430/%EC%9D%BC%EC%A0%95%ED%95%9C_%ED%8C%A8%ED%84%B4.png?type=w773)

즉, 점들이 퍼져있는 모습에서 일정한 패턴을 찾아내고 이 일정한 패턴을 활용해서 무엇인가를 예측하는 분석이다.  

이때 패턴을 활용하려면 **'회귀식'** 을 구해야한다.  

회귀식
$$ y = b_{0}  + b_{1}x $$

y절편과 기울기를 구해야 예측을 할 수가 있게 된다.  
회귀식은 기울기를 알아야 y절편을 구할 수 있으므로, 보통 기울기를 먼저 구한다. 

![](https://postfiles.pstatic.net/MjAyMjA2MTdfODUg/MDAxNjU1NDQyNDg1MjA1.L2NQLiDLjtcIx0IMh3iF0_t50JDpeCU4WbJCMzj4AsEg.WqX_ztjUw1QL0qRFkJMMzVqTf9hP3AktED3_pQs9Xa0g.PNG.kimsanga0430/b1%EA%B5%AC%ED%95%98%EB%8A%94_%EA%B3%B5%EC%8B%9D.png?type=w773)

회귀식이 완성되면 이후부터 무엇인가를 예측하는 기법으로 사용 가능!!  

![](https://postfiles.pstatic.net/MjAyMjA2MTdfNjgg/MDAxNjU1NDQyNDg1MjA4.k3KQlJY4boS5lzQvK7dpl0WoslxJd0vg1YNuqmMajc4g.PTscIjBkO5_Fwrlvw-tzD0_sFQ9Akjc_xOpq-PUILSwg.PNG.kimsanga0430/%ED%9A%8C%EA%B7%80%EC%8B%9D_%EC%A0%95%EB%A6%AC.png?type=w773)

[부모의 키와 자식의 키의 관계]

- 부모와 자식의 키의 관계를 알아보기 위해 무작위로 몇 명을 뽑아, 아버지의 키와 아들의 키를 조사하였더니 다음과 같이 나왔다. 아래의 자료를 바탕으로 회귀식을 구하고, 아버지의 키가 165일때, 아들의 키는 얼마인지 예측하시오.  

![](https://postfiles.pstatic.net/MjAyMjA2MTdfOTEg/MDAxNjU1NDQyNDg1MjAy.aIuHRh34G3JE3PIoeWvmF84g3ML-bgFm4Zk4AzzoCa8g.KJQKsX5d3soyR1NUyeZ-nVe0Khm2UtEijbcA1xCA7U4g.PNG.kimsanga0430/%EC%95%84%EB%B2%84%EC%A7%80%EC%9D%98%ED%82%A4_%EC%95%84%EB%93%A4%EC%9D%98%ED%82%A4.png?type=w773)

회귀식을 한번에 구하는건 계산하기 힘들기 때문에 기울기를 구할때 사용하는 값은 먼저 표로 적어놓는 것이 좋다.

![](https://postfiles.pstatic.net/MjAyMjA2MTdfMTYx/MDAxNjU1NDQyNDg1MzE3.68PvhVfImXphsvQilARsB31dzggFN3WUYw8IXdHEnbgg.UQnQVpU9uNDvG1i1P7-IqFMVhjIu_WLkiZJ4RtLSskEg.PNG.kimsanga0430/%ED%9A%8C%EA%B7%80%EC%8B%9D_%ED%91%9C.png?type=w773)

![](https://postfiles.pstatic.net/MjAyMjA2MTdfMTE2/MDAxNjU1NDQyNDg1MjA2.7EB3bkLrkgkY7Q9Fi9cWaoq-mOV5LY-pl6CR9IXrTcwg.O8E3hvHvS1zS7nYDqqbzMTveecLINs726sRNnPpEkr4g.PNG.kimsanga0430/b1b0_r%EA%B5%AC%ED%95%98%EB%8A%94_%EA%B3%B5%EC%8B%9D.png?type=w773)

따라서 기울기 = 0.45, y절편 = 98.25이므로 회귀식은 다음과 같다.

$$ y = 0.45x + 98.25 $$

![](https://postfiles.pstatic.net/MjAyMjA2MTdfMjkx/MDAxNjU1NDQyNDg1MjA0.3NMqjecxLPodE1KkvKECG8osvsU_6-sgwPajBZyhni0g.DrD9WJMkdrGPphpFgX-gZcMIipX6HeAU0hrkUmLRGv4g.PNG.kimsanga0430/165%EC%9D%BC%EB%96%84_%EC%95%84%EB%93%A4%EC%9D%98_%ED%82%A4.png?type=w773)

아버지의 키가 165cm일 때, 아들의 키는 172.5cm 일거라고 예측된다.

### 유전 알고리즘에서의 돌연변이 연산
여러가지 연산들을 이용해서 검색을 진행하면, 유전 알고리즘은 지역 최적점에 도달하게 될 것이다. 유전 알고리즘에서는 지역 최적점에 빠지는 문제를 해결하기 위해 새롭게 생선된 염색체에 확률적으로 돌연변이가 발생하도록 한다.  
보통은 0.1%, 0.05% 정도로 낮은 확률로 발생하도록 한다.  

(지역 최적점 : 최적화 알고리즘은 기본적으로 이웃 검색을 기반으로 동작되기 때문에 현재의 솔루션이 개선되는 방향으로만 진행하려는 성질이 있다. 이러한 성질로 인해 유전 알고리즘은 빈번하게 같은 지역 최적점에 수렴한다.)

## 모수 값 추정

모수 : 모집단의 특성을 나타내는 값으로 이 값을 모집단을 전수조사해야만 알 수 있는 값  

일반적으로 전체 모집단을 측정하는 것이 불가능하기 때문에 해당 모집단에서 랜덤 표본을 추출한다. 이 표본을 사용하여 해당하는 표본 특성을 계산하며, 이 표본 특성이 알 수 없는 모집단 특성에 대한 정보를 요약하는데 사용된다. 해당하는 표본 특성을 모수 추정치라고 한다. 
