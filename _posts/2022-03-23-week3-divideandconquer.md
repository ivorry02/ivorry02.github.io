# 분할 정복 알고리즘

주어진 문제의 입력을 분할하여 문제를 해결(정복)하는 방식의 알고리즘.  
분할된 입력에 대하여 동일한 알고리즘을 적용하여 해를 계산하며, 이들의 해를 취합하여 원래 문제의 해를 얻는다.  

![](https://search.pstatic.net/common/?src=http%3A%2F%2Fblogfiles.naver.net%2F20130730_229%2Fseiyeonyim_1375181514750MO9jR_JPEG%2F%25C1%25A6%25B8%25F1_%25BE%25F8%25C0%25BD-3.jpg&type=sc960_832)  

  \<부분 문제\>  
* 분할된 입력에 대한 문제  
* 더 이상 분류할 수 없을 때까지 분류함    

## 합병 정렬
입력이 두 개의 부분문제로 분할되고, 부분문제의 크기가 1/2로 감소하는 분할 정복 알고리즘  

![](https://search.pstatic.net/common/?src=http%3A%2F%2Fblogfiles.naver.net%2FMjAyMDA3MzBfOTAg%2FMDAxNTk2MDcxMTY3Mzkw.HBZBJDLMu2fM7CcS_jBAbfI8mmHSaMZDzGp75iKUTHog.Y5exv5QkBOV_2V1B6zORlBjX_OCPIpnptnD89FF3cr8g.PNG.wongoni%2F%25C4%25B8%25C3%25B3.PNG&type=a340)  

\<합병\>
* 2개의 각각 정렬된 숫자들을 1개의 정렬된 숫자들로 합치는 것  

### 합병 정렬 알고리즘  
```java
MergeSort(A,p,q)  
입력 : A[p]~A[q]  
출력 : 정렬된 A[p]~A[q]  
if(p < q>) {             //배열의 원소의 수가 2개 이상이면
    k = |(p+q)/2|        //k=반으로 나누기 위한 중간 원소의 인덱스
    MergeSort(A,p,k)    //앞부분 순환 호출
    MergeSort(A,k+1,q)  //뒷부분 순환 호출
    A[p]~A[k]와 A[k+1]~A[q]를 합병한다.  
}
```

### 합병 정렬의 시간 복잡도  

* 시간복잡도 : 알고리즘이 어떤 문제를 해결하는데 걸리는 시간  
* 정렬의 시간복잡도 : 숫자의 비교 횟수로 나타냄

$$(층수)*O(n)=\log_2n*O(n)=O(n\log n)$$


## 퀵 정렬
문제를 두 개의 부분문제로 분할하는데, 각 부분문제의 크기가 일정하지 않은 형태의 분할 정복 알고리즘  

![](https://search.pstatic.net/common/?src=http%3A%2F%2Fblogfiles.naver.net%2FMjAyMTAxMDFfMTA5%2FMDAxNjA5NTAxNzkzMjYx.5-lxR0sFwTfga8VYs7tmjYQ2tRHGwQzAR1don6EKgV8g.jTeydeOzplsKuJNBQz7B4uwjl_5NqzUcXqNGHU5GuYEg.JPEG.bakarim0309%2Fbasic2.jpg&type=a340)

\<피봇\>  
* 임의적으로 선택되어 기준이 되는 숫자  
* 피봇은 분할된 왼편이나 오른편 부분에 포함되지 않음
* 피봇이라 일컫는 배열의 원소(숫자)를 기준으로 피봇보다 작은 숫자들은 왼편으로, 피봇보다 큰 숫자들은 오른편에 위치하도록 분할하고, 피봇을 그 사이에 놓는 것  


**피봇 선정 방법**  
1. 랜덤하게 선정하는 방법
2. 가장 왼쪽 숫자, 중간 숫자, 가장 오른쪽 숫자 중에서 하나를 선정하는 방법
3. 입력을 3등분하여 각 부분에서 3 숫자의 중앙값을 찾아서 3개의 중앙값에서 중앙값을 피봇으로 선정하는 방법  
  

### 퀵 정렬 알고리즘  

```java
QuickSort(A, left, right)
입력 : 배열 A[left]~A[right]
출력 : 정렬된 배열 A[left]~A[right]
if(left < right) {
  피봇을 A[left]~A[right] 중에서 선택하고, 피봇을 A[left]와 자리를 바꾼 후, 피봇과 배열의 각 원소를 비교하여 피봇보다 작은 숫자들은 A[left]~A[p-1]로 옮기고, 피봇보다 큰 숫자들은 A[p+1]~A[right]로 옮기며, 피봇은 A[p]에 놓는다. 
  QuickSort(A,left,p-1)  //피봇보다 작은 그룹
  QuickSort(A,p+1,right)  //피봇보다 큰 그룹
}
```

### 합병 정렬의 시간 복잡도  

* 피봇으로 가장 작은 숫자 또는 가장 큰 숫자가 선택되면, 한 부분으로 치우치는 분할을 야기함

**최선의 경우 시간복잡도**  
$$(층수)*O(n)=O(n)*(\log_2n)=O(n\log_2n) (층수가 \log_2n인 이유는 n/2^k=1 일 때 k=\log_2n이기 때문이다)$$