# Task5 — GraphQL для client-info

- Цель: сократить количество запросов к `client-info` за счёт выборочного получения нужных полей и связанных сущностей.
- Результат: схема GraphQL в `Task5/schema.graphql`.

## Соответствие REST → GraphQL
- GET /clients/{id} → `client(id: ID!): Client`
- GET /clients/{id}/documents → `clientDocuments(id: ID!): [Document!]!`
- GET /clients/{id}/relatives → `clientRelatives(id: ID!): [Relative!]!`

Также через расширенную модель можно получать вложенные данные за 1 запрос:
- `client(id).documents`
- `client(id).relatives`

## Примеры запросов

Запрос клиента с базовыми полями:
```graphql
query GetClient($id: ID!) {
  client(id: $id) {
    id
    name
    age
  }
}
```

Клиент с документами и родственниками одним запросом:
```graphql
query GetClientFull($id: ID!) {
  client(id: $id) {
    id
    name
    documents { id type number expiryDate }
    relatives { id relationType name }
  }
}
```

Только документы (эквивалент отдельного REST ресурса):
```graphql
query GetClientDocuments($id: ID!) {
  clientDocuments(id: $id) { id type number }
}
```
