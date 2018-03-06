전 회사에서는 [Gson](https://github.com/google/gson)을 사용하지 않아 존재만 알고 있었다. 하지만 현재 회사에서는 Gson을 사용한다. 업무나 나를 위해서 익숙해지는게 좋기 때문에 새로운 것이 발견될 때마다 기록하려고 한다.

요 근래에 회사의 자바 서버를 만지면서 Entity를 수정해야하는 일이 있었다. Entity에 정의된 필드에서 한 가지 모르는 Annotation을 발견했는데 바로 @SerializedName이다. Gson에서 호출되는 녀석인데 일단 Gson의 정의부터 알아보면 다음과 같다.

## Gson?
Gson은 자바 객체와 JSON 간의 직렬화 및 역직렬화를 위한 오픈소스 자바 라이브러리이다. 

Gson의 정의를 알아보니 이름만 봐도 @SerializedName이 무엇을 해주는 녀석인지 대충 눈에 보인다. 간단한 예제를 통해 알아보면 다음과 같다.

## Gson @SerializedName?

```java
public class Person {
    @SerializedName(value = "name")
    private String personName;

    @SerializedName(value = "bd")
    private String birthDate;
}

```
Person Class에는 personName, birthDate라는 2개의 field가 있다. @SerializedName annotation의 value는 객체를 직렬화 및 역직렬화 할 때 이름으로 사용된다. 위에 personName field는 JSON에서 name으로 표출된다.

```
{
    "name":"cherrypick",
    "bd":"1989-10-24"
}
```



reference<br>
https://stackoverflow.com/questions/28957285/what-is-the-basic-purpose-of-serializedname-annotation-in-android-using-gson