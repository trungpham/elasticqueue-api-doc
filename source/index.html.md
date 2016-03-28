---
title: ElasticQueue API Reference

language_tabs:
  - http

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

# Authentication


# Messages

## Enqueue message

```http
POST /v1/queues/queue-name/messages HTTP/1.1
Accept: application/vnd.api+json
Content-Type: application/vnd.api+json
Authorization: xxxxxxxxxxxxxxx
{
  "data": {
    "type": "message",
    "attributes": {
      "body": "body-of-message-1",
      "wait-until": 1459121798238
    }
  }
}
```

> If successful, you'll receive this response: 

```http
HTTP/1.1 204 Accepted
Content-Type: application/vnd.api+json
Authorization: xxxxxxxxxxxxxxx

{
  "data": {
    "type": "message",
    "id": "72301093732",
    "links": {
      "self": "https://www.elasticqueue.com/v1/api/queues/my-queue/messages/72301093732"
    }
  }
}
```

Enqueue a single message to run right away or some time in the future

### Parameters

Parameter | Type | Required | Default | Description
--------- | ---------- | -------- | ------- | -----------
data/type | String | true | | If set to true, the result will also include cats.
data/attributes/body | String | true | | The body of the message. This can be anything.
data/attributes/wait-until | Integer | false | 0 | When to send out the message. By default this message will run as soon as possible. Epoch time in seconds


## Bulk enqueue messages

```http
POST /v1/queues/queue-name/messages/_bulk HTTP/1.1
Accept: application/vnd.api+json
Content-Type: application/vnd.api+json

{
  "data": [
    {
      "type": "message",
      "attributes": {
        "body": "body-of-message-1",
        "wait-until": 1459121798238
      }
    },
    {
      "type": "message",
      "attributes": {
        "body": "body-of-message-2",
        "wait-until": 1459121798238
      }
    }
  ]
}
```

> If successful, you'll receive this response:

```http
HTTP/1.1 204 Accepted
Content-Type: application/vnd.api+json

{
  "data": [
    {
      "type": "message",
      "id": "72301093732",
      "links": {
        "self": "https://www.elasticqueue.com/v1/api/queues/my-queue/messages/72301093732"
      },
      "type": "message",
      "id": "72301093737",
      "links": {
        "self": "https://www.elasticqueue.com/v1/api/queues/my-queue/messages/72301093737"
      }
    }
  ]
}
```
Use this bulk api to enqueue multiple message in a single request. All or nothing bulk operation. If one message has an error, then all other valid messages will fail as well.
### Parameters

Parameter | Type | Required | Default | Description
--------- | --------- | -------- | ------- | -----------
data[]/type | String | true | | If set to true, the result will also include cats.
data[]/attributes/body | String | true | | The body of the message. This can be anything.
data[]/attributes/wait-until | Integer | false | 0 | When to send out the message. By default this message will run as soon as possible. Epoch time in seconds

