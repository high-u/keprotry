# note

## hasura

Postgre と GraphQL(hasura) の型
https://hasura.io/docs/1.0/graphql/core/api-reference/postgresql-types.html

## Table

post

|name|type|note|
|:--|:--|:--|
|id|big int (auto increment)||
|message|text||
|room_key|text||
|username|text||
|lane_name|text||
|received_at|timestamp||

## GraphQL

```graphql
mutation {
  insert_post(objects:[
    {
      message: "My Second Todo",
      room_key: "x",
      username: "h",
      lane_name: "l"
    }
  ]) {
    affected_rows
  }
}
```

```graphql
mutation {
  insert_post_one(object:
    {
      message: "My Second Todo",
      room_key: "x",
      username: "h",
      lane_name: "l"
    }
  ) {
    id
    message
    room_key
    username
    lane_name
  }
}
```

```graphql
mutation {
  delete_post_by_pk(
      id: 1
  ) {
    id
  }
}
```

```graphql
{
  post(order_by: {received_at: asc}, where: {room_key: {_eq: "xxx"}}) {
    id
    username
    message
    received_at
    lane_name
  }
}
```

Error Response

```json
{
  "data": {
    "errors": [
      {
        "extensions": {
          "path": "$.query",
          "code": "validation-failed"
        },
        "message": "not a valid graphql query"
      }
    ]
  },
  "status": 200,
  "statusText": "OK",
  "headers": {
    "content-type": "application/json; charset=utf-8"
  },
  "config": {
    "url": "http://localhost:8080/v1/graphql",
    "method": "post",
    "data": "{\"query\":\"\\n          insert_post(objects:[\\n            {\\n              message: \\\"abc\\\",\\n              room_key: \\\"xxxxxx\\\",\\n              username: \\\"hoge\\\",\\n              lane_name: \\\"keep\\\",\\n              received_at: 1607231934800\\n            }\\n          ])\\n          \"}",
    "headers": {
      "Accept": "application/json, text/plain, */*",
      "Content-Type": "application/json;charset=utf-8"
    },
    "transformRequest": [
      null
    ],
    "transformResponse": [
      null
    ],
    "timeout": 0,
    "xsrfCookieName": "XSRF-TOKEN",
    "xsrfHeaderName": "X-XSRF-TOKEN",
    "maxContentLength": -1,
    "maxBodyLength": -1
  },
  "request": {}
}
```

subscription

```graphql
subscription {
  post (order_by: {received_at:desc}, limit: 1) {
    id
    username
    message
    received_at
    lane_name
  }
}
```


## 参考

https://github.com/zino-app/graphql-flutter/blob/dead29ecad247377289b3e23a50d2c698f0a21f5/packages/graphql/test/socket_client_test.dart#L54

chrome 拡張
https://chrome.google.com/webstore/detail/alpinejs-devtools/fopaemeedckajflibkpifppcankfmbhk/related?hl=ja


websocket

```json
{"type":"connection_init","payload":{"authorization":{"headers":"Bearer 8itDnC0s7Lt1-vej-bn6DGzvhcQ"}}}
```

```json
{"type":"start","id":"01020304-0506-4708-890a-0b0c0d0e0f10","payload":{"operationName":null,"query":"subscription {\n  \n}","variables":{}}}
```
