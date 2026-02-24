# Auth & Account API Reference

**Base URL:** `https://api.clawapps.ai/api/v1`

---

## Login

Use `@clawapps/cli` to authenticate. Token is stored at `~/.clawapps/credentials.json`.

```bash
claw login
```

## Read Token

```bash
TOKEN=$(cat ~/.clawapps/credentials.json | jq -r .access_token)
```

## GET /auth/me

Verify the current user.

```bash
curl -s https://api.clawapps.ai/api/v1/auth/me \
  -H "Authorization: Bearer $TOKEN"
```

**Response:**
```json
{
  "code": "OK",
  "data": {
    "id": "uuid",
    "name": "Username",
    "email": "user@gmail.com",
    "provider": "google"
  }
}
```

## POST /auth/refresh

Refresh an expired access token.

```bash
REFRESH=$(cat ~/.clawapps/credentials.json | jq -r .refresh_token)
curl -s -X POST https://api.clawapps.ai/api/v1/auth/refresh \
  -H "Content-Type: application/json" \
  -d "{\"refresh_token\": \"$REFRESH\"}"
```

After a successful refresh, update `~/.clawapps/credentials.json` with the new tokens.

If refresh also fails (refresh token expired), instruct the user to re-login with `claw login`.

## POST /auth/logout

```bash
curl -s -X POST https://api.clawapps.ai/api/v1/auth/logout \
  -H "Authorization: Bearer $TOKEN" \
  -H "Content-Type: application/json" \
  -d "{\"refresh_token\": \"$REFRESH\"}"
```

Or via CLI:

```bash
claw logout
```

## Check Login Status

```bash
claw whoami
```

---

## Plans & Credits

ClawApps uses a credit-based system. Each account has a plan tier that determines available features and credit limits.

### Plan Tiers

| Tier | Price | Credits/month | Features |
|------|-------|---------------|----------|
| Free | $0 | 100 | Basic app publishing, community access |
| Pro | $9.99/mo | 1,000 | Priority publishing, advanced analytics, custom domains |
| Team | $29.99/mo | 5,000 | Team collaboration, API rate limit increase, priority support |
| Enterprise | Custom | Custom | Dedicated support, SLA, custom integrations |

### Credit Usage

| Operation | Credits |
|-----------|---------|
| App publish | 10 |
| App upload (per 100MB) | 5 |
| Analytics export | 20 |
| Premium API calls | 1 per call |

### GET /account/credits

Check account balance.

```bash
curl -s https://api.clawapps.ai/api/v1/account/credits \
  -H "Authorization: Bearer $TOKEN"
```

### Handling Insufficient Credits (402 / INSUFFICIENT_CREDITS)

1. Check current balance with the credits endpoint above
2. Inform the user of remaining credits and the cost of the operation
3. Direct the user to purchase more credits: https://clawapps.ai/pricing

### Handling Plan Upgrade Required (403 / PLAN_UPGRADE_REQUIRED)

1. The requested feature is not available on the user's current plan
2. Inform the user which plan tier is required
3. Direct the user to upgrade: https://clawapps.ai/pricing
