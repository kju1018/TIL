# Android - RecyclerView

## RecyclerView 동작

RecyclerView는 안드로이드 개발을 할 때 아주 많이 사용한다. 이 RecyclerView는 실제로 어떻게 작동하고, 데이터가 어떻게 사용자에게 보여지는 건지 공부해보았다.

## ListView VS RecyclerView

ListView가 있는데 왜 RecyclerView가 생겼을까?

먼저 ListView는 몇 가지 단점이 있었다.

- 스크롤 시 버벅임 : ListView는 데이터셋에  데이터가 있는 만큼 뷰를 생성하는 습관이 있다. 이렇게 뷰를 만들고

```
findViewById()
```

메소드를 사용하는 것은 비용이 상당히 많이 드는 작업이다.

- 기본 애니메이션의 지원이 없다: ListView는 애니메이션에 대한 기본 지원이 없다.
- 오직 수직 스크롤만 가능: ListView는 오로지 수직 스크롤만 가능하다.

## RecyclerView란?

공식 안드로이드 문서에는 다음과 같이 설명되어 있다.

```
RecyclerView는 스크롤 리스트를 만들 수 있는 UI컴포넌트 입니다. 기본적으로 Viewholder
패턴을 사용하여 수평/ 수직/ 그리드 또는 staggerd한 그리드 방식으로 어댑터 기반의
뷰를 랜더링하는데 사용되는 새로운 ViewGroup입니다.
```

RecyclerView의 4가지 주요 컴포넌트

- RecyclerView.Adapter: 앱의 데이터셋에서 RecyclerView에 표시되는 아이템 뷰에 바인딩을 제공
- RecyclerView.LayoutManager: RecyclerView내에 아이템을 배치 한다. 여러가지 매니저 중 하나, 커스텀을 구현하여 사용 할 수 있다.
- RecyclerView.ItemAnimator: RecyclerView에는 기본 애니메이션이 함께 제공된다.
- RecyclerView.ViewHolder: RecyclerView와 함께 의무적으로 사용해야 하며, 화면에 그리고 싶은 개별적인 아이템의 UI를 그릴 수 있도록 도와준다.

## 동작원리

<img src = "https://user-images.githubusercontent.com/61860897/106288823-db0d7300-628b-11eb-8f3e-6f05cffc0dca.png">

<출처: MicroSoft>

RecyclerView는 데이터들의 모든 아이템에 대해 아이템 뷰를 할당하지 않는다.

대신 화면에 맞는 아이템 뷰의 수만 할당하고 사용자가 스크롤 할 때 해당 아이템 레이아웃을 다시 재활용한다. 뷰가 스크롤 되어 보이지 않게 되면 위 사진과 같이 재활용 과정을 거친다.

- 뷰가 보이지 않고 더 이상 표시되지 않으면 scrap View가 된다.

ScrapView: RecyclerView는 ScrapView를 위한 Scrap Heap캐싱 시스템이 존재한다. 이는 뷰를 어댑터로 다시 전달하지 않고도 뷰를 레이아웃 매니저로 직접 반환할 수 있는 경량화된 컬렉션이다. 이것이 가능한 이유는 데이터가 여전히 뷰홀더에 연결되어 있기 때문이다. 따라서 데이터를 바인딩하기 위해 어댑터에 다시 전달할 필요가 없다. 여기서 배치된 뷰가 일시적으로 분리되지만 동일한 레이아웃을 그릴 때 재사용 된다.

뷰가 보여지는 공간 바로 위와 아래의 보이지 않는 뷰는 분리된 뷰다. 분리된 뷰는 코드가 리턴되기 전에 다시 연결되어야한다.

- 새로운 아이템을 표시할 경우 재사용하기 위해 recycle pool에서 뷰를 가져온다. 이 뷰를 표시하기 전에 어댑터에 의해 다시 바인딩 되어야 하므로 dirty 뷰라고한다.

Scrap Heap과 마찬가지로 다음과 같은 타입의 뷰에 대한 다른 캐싱 시스템이 있다. 이 시스템은 바로 Recycle Pool이다.

Recycle Pool: 이 컬렉션은 잘못된 데이터(다른 위치 또는 인덱스의 데이터)가 있는 것으로 가정되는 뷰로 구성되어 있으며, 데이터를 뷰홀더에 다시 연결하거나 바인딩한 다음 레이아웃 매니저로 반환할 수 있도록 항상 어댑터에 전달된다.

Recycler 인스턴스는 새 뷰를 얻거나 이전 뷰를 재활용할 수 있도록 레이아웃 매니저에게 제공된다.

dirty 뷰 재활용 : 어댑터는 표시할 다음 아이템의 데이터를 찾고 이 데이터를 이 아이템의 뷰에 복사한다. 이러한 뷰에 대한 참조는 재활용 뷰의 뷰홀더에서 검색된다.

리사이클된 뷰는 화면에 표시되려고 하는 RecyclerView의 아이템 리스트에 추가된다.