# Android - Kotlin 복습

## 함수

```
//함수를 선언하는 방법
//fun 함수면(변수명: 타입, 변수명: 타입, 변수명: 타입....) : 반환형 {
//      함수내용
//      return 반환값
//}
fun plus(first: Int, second : Int): Int {
    println(first)
    println(second)
    val result : Int = first + second
    println(result)
    return result
}

// - 디폴트 값을 갖는 함수 만들기
fun plusFive(first: Int, second: Int = 5) : Int{
    val result : Int = first + second

    return result
}

//반환값이 없는 함수 만들기
fun printPlus(first: Int, second: Int) {
    val result: Int = first + second
    println(result)
}

fun printPlus2(first: Int, second: Int){
    val result: Int = first + second
    println(result)
}

//간단하게 함수를 선어하는 방법
fun plusShort(first: Int, second: Int) = first + second

//가변인자를 갖는 함수 선언한느 방법
fun plusMany(vararg numbers: Int){
    for (number in numbers)
        println(number)
}

fun main(array: Array<String>){
    //함수를 호출하는 방법
    val result = plus(5, 10)
    println(result)

    //인수를 명시적으로 전달하는 방법
    val result2 = plus(first = 20, second = 30)
    println(result2)

    val result3 = plus(second = 100, first = 122)
    println(result3)

    println()
    //디폴트 값을 갖는 함수 호출하기
    val result4 = plusFive(10, 20)
    println(result4)

    println()

    val result5 = plusFive(10)
    println(result5)

    printPlus(10, 50)
    println()
    printPlus2(10, 50)

    val result6 = plusShort(50, 50)
    println(result6)

    plusMany(12,13,14,11,2,3,4)
}
```

## 제어 흐름

```
//When 구문

fun main(args: Array<String>) {

    val value : Int = 3

    when(value) {
        1 -> println("value is 1")
        2 -> println("value is 2")
        3 -> println("value is 3")
        else -> println("I do not know value")
    }
    val value2 = when(value) {
        1 -> 10
        2 -> 20
        3 -> 30
        else -> 100
    }
    println(value2)
}
```

## 배열

```
fun main(array: Array<String>) {

    //작업을 하는곳
    println(group1 is Array)//group1이 Array냐? true
    println(group1)
    //배열을 생성하는 방법(2)
    var group2 = arrayOf(1, 2, 3.5, "Hello")//변수 타입 생략 : 아무거나 다 넣을 수 있음

    //Array를 만드는 방법(3)

    val a1 = intArrayOf(1, 2, 3)
    //val a2 = intArrayOf("hello")
    val a2 = charArrayOf('b', 'b')
    val a3 = doubleArrayOf(1.2, 100.345)
    val a4 = booleanArrayOf(true, false, true)

    //Array를 만드는 방법(4) -> lambda를 활용한 방법
    var a5 = Array(10, { 0 })
    var a6 = Array(5, { 1;2;3;4;5 })
    println(a5[2])

    //Index란
    //[1,2,3,4,5]
    // "0"부터 시작

    //배열의 값을 꺼내는 방법(1)
    val test1 = group1.get(0)
    val test2 = group1.get(4)
    println(test1)
    println(test2)

    //배열의 값을 꺼내는 방법(2)
    val test3 = group1[0]
    println(test3)

    //배열의 값을 바꾸는 방법(1)

    group1.set(0, 14)
    println(group1[0])

    group1[0] = 200
    println(group1[0])
}
```

## 콜렉션

```
fun main(args: Array<String>) {
    //Immutable Collection 변경X
    //List - >중복을 허용한다.
    val numberList = listOf<Int>(1, 2, 3)
    println(numberList)
    println(numberList.get(0))
    println(numberList[0])

    //Set -> 중복을 허용하지 않는다
    //-> 순서가 없다. 그래서 인덱스가 없다.
    val numberSet = setOf<Int>(1, 2, 3, 3, 3)
    println(numberSet)
    println()
    numberList.forEach {
        println(it)
    }

    //Map -> Key, Value 방식으로 관리한다.
    val numberMap = mapOf<String, Int>("one" to 1, "two" to 2)
    println()
    println("Map 첫번째 값: " + numberMap.get("one"))

    //Mutable Collection (변경가능)

    val mNumberList = mutableListOf<Int>(1, 2, 3)
    mNumberList.add(3, 4)
    println()
    println(mNumberList)

    val mNumberSet = mutableSetOf<Int>(1, 2, 3, 4, 4, 4)
    mNumberSet.add(10)
    println()
    println(mNumberSet)

    val mNumberMap = mutableMapOf<String, Int>("one" to 1)
    mNumberMap.put("two", 2)
    println()
    println(mNumberMap)

}
```