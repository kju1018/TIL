# Android - Serializable, Parcelable

Android에서는 액티비티 간 데이터를 전달하기 위해 인텐트에 데이터를 추가한다.

전달할 데이터가 class인 경우 Serializable, Parcelable을 사용해야 한다.

## 직렬화 & 역직렬화

- 직렬화: 자바 시스템 내부에서 사용되는 Object 또는 Data를 외부의 자바 시스템에서도 사용할 수 있도록 byte 형태로 데이터를 변환하는 기술이다.
- 역직렬화: Byte로 변환된 data를 원래대로 object나 data로 변환하는 기술이다.

## Serializable

Serializable은 Android SDK가 아닌 JAVA interface로 해당 class가 직렬화 대상이라고 알려주는 marker interface이다. 구현해야할 메소드가 따로 없고 "Serializable"를 상속만 하면 된다.

```
data class Book (
    val title: String,
    val contents : String,
    val price : Int
) : Serializable
```

단점으로는 Serializable은 reflection을 사용하여 직렬화를 처리함으로 성능저하가 발생할 수 있다.

(reflection이란 객체를 통해 클래스의 정보를 분석해 내는 프로그램 기법을 말한다. 메소드를 호출 할 때, 타겟이 실제로 메소드 선언 자의 인스턴스인지, 올바른 인수 번호를 가지고 있는지 여부, 각 인수의 유형이 올바른지 여부 등을 확인해야한다. 즉 런타임에 코드의 동작을 유지하고 수정하는 유연하지만 느린 방법이다.)

## Parcelable

Parcelable은 Android SDK interface 로 reflection을 사용하지 않게 설계된 interface이다.

Parcelable 은 직렬화한 데이터 그 자체로 직렬화 처리 방법을 사용자가 명시적으로 작성하기 때문에 자동으로 처리하기 위한 reflection 이 필요 없다.

Parcelable은 Serializable보다 직렬화의 방법이 더 복잡하다.

1. Parcelable을 상속
2. 객체를 송신하기 위해 writeToParcel() 에 전달할 데이터를 순차적으로 저장.
3. 객체를 수신하기 위해 CREATOR를 작성하고 createFromParcel()로 전달받은 데이터를 순차적으로 읽어온다.

```
data class Book(
    val title: String?,
    val contents: String?,
    val price: Int
) : Parcelable {
    constructor(parcel: Parcel) : this(
        parcel.readString(),
        parcel.readString(),
        parcel.readInt()
    )

    override fun writeToParcel(parcel: Parcel, flags: Int) {
        parcel.writeString(title)
        parcel.writeString(contents)
        parcel.writeInt(price)
    }

    override fun describeContents(): Int {
        return 0
    }

    companion object CREATOR : Parcelable.Creator<Book> {
        override fun createFromParcel(parcel: Parcel): Book {
            return Book(parcel)
        }

        override fun newArray(size: Int): Array<Book?> {
            return arrayOfNulls(size)
        }
    }
}
```

### 비교

------

일반적으로 Serializable이 Parcelable보다 느리다고 한다. 하지만 특정 method (writeObject, readObject, readObjectNoData)를 커스텀한 Serializable은 Parcelable보다 빠르다고 한다.

속도 순서

1. 특정 method (writeObject, readObject, readObjectNoData)를 커스텀한 Serializable
2. Parcelable
3. Serializable