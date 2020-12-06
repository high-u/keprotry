# note

## Table

post

|name|type|note|
|:--|:--|:--|
|id|big int (auto increment)||
|message|text||
|room_key|text||
|username|text||
|received_at|big int||

## GraphQL

```graphql
mutation {
  insert_post(objects:[
    {
      message: "My Second Todo",
      room_key: "x",
      username: "h",
      received_at: 1
    }
  ]) {
    affected_rows
  }
}
```
