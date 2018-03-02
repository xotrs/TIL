## 레일즈 Inline conditionals

입사 전에도 루비의 경험은 있었지만 기초가 부족했고 큰 규모의 프로덕션에서 보는 것은 처음이었다. 그렇다보니 다양한 expression을 몰랐고 대충 눈치로만 파악하고 있었다. 이번 기회에 하나씩 정리하려고 마음먹었고 그 첫번째는 inline conditionals이다. 사용법은 다음과 같다.

```ruby
if password.length < 8
  puts "Password too short"
end

unless username
  puts "No user name set"
end
```

위의 코드를 inline if / unless로 변경하면 다음과 같다.

```ruby
puts "Password too short" if password.length < 8
puts "No user name set" unless username
```

reference : Codeschool : Ruby bits 