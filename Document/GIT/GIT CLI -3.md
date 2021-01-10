# GIT CLI - 3

## 버전 변경

```
git checkout master 입력
결과: 다시 최신버전으로 돌아간다.
```

## 보충 명령어

```
git add . 입력
결과: 현재디렉토리 밑에 있는 모든 파일을 add한다.

git commit -am "" 입력
결과: commit, add를 한번에 해준다.
※Untracked file은 자동으로 추가가 안된다. 즉 한번은 파일을 add하여 tracked 상태여야 한다.

git commit 입력
결과: 기본 에디터가 나타난다. 여러줄의 commit메시지를 좀 더 편하게 작성할 수 있다.

git config --global core.editor "nano"
결과: nano로 기본 에디터가 변경된다.
```

## 버전 삭제

```
git reset --hard 51276d5f9f9ef54ad0b502c3708803e88816bc72
결과: 51276d5f9f9ef54ad0b502c3708803e88816bc72 버전으로 reset한다.
※ 해당 버전을 reset 하겠다는 뜻이 아니라 해당 버전이 되겠다는 뜻이다.

git reset에는 
--soft, --misxed, --hard, --merge가 존재
--hard: 수정하고 있던것도 삭제
```

## 되돌리기

```
git revert [해당버전] 입력
결과: 새로운 버전이 생기면서 [해당버전]의 변화를 취소한다.([해당버전]은 삭제하지 않는다.)

즉
버전3
버전2
버전1

git revert [버전3] 입력

버전3'
버전3
버전2
버전1

버전3'는 버전2와 같다. 하지만 버전3는 삭제하지 않는다.

버전1로 돌아가고 싶을때
git revert [버전3] 입력
git revert [버전2] 입력

즉 한단계씩 돌아가야한다.
```



### 강의

------

- [생활코딩 POSIX CLI](https://opentutorials.org/course/3839/22595)