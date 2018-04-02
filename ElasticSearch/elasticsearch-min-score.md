## 엘라스틱서치(ElasticSearch) min score

score에 지정된 값보다 작은 문서는 제외 시킨다.

```
GET /_search
{
    "min_score": 0.5,
    "query" : {
        "term" : { "user" : "kimchy" }
    }
}
```

엘라스틱서치 레퍼런스에서는 대부분의 경우에는 이 방법이 적합하지 않다고 나와 있다. 내 생각에는 쿼리의 구성 요소에 따라 score가 천차만별일 텐데 적합한 min_score를 찾기 힘들어서 그렇지 않을까 생각한다. 