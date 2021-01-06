# POSIX CLI 실습-1



## 수업의 목적

CLI의 핵심은 File을 배우고, Directory를 다루는 방법이라고 생각한다.

오늘의 수업 목표는 File, Directory의 CRUD(Create, Read, Update, Delete)를 배우는 것이다.

즉 저장된 데이터를 처리하는 방법을 배운다.



## 실습



### Directory의 기본적인 사용법

------

처음 터미널을 실행했을 때 위치한 곳은 Home Directory이다.

ex) /c/Users/aaa

- **pwd** 명령어

  Print working directory의 약자로 지금 위치하고 있는 디렉토리를 나타낸다.

  ```
  **pwd**
  결과: ex) /c/Users/aaa
  ```

- **cd** 명령어

  내가 위치하고 있는 디렉토리를 바꾸는 명령어이다.

  ```
  **cd /**
  결과: 더 이상 위로 올라갈 수 없는 최상위 디렉토리로 이동
   
  **cd /c/Users/aaa**
  결과: /c/User/aaa로 이동
  
  **cd/ ~**
  결과: 어디 있든지 자신의 Home Directory로 이동
  
  **cd posix = cd ./posix**
  결과: 현재 디렉토리에서 posix디렉토리로 이동
  ※'./'는 현재 디렉토리를 의미한다.
  
  **cd /posix**
  결과: 최상위 디렉토리에 있는 posix로 이동
  ※ ./posix와 다르게 '/' 앞에 '.'이 없으면 최상위 디렉토리로 이동
  
  **cd .posix**
  결과: 숨겨져있는 posix디렉토리로 이동
  ```

- **ls, touch** 명령어

  ls는 현재 디렉토리에 어떤 파일과 디렉토리가 있는지를 알아내는 명령어이다.

  touch는 내용이 없는 간단한 파일을 만들어주는 명령어이다.

  ```
  **ls**
  결과: 현재 디렉토리에 어떤 파일과 디렉토리가 있는지를 나타내줌
  
  **ls --help**
  결과: ls명령어의 사용법을 나타내줌(이 기능이 없다면 man ls명령어 사용)
  ```

  ![help](https://user-images.githubusercontent.com/61860897/103775480-720e5300-5071-11eb-86d2-9317bde9718a.png)

  <ls -help 실행>

  ```
  **ls -l**
  결과: 각 디렉토리의 많은 정보를 보여준다.(자세히 보기 기능)
  
  **touch showfile.txt**
  결과: showfile.txt라는 내용없는 파일 생성
  
  **touch .hidden.txt**
  결과: .hidden.txt라는 감춰진 파일을 생성
  ※POSIX시스템에서는 파일명 앞에 .이 있으면 감춰진 파일이 된다.
  
  **ls -a**
  결과: .으로 시작하는 감춰진 파일도 다 보여준다.
  
  **ls -a -l = ls -al = ls -la**
  결과: 자세히 보기를 하면서 감춰진 파일을 보여준다. 
  ```

  - **mkdir** 명령어

    make directory의 줄임말로 디렉토리를 생성할 때 사용하는 명령어이다.

    ```
    **mkdir posix**
    결과: posix 디렉토리 생성
    ```

  - **mv** 명령어

    mv는 디렉토리의 이름을 변경하는 명령어이다.

    ```
    **mv dummy dummy2**
    결과: dummy디렉토리의 이름이 dummy2로 변경
    ```

  - **rm** 명령어

    rm명령어는 삭제 명령어이다.

    ```
    **rm dummy2**
    결과: 삭제가 안된다.
    ※rm 뒤에는 기본적으로 파일 이름이 온다. 디렉토리를 삭제하고 싶으면 디렉토리명 앞에
    -r을 추가해야 한다.
    이유: 디렉토리 안에는 여러 파일이 있을 수 있기 때문에 파일을 삭제하는 것보다 더 위험하다.
    그걸 방지하기 위한 안전장치이다.
    
    **rm -r dummy2**
    결과: dummy2 디렉토리 삭제
    ```

    ### 강의

    ------

    - [생활코딩 POSIX CLI](https://www.opentutorials.org/module/3747/22521)

