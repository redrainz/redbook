1. bool query(`bool`)
    1. 与文档匹配的查询，这些文档与其他查询的布尔组合匹配
    2. 参数
    
     参数 | 描述|非空|
     ---|---|---
     `must`| 必须匹配(AND)|N
     `should` |最好匹配（OR）|N
     `must_not`| 不能匹配（NOT）|N
     `filter`| 过滤，不影响score|N
     `minimum_should_match`|指定should返回的子句必须匹配的子句的数量或百分比。|N

2. boosting query(`boosting`)
    1. 返回与`positive`查询匹配的文档，同时降低与`negative`查询匹配的文档相关性得分
    2. 参数
    
     参数 | 描述|非空|
     ---|---|---
     `positive` |返回的所有文档都必须与此查询匹配。|Y
     `negative` |查询用于降低匹配文档的相关性得分|Y
     `negative_boost`|介于之间的浮点数0-1， 从positive查询中获取原始的相关性分数将分数乘以negative_boost值|Y
3. constant score query(`constant_score`)
    1. 包装过滤查询，并返回每个相关文档的相关性得分等于boost 参数值
    2. 参数

    参数 | 描述|非空|
     ---|---|---
     `filter`| (非空)过滤要运行的查询。返回的所有文档都必须与此查询匹配。|Y
     `boost` |文档的score,默认为1.0。|N
4. disjunction max query (`dis_max`)
    1.  查询多条语句根据相关性评分
    2.  参数
    
     参数 | 描述|非空|
     ---|---|---
     `queries`| 包含一个或多个查询子句。返回的文档必须与这些查询中的一个或多个匹配。如果一个文档匹配多个查询，Elasticsearch将使用最高的相关性得分|Y
     `tie_breaker` |介于之间的浮点数0，1.0用于增加与多个查询子句匹配的文档的相关性得分。默认为0.0|N

5. Function score query(`function_score`)
    1.  是专门用于处理文档_score的DSL，它允许爲每个主查询query匹配的文档应用加强函数， 以达到改变原始查询评分 score的目的


