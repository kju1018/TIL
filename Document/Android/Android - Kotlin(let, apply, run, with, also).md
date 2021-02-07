# Android - Kotlin(let, apply, run, with, also)

## let

```
fun main(args: Array<String> ){
    val string = "let"
    var letResult= string.let {
        "letResult!!!"
    }
    println(letResult)

    letResult= string.let {
        "letResult!!!"
        it
    }

    println(letResult)

    letResult= string.let {
        "letResult!!!"
        it
        "123"
    }

    println(letResult)
}
결과
-----------------------------------
letResult!!!
let
123
```

- let함수에서 it은 let을 호출한 객체이다
- 끝에 입력된 값을 리턴

## apply

```
fun main(args: Array<String> ){
    val book = Book("title", "content", 10000)

    var applyResult = book.apply {
        this.title = "titleChange"
        contents = "contentChange"
    }
    println(applyResult)
}
결과
---------------------------------
Book(title=titleChange, contents=contentChange, price=10000)
```

- apply 함수에서 this는 apply를 호출한 객체이다.
- apply를 호출한 객체를 반환

## with

```
val string  = "with"
    var withResult = with(string) {
        "result!!"
    }
    println(withResult)

    withResult = with(string){
        "result!!"
        string
    }
    println(withResult)

    withResult = with(string){
        "result!!"
        string
        this
    }

    println(withResult)
결과
---------------------------------------
result!!
with
```

- with는 일반함수로 receiver를 직접 입력받음
- this는 receiver
- 끝에 입력된 값을 리턴

## Run

```
val string = "run"
var runResult = string.run {
        "result!!"
}
println(runResult)

runResult = string.run {
    "result!!"
    this
}
println(runResult)
결과
---------------------------------------
result!!
run
```

- this는 run을 호출한 객체
- 끝에 입력된 값을 리턴

## also

```
val book = Book("title", "content", 10000)

var applyResult = book.also {
    it.title = "titleChange"
    it.contents = "contentChange"
}
println(applyResult)
결과
---------------------------------
Book(title=titleChange, contents=contentChange, price=10000)
```

- it은 also를 호출한 객체
- 호출한 객체를 반환

<img src = "https://user-images.githubusercontent.com/61860897/107147584-2c0b1e80-6992-11eb-95e4-46bfc99eb11e.png">

### Input

------

apply, run, also, let : 확장함수 T().apply, run, also, let {}

with : 일반함수 with(T()) {}

### binding in lambda

------

apply, run, with : this

also, let : it

### Output

------

apply, also : 객체

run, with, let : 끝에 입력된 값