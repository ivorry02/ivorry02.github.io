---
layout: post
title:  "huffmancode"
date:   2022-04-12 17:44:00 +0900
---

# 허프만코드 (Huffman Code)

**데이터를 효율적으로 압축하는데 사용하는 그리디 알고리즘**

## 허프만 코드 절차  

1. 문자열 텍스트파일 주소를 입력받는다. 
2. 입력받은 문자열을 문자 단위로 끊어 해시 맵에 저장한 뒤에 빈도수를 체크한다. 
3. 이후에 빈도수가 1 이상인 문자에 한해서 우선순위 큐에 삽입한다. 
4. 우선순위 큐에 삽입하면서 자동으로 빈도수라는 우선순위에 따라 최소 힙과 같은 형태가 된다. 
5. 루트 노드에서부터 순회하며 0 또는 1을 붙여 허프만 코딩 알고리즘을 적용한다.
6. 결과적으로 처음 입력 받은 문자열을 해시 맵과 대조하여 압축된 2진형을 출력한다. 

## 허프만 코드 설명  

### 빈도수 체크
원본 데이터에서 자주 출현하는 문자는 적은 비트의 코드로 변환하여 표현하고 출현빈도가 낮은 문자는 많은 비트의 코드로 변환하여 표현함으로써 전체 데이터를 표현하는데 필요한 비트 수를 줄이는 방식

빈도수가 낮은 두 개 노드를 골라서 빈도수합으로 결합 노드 개수(n)만큼 반복  
```c
  public static Node huffmanCoding(int n) {
        for (int i = 0; i < n - 1; i++) {
            Node z = new Node();
            z.right = queue.poll();
            z.left = queue.poll();
            z.frequency = z.right.frequency + z.left.frequency;
            queue.add(z); 
        }
        return queue.poll();

    }
```

각각의 문자에 대한 빈도수를 체크하는 변수 선언
```c
 HashMap <Character, Integer> hashmap = new HashMap<Character,Integer>();
```

### 파일 적재
txt파일의 위치를 입력받아 파일에 들어있는 문자들을 읽는 방식

""사이에 텍스트파일 위치 입력  
```c
Scanner scanner = new Scanner (new File("C:\Users\Kim sanga\Desktop\2022 1학기 수업\컴퓨터알고리즘\허프만코드"));
```

### 압축률
**압축률 = 원본사이즈 / 압축사이즈**  

### 우선순위 큐
노드 생성
```c
class Node{
    public char character;  //문자 하나를 의미  
    public int frequency; //출현 빈도수를 의미
    public Node left,right; //읜쪽 노드와 오른쪽 노드
}
```
우선순위 큐의 정렬을 담당하는 빈도수 측정
```c
class FrequencyComparator implements Comparator<Node>{
    public int compare(Node a,Node b){
        int frequencyA=a.frequency;
        int frequencyB=b.frequency;
        return frequencyA-frequencyB; //빈도수 비교
    }
}
```

모든 노드를 우선순위 큐에 추가함으로써 트리 형성  
```c
queue=new PriorityQueue<Node>(100,new FrequencyComparator());
        int number =0;
```

해시맵에 저장된 빈도수와 문자를 우선순위 큐에 삽입  
```c
for(Character c: hashmap.keySet()){
            Node temp = new Node();
            temp.character=c;
            temp.frequency=hashmap.get(c);
            queue.add(temp);
            number++; 
        }
```

전제 노드 개수만큼 재배열하여 우선순위 큐 상에서의 노드 재배열
```c
Node root=huffmanCoding(number);
```

각 노드에 0과 1을 입력하기 위한 트리순회 함수
```c
traversal(root,new String());
```

왼쪽은 0 오른쪽은 1 이라는 수를 부여하는 트리 순회
```c
public static void traversal(Node n,String s) 
    {
        if(n==null)
            return;
        traversal(n.left,s+"0");
        traversal(n.right,s+"1");
        if(n.character!='\0')
        {
            System.out.println(n.character+"("+n.frequency+")"+":"+s);
            charToCode.put(n.character,s);
        }
    }
```

### 해시맵

*해싱*  
- 많은 양의 데이터들을 그보다는 작은 크기의 테이블로 대응시켜 저장할 수 있또록 하는 일종의 데이터 관리 기법  
  
*해시맵*  
해싱이 된 <u>맵</u> (키와 값 두 쌍으로 데이터를 보관하는 자료구조)  

해시맵 선언  
```c
 public static HashMap<Character, String> charToCode = new HashMap<Character, String>();
 ```

