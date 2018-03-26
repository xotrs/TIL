개발을 하다보면 request cost나 시간이 많이 걸리는 API가 있다. 이 문제는 레일즈의 cache method를 통해서 어느정도 해결할 수 있다. 최신의 데이터를 가지고 있을 때는 query로 데이터를 요청하지 않고 cache를 통해 데이터를 불러 올 수 있다. 그 중에서도 많이 사용하는 write, read, fetch 3개의 method를 간략하게 정리했다.

### write

write는 cache key와 cache value 두 개의 argument를 가진다 .

```ruby
Rails.cache.write 'my_caching_key', some_data
```

이 데이터는 cached 됐고 필요할 때 불러서 사용할 수 있다. 그리고 expiry period(캐시의 만료 시간) 같은 추가 옵션도 있다. 

```ruby
Rails.cache.write 'my_caching_key', some_data, expires_in: 1.hour
```

cache가 만료되었을 때는 nil을 return 한다.
caching key가 굳이 string 일 필요는 없다. array, hash와 같은 object일 수도 있다. 


```ruby
Rails.cache.write(['some_data', @user], some_data)
Rails.cache.write({key: 'important_data', owner: @user}, some_data)
```

### read

read는 cache key를 통해서 데이터를 가져온다. 먄약에 데이터가 존재하지 않을 때에는 nil을 반환한다.

```ruby
Rails.cache.read 'my_caching_key'
```

또한 write와 같이 non scalar key로 데이터를 가져올 수 있다.

```ruby
Rails.cache.read({key: 'important_data', owner: @user})
```

### fetch

fetch는 read와 write 둘 다 수행한다. cache가 존재하면 그것을 return하고 아니면 block을 수행하고 cache에 write 한 다음 return 한다. 

```ruby
Rails.cache.fetch('some_key', expires_in: 10.minutes) do
  some_caculation
end
```

some key가 현재 cache key라면, cached data가 return 되고, 아니라면 block을 수행하고 some key에 return value를 저장한다. 