## after_action
controller에서 action이 동작한 후 수행되어야 하는 작업이 있다. after_action을 사용하면 공통된 작업을 수행하고 중복 코드를 줄일 수 있다. <br>아래는 test1, test2에서만 after_action으로 test4를 수행하는 코드를 보여준다.

```ruby
class SomeController < ApplicationController
    after_action :test4, only: [:test1, :test2]

    def test1
      ...
    end

    def test2
      ...
    end

    def test3
      ...
    end

    def test4
      ...
    end
end
```

after_action을 수행할 때 넘겨야하는 파라미터가 있다면 다음과 같이 작성할 수 있다.
```ruby
after_action -> { test4(p1, p2) }, only: [:test1, :test2]
```
