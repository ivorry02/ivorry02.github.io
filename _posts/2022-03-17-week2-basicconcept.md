# 컴퓨터알고리즘

## About markdown

### **markdown이란?**
일반 텍스트 기반의 경량 마크업 언어  
서식이 있는 문서를 작성하는데 사용되며, 문법이 쉽고 간단한 것이 특징이다. HTML 등 서식 문서로 쉽게 변환이 되기 때문에 응용 소프트웨어와 함께 배포되는 README 파일이나 온라인 게시물 등에 많이 사용된다.

### **markdown 문법**

* 제목      
      # C언어 문법  
      ## 반복문  
      ### while  
(#은 최대 6개까지 가능)  

ex) 
# C언어 문법
## 반복문
### while  
  

* 강조    
  - 굵은글씨  
   ** 중요 **   
   ex) **중요**

  - 기울임꼴  
    *참고 *  
    ex) *참고*

* 줄바꿈  
   스페이스바 두번  
     
   ex) 안녕하세요!  
   저는 ~~입니다.

* 하이퍼링크  
  [단어](해당 링크)  
  ex) [Instagram](https://www.instagram.com/?hl=ko)

* 사진 첨부  
  ![](이미지 링크)  
    
   ![](https://search.pstatic.net/common/?src=http%3A%2F%2Fblogfiles.naver.net%2FMjAyMjAzMDZfMTkz%2FMDAxNjQ2NTQxMjYwMjky.6Ek3pZjYi9sN7wAZRnjyO0_n7mAC5SPywl3CiBIc-cAg.-I2pUh_E7vvz6E4xcAHQUFItyqX9TqpYF8x20ePvgA0g.JPEG.aram627%2FIMG_0294.jpg&type=a340)
  

## 수업 내용 정리  

### **Git**
내 컴퓨터에서 저장하는 저장소
버전을 만들어서 저장함

### **Jekyll**
Vscode로 만든 것을 저장한 뒤 github에 올리면 마크다운이 바로 적용되지 않는다. Jekyll은 Vscode로 만든 것은 git에 저장되는데 그 다음 github에 올렸을 때 마크다운이 바로 적용될 수 있도록 해주는 장치역할이다.

### **cmd에 입력하는 명령어**
* d:  
  d드라이브로 저장 위치를 바꿈  
  ex) c:  

* cd my-awesome-site  
  my-awesome-site로 이동해서 시작함 (처음에 자신이 코드를 어디에 저장할 것인지 **꼭** 명령어로 입력해줘야 함)  
  ex) cd _posts  

* git init .  
  git에 비어 있는 저장소로 초기화 됨  

* git add .
  모든 파일을 무대에 올림

* git commit -m "message"
  수정본에 주석을 올린 파일을 봤을 때 어떤 것을 수정했나 알 수 있게 해줌  
  ex) git commit -m "modify last part"  

* git push  
  파일을 올림

* bundle exec jekyll serve  
  github 블로그에 올리기 전에 내가 맞게 했는지 테스트 하기 위함  
  (밑에서 세번째 줄에 "http://~~" 이 부분을 복사해서 인터넷 주소창에 붙여넣기)  

### Vscode 단축어

* Ctrl + Shift + P = 찾기


    