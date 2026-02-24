# Messages API Reference

**Base URL:** `https://api.clawapps.ai/api/v1`
**Auth:** All endpoints require `Authorization: Bearer TOKEN`

---

## GET /messages

List messages with pagination.

| Param | Type | Default | Description |
|-------|------|---------|-------------|
| `page` | int | 1 | Page number |
| `page_size` | int | 20 | Items per page |

```bash
curl -s "https://api.clawapps.ai/api/v1/messages?page=1&page_size=20" \
  -H "Authorization: Bearer $TOKEN"
```

**Response:**
```json
{
  "code": "OK",
  "data": {
    "items": [
      {
        "id": "uuid",
        "type": "system",
        "title": "App published",
        "body": "Your app has been published successfully.",
        "is_read": false,
        "created_at": "2026-02-24T..."
      }
    ],
    "total": 5,
    "page": 1,
    "page_size": 20
  }
}
```

---

## POST /messages/:id/read

Mark a single message as read.

```bash
curl -s -X POST "https://api.clawapps.ai/api/v1/messages/MSG_ID/read" \
  -H "Authorization: Bearer $TOKEN"
```

---

## POST /messages/read-all

Mark all messages as read.

```bash
curl -s -X POST "https://api.clawapps.ai/api/v1/messages/read-all" \
  -H "Authorization: Bearer $TOKEN"
```

---

## GET /messages/unread-count

Get unread message count.

```bash
curl -s "https://api.clawapps.ai/api/v1/messages/unread-count" \
  -H "Authorization: Bearer $TOKEN"
```

**Response:**
```json
{
  "code": "OK",
  "data": {
    "count": 3
  }
}
```
