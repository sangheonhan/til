# Elasticsearch 동기화 검색

ElasticSearch의 Index, Update, Delete, Bulk API는 비동기로 동작한다. 즉, 요청에 대한 응답을 받았다 하더라도 검색 결과에 아직 반영이 안 된 상태일 수 있다.

`refresh=wait_for`라는 쿼리 파라미터를 추가하여 검색 결과에 반영 후 응답하도록 한다.

[Elasticsearch-PHP](https://www.elastic.co/guide/en/elasticsearch/client/php-api/current/index.html)에서는 파라미터에 `'refresh' => 'wait_for'` 필드를 추가하면 된다.

```php
$params = [
    'index' => 'my_index',
    'type' => 'my_type',
    'id' => 'my_id',
    'refresh' => 'wait_for',
    'body' => [ 'testField' => 'abc']
];

$response = $client->index($params);
```

다만, [Delete By Query API](https://www.elastic.co/guide/en/elasticsearch/reference/current/docs-delete-by-query.html)는 `wait_for`를 지원하지 않기에, `'refresh' => true`를 추가한다.
