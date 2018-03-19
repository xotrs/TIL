## term
term은 필드에 지정한 term이 들어있는 도큐먼트와 매칭되며, 용어 분석을 하지 않고 완전히 일치할 때만 매칭된다. 또한 standard_analyzer는 lowercase filter가 적용되기 때문에 텍스트는 소문자여야 하고, 대문자로 입력하면 검색되지 않는다.

## filter
필터는 점수 계산 방식을 바꾸지 않고도 쿼리를 사용하여 다른 절과 일치할 문서를 매칭할 수 있다. 

대문자 검색 안 되는 줄 모르고 계속 대문자로 넣고 hit 안돼서 삽질했다...
 
아래의 term 필터는 status 필드가 published인 도큐먼트와 매칭된다.

```
GET /_search
{
  "query": { 
    "bool": { 
      "must": [
        { "match": { "title":   "Search"        }}, 
        { "match": { "content": "Elasticsearch" }}  
      ],
      "filter": [ 
        { "term":  { "status": "published" }}
      ]
    }
  }
}
```
