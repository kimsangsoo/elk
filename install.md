# ELK

## Install
* brew install elastic/tap/elasticsearch-full
* brew install elastic/tap/logstash-full 
* brew install elastic/tap/kibana-full

## Start
* brew services start elastic/tap/elasticsearch-full
* brew services start elastic/tap/logstash-full
* brew services start elastic/tap/kibana-full

## 테이블 관계
|Elastic Search|Relational DB|
|------|---|
|Index|Database|
|Type|Table|
|Document|Row|
|Field|Column|
|Mapping|Schema|


## 구문 관계
|Elastic Search|Relational DB|
|------|---|
|GET|Select|
|PUT|Update|
|POST|Insert|
|DELETE|Delete|

## API
|동작|API|
|------|---|
|인덱스 생성|curl -XPUT http://localhost:9200/classes
|인덱스 조회|curl -XGET http://localhost:9200/classes/?pretty
|다큐먼트 추가|curl -XPOST http://localhost:9200/classes/class/1/ -d '{"title" : "Algorithm", "professor" : "John"}' -H 'Content-Type: application/json'
|다큐먼트 조회|curl  -XGET http://localhost:9200/classes/class/1?pretty
|다큐먼트 업데이트|curl -XPOST http://localhost:9200/classes/class/1/_update?pretty -d '{"doc" : {"unit" : 1}}' -H 'Content-Type: application/json'
|파일에 다큐먼트가 있는 경우|curl -XPOST http://localhost:9200/classes/class/1 -d @onceclass.json -H 'Content-Type: application/json'
|다큐먼트 업데이트|curl -XPOST http://localhost:9200/classes/class/1/_update -d '{"script":"ctx._source.unit +=5"}' -H 'Content-Type: application/json'
|Bulk 입력|curl -XPOST http://localhost:9200/_bulk?pretty --data-binary @classes.json -H 'Content-Type: application/json'
|다큐먼트 삭제|curl -XDELETE http://localhost:9200/classes
|인덱스 매핑|curl -XPUT http://localhost:9200/classes/class/_mapping?include_type_name=true -d @classesRating_mapping.json -H 'Content-Type: application/json'
|ch03 다큐먼트 삽입 (simple_basketball.json)|curl -XPOST 'http://localhost:9200/_bulk?pretty' --data-binary @simple_basketball.json -H 'Content-Type: application/json'
|ch03 다큐먼트 조회 (simple_basketball.json)|curl -XGET http://localhost:9200/basketball/record/_search?pretty
|ch03 다큐먼트 조회 - query (simple_basketball.json)|curl -XGET 'http://localhost:9200/basketball/record/_search?q=points:30&pretty'
|ch03 다큐먼트 조회 - requestBody (simple_basketball.json)|curl -XGET http://localhost:9200/basketball/record/_search?pretty -H 'Content-Type: application/json' -d '{"query" : {"term" : {"points":30}}}'
|Aggregation(평균) (ch03 : avg_points_aggs.json)|curl -XGET localhost:9200/_search?pretty --data-binary @avg_points_aggs.json -H 'Content-Type: application/json'
|Aggregation(최고값) (ch03 : max_points_aggs.json)|curl -XGET localhost:9200/_search?pretty --data-binary @max_points_aggs.json -H 'Content-Type: application/json'
|Aggregation(최소값) (ch03 : min_points_aggs.json)|curl -XGET localhost:9200/_search?pretty --data-binary @min_points_aggs.json -H 'Content-Type: application/json'
|Aggregation(합계) (ch03 : sum_points_aggs.json)|curl -XGET localhost:9200/_search?pretty --data-binary @sum_points_aggs.json -H 'Content-Type: application/json'
|Aggregation(전부) (ch03 : stats_points_aggs.json)|curl -XGET localhost:9200/_search?pretty --data-binary @stats_points_aggs.json -H 'Content-Type: application/json'
|ch04 - 인덱스 생성|curl -XPUT localhost:9200/basketball
|ch04 - mapping 추가|curl -H 'Content-type: application/json' -XPUT 'localhost:9200/basketball/record/_mapping?include_type_name=true&pretty' -d @basketball_mapping.json
|ch04 - 다큐먼트 추가|curl -XPOST 'http://localhost:9200/_bulk?pretty' --data-binary @twoteam_basketball.json -H 'Content-Type: application/json'
|ch04 - TERM AGGS(GROUP BY TEAM)|curl -XGET localhost:9200/_search?pretty --data-binary @terms_aggs.json -H 'Content-Type: application/json'
|ch04 - AGGS(STATS GROUP BY TEAM)|curl -XGET localhost:9200/_search?pretty --data-binary @stats_by_team.json -H 'Content-Type: application/json'

## 참조
 * Document API 모음
 * Java High Level REST Client v6.8
 * https://www.elastic.co/guide/en/elasticsearch/client/java-rest/6.8/java-rest-high-supported-apis.html
 * https://joyhong.tistory.com/107?category=898109
* https://github.com/joyhong85/elasticsearch-client/blob/master/Elasticsearch-Client/src/main/java/com/tistory/joyhong/elasticsearch/client/api/DocumentApi.java