전체 문자열의 크기만큼 반복하여 해시맵에 문자열을 문자단위로 삽입
```c
for(int i=0;i<str.length();i++)
        {
            char temp = str.charAt(i);
            if(hashmap.containsKey(temp)){
                hashmap.put(temp,hashmap.get(temp)+1);
            }
            else
                hashmap.put(temp,1);
        }
```
### 출력

허프만 코드로 압축된 비트 출력
```c
System.out.println(bitresult); 
```

압축 후 비트값과 원래 비트값
```c
for(int i=0;i<bitresult.length();i++)
    count++;

int count3=count2*7; //원래 비트값
```

압축률
```c
double count4=(double)count3/count;
String formattedResult = String.format("%.2f", count4); 
```
출력값
```c
System.out.println("원래 비트 값: "+count3);
System.out.println("압축 비트 값: "+count);
System.out.println("압축률: "+formattedResult);
```

### 트리 형태
![](https://postfiles.pstatic.net/MjAyMjA0MTNfMjU2/MDAxNjQ5ODIwNzQ3MDAw.jPkk8UHGna6rj9gNhePWKroyGxr3c7IYxztBUfo_UMkg.YcDp5y04Ea8jfurgh6u4E6NJ7Slf4D1qXWi1ABTROIsg.PNG.kimsanga0430/%ED%8A%B8%EB%A6%AC_%EA%B5%AC%ED%98%84.png?type=w773)

## 허프만 코드  

```c
import java.util.Comparator;
import java.util.PriorityQueue;
import java.util.Scanner;
import java.io.File;
import java.io.FileNotFoundException;
import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;
import java.util.HashMap;
import java.util.*;
import java.io.*;

class Node{
    public char character;  //문자 하나를 의미  
    public int frequency; //출현 빈도수를 의미
    public Node left,right; //읜쪽 노드와 오른쪽 노드
}

class FrequencyComparator implements Comparator<Node>{
    public int compare(Node a,Node b){
        int frequencyA=a.frequency;
        int frequencyB=b.frequency;
        return frequencyA-frequencyB; 
    }
}

public class Huffman {
    public static HashMap<Character, String> charToCode = new HashMap<Character, String>(); 
    public static PriorityQueue<Node> queue; 
 
    public static Node huffmanCoding(int n) {
        for (int i = 0; i < n - 1; i++) {
            Node z = new Node();
            z.right = queue.poll();
            z.left = queue.poll();
            z.frequency = z.right.frequency + z.left.frequency;
            queue.add(z); 
        }
        return queue.poll();

    }

    public static void main(String args[]) throws FileNotFoundException {

        HashMap <Character, Integer> hashmap = new HashMap<Character,Integer>(); 
        String str = null;
        Scanner scanner = new Scanner (new File("C:\Users\Kim sanga\Desktop\2022 1학기 수업\컴퓨터알고리즘\허프만코드")); 
        while(scanner.hasNext()){
            str=scanner.next();
        }

        for(int i=0;i<str.length();i++)
        {
            char temp = str.charAt(i);
            if(hashmap.containsKey(temp)){
                hashmap.put(temp,hashmap.get(temp)+1);
            }
            else
                hashmap.put(temp,1);
        }

        queue=new PriorityQueue<Node>(100,new FrequencyComparator());
        int number =0;

        for(Character c: hashmap.keySet()){
            Node temp = new Node();
            temp.character=c;
            temp.frequency=hashmap.get(c);
            queue.add(temp);
            number++; 
        }

        Node root=huffmanCoding(number);

        traversal(root,new String()); 

        int count=0;
        int count2=0;

        String bitresult = new String();
        for(int i =0;i<str.length();i++)
        {
            bitresult = bitresult + charToCode.get(str.charAt(i)) + "";
            count2++;
        }

        System.out.println(bitresult); 

        for(int i=0;i<bitresult.length();i++)
            count++; 

        int count3=count2*7; 

        double count4=(double)count3/count;
        String formattedResult = String.format("%.2f", count4); 

        System.out.println("원래 비트 값: "+count3);
        System.out.println("압축 비트 값: "+count);
        System.out.println("압축률: "+formattedResult);

    }

    public static void traversal(Node n,String s) 
    {
        if(n==null)
            return;
        traversal(n.left,s+"0");
        traversal(n.right,s+"1");
        if(n.character!='\0')
        {
            System.out.println(n.character+"("+n.frequency+")"+":"+s);
            charToCode.put(n.character,s);
        }
    }
}

```
### 파트배분
이건우 - 코드 절차 5-6  
박세용 - 코드 절차 1-4  
김상아 - README 파일 작성  
