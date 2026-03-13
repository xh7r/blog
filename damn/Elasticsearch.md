# 运行端口

elasticsearch: 

- 9200: 给外部用户(客户端)调用
- 9300: 给ES集群内部通讯的(外部调用不了)

kinaba: 5610

# syntax

add:

```
POST xhr_test/_doc
{
  "title": "test",
  "desc": "test's description"
}
```



delete:

```
Delete _data_stream/logs-my_app-default
```

update: 

```
POST xhr_test/_doc/6gOfPYwBAb1KBv7za7Tz
{
  "title": "test2",
  "desc": "test's description"
}
```

search:

```
GET xhr_test/_doc/6gOfPYwBAb1KBv7za7Tz
```

analyser 分词器测试

```
POST _analyze
{
  "analyzer": "ik_smart",
  "text": "我是大傻逼!"
}
```



# Ik 分词器(ES 插件)

注意版本与ES一致

https://github.com/medcl/elasticsearch-analysis-ik

让IK按自己想法分词: 自定义词典

分词模式:

- ik_smart
- ik_max_word

# Java操作ES

1. ES官方的API

2. Spring Data ElasticSearch

   Sprint Data 系列: spring提供的操作数据库的框架

