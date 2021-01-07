# POSIX CLI 실습-2

## 절대경로 VS 상대경로

절대경로: 어떤 디렉토리에 있던지 언제나 그 경로를 가리킨다.

상대경로: 어떤 디렉토리에 있느냐에 따라 달라진다.

```
현재 위치: /Users/aaa/posix 라고 가정
**상대경로**

**cd .. = cd ../**
결과: /Users/aaa로 이동
(부모 디렉토리로 이동)

현재위치: /Users/aaa

**cd ./posix**
결과: /Users/aaa/posix로 이동

현재위치 /Users/aaa/posix
**절대경로**

현재위치: /Users/bbb

**cd /Users/aaa/posix**
결과: /Users/aaa/posix로 이동

현재위치 /Users/aaa/posix
```

## 파일 다루기

파일을 다루는 데에 아주 중요한 부분은 편집기를 사용하는 것이다.

### 파일 생성

------

nano 사용

```
nano 입력

Ctrl + o : 저장
Ctrl + x : 나가기
```

결과:

![nano](https://user-images.githubusercontent.com/61860897/103905705-4d35e080-5142-11eb-9549-0f0ccd4fe8e9.png)

hello world 입력 후 Ctrl + o 입력

결과:

![nanosave](https://user-images.githubusercontent.com/61860897/103905770-5d4dc000-5142-11eb-95f6-6e34b596a362.png)



파일명 입력후 엔터

결과:

![save결과](https://user-images.githubusercontent.com/61860897/103905849-78203480-5142-11eb-943e-2d934d2a4ca1.png)

![save결과bash](https://user-images.githubusercontent.com/61860897/103905874-7f474280-5142-11eb-8cfb-bb5d2461d783.png)

```
nano hello.txt 입력
결과: 다시 hello.txt파일로 들어가진다.
```

Cat 명령어

안에 내용을 간단하게 보고 싶을 때 사용한다.

```
cat hello.txt 입력
결과:
```

![cat](https://user-images.githubusercontent.com/61860897/103905935-971ec680-5142-11eb-80b0-5073ce26879a.png)

### 수정

------

파일 내용 수정

```
1. nano hello.txt입력
2. 내용 수정
3. Ctrl + o
4. 저장
```

파일 이름 수정

```
mv hello.txt hello_world.txt 입력
결과: hello_world.txt로 파일명 변경

※mv hello_world.txt ../hello_world.txt는 우리가 알고 있는 이동을 한다.
```

### 삭제

------

```
rm hello_world.txt입력
결과: 삭제
```

### 순서대로 실행하기

------

CLI를 순서대로 실행하기 위해서는 명령어 사이에 ';'를 사용하면 된다.

```
mkdir dummy;cd dummy;touch hello.txt;cd ..;ls -R 입력
결과: 
1. dummy 디렉토리 생성
2. dummy 딜렉토리로 이동
3. hello.txt생성
4. 부모 디렉토리로 이동
5. 하위 디렉토리, 파일 보기
```

### 강의

------

- [생활코딩 POSIX CLI](https://www.opentutorials.org/module/3747/22522)