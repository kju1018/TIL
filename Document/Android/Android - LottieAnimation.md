# Android - LottieAnimation

오늘은 LottieAnimation실습을 진행해보았다.

1. 

```
build.gradle
implementation "com.airbnb.android:lottie:3.6.0"
이것을 추가해준다.
```

2. 

json형식에 파일을 assets폴더에 넣어준다.

3. 코드구현

```
var like_btn:LottieAnimationView = findViewById(R.id.like_btn)

isLiked = false
```

LottieAnimationView와 애니메이션을 구간으로 나누기위한 boolean타입의 변수를 선언해준다.

4. 

```
//좋아요버튼 클릭 리스너
like_btn.setOnClickListener {

    if(isLiked) {
        val animator = ValueAnimator.ofFloat(0.5f, 1f).setDuration(300)
        animator.addUpdateListener {
            like_btn.setProgress(it.getAnimatedValue() as Float)
        }
        animator.start()
        isLiked = false

    }else {
        val animator = ValueAnimator.ofFloat(0f, 0.5f).setDuration(1000)
        animator.addUpdateListener {
            like_btn.setProgress(it.getAnimatedValue() as Float)
        }
        animator.start()
        isLiked = true
    }
}
```

LottieAnimationView를 클릭할경우 Lottie파일의 반을 진행시켜주고

한번 더 클릭했을경우 나머지 반을 진행시켜주는 코드로 작성했다.

한번클릭시

<img src = "https://user-images.githubusercontent.com/61860897/106608103-5716fc00-65a7-11eb-83f0-eebc8804171b.gif" width="300px">

한번 더 클릭시

<img src = "https://user-images.githubusercontent.com/61860897/106608110-58e0bf80-65a7-11eb-9963-343e5808236c.gif" width="300px">



