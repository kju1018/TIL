# GIT CLI - 1



## GIT이란?

GIT이란 버전 관리 시스템(Version Control System)의 한 종류이다.

'분산형 버전 관리 시스템'이라고 하는데 원래는 Linux 소스코드를 관리할 목적으로  개발 되었다고 한다.



## 버전관리란?

버전 관리란 파일들을 하나의 버전으로 묶어 관리하는 것이다. 예를 들어 우리가 프로젝트를 진행할 때 'project1', 'project2',... 이런 식으로 내용일 바뀔 때마다 다른 이름으로 저장하는 경우가 있었을 것이다. 이렇게 파일들을 복사, 백업 등을 하였고 이것이 버전 관리이다.



## GIT의 장점

위에 적은 것처럼 'poject1', 'project2',... 이런 식으로 내용일 바뀔 때마다 다른 이름으로 저장하는 경우 파일이 작을 때는 괜찮겠지만 파일이 수백, 수천 개로 늘어나면 하나하나 다 이름을 바꾸기는 쉽지 않다. 이런 버전관리를 쉽게 해주는 기능이 있다.

또한 소스 코드를 직접 주고 받을 필요 없이, 같은 파일을 여러명이 동시에 작업하는 병렬 개발이 가능하다.



## GIT CLI

GIT CLI는 명령어를 이용해서 GIT을 제어하는 것이다. GUI보다는 어렵지만 그래도 계속 사용하는 이유는 익숙해지면 GUI없이 GIT을 다룰 수 있고 처리해야할 일을 한번에 명령해서 자동화가 가능하다.



## 실습

```
git init .
결과: 현재 있는 디렉토리를 버전관리 하고 싶을때 사용한다.
			.git 폴더 생성
```

![1-1](https://user-images.githubusercontent.com/61860897/104028155-bf262c80-520b-11eb-8045-50689cd3a01f.png)

```
git status
결과: 현재 git의 상태를 나타낸다.

아직 버전을 추가한적이 없기때문에 No commits yet이 나타난다.
```

![1-2](https://user-images.githubusercontent.com/61860897/104028185-c9482b00-520b-11eb-8625-641ffd9e61f2.png)

```
git add hello1.txt
결과: hello1.txt파일을 Staging Area로 올려놓는다.

git commit
결과: 버전을 만드는 명령어이고 에디터가 나타난다.

git commit -m "Message 1"
결과: 버전을 만드는 명령이이고 에디터가 나타나지 않고 커밋이 된다.

git log
결과: git버전이 잘 만들어졌는지 기록이 나타난다.
```

![1-3](https://user-images.githubusercontent.com/61860897/104028222-d1a06600-520b-11eb-87c9-0eb6d78f91f3.png)

```
git commit -m "Message 2"
내용을 변경후 다시 커밋

git log
```

![1-4](https://user-images.githubusercontent.com/61860897/104028231-d36a2980-520b-11eb-8900-3bfa71080e64.png)



### 강의

------

- [생활코딩 POSIX CLI](https://opentutorials.org/course/3839)