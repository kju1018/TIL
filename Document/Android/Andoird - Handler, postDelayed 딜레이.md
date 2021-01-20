# Andoird - Handler, postDelayed 딜레이

보통 Splash 페이지(앱 시작 로딩 화면) 구현 시 사용하는 Handler, postDelayed를 간단히 구현해볼 생각이다.

(SplashActivity.clss)

```
Handler hd = new Handler();
        hd.postDelayed(new Runnable() {
            @Override
            public void run() {
                
                Intent intent;
                intent = new Intent(SplashActivity.this, MainActivity.class);
                startActivity(intent);
                finish();
            }
        }, 3000);//3초 시간 지연
```

우선 안드로이드 스튜디오 새로운 프로젝트들은 기본적으로 ManinActiviy가 실행된다.

이것을 SplashActivity로 바꾸기위해

```
<activity android:name=".ui.activity.SplashActivity">
    <intent-filter>
        <action android:name="android.intent.action.MAIN" />

        <category android:name="android.intent.category.LAUNCHER" />
    </intent-filter>
</activity>
```

빨간부분을 SplashActivity로 바꿔준다.

그럼 3초동안 SplashActivty의 xml이 실행되고 자동으로 MainActivity로 이동한다.