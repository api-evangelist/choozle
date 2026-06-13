# Choozle

Choozle is a self-service digital advertising platform providing REST APIs for managing programmatic campaigns, audience segments, creative assets, publisher deals, and performance reporting across Display, CTV, Video, Audio, Native, DOOH, Search, and Social channels.

## Resources

- **Website:** https://choozle.com/
- **Platform Overview:** https://choozle.com/the-platform/
- **Help Center:** https://help.choozle.com/
- **Reporting API Docs:** https://help.choozle.com/connecting-to-choozles-reporting-api
- **API Reference:** https://app.choozle.com/apidoc/
- **Blog:** https://choozle.com/blog/
- **Terms of Service:** https://choozle.com/terms-of-service/

## APIs

### Choozle Reporting API

REST API for accessing campaign performance data, account information, and advertising metrics.

- **Base URL:** `https://app.choozle.com/api`
- **Authentication:** HMAC-SHA256 token (email + timestamp + API secret key)
- **Token Expiry:** 2 hours

#### Key Endpoints

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/api/accounts` | GET | Retrieve account details |
| `/api/reports` | GET | Retrieve campaign performance metrics |

#### Report Query Parameters

- `account_id` — Target account identifier
- `date_start` — Report start date (YYYY-MM-DD)
- `date_end` — Report end date (YYYY-MM-DD)
- `ad_group_id` — (Optional) Filter by ad group

## Plans

See [plans/plans.md](plans/plans.md) for subscription plan details. Pricing starts at $99/month with a prepaid media balance model.

## Rate Limits

See [rate-limits/rate-limits.md](rate-limits/rate-limits.md). No explicit rate limits are publicly documented; tokens expire after 2 hours.

## FinOps

See [finops/finops.md](finops/finops.md) for financial operations guidance including spend monitoring via API and cost optimization strategies.
