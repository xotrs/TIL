## 루비 short circuit
short circuit는 논리합(||), 논리곱(&&)을 통해 남은 연산을 생략하는 기법을 뜻하는 듯하다. 모든 언어에 short circuit이 존재하겠지만 루비의 경우 몇 가지를 정리해보면 다음과 같다.

###short circuit **and**
```ruby
if user
  if user.signed.in?
    #...
  end
end
```
user가 nil이면 user.signed_in은 동작하지 않는다.
```ruby
if user && user.signed_in?
  #...
end
```

###short circuit **assignment**
논리합으로 값을 할당하면 다음과 같이 동작한다.
```ruby
result = nil || 1 # 1
result = 1 || nil # 1
result = 1 || 2 # 1
```

###short circuit evaluation
```ruby
def sign_in
  current_session || sign_user_in
end
```
current_session이 nil이 아니면 sign_user_in은 동작하지 않는다.