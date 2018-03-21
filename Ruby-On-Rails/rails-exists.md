## Rails exists?

단순히 객체의 존재를 확인하고 싶다면 exists라는 메소드가 있다. 이 메서드는 find와 같은 쿼리를 사용하여 질의를 날린다. 그러나 객체 또는 객체 Collection을 반환하는 대신 true 또는 false를 리턴한다. 사용법은 다음과 같다.


exists? 메서드 또한 여러개의 id를 사용할 수 있지만 데이터가 하나라도 존재할 경우 true가 리턴되는 단점이 있다.
```ruby
Client.exists?(1,2,3)
# or
Client.exists?([1,2,3])
```
<br>
아래의 경우에는 clients 테이블이 비어있으면 false를 리턴하고 그렇지 않은 경우에는 true를 리턴한다.
<br>

```ruby
Client.exists?
```
<br>
아래의 경우에는 clients 테이블에 first_name이 Ryan인 사람이 하나라도 있으면 true를 리턴하고 그렇지 않으면 false를 리턴한다.
<br>

```ruby
Client.where(:first_name => 'Ryan').exists?
```
