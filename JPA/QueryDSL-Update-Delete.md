## QueryDSL Update / Delete

JPQL 배치 쿼리와 같이 영속성 컨텍스트를 무시하고 데이터베이스를 직접 쿼리한다.

### Update

```java
QItem item = Qitem.item;
JPAUpdateClause updateClause = new JPAUpdateClause(em, item);
long count = updateClause.where(item.name.eq("체리픽")).set(item.price, item.price.add(100)).execute();

```

수정 배치 쿼리는 com.mysema.query.jpa.impl.JPAUpdateClause를 사용한다.

### Delete

```java
QItem item = Qitem.item;
JPAUpdateClause deleteClause = new JPADeleteClause(em, item);
long count = deleteClause.where(item.name.eq("체리픽")).execute();

```

삭제 배치 쿼리는 com.mysema.query.jpa.impl.JPADeleteClause를 사용한다.
