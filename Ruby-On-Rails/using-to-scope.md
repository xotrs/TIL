## 레일즈 Named Scope

### Named Scope?
Named scope는 특정한 조건식 또는 정렬식 등을 미리 모델 쪽에 이름을 붙여 저장해두고, 이후에 해당 조건식 또는 정렬식을 이용하고 싶을 때는 이름을 호출해서 사용하는 것을 말한다. named scope를 사용하면 직관적이고 조건 변경을 해야하는 경우에도 named scope를 정의한 부분만 수정하면 된다는 장점이 있다.

named scope를 정의하기 위한 구문은 다음과 같다.
```
scope name, -> {exp}
--------------------
name: 스코프 이름
exp: 조건식
```
실제 사용 예제는 다음과 같다.
```ruby
class Book < ActiveRecord::Base
  scope :jpub, -> { where(publish: '제이펍') } # 제이펍의 도서만 추출하는 jpub 스코프
  scope :newer, -> { order(published: :desc) } # 새롭게 출간된 도서 순서로 정렬해서 추출하는 newer 스코프
  scope :top10, -> { newer.limit(10) } # 새롭게 출간된 도서 순서로 10개를 추출하는 top10 스코프, 기존의 named scope를 기반으로 새로운 스코프를 생성 가능
end
```
아래와 같이 스코프를 메서드 체인처럼 연결해서 사용할 수도 있다.
```ruby
def scope
  @books = Book.jpub.top10
  render 'hello/list'
```

### default_scope?
자동으로 조건이 적용되게 한다.

default scope를 정의하기 위한 구문은 다음과 같다.
```
default_scope exp
--------------------
exp: 조건식
```
사용 예제는 다음과 같다.

```ruby
class Review < ActiveRecord::Base
  ...
  default_scope { order(updated_at: :desc) }
end
```

default scope에서 지정된 조건식은 개별적으로 order와 where 메서드를 지정해도 취소되지 않는다. 개별적으로 지정된 조건은 order 메서드의 경우 두번째 키 이후로 추가되고, where 메서드의 경우 AND 연산자로 추가된다.

reference
퍼펙트 루비 온 레일즈[제이펍 출판사]
