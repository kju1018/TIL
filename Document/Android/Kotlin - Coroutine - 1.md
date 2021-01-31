# Kotlin - Coroutine - 1

## Coroutine이란

코루틴은 Background작업을 대신할 수 있는 Asynchronous/Non-Blocking Programming 제공하는 경량스레드(Light-Weight Threads)이다. 실행의 지연과 재개를 허용함으로서, 비 선점적 멀티태스킹을 위한 서브루틴을 일반화한 컴퓨터 프로그램 구성요소이다.

## -**서브루틴(subroutine)과 코루틴(coroutine)**

코루틴도 루틴의 일종이다. 다만 3가지의 차이점이 있는데

1. 코루틴에서는 메인-서브의 개념이 없다. 모든 루틴들이 서로를 호출할 수 있다.
2. 서브루틴의 경우에는 메인루틴에서 특정 서브루틴의 공간으로 이동한 후에 return 의해 호출자로 돌아와 다시 프로세스를 진행하는데 반해, 코루틴의 경우에는 루틴을 진행하는 중간에 멈추어서 특정 위치로 돌아갔다가 다시 원래 위치로 돌아와 나머지 루틴을 수행할 수 있다.
3. 서브루틴은 진입점과 반환점이 단 하나밖에 없어 메인루틴에 종속적이지만, 코루틴은 진입지점이 여러개이기 때문에 메인루틴에 종속적이지 않아 대등하게 데이터를 주고 받을 수 있다는 특징이 있다.

<img src = "https://user-images.githubusercontent.com/61860897/106386970-e7740600-641a-11eb-8cea-dd75c3ced746.png">

## -**비선점형 멀티태스킹(Non-preemptive Multitasking) 과 선점형 멀티태스킹(Preemptive Multitasking)**

하나의 Task가 Scheduler로 부터 CPU 사용권을 할당 받았을 때, Scheduler가 강제로 CPU 사용권을 뺐을 수 없으면 비선점형 멀티태스킹이고, 뺐을 수 있으면 선점형 멀티태스킹이다.

코루틴은 비 선점형 멀티태스킹이고, 쓰레드는 선점형 멀티태스킹이다. 이 말은 즉 코루틴은 병행성(Concurrency)을 제공하지만 병렬성(Parallelism)을 제공하지 않는 다는 의미이다.

## 실습

1. 

```
GlobalScope.launch {
    delay(5000)
    println("World!")
}
println("Hello,")
Thread.sleep(10000L)
```

결과: "Hello"출력 5초후 "World!" 출력 그리고 5초 후 종료

GlobalScope의 lifetime은 전체 application process에 의존하므로, application이 종료되면 같이 끝나게 되기 때문에 끝에서 sleep을 걸고 기다려야 launch 내부 동작을 실행할 수 있다.

launch는 현재 스레드를 blocking하지 않고 코루틴으로 실행한다.

위에서 delay함수는 blocking 할 수 없는 suspending 함수이기 때문에 GlobalScope.launch대신 Thread를 사용하면 에러가 발생한다.

1. blocking을 하기위해 runBlocking사용

```
runBlocking<Unit> {
    launch {
        delay(5000)
        println("launch에서 실행")
    }
    println("out")
    delay(10000)
}
println("마지막실행")
```

결과: "out" 출력 5초후 "launch에서 실행" 출력 5초 후 "마지막실행"

runBlocking을 만나면 main thread는 내부 코드가 완료될때 까지 block된다.

1. 작업이 완료될 때까지 기다림

```
fun main() = runBlocking {
    val job = GlobalScope.launch {
        delay(5000)
        println("World!")
    }
    println("Hello,")
    job.join()
}
```

join()을 사용해서 기다린다.



우선 코루틴을 처음 공부해서 그런지 헷갈리는게 많아서 정리하고 내일 다시 올려야겠다.

참고 사이트:

https://kotlinlang.org/docs/reference/coroutines/basics.html

https://wooooooak.github.io/kotlin/2019/08/25/코틀린-코루틴-개념-익히기/