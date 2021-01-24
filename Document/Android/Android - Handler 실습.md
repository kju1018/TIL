# Android - Handler 실습

오늘은 실습을 통해 Handler를 알아볼 것이다.

```
class MyHandler extends Handler {

    @Override
    public void handleMessage(@NonNull Message msg) {
        super.handleMessage(msg);
        Bundle bundle = msg.getData();
        int value = bundle.getInt("value");
        textView.setText("현재 값 : "+value);
    }
}
```

우선 핸들러 클래스를 작성해주고 handleMessage메소드를 구현시켜 준다. 그럼 thread에서 sendMessage를 통해 보낸 Message가 들어온다.

```
class BackgroundThread extends Thread {
    int value = 0;
    boolean running = false;

    public void run() {
        running = true;
        while (running) {
            value += 1;

            Message message = handler.obtainMessage();
            Bundle bundle = new Bundle();
            bundle.putInt("value", value);
            message.setData(bundle);
            handler.sendMessage(message);

            try {
                Thread.sleep(1000);
            } catch (Exception e) {
            }
        }
    }
}
```

그리고 Main Thread대신 새로운 Thread를 만들어준다.

여기서는 직접 UI를 다루지 못하기 때문에 원하는 값을 sendMessage를 통해 보내준다.

```
TextView textView;
MyHandler handler = new MyHandler();
@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);
    textView =findViewById(R.id.textview);

    BackgroundThread thread = new BackgroundThread();
    thread.start();
}
```

백그라운드 실행

순서는 MainActivty에서 Thread실행

Thread에서 sendMessage를 통해 Message전달

Handler에서 전달 받은 Message를 handleMessage를 통해 받아 Textview를 변경해준다.

<img src = "https://user-images.githubusercontent.com/61860897/105632156-1f1c0480-5e95-11eb-97ea-fd1e213317eb.png" width="300px"><img src = "https://user-images.githubusercontent.com/61860897/105632155-1e836e00-5e95-11eb-8f77-351ef5f00c5e.png" width="300px">

