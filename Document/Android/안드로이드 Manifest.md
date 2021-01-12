# 안드로이드 Manifest

## 매니페스트 파일

Android 시스템이 앱 구성 요소를 시작하려면 매니페스트파일, AndroidManifest.xml을 읽어서 해당 구성 요소가 존재하는지 확인한다. 앱은 이 파일 안에 모든 구성요소를 선언해야 하며, 이 파일은 앱 프로젝트 디렉토리의 루트에 있어야 한다.

매니페스트는 앱의 구성요소 선언 이외에도 많은 역할은 한다.

- 앱이 요구하는 모든 사용자 권한을 식별
- 앱에서 요구하는 최소 API레벨을 선언
- 앱에서 사용하거나 요구하는 하드웨어, 소프트웨어기능(카메라, 블루투스 등)을 선언

## 구성요소 선언

안드로이드의 4대 컴포넌트들은 매니페스트 파일에 등록을 해줘야 한다.

- <activity> Activity
- <service> Service
- <receiver> Broadcast Receiver
- <provider> Content Provider

소스에는 포함시키지만 매니페스트에서는 선언하지 않는 액티비티, 서비스, 콘텐츠 제공자는 시스템에 표시되지 않으며, 실행될 수 없다. 하지만 Broadcast Receiver는 매니페스트에서 선언해도 되고 코드를 사용해서 (객체로) 동적으로 생성한 다음 시스템에 등록해도 된다.(registerReceiver()를 호출)

4대 구성요소는 각각 인텐트에 의해 활성화 된다. 인텐트는 메시지 객체로 어떤 행동을 수행할지에 대한 명령이나 작업에 필요한 데이터를 포함한다.

<intent-filter>는 해당 구성요소(Activity,Service,Broadcast Receiver 등)가 어떤 암시적 Intent를 처리할 수 있는지 정의한다.

## 권한

매니페스트의 중요한 역할 중 하나가 권한 설정이다. 권한이라는 것은 안드로이드에서 민감하게 다루고 있는 관심사 중 하나다. 안드로이드 앱은 민감한 유저 정보나 카메라, 인터넷 등 특정 시스템 기능을 사용할 때 반드시 권한을 요청해야 한다.

```
Ex) <uses-permission android:name="android.permission.SEND_SMS"/>
<uses-permission android:name="android.permission.INTERNET"/> 등이 있다.
```

## 앱 요구사항 선언

매니페스트 파일에는 앱이 필요로 하는 하드웨어나 소프트웨어 특징을 명시할 수 있다.

예를 들어, 카메라 앱을 만들 경우에 카메라가 필수로 있어야 하니 카메라가 있는 기기에서만 Play Stroe 에서 해당 앱이 다운로드 될 수 있도록 명시하는 것이다.

매니페스트 파일에 <uses-feature> 태그를 사용하면 명시할 수 있다.

또한 <uses-sdk> 태그를 통해 요구되는 sdk 버전을 명시할 수도 있다.

하지만 min sdk 설정은 build.gradle파일에 선언하는 것이 좋다.

```
<manifest ... >
    <uses-feature android:name="android.hardware.camera.any"
                  android:required="true" />
    <uses-sdk android:minSdkVersion="7" android:targetSdkVersion="19" />
    ...
</manifest>
```