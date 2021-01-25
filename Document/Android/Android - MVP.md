# Android - MVP

## MVP란

MVP 패턴이란 Model, View, Presenter의 첫 글자를 따서 이름이 지어졌다.  MVP의 핵심 설계는 MVC와는 다르게 UI(View)와 비즈니스 로직(Model)을 분리하고, 서로 간에 상호작용을 다른 객체(Presenter)에 그 역할을 줌으로써 서로의 영향(의존성)을 최소화하는 것에 있다.

<img src = "https://user-images.githubusercontent.com/61860897/105716458-2bba5e80-5f62-11eb-9ba8-f05eb1e25cf9.png" width="300px">

## 각각의 기능

- Model
  - 프로그램 내부적으로 쓰이는 데이터를 저장하고, 처리하는 역할을 함.(비즈니스 로직)
  - View 또는 Presenter 등 다른 어떤 요소에도 의존적이지 않은 독립적인 영역임.
- View
  - UI를 담당하며 안드로이드에서는 Activity, Fragment가 대표적인 예.
  - Model에서 처리된 데이터를 Presenter를 통해 받아서 유저에게 보여줌.
  - 유저 액션(Action) 및 액티비티 라이프사이클 상태 변경을 주시하며 Presenter에 보내는 역할임.
  - Presenter를 이용해 데이터를 주고받기 때문에 Presenter에 매우 의존적임.
- Presenter
  - Model과 View사이의 매개체.
  - 모델과 뷰를 매개체라는 점에서 Controller와 유사하지만, View에 직접 연결되는 대신 인터페이스를 통해 상호작용 한다는 점이 다름.
  - 인터페이스를 통해 상호작용 하므로 MVC가 가진 테스트 문제와 함께 모듈화/유연성 문제 역시 해결할 수 있음.
  - 뷰에게 표시할 내용(Data)만 전달하며 어떻게 보여줄지는 View가 담당.