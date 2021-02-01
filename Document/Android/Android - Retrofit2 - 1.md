# Android - Retrofit2 - 1

아직 코루틴 정리가 안끝나서 Retrofit을 먼저 정리 해야겠다

## Retrofit2

Retrofit2는 Square사에서 만든 http통신을 간편하게 만들어주는 라이브러리 이다.

이 Retrofit2과 네이버 영화검색 api를 이용한 실습을 진행했다.

- https://developers.naver.com/main/ 여기 사이트에 들어가서 앱등록, ClientId, ClientSecret를 발급받는다.
- 안드로이드 스튜디오로 돌아와서 defendencies에 추가해준다.

```
implementation 'com.squareup.retrofit2:retrofit:2.9.0'
implementation 'com.squareup.retrofit2:converter-gson:2.9.0'
```

- 인터페이스 생성

```
interface RetrofitService {
    @Headers("X-Naver-Client-Id: 발급받은 아이디",
        "X-Naver-Client-Secret: 발급받은 Secret")
    @GET("v1/search/movie")
    fun getMovies(
        @Query("query") query:String
    ) : Call<Movie>

}
```

간단하게 query (검색어)만 적용해서 GET으로 받아오겠다.

- <img src = "https://user-images.githubusercontent.com/61860897/106457354-3630a700-64d2-11eb-91d0-b98b82d6509b.png" width="500px">

postman으로 미리 불러온 데이터들이다.

문서를 봐도 되지만 이것을 보고 Data class를 만들어 줬다.

```
data class Movie (
    var lastBuildDate:String? = null,
    var total:Int? = null,
    var start:Int? = null,
    var display:Int? = null,
    var items:ArrayList<Items>? = ArrayList<Items>()

) : Serializable
data class Items (
    var title:String? = null,
    var link:String? = null,
    var image:String? = null,
    var subtitle:String?= null,
    var pubDate:String?= null,
    var director:String?=null,
    var actor:String? = null,
    var userRating:Double?= null
) : Serializable
```

- retrofit 생성

```
val retrofit = Retrofit.Builder()
        .baseUrl("<https://openapi.naver.com/>")
        .addConverterFactory(GsonConverterFactory.create())
        .build()
val service = retrofit.create(RetrofitService::class.java)
```

baseUrl과 ConverterFactory를 만들어주고 service를 연결시켜준다,

```
service.getMovies("반도").enqueue(object : Callback<Movie> {

    override fun onFailure(call: Call<Movie>, t: Throwable) {
        Log.d("asdf", "onFailure: 실패" + t.localizedMessage)
    }

    override fun onResponse(call: Call<Movie>, response: Response<Movie>) {
        if (response.isSuccessful){
            val moviews = response.body()

            Log.d("asdf", "onResponse: ${moviews?.items?.size}")
        }
    }

})
```

비동기 콜백을 이용해서 처리해준다.

- 

<img src = "https://user-images.githubusercontent.com/61860897/106457358-36c93d80-64d2-11eb-862b-8bec7b8467d4.png" width="500px">