## 루비 Range(범위)에서 '..', '...' 차이

루비에서 .. 과 ... 의 범위 차이는 다음과 같다.
<br>

```ruby
a..b # a <= x <= b
a...b # a <= x < b 
```

to_a는 정수의 집합을 제공하지만, Range는 값의 집합이 아니라 단순히 시작과 끝, 두 개의 값이다. (4),(5)


```ruby
(1..5).include?(5)           #=> true
(1...5).include?(5)          #=> false

(1..4).include?(4.1)         #=> false
(1...5).include?(4.1)        #=> true
(1..4).to_a == (1...5).to_a  #=> true (4)
(1..4) == (1...5)            #=> false (5)
```

reference<br>
https://stackoverflow.com/questions/9690801/difference-between-double-dot-and-triple-dot-in-range-generation



