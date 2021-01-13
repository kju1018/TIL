# Activity 생명주기

오늘은 장례식장을 갔다 왔기 때문에 간단하게 복습의 의미로 안드로이드 생명주기를 정리해 볼 것이다.

## Activity 생명주기

![activity_lifecycle](https://user-images.githubusercontent.com/61860897/104467838-1c4e2380-55fa-11eb-8775-fe78fc9f4af6.png)

위 그림이 바로 Android Developer에서 공식으로 제공하는 생명주기 그림이다.

안드로이드는 앱이 실행된 후 다른 액티비티 화면으로 전환되거나, 스마트폰 화면이 꺼지거나 혹은 앱이 종료될 때와 같이 상태 변화가 있을 때마다 화면에 보이는 액티비티의 생명주기 메소드를 호출해서 상태 변화를 알려준다.

onCreate(), onStart(), onResume(), onPause(), onStop(), onDestroy() 6가지가 핵심 상태이다.

### Activity launched

------

액티비티가 실행되었다. 실행 후 액티비티는 'Created' 상태가 된다.

### onCreate()

------

이 콜백은 액티비티를 생성할 때 실행되는 것으로, 필수적으로 구현해야 한다. 액티비티가 생성되면 'Created' 상태가 되고, onCreate() 메소드가 실행을 완료하면 'Started' 상태가 된다. 액티비티 전체 생명 주기 동안 한 번만 발생해야한다.

### onStart()

------

onStart()가 호출되면 액티비티가 사용자에게 표시되고, 앱은 액티비티를 상호작용할 수 있도록 준비한다. 실행을 완료하면 'Resumed' 상태가 된다.

### onResume()

------

앱이 사용자와 상호 작용을하고 포커스가 떠날 때까지 이 상태에 머무른다.

### Activity running

------

실제로 액티비티와 상호작요이 가능한 환경에 있다.

### onPause()

------

액티비티가 foreground에 있지 않으면 호출된다. 'Paused' 상태가 된다.

### onStop()

------

액티비티가 화면을 완전히 벗어나면 호출된다. 실행 후 액티비티는 'Stopped' 상태가 된다.

### onDestory()

------

액티비티가 소멸되기 전 호출된다.

### Activity shut down

------

액티비티 종료

## 순서

- 액티비티가 실행되면 onCreate() → onStart() → onResume() 순서로 실행
- 다른 화면때문에 일부가 가려지면 onPause() 실행
- 전체가 가려지만 onStop() 실행
- 'Paused' 상태에서 다시 돌아오면 onResume() 실행
- 'Stopped' 상태에서 다시 돌아오면 onRestart() → onStart() → onResume() 순서로 실행
- 종료하면 onPause() → onStop() → onDestory() 순서로 실행 후 종료