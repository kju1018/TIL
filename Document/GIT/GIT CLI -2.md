#  GIT CLI - 2

## 여러 개의 파일을 버전으로 만들기

먼저 저번에 만들었더 hello1.txt 파일을 수정한 후 다시 저장한다.

그리고 새로운 hello2.txt 파일을 생성한다.

```
git status 입력
```

![2-1](https://user-images.githubusercontent.com/61860897/104094371-e811f480-52d3-11eb-83f5-abc595e8be86.png)

hello1.txt 파일은 이미 버전 관리가 되고 있는 파일이고 hello2.txt는 아니기 때문에 다른 멘트가 나온다.

```
git add hello1.txt
git add hello2.txt 입력
결과: 둘 다 버전관리가 된다.
```

그 후 커밋.

각각의 커밋마다 어떤 파일이 연관되어 있는지 알고 싶을 때

```
git log --stat입력
```

![2-2](https://user-images.githubusercontent.com/61860897/104094372-e9432180-52d3-11eb-928f-8490a769eb3d.png)

## 버전 차이점 비교

```
git diff 입력
결과: 올라간 파일과 변경된 파일을 비교할 수 있다.

초록색이 추가된 부분
```

![2-3](https://user-images.githubusercontent.com/61860897/104094374-eba57b80-52d3-11eb-85b3-f702d4153796.png)

```
git reset --hard 입력
결과: 마지막버전으로 다시 돌아간다.
```

![2-4](https://user-images.githubusercontent.com/61860897/104094377-ecd6a880-52d3-11eb-9966-8e097ca6f97c.png)

```
git log -p입력
결과: 각 버전마다 어떤 파일에 어느 부분이 변경되었는지 알 수 있다.
```

![2-5](https://user-images.githubusercontent.com/61860897/104094380-ee07d580-52d3-11eb-9b15-b71b9d35bdb3.png)

## 버전 변경 Checkout

```
git checkout 51276d5f9f9ef54ad0b502c3708803e88816bc72 입력
결과: Message 2 버전으로 돌아간다.
hello2.txt 파일이 없어졌다
```

![2-6](https://user-images.githubusercontent.com/61860897/104094382-eea06c00-52d3-11eb-83b3-544e2aa7c732.png)