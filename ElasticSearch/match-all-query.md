## match_all query

엘라스틱서치를 하다보면 매칭한 도큐먼트 가져오는 작업을 많이하게 된다. 지금까지 진행한 작업은 검색어가 존재했는데 처음으로 검색어가 없이 최신 순으로 5개 가져오는 쿼리를 작성하게 되었다. 그냥 SQL이었으면 `select * from table order by created_at desc limit 5` 같은 쿼리로 처리가 됐을텐데 엘라스틱서치에서는 처음이라 검색이 필요했다. 검색해보니 지정된 색인의 모든 문서를 검색하는 match_all 쿼리가 있었다. 사용법과 예시는 다음과 같다.

```
GET /bank/_search
{
  "query": { "match_all": {} },
  "from": 0,
  "size": 5,
  "sort": { "created_at": { "order": "desc" } }

}
```
match_all을 수행하고 created_at 기준 내림차순으로 결과를 정렬한 다음 상위 5개 문서를 반환하는 예시이다.


- query : match_all을 지정
- from : (0 기반) 어떤 문서 색인에서 시작할지 지정
- size : from 매개변수에서 시작하여 몇 개의 문서를 반환할지 지정
- sort : 정렬 지정

from이 지정되지 않으면 기본값은 0이며, size가 지정되지 않으면 기본값은 10이다.


### 2018.07.05 추가
```
GET /bank/_search
{
  "from": 0,
  "size": 5,
  "sort": { "created_at": { "order": "desc" } }
}
```
query 절이 없어도 잘 동작한다!앞으로는 이렇게 작성하면 될 거 같다.
