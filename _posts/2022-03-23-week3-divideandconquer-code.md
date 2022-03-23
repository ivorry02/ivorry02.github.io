---
layout: post
title:  "week3-divideandconquer-code"
date:   2022-03-23 18:50:00 +0900
---

# 분할 정복 알고리즘

### **분할정복법의 설계법**
1. 문제 사례를 <u>하나 이상</u>의 작은 사례로 분할한다. (Divide)
2. 작은 사례들을 각각 정복한다. (Conquer) 작은 사례가 충분하지 작지 않은 이상 재귀를 사용한다. 
3. 작은 사례에 대한 해답을 통합하여 원래 사례의 해답을 구한다. (Combine) 

### 장단점

\<장점\>  
* 어려운 문제를 나눔으로써 쉽고 효율적으로 해결할 수 있음.  
* 문제를 나누어 해결한다는 특징상 병렬적으로 문제를 해결하는데 큰 강점이 있음.  

\<단점\>  
* 스택에 다양한 데이터를 보관하고 있어야 하므로 스택 오버플로우가 발생하거나 과도한 메모리 사용을 하게 됨. 


   
### 분할 정복 코드 예시 (C언어)  

**합병 정렬**  
랜덤으로 숫자를 뽑아 합병 정렬로 배열을 정리하는 프로그램 

```C
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

#define SIZE 15

void makeList(int list[])
{
    for(int i = 0; i < SIZE; i++)
        list[i] = rand() % 100 + 1;
}

void printList(int list[])
{
    for(int i = 0; i < SIZE; i++)
        printf("%d ", list[i]);
    printf("\n");
}

void merge(int list[], int sorted[], int left, int mid, int right)
{
    int i, j, k, l;
    i = left, j = mid + 1, k = left;
    
    while(i <= mid && j <= right)
    {
        if(list[i] <= list[j])
            sorted[k++] = list[i++];
        else
            sorted[k++] = list[j++];
    }
    
    if(i > mid)
        for(l = j; l <= right; l++)
            sorted[k++] = list[l];
    else
        for(l = i; l <= mid; l++)
            sorted[k++] = list[l];
            
    for(l = left; l <= right; l++)
        list[l] = sorted[l];
}

void mergeSort(int list[], int sorted[], int left, int right)
{
    int mid;
    if(left < right)
    {
        mid = (left + right) / 2;
        mergeSort(list, sorted, left, mid);
        mergeSort(list, sorted, mid + 1, right);
        merge(list, sorted, left, mid, right); 
    }
}

int main()
{
    int list[SIZE], sorted[SIZE];
    srand(time(NULL));
    
    makeList(list);
    printList(list);
    
    mergeSort(list, sorted, 0, SIZE - 1);
    printList(list);
    
    return 0;
}
```
### 분할 정복 알고리즘 예시  

**하는 일이 똑같지만 많이 반복되는 경우!!**
ex) 수열의 빠른 합, 행렬의 빠른 제곱
