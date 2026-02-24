# Analytics API Reference

**Base URL:** `https://api.clawapps.ai/api/v1`
**Auth:** All endpoints require `Authorization: Bearer TOKEN`

---

## GET /apps/:id/analytics/overview

App overview statistics for a given period.

| Param | Type | Default | Description |
|-------|------|---------|-------------|
| `period` | string | 7d | Time period: 1d, 7d, 30d, 90d |

```bash
curl -s "https://api.clawapps.ai/api/v1/apps/APP_ID/analytics/overview?period=7d" \
  -H "Authorization: Bearer $TOKEN"
```

**Response:**
```json
{
  "code": "OK",
  "data": {
    "total_views": 1234,
    "unique_users": 567,
    "avg_session_duration": 180,
    "period": "7d"
  }
}
```

---

## GET /apps/:id/analytics/views

Page view statistics over time.

| Param | Type | Default | Description |
|-------|------|---------|-------------|
| `period` | string | 7d | Time period: 1d, 7d, 30d, 90d |
| `granularity` | string | day | Grouping: hour, day, week |

```bash
curl -s "https://api.clawapps.ai/api/v1/apps/APP_ID/analytics/views?period=7d&granularity=day" \
  -H "Authorization: Bearer $TOKEN"
```

**Response:**
```json
{
  "code": "OK",
  "data": {
    "points": [
      { "date": "2026-02-18", "views": 150 },
      { "date": "2026-02-19", "views": 200 }
    ],
    "total": 1234
  }
}
```

---

## GET /apps/:id/analytics/users

Active user statistics over time.

| Param | Type | Default | Description |
|-------|------|---------|-------------|
| `period` | string | 7d | Time period: 1d, 7d, 30d, 90d |
| `granularity` | string | day | Grouping: hour, day, week |

```bash
curl -s "https://api.clawapps.ai/api/v1/apps/APP_ID/analytics/users?period=7d&granularity=day" \
  -H "Authorization: Bearer $TOKEN"
```

**Response:**
```json
{
  "code": "OK",
  "data": {
    "points": [
      { "date": "2026-02-18", "users": 80 },
      { "date": "2026-02-19", "users": 95 }
    ],
    "total": 567
  }
}
```
