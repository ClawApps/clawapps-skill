# My App Manager API Reference

**Base URL:** `https://api.clawapps.ai/api/v1`
**Auth:** All endpoints require `Authorization: Bearer TOKEN`

Manage your own apps — create, list, update, delete, upload, download, publish, and unpublish.

---

## GET /apps

List your apps with pagination.

| Param | Type | Default | Description |
|-------|------|---------|-------------|
| `page` | int | 1 | Page number |
| `page_size` | int | 20 | Items per page |
| `status` | string | — | Filter: draft, published, archived |

```bash
curl -s "https://api.clawapps.ai/api/v1/apps?page=1&page_size=20" \
  -H "Authorization: Bearer $TOKEN"
```

**Response:**
```json
{
  "code": "OK",
  "data": {
    "items": [
      { "id": "uuid", "name": "My App", "status": "draft", "created_at": "..." }
    ],
    "total": 42,
    "page": 1,
    "page_size": 20
  }
}
```

---

## GET /apps/:id

Get app details.

```bash
curl -s "https://api.clawapps.ai/api/v1/apps/APP_ID" \
  -H "Authorization: Bearer $TOKEN"
```

---

## POST /apps

Create a new app.

```bash
curl -s -X POST https://api.clawapps.ai/api/v1/apps \
  -H "Authorization: Bearer $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "name": "My App",
    "description": "App description",
    "category": "productivity",
    "is_public": true
  }'
```

| Field | Required | Type | Description |
|-------|----------|------|-------------|
| `name` | Yes | string | App name |
| `description` | Yes | string | App description |
| `category` | No | string | Category |
| `is_public` | No | bool | Public visibility |

---

## PUT /apps/:id

Update app metadata (partial update).

```bash
curl -s -X PUT "https://api.clawapps.ai/api/v1/apps/APP_ID" \
  -H "Authorization: Bearer $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"name": "New Name", "description": "Updated"}'
```

---

## DELETE /apps/:id

Delete an app. This is destructive and irreversible.

```bash
curl -s -X DELETE "https://api.clawapps.ai/api/v1/apps/APP_ID" \
  -H "Authorization: Bearer $TOKEN"
```

---

## POST /apps/:id/upload

Upload a zip package (multipart/form-data).

```bash
curl -s -X POST "https://api.clawapps.ai/api/v1/apps/APP_ID/upload" \
  -H "Authorization: Bearer $TOKEN" \
  -F "file=@package.zip"
```

**Response:**
```json
{
  "code": "OK",
  "data": {
    "version": "1.0.1",
    "size": 102400,
    "uploaded_at": "2026-02-12T..."
  }
}
```

---

## GET /apps/:id/download

Download app package.

```bash
curl -s -o app.zip "https://api.clawapps.ai/api/v1/apps/APP_ID/download" \
  -H "Authorization: Bearer $TOKEN"
```

---

## POST /apps/:id/publish

Publish an app.

```bash
curl -s -X POST "https://api.clawapps.ai/api/v1/apps/APP_ID/publish" \
  -H "Authorization: Bearer $TOKEN"
```

---

## POST /apps/:id/unpublish

Unpublish an app.

```bash
curl -s -X POST "https://api.clawapps.ai/api/v1/apps/APP_ID/unpublish" \
  -H "Authorization: Bearer $TOKEN"
```
