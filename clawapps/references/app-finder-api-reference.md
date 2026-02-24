# App Finder API Reference

**Base URL:** `https://api.clawapps.ai/api/v1`
**Auth:** All endpoints require `Authorization: Bearer TOKEN`

Discover, search, and use apps on the ClawApps marketplace.

---

## GET /store/apps

Browse published apps in the store with pagination and filtering.

| Param | Type | Default | Description |
|-------|------|---------|-------------|
| `page` | int | 1 | Page number |
| `page_size` | int | 20 | Items per page |
| `category` | string | — | Filter by category (e.g. productivity, creative, education) |
| `sort` | string | popular | Sort by: popular, newest, top_rated |

```bash
curl -s "https://api.clawapps.ai/api/v1/store/apps?page=1&page_size=20&sort=popular" \
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
        "name": "ChatBot Pro",
        "description": "AI-powered chatbot builder",
        "category": "productivity",
        "author": "developer_name",
        "rating": 4.8,
        "downloads": 1200,
        "is_free": true
      }
    ],
    "total": 150,
    "page": 1,
    "page_size": 20
  }
}
```

---

## GET /store/apps/search

Search apps by keywords.

| Param | Type | Default | Description |
|-------|------|---------|-------------|
| `keywords` | string | — | Comma-separated search keywords (required) |
| `page` | int | 1 | Page number |
| `page_size` | int | 20 | Items per page |
| `category` | string | — | Filter by category |

```bash
curl -s "https://api.clawapps.ai/api/v1/store/apps/search?keywords=chat,ai&category=productivity" \
  -H "Authorization: Bearer $TOKEN"
```

---

## GET /store/apps/:id

Get detailed info of a published app.

```bash
curl -s "https://api.clawapps.ai/api/v1/store/apps/APP_ID" \
  -H "Authorization: Bearer $TOKEN"
```

**Response:**
```json
{
  "code": "OK",
  "data": {
    "id": "uuid",
    "name": "ChatBot Pro",
    "description": "Full description...",
    "category": "productivity",
    "author": "developer_name",
    "version": "1.2.0",
    "rating": 4.8,
    "reviews_count": 56,
    "downloads": 1200,
    "is_free": true,
    "price_credits": 0,
    "screenshots": ["url1", "url2"],
    "created_at": "...",
    "updated_at": "..."
  }
}
```

---

## GET /store/apps/categories

List all available app categories.

```bash
curl -s "https://api.clawapps.ai/api/v1/store/apps/categories" \
  -H "Authorization: Bearer $TOKEN"
```

**Response:**
```json
{
  "code": "OK",
  "data": [
    { "slug": "productivity", "name": "Productivity", "count": 45 },
    { "slug": "creative", "name": "Creative", "count": 32 },
    { "slug": "education", "name": "Education", "count": 18 }
  ]
}
```

---

## GET /store/apps/featured

Get featured and recommended apps.

```bash
curl -s "https://api.clawapps.ai/api/v1/store/apps/featured" \
  -H "Authorization: Bearer $TOKEN"
```

---

## POST /store/apps/:id/launch

Launch (use) an app. Returns the app launch URL or session.

```bash
curl -s -X POST "https://api.clawapps.ai/api/v1/store/apps/APP_ID/launch" \
  -H "Authorization: Bearer $TOKEN"
```

**Response:**
```json
{
  "code": "OK",
  "data": {
    "session_id": "uuid",
    "launch_url": "https://clawapps.ai/app/APP_ID/session/SESSION_ID",
    "expires_at": "2026-02-24T..."
  }
}
```

---

## POST /store/apps/:id/rate

Rate an app (1-5 stars) with optional review.

```bash
curl -s -X POST "https://api.clawapps.ai/api/v1/store/apps/APP_ID/rate" \
  -H "Authorization: Bearer $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"rating": 5, "review": "Excellent app!"}'
```

| Field | Required | Type | Description |
|-------|----------|------|-------------|
| `rating` | Yes | int | 1-5 stars |
| `review` | No | string | Optional review text |
