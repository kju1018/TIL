# Android - Looper

## Looper

루퍼는 MainThread에 존재하며 Android 내에서 백그라운드 처리에 사용된다. 루퍼는 하나의 스레드만을 담당할 수 있고 하나의 스레드도 오직 하나의 루퍼만을 가질 수 있다. 루퍼는 MessageQueue가 비어있는 동안은 아무 행동도 안하고 메시지가 들어오면 해당 메시지를 꺼내 적절한 Handler로 전달한다.

## 동작과정

루퍼는 Handler와 같이 사용된다.

1. 메시지는 다른 스레드에 속한 Messge Queue에서 전달된다
2. Message Queue에 메시지를 넣을 땐 Hanlder의 sendMessage()를 이용
3. 루퍼는 Messgae Queue에서 Loop()를 통해 반복적으로 처리할 메시지를 Handler에 전달
4. Handler는 handleMessage를 통해 메시지를 처리

생성방법

```
Thread thread = new Thread(new Runnable(){     
        @Override     public void run() {         
            Looper.prepare();         
            handler = new Handler();         
            Looper.loop();     
        } 
    }); 
thread.start();
```