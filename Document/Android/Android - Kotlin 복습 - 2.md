# Android - Kotlin 복습 - 2 

오늘은 아주 간단하게만 class에 대해 복습 할 예정이다.

## Class

```
//클래스를 만드는 방법(1)
class Car(var engine: String, var body: String) {//이건 기본 생성자
    var price = 0;
    constructor(engine: String, body: String, price: Int): this(engine, body){
        this.price = price
    }
}
//클래스를 만드는 방법(1-1) ->1번 방법의 확장!
class Car1(engine: String, body: String) {
    //constructor() 적어줘도 가능 Car1 constructor(engine: String, body: String)
    //반드시 필요한 생성자 인자(매개변수)을 괄호에 적어줌 engine, body
    var door: String = ""

    constructor(engine: String, body: String, door: String) : this(engine, body) {//생성자
        this.door = door
    }
    /*
    constructor(engine: String, body: String, door: String){
        this.engine = engine
        this.body = body
        this.door = door
    }이건 안된다
     */
}
//클래스를 만드는 방법(2)
class SuperCar {
    var engine: String
    var body: String
    var door: String

    constructor(engine: String, body: String, door: String) {//생성자
        this.engine = engine
        this.body = body
        this.door = door
        println(this.body)
    }

}
//클래스 만드는 방법 (2-1) -> 2번 방법의 확장
class Car2 {
    var engine: String = "" // ="" 생략가능
    var body: String = "" // ="" 생략 가능
    var door: String = ""

    constructor(engine: String, body: String) {//반드시 필요한 것
        this.engine = engine
        this.body = body
    }

    constructor(engine: String, body: String, door: String) {
        this.engine = engine
        this.body = body
        this.door = door
    }
}
//init
class RunableCar2 {
    var engine: String
    var body: String

    constructor(engine: String, body: String) {
        this.engine = engine
        this.body = body
    }

    init {//객체를 만들면 이부분이 무조건 실행이 됨
        //초기셋팅을 할 때 유용하다.
        println("RunableCar2가 만들어 졌습니다.")
    }
}
```