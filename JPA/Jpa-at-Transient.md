## Jpa @Transient

엔티티 클래스의 변수들은 대부분 테이블 컬럼과 매핑된다. 그러나 몇몇 변수는 매핑되는 칼럼이 없거나 매핑에서 제외해야만 하는 경우도 있다. @Transient는 엔티티 클래스 내의 특정 변수를 영속 필드에서 제외할 때 사용한다.

```java
@Entity
@Table(name = "USER")
public class User {
    private String name;

    private String password;
    @Transient
    private String confirmPassword;
```

User 클래스의 confirmPassword는 USER 테이블에서 매핑되는 컬럼이 없을뿐 아니라 각 변수에 저장된 값을 테이블에 저장할 필요도 없다.