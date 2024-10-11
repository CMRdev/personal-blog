# 查询和过滤器 DSL

- 过滤器限定了需要计算得分的文档数量，所以要比在同一搜索中融入整个查询快得多
- ES 会在位集合（bitset）中缓存过滤结果，如果过滤器用于另一个搜索请求，位集合就没必要重新计算了
- 如：term 过滤器、range 过滤器(在 99%的用例中，使用 range 过滤器而不是 range 查询，是正确的选择)、bool 过滤器
  ```js
  GET /newbank/_search
  {
    "query": {
      "bool": {
        "must": [
          {
            "term": {
              "firstname": "chen"
            }
          }
        ],
        "filter": [
          {
            "range": {
              "age": {
                "gte": 10,
                "lte": 30
              }
            }
          }
        ]
      }
    }
  }
  ```
- term 查询会计算得分、term 过滤器不会计算得分[term 查询的词条不会被分析]
- terms - 可搜索文档中的多个词条
  ```js
  GET /newbank/_search
  {
    "query": {
      "terms": {
        "firstname": ["chen", "zhou"]
      }
    }
  }
  ```
- match [词条在搜索前会执行分析步骤]
  ```js
  GET /newbank/_search
  {
    "query": {
      "match": {
        "firstname": {
          "query": "chen zhou",
          "operator": "or"
        }
      }
    }
  }
  ```
- prefix 查询和过滤器，prefix 在搜索之前是没有经过分析的。在搜索大写字母时可能匹配不到，如“Liber"
- wildcard 通配符查询 [注意：查询词条中越早出现通配符，ES 就需要做更多的工作来进行匹配]
  ```js
  GET /newbank/_search
  {
    "query": {
      "wildcard": {
        "firstname": {
          "value": "z*"
        }
      }
    }
  }
  ```
- exists 过滤器
  ```js
  GET /newbank/_search
  {
    "query": {
      "bool": {
        "filter": [
          {
            "exists": {
              "field": "account_number"
            }
          }
        ]
      }
    }
  }
  ```
