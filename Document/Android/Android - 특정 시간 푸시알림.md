# Android - 특정 시간 푸시알림

## 목표

시간, 내용 등을 입력하여 저장을 하면 특정 시간에 푸시 알림이 오도록 할 것이다.

## 내용

실제 코드를 작성한 순서와 다르다. 내가 작성한 코드의 동작 방식은 제목, 내용, 시간, requestCode를 입력받아 Data라는 객체로 만들어 특정 시간에 Receiver로 전달해주어 내가 작성한 제목, 내용이 들어있는 푸시 알림을 받는 방식이다.

### 알람을 생성해줄 Activity생성

(Activity.class)

```
		private AlarmManager alarmManager;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_alarm);

        title_edit = findViewById(R.id.title_edit);
        content_edit = findViewById(R.id.content_edit);
        time_edit = findViewById(R.id.time);
        code_edit = findViewById(R.id.code);
        Button button = findViewById(R.id.create);

        alarmManager = (AlarmManager) getSystemService(Context.ALARM_SERVICE);

        button.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                String title = title_edit.getText().toString();
                String content = content_edit.getText().toString();
                String time = time_edit.getText().toString();
                String code = code_edit.getText().toString();
                data = new Data(title, content, time,code);
                setAlarm(data);
            }
        });
        
    }
    private void setAlarm(Data data) {
        Intent receiverIntent = new Intent(Alarm.this, AlarmReceiver.class);

        Bundle todoBundle = new Bundle();
        todoBundle.putParcelable("todo", data);
        receiverIntent.putExtra("todoBundle", todoBundle);
        PendingIntent pendingIntent = PendingIntent.getBroadcast(Alarm.this, Integer.parseInt(data.code), receiverIntent, PendingIntent.FLAG_UPDATE_CURRENT);

        SimpleDateFormat dateFormat = new SimpleDateFormat("yyyy-MM-dd HH:mm");
        Date datetime = null;

        try {
            datetime = dateFormat.parse(data.getTime());
        } catch (ParseException e) {
            e.printStackTrace();
        }
        Calendar calendar = Calendar.getInstance();
        calendar.setTime(datetime);

        alarmManager.set(AlarmManager.RTC_WAKEUP, calendar.getTimeInMillis(), pendingIntent);
    }
}
```

1. 알람매니저를 생성해준다.
2. 버튼을 눌렀을때 내용들을 담은 Data 객체를 만들어주고 setAlarm 메소드에 전달해준다.
3. Receiver를 호출할 Intent를 만들어준다. (안드로이드 4대 컴포넌트들은 Intent를 통해 다른 구성요소를 호출한다.)
4. 그 Intent를 담을 PendingIntent를 만들어준다. 여기서 Integer.parseInt(data.code) 이 부분이 requestCode부분인데 이 부분이 달라야 다른 PendingIntent가 된다. 즉 2개의 알림을 만들고 싶으면 다른 requestCode를 만들어 줘야한다.
5. 그 후 alarmManager을 통해 시간, pendingIntent를 set해준다.

### Receiver를 생성

(AlarmReceiver.class)

```
public class AlarmReceiver extends BroadcastReceiver {

    public AlarmReceiver() {
    }

    NotificationManager manager;
    NotificationCompat.Builder builder;

    private static String CHANNEL_ID = "channel1";
    private static String CHANNEL_NAME = "Channel1";

    @Override
    public void onReceive(Context context, Intent intent) {
		    Data todo = new Data();

        Bundle todoBundle = intent.getBundleExtra("todoBundle");
        if(todoBundle != null){
            todo = todoBundle.getParcelable("todo");
        }

        builder = null;

        manager = (NotificationManager) context.getSystemService(Context.NOTIFICATION_SERVICE);

        manager.createNotificationChannel(
                new NotificationChannel(CHANNEL_ID, CHANNEL_NAME, NotificationManager.IMPORTANCE_DEFAULT)

        );
        builder = new NotificationCompat.Builder(context, CHANNEL_ID);

        Intent intent2 = new Intent(context, MainActivity.class);
        PendingIntent pendingIntent = PendingIntent.getActivity(context,101,intent2, PendingIntent.FLAG_UPDATE_CURRENT);
        //FLAG_UPDATE_CURRENT이미 실행이 되어있으면 내용을 업데이트 해줌

        //알림창 제목
        builder.setContentTitle(todo.getTitle());

        builder.setContentText(todo.getContent());
        //알림창 아이콘
        builder.setSmallIcon(R.drawable.ic_launcher_background);
        //알림창 터치시 자동 삭제
        builder.setAutoCancel(true);

        builder.setContentIntent(pendingIntent);

        Notification notification = builder.build();
        manager.notify(1,notification);
    }
}
```

BroadcastReceiver를 상속 받는 AlarmReceiver를 만들어 준다.

이 클래스의 역할은 특정 시간이 되었을때 실행이 되어 푸시 알림을 해준다.

1. 오레오 이후 버전부터는 Notification 체널을 설정해줘야한다.
2. PendingIntent 작성
3. 여러 설정들을 해주고 notify해주면 푸시 알림이 생성된다.

### manifest 등록

------

```
<receiver
    android:name=".AlarmReceiver"
    android:enabled="true"
    android:exported="true">
    <intent-filter>
        <action android:name="android.intent.action.BOOT_COMPLETED"/>
    </intent-filter>

</receiver>
```

BroadCastReceiver는 안드로이드 4대 컴포넌트중 하나로 매니페스트에 등록해 줘야한다.

### 알림 삭제

------

```
alarmManager = (AlarmManager) getSystemService(Context.ALARM_SERVICE);
Intent intent = new Intent(MainActivity.this, AlarmReceiver.class);
PendingIntent pendingIntent =PendingIntent.getBroadcast(MainActivity.this, 1, intent, 0);
alarmManager.cancel(pendingIntent);
```

알림을 삭제 하고 싶으면 requestCode 가 같은 PendingIntent를 alarmManager.cancel을 통해 삭제시켜준다.