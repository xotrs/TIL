### QueryDSL?

QueryDSL은 오픈소스 프로젝트이다. 처음에는 HQL(Hibernate Query Language)을 코드로 작성할 수 있도록 해주는 프로젝트로 시작해서 지금은 JPA, JDBC, Lucene, 몽고 DB, Hibernate Search 등을 다양하게 지원한다. QueryDSL은 데이터를 조회하는 데 기능이 특화되어 있다.

### 설정
라이브러리를 버전에 따라 Gradle이나 Maven을 통해 추가할 수 있다.

### 시작

```java
public void queryDSL() {
    EntityManager em = emf.createEntityManager();

JPAQuery query = new JPAQuery(em);
QMember qMember = new QMember("m"); //생성되는 JPQL의 별칭이 m
List<Member> members = query.from(qMember).where(qMember.name.eq("회원1")).orderBy(qMember.name.desc()).list(qMember);
```

1. 엔티티 매니저를 JPAQuery 생성자에게 넘겨준다.
2. 사용할 쿼리 타입(Q)을 생성하는데 생성자에는 별칭을 주면 된다.

위에서 작성한 QueryDSL을 JPQL로 바꿔보면 다음과 같다.

```sql
select m from Member m
where m.name = ?1
order by m.name desc
```
<br>

### 기본 Q 생성
```java
public class Qmember extends EntityPathBase<Member> {
    public static final Qmember member = new QMember("member1");
    ...
}
```

쿼리 타입(Q)은 사용하기 편리하도록 기본 인스턴스를 보관하고 있다. 하지만 같은 엔티티를 조인하거나 같은 엔티티를 서브쿼리에 사용하면 같은 별칭이 사용되므로 이때는 별칭을 직접 지정해서 사용해야 한다.

쿼리 타입은 다음과 같이 사용한다.
```java
QMember qMember = new QMember("m") // 직접 지정
QMember qMember = QMember.member // 기본 인스턴스 사용
```

쿼리 타입의 기본 인스턴스를 사용하면 import static을 활용해서 코드를 더 간결하게 작성할 수 있다.

```java
import static jpabook.jpashop.domain.Qmember.member //기본 인스턴스

public void basic() {
    EntityManager em = emf.createEntityManager();

JPAQuery query = new JPAQuery(em);
QMember qMember = new QMember("m"); //생성되는 JPQL의 별칭이 m
List<Member> members = query.from(member).where(member.name.eq("회원1")).orderBy(member.name.desc()).list(member);
```