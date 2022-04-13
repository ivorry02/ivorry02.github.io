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
    public char character;
    public int frequency;
    public Node left,right;
}

class FrequencyComparator implements Comparator<Node>{
    public int compare(Node a,Node b){
        int frequencyA=a.frequency;
        int frequencyB=b.frequency;
        return frequencyA-frequencyB;//빈도수 비교
    }
}
public class Huffman {
    public static HashMap<Character, String> charToCode = new HashMap<Character, String>();//해시맵 선언
    public static PriorityQueue<Node> queue;//우선순위큐 선언

    public static Node huffmanCoding(int n) {
        for (int i = 0; i < n - 1; i++) {
            Node z = new Node();
            z.right = queue.poll();
            z.left = queue.poll();
            z.frequency = z.right.frequency + z.left.frequency;
            queue.add(z);//빈도수가 낮은 두개노드 골라서 빈도수합으로 결합 노드개수(n)만큼 반복
        }
        return queue.poll();

    }
    public static void main(String args[]) throws FileNotFoundException {


        HashMap <Character, Integer> hashmap = new HashMap<Character,Integer>();//해시맵선언
        String str = null;
        Scanner scanner = new Scanner (new File("C:\\Users\\kongb\\OneDrive\\문서\\카카오톡 받은 파일\\허프만 예시1.txt"));//""사이에 텍스트파일위치입력
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
        }//해시맵에 문자열 문자단위로 삽입
        queue=new PriorityQueue<Node>(100,new FrequencyComparator());
        int number =0;

        for(Character c: hashmap.keySet()){
            Node temp = new Node();
            temp.character=c;
            temp.frequency=hashmap.get(c);
            queue.add(temp);
            number++;//해시맵에 저장된 빈도수와 문자를 우선순위큐에 삽입
        }
        Node root=huffmanCoding(number);

        traversal(root,new String());// 각 노드에 0과 1을 입력하기 위한 트리순회 함수

        int count=0;
        int count2=0;

        String bitresult = new String();
        for(int i =0;i<str.length();i++)
        {
            bitresult = bitresult + charToCode.get(str.charAt(i)) + "";
            count2++;
        }
        System.out.println(bitresult);//허프만 코드로 압축된 비트 출력

        for(int i=0;i<bitresult.length();i++)
            count++;// 압축 후 비트값

        int count3=count2*7;//원래 비트값

        double count4=(double)count3/count;
        String formattedResult = String.format("%.2f", count4);// 압축률 출력

        System.out.println("원래 비트 값: "+count3);
        System.out.println("압축 비트 값: "+count);
        System.out.println("압축률: "+formattedResult);

    }

    public static void traversal(Node n,String s)// 왼쪽은 0 오른쪽은 1 이라는 수를 부여하는 트리 순회
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
