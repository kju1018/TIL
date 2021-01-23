# Android - 백그라운드 작업

![다운로드](https://user-images.githubusercontent.com/61860897/105479631-06222080-5ce8-11eb-9493-1a9d6418d8c6.png)

- 즉시:

  Kotlin의 코루틴

  WorkManager

- 지연:

  Workmanager

- 정시:

  AlarmManager

## AlarmManager

안드로이드의 알람 서비스 시스템에 접근하는 것을 제공해주는 클래스이다.

- 주어진 시간이나 기간마다 Intent를 실행한다.
- Broadcast Receiver와 조합해서 서비스를 시작하고 다른 작업을 시작할 수 있다.
- 앱이 실행 중이 아닐 때도 작업을 트리거할 수 있다.
- busy wait 없이 작업을 예약할 수 있다. → 앱 리소스 최적화에 도움이 된다.

## JobScheduler

개발자가 백그라운드 작업(task)을 정의하고 언제 이 작업이 실행될지 타이밍을 정할 수 있게 도와준다. 이런 구조로 필요할 때만 디바이스가 깨어있게 되어 전력 소비를 줄일 수 있다.

JobScheduler는 개발자가 정의한 작업을 스케쥴링해주는 서비스이다. 이 객체에서 제공해주는 API를 사용하여 작업을 예약할 수 있다. 실행될 작업에 대한 구현은 JobService에 정의되어 있다. 그리고 작업이 언제, 어떤 상황에서 실행되어야 하는지는 JobInfo에 정의된다. JobInfo가 JobScheduler에 전달되면, JobScheduler는 적당한 때에 JobService를 실행시킨다.

JobService(잡서비스)는 개발자가 작업을 정의해야 하는 클래스이다. JobScheduler(잡스케줄러)는 예약된 작업을 실행할 때 JobService에 정의되어있는 `onStartJob` 함수를 호출해준다. 만약 어떤 이유로 작업을 중지해야 할 때 JobService에 정의되어 있는 `onStopJob` 함수를 호출해준다.

JobScheduler가 호출하는 `onStartJob` 등의 메소드는 모두 main thread에서 실행된다. 그렇기 때문에 무거운 작업을 여기서 모두 처리하면 안된다. 작업을 처리하는 다른 서비스나 쓰레드를 만들어 무거운 작업들을 위임해야 한다.

## WorkManager

앱이 종료되거나 기기가 다시 시작되더라도 실행이 예상되는 연기 가능한 비동기 작업을 쉽게 예약할 수 있는 라이브러리

기존에 JobScheduler가 이와 비슷한 역할을 하였는데 편의기능을 더하여 WorkManager를 만들었다. WorkManager는 내부적으로 JobScheduler를 사용하며(API 23 이상) JobScheduler를 지원하지 않는 단말(API 14~22)은 AlarmManager 또는 BroadcastReceiver를 사용하도록 구현되었다.
