# 정렬알고리즘의 성능 분석 및 비교

[시간 복잡도]  
**문제를 해결하는데 걸리는 시간과 입력의 함수 관계**  
알고리즘의 수행 시간을 분석할 때 사용함  


## 버블정렬
시간복잡도
- 평균 : O(N^2)  
- 최선 : O(N^2)  
- 최악 : O(N^2)  

### 버블정렬 시간복잡도 그래프  
![](https://postfiles.pstatic.net/MjAyMjA1MDVfMTQg/MDAxNjUxNzM4MDM5OTMx.UUuusBJXCtiVXd8_7UbZizmhOc3Cnh4Xm3ALIWxY9r0g.bx1M6r7VAomPYtq--DtTZiOIpBDUOfJP9vA95-nW3SAg.JPEG.kimsanga0430/KakaoTalk_20220505_170431488_02.jpg?type=w773)


```c
public class Bubble_Sort {
 
	public static void bubble_sort(int[] a) {
		bubble_sort(a, a.length);
	}
	
	private static void bubble_sort(int[] a, int size) {
		 
		for(int i = 1; i < size; i++) {
			
		for(int j = 0; j < size - i; j++) {
				
				
				if(a[j] > a [j + 1]) {
					swap(a, j, j + 1);
				}
			}
		}
	}
	
	private static void swap(int[] a, int i, int j) {
		int temp = a[i];
		a[i] = a[j];
		a[j] = temp;
	}
}
```

## 선택정렬  
시간복잡도
- 평균 : O(N^2)  
- 최선 : O(N^2)  
- 최악 : O(N^2)  

### 선택정렬 시간복잡도 그래프  
![](https://postfiles.pstatic.net/MjAyMjA1MDVfNDIg/MDAxNjUxNzM4MDM5NzUz.tQegwtqQEgeEuHEp9OAWDCnd2QBDL0yS89GHokBcPrsg.d9xCawRV6xIyVxictL9w6OM90QPt37B7R6ouT3F_njog.JPEG.kimsanga0430/KakaoTalk_20220505_170431488_03.jpg?type=w773)

```c
public class Selection_Sort {
 
	public static void selection_sort(int[] a) {
		selection_sort(a, a.length);
	}
	
	private static void selection_sort(int[] a, int size) {
		
		for(int i = 0; i < size - 1; i++) {
			int min_index = i;	
			 
			for(int j = i + 1; j < size; j++) {
				if(a[j] < a[min_index]) {
					min_index = j;
				}
			}
		
			swap(a, min_index, i);
		}
	}
	
	private static void swap(int[] a, int i, int j) {
		int temp = a[i];
		a[i] = a[j];
		a[j] = temp;
	}
	
}
```

## 삽입정렬 
시간복잡도
- 평균 : O(N^2)  
- 최선 : O(N^2)  
- 최악 : O(N^2)  

### 삽입정렬 시간복잡도 그래프  
![](https://postfiles.pstatic.net/MjAyMjA1MDVfMjMx/MDAxNjUxNzM4MDQwMDAw.HnaO_jsZu_iivtoOunxXAAzl1jKGynqOol1_RtKogaQg.KsRCL32K1NSQm9Iwa0lze9Q5OKbqpicAHmGIIb7SfZAg.JPEG.kimsanga0430/KakaoTalk_20220505_170431488_01.jpg?type=w773)

```c
public class Insertion_Sort {
 
	public static void insertion_sort(int[] a) {
		insertion_sort(a, a.length);
	}
	
	private static void insertion_sort(int[] a, int size) {
		
		
		for(int i = 1; i < size; i++) {
			
			int target = a[i];
			
			int j = i - 1;
			
			while(j >= 0 && target < a[j]) {
				a[j + 1] = a[j];	
				j--;
			}
			
			a[j + 1] = target;	
		}
		
	}
}
```

## 쉘정렬
시간복잡도
- 평균 : O(N^1.5)  
- 최선 : O(N^1.5)  
- 최악 : O(N^2)  

```c
public class Shell_Sort {
	
	private final static int[] gap = 
		{32, 64, 128, 256, 512, 1024, 2048, 4096, 8192, 16384, 32768, 65536, 131072, 262144, 524288, 1048576};		
 
	
	public static void shell_sort(int[] a) {
		shell_sort(a, a.length);
		
	}
 
	private static int getGap(int length) {
		int index = 0;
		
		int len = (int)(length / 2.25);	
		while (gap[index] < len) {
			index++;
		}
		return index;
	}
 
	private static void shell_sort(int[] a, int size) {
		int index = getGap(size);	
 
		for (int i = index; i >= 0; i--) {
 
			for (int j = 0; j < gap[i]; j++) {	
				insertion_sort(a, j, size, gap[i]);
			}
		}
	}

	private static void insertion_sort(int[] a, int start, int size, int gap) {
		for (int i = start + gap; i < size; i += gap) {
 
			int target = a[i];
			int j = i - gap;

			while (j >= start && target < a[j]) {
				a[j + gap] = a[j];	
				j -= gap;
			}
			a[j + gap] = target;
 
		}
	}
}
```

## 힙정렬
시간복잡도
- 평균 : O(N*log n)  
- 최선 : O(N*log n)  
- 최악 : O(N*log n)  

```c
import java.util.PriorityQueue;
 
public class test {
	public static void main(String[] args) {
    
		int[] arr = {32, 64, 128, 256, 512, 1024, 2048, 4096, 8192, 16384, 32768, 65536, 131072, 262144, 524288, 1048576};

		System.out.print(" 정렬 전 original 배열 : ");
		for(int val : arr) {
			System.out.print(val + " ");
		}
		
		PriorityQueue<Integer> heap = new PriorityQueue<Integer>();
		
		for(int i = 0; i < arr.length; i++) {
			heap.add(arr[i]);
		}
		
		for(int i = 0; i < arr.length; i++) {
			arr[i] = heap.poll();
		}
		
		
		System.out.print("\n 정렬 후 배열 : ");
		for(int val : arr) {
			System.out.print(val + " ");
		}
		
	}
}

## 퀵정렬
시간복잡도
- 평균 : O(N*log n)  
- 최선 : O(N*log n)  
- 최악 : O(N^2)

### 퀵정렬 시간복잡도 그래프  
![](https://postfiles.pstatic.net/MjAyMjA1MDVfNTYg/MDAxNjUxNzM4Mzc0NTk3.lLgpkRtNQtg1mu_7M7zBUqxsQ-UYwF4syKOQNqQ5v8wg.zvkrUH2HE6riskGEDB2qPzRoK-xZyc02jweAnGWco1Eg.JPEG.kimsanga0430/KakaoTalk_20220505_170431488.jpg?type=w773)

```c
public class QuickSort {
	
	public static void sort(int[] a) {
		l_pivot_sort(a, 0, a.length - 1);
	}

	private static void l_pivot_sort(int[] a, int lo, int hi) {
		
		if(lo >= hi) {
			return;
		}
		
		int pivot = partition(a, lo, hi);	
		
		l_pivot_sort(a, lo, pivot - 1);
		l_pivot_sort(a, pivot + 1, hi);
	}
	
	private static int partition(int[] a, int left, int right) {
		
		int lo = left;
		int hi = right;
		int pivot = a[left];		
		
		while(lo < hi) {
			
			while(a[hi] > pivot && lo < hi) {
				hi--;
			}
			
			while(a[lo] <= pivot && lo < hi) {
				lo++;
			}
			
			swap(a, lo, hi);
		}
		
		swap(a, left, lo);
		
		return lo;
	}
 
	private static void swap(int[] a, int i, int j) {
		int temp = a[i];
		a[i] = a[j];
		a[j] = temp;
	}
}
```

