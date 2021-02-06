# Android - BottomSheetDialogFragment

# 구현방법

```
public class Todo_add_dialog extends BottomSheetDialogFragment {

    @Override
    public void onCreate(@Nullable Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
    }

    @Nullable
    @Override
    public View onCreateView(@NonNull LayoutInflater inflater, @Nullable ViewGroup container, @Nullable Bundle savedInstanceState) {
        return inflater.inflate(R.layout.todo_add_dialog,container, false);
    }
}
BottomSheetDialogFragment를 상속받는 클래스 생성
private Todo_add_dialog todo_add_dialog;
todo_add_dialog = new Todo_add_dialog();
FragmentManager fm = getSupportFragmentManager();
todo_add_dialog.show(fm, "todo_add_dialog");

로 사용
```

- EditText가 있을경우 키보드가 가릴때

  <img src = "https://user-images.githubusercontent.com/61860897/107116776-ededfc00-68b8-11eb-8494-b7d80e60ed00.png" width="300px">

  <img src = "https://user-images.githubusercontent.com/61860897/107116778-f1818300-68b8-11eb-9c4e-56d942b4b91b.png" width="300px">

  이렇게 editText가 있어서 키보드가 올라갈경우 다른 view들을 가리게된다.

  해결방법:

  ```
  <style name="DialogStyle" parent="Theme.Design.Light.BottomSheetDialog">
      <item name="android:windowIsFloating">false</item>
      <item name="android:statusBarColor">@android:color/transparent</item>
      <item name="android:windowSoftInputMode">adjustResize</item>
  </style>
  이 스타일을 입력해준다.
  ```

  ```
  @Override
  public void onCreate(@Nullable Bundle savedInstanceState) {
      super.onCreate(savedInstanceState);
  
      setStyle(DialogFragment.STYLE_NORMAL, R.style.DialogStyle);
  //이 코드 입력
  }
  ```

  <img src = "https://user-images.githubusercontent.com/61860897/107116782-f34b4680-68b8-11eb-8b4a-3d9801988252.png" width="300px">

  코드 입력 후 스크린샷

- EditText가 있을경우 키보드가 자동으로 올라옴

  스타일에서 적용

  ```
  <style name="DialogStyle" parent="Theme.Design.Light.BottomSheetDialog">
      <item name="bottomSheetStyle">@style/AppModalStyle</item>
      <item name="android:windowIsFloating">false</item>
      <item name="android:statusBarColor">@android:color/transparent</item>
      <item name="android:windowSoftInputMode">adjustResize|stateVisible</item>
  </style>
  ```

- 배경 라운드 처리

  상단이 라운드 처리된 xml생성

  ```
  <?xml version="1.0" encoding="utf-8"?>
  <selector xmlns:android="<http://schemas.android.com/apk/res/android>">
      <item>
          <shape android:shape="rectangle">
              <solid android:color="@color/white" />
              <corners android:radius="1dp"
                  android:topLeftRadius="20dp"
                  android:topRightRadius="20dp"
                  android:bottomLeftRadius="0dp"
                  android:bottomRightRadius="0dp"/>
          </shape>
      </item>
  </selector>   <!--상단만 라운드처리-->
  ```

  스타일 적용

  ```
  <style name="DialogStyle" parent="Theme.Design.Light.BottomSheetDialog">
      <item name="bottomSheetStyle">@style/AppModalStyle</item>
      <item name="android:windowIsFloating">false</item>
      <item name="android:statusBarColor">@android:color/transparent</item>
      <item name="android:windowSoftInputMode">adjustResize</item>
  </style>
  
  <style name="AppModalStyle" parent="Widget.Design.BottomSheet.Modal">
      <item name="android:background">@drawable/circularbackground</item>
  </style>
  ```