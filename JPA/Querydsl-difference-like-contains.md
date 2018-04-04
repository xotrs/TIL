회사에서 어드민 페이지를 개발했는데 포인트 지급내역 페이지이다보니 검색 기능이 필요하다. Querydsl의 `like`로 코드를 작성하고 확인해보니 컬럼의 풀텍스트가 일치하는 것만 출력이 된다. 앞뒤로 `%`를 붙이니 부분 텍스트만 입력해도 일치하는 것으로 리스트가 출력된다. `contains`는 어떨까 싶어서 확인해보니 `%`를 넣지 않아도 `like`에다가 `%`를 앞뒤로 붙인 것과 같은 결과가 출력된다. 
차이를 레퍼런스를 통해서 확인했는데 둘 다 StringExpression 클래스에 속해있고 간단한 설명은 다음과 같다.

```java
query = query.where(qUserEntity.email.like(userEmail));
//지정된 str(userEmail)과 같으면 return
```

```java
query = query.where(qUserEntity.email.contains(userEmail));
//지정된 str(userEmail)이 포함되는 경우 true를 return
```


