## 루비 unless

아래와 같이 사용한다.

```ruby
if ! tweets.empty?
  puts "Timeline:"
  puts tweets
end
```

위의 코드를 unless를 사용해서 직관적으로 바꾸면 다음과 같다.

```ruby
unless tweets.empty?
  puts "Timeline:"
  puts tweets
end
```

그리고 아래와 같이 else 문과 같이 사용한다면 unless보다 if 문을 사용하는게 더 낫다.

```ruby
unless tweets.empty?
  puts "Timeline:"
  puts tweets
else
  puts "No tweets found - better follow some people!"
end
```


```ruby
if tweets.empty?
  puts "No tweets found - better follow some people!"
else
  puts "Timeline:"
  puts tweets
end
```

**reference**<br>
Codeschool : Ruby bits 
