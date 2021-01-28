# Android - Kotlin 복습 - 3

## 반복문

Kotlin에서 사용하는 반복문은 Java와는 조금 다르다.

```
val a = mutableListOf<Int>(1, 2, 3, 4, 5, 6, 7, 8, 9)
```

- 방법 1

```
for (item in a){
    if(item == 5){
        println("Five")
    }else
        println(item)
}
```

- 방법 2

```
for ((index, item) in a.withIndex()){
    println("index: $index value: $item")
}
```

- 방법 3

```
a.forEach { it ->
    println(it)
}
```

- 방법 4

```
a.forEachIndexed { index, item ->
        println("index: $index value: $item")
    }
```

- 방법 5

```
for(i in 0 until a.size) {
        //0 ~ 8까지
        //until은 마지막 포함 x
        println(a.get(i))
    }
```

- 방법 6

```
for(i in 0 until a.size step (2)){
        println(a.get(i))
    }
step (2) 는 2씩 증가한다는 뜻
```

- 방법 7

```
for( i in a.size - 1 downTo (0)){
        println(a.get(i))
    }
downTo 는 값이 줄어듦
```

- 방법 8

```
for (i in a.size -1 downTo (0) step (2)){
        println(a.get(i))
    }
```

- 방법 9

```
for(i in 0..10){
        println(i)
    }//..은 마지막 포함
```

- 방법 10

```
var b: Int = 0
    var c: Int = 4

    while (b < c){
        b++
        println("b + $b")
    }
```

- 방법 11

```
do {
        println("hello")
        b++
    }while (b < c)
```

## 상속

------

상속은 자바와 비슷하지만 약간 다르다.

```
open class Character(var hp: Int, val power: Int) {
}//부모 클래스
class SuperMonster(hp: Int, power: Int) : Character(hp, power) {
   
}
class SuperNight(hp: Int, power: Int) : Character(hp, power) {
    
}
```

코틀린에서 자식 클래스가 인스턴스화 되기 위해서 부모 클래스 선행되서 인스턴스화 되어야 한다

### 자바

```
public class Character {
    private int hp;
    private int power;

    public Character() {
    }

    public Character(int hp, int power) {
        this.hp = hp;
        this.power = power;
    }
}
public class SuperMonster extends Character {
    private String name;

    public SuperMonster(String name) {
    }
}
 public Character() {
    }
```

자바로 처음에 디폴트 생성자 없이

```
public Character(int hp, int power) {
        this.hp = hp;
        this.power = power;
    }
```

만 생성하니까 자식 클래스에도 super를 생성해 줘야함

```
public SuperMonster(int hp, int power) {
    super(hp, power);
}
```