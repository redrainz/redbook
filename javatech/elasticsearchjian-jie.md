### 1. 简介
---
es是基于Lucene构建的分布式全文搜索引擎，存入的每个字段都会被索引且可以被搜索，它的水平扩展性很强。

### 2.安装并运行最新版的es
---
- docker
    
```
docker pull docker.elastic.co/elasticsearch/elasticsearch:7.7.1

docker run -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" docker.elastic.co/elasticsearch/elasticsearch:7.7.1
```

### 3.基本概念
---
1. 倒排索引 由属性值来确定记录的一种索引，这个是搜索引擎的一种常用的方式
2. index 相当于数据库的概念，具有相同数据结构的集合
3. type 相当于数据表的概念，对index进行分组，在新版es中一个index一般只能有一个type
4. document 相当于表里的一条记录，它是使用JSON格式进行组织，原始数据就存在_source中
5. mapping 相当于数据表的结构，描述数据的类型，与数据库不同的是，它描述的是index下的所有数据

### 4. 使用
---
es是通过RESTful风格的http调用，来对es进行操作的，每一种请求方式都有其作用。创建数据或索引用POST ，更新用PUT，删除用DELETE，查询使用GET
方法。
1. 创建一条记录
```
POST localhost:9200/index/type
{
  "name": "John Doe2"
}
```
2. 更新一条记录
```
PUT localhost:9200/index/type/ULKuiXIBG106HA8fs02y
{
  "name": "John D"
}
```
3. 获取一条记录
```
GET localhost:9200/index/type/ULKuiXIBG106HA8fs02y
```
4. 搜索一条记录 
```
GET localhost:9200/index/type/_search  # (index,type可以不加)
{
    "query": {
        "match_all": {}
    }
}
```
5. 查询index映射结构
```
GET localhost:9200/index/_mappings

resp:
{
    "index": {              # 索引名
        "mappings": {
            "properties": {
                "name": {    #属性名
                    "type": "text", # 属性类型
                    "fields": {
                        "keyword": {
                            "type": "keyword",
                            "ignore_above": 256
                        }
                    }
                }
            }
        }
    }
}
```

6. 批量插入(数据最后必须留一个空行)
```
POST localhost:9200/index/_bulk
{"index":{"_id":"1"}}
{"name":"sss"}
{"index":{"_id":"2"}}
{"name":"ss2"}

```
