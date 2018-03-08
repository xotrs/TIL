## @Converter?
컨버터를 사용하면 엔티티의 데이터를 변환해서 데이터베이스에 저장할 수 있다. 우리 회사에서는 개인 정보와 같이 암호화/복호화 해야 되는 정보에 어노테이션이 붙어있다.

### Example

JPA를 사용하면 자바의 boolean 타입은 **방언**에 따라 다르지만 데이터베이스에 저장될 때 0 또는 1인 숫자로 저장된다. 그런데 데이터베이스에 숫자 대신 문자 Y 또는 N으로 저장하고 싶다면 컨버터를 사용하면 된다.

**방언** : 서로 다른 데이터베이스 간의 SQL 문법 차이를 의미한다.

아래의 코드는 @Converter를 적용해서 데이터베이스에 저장되기 직전에  BooleanToYNConverter 컨버터가 동작한다. Member 엔티티의 vip 필드는 boolean 타입이다.

```java
@Entity
@Data
public class Member {

    @Id
    private String id;

    private String name;

    @Convert(converter = BooleanToYNConverter.class)
    private boolean vip;

    //Getter, Setter
}
```

```java
@Converter
public class BooleanToYNConverter implements AttributeConverter<Boolean, String> {

    public String convertToDatabaseColumn(Boolean attribute) {
      return (attribute != null && attribute) ? "Y" : "N";
    }

    public Boolean convertToEntityAttribute(String s) {
      return "Y".equals(s);
    }
}
```

컨버터는 @Converter 어노테이션을 사용하고 AttributeConverter 인터페이스를 구현해야 하며 다음과 같다.

```java
@Converter
public interface AttributeConverter<X,Y> {
    public Y convertToDatabaseColumn(X attribute); // Entity to Database
    public X convertToEntityAttribute(Y dbData); // Database to Entity
}
```
### 클래스 레벨에서 지정하기
클래스 레벨에서도 설정할 수 있으며, 어떤 필드에 컨버터를 적용할지 명시해야 한다.
```java
@Entity
@Data
@Convert(converter = BooleanToYNConverter.class, attributeName = "vip")
public class Member {

    @Id
    private String id;

    private String name;

    @Convert(converter = BooleanToYNConverter.class)
    private boolean vip;

    //Getter, Setter
}
```
### 글로벌 설정
모든 Boolean 타입에 컨버터를 적용하려면 @Converter(autoApply = true)옵션을 적용하면 된다.

```java
@Converter(autoApply = true)
public class BooleanToYNConverter implements AttributeConverter<Boolean, String> {

    public String convertToDatabaseColumn(Boolean attribute) {
      return (attribute != null && attribute) ? "Y" : "N";
    }

    public Boolean convertToEntityAttribute(String s) {
      return "Y".equals(s);
    }
}
```
