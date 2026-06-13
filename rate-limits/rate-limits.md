# Choozle API Rate Limits

Choozle does not publish explicit rate limit thresholds in their public documentation. The following information is based on available knowledge base and integration partner documentation.

## Reporting API

- **Base URL:** `https://app.choozle.com/api/`
- **API Version:** v2
- **Rate Limit Details:** Not publicly documented
- **Token Expiration:** Access tokens expire after 2 hours and must be refreshed

## Authentication Token Limits

- Tokens are generated per API profile (email + timestamp + HMAC-SHA256 secret)
- Each token is valid for a 2-hour window
- A new token must be generated after expiration

## Integration Partner Observations

Third-party integration partners (e.g., Improvado) report:
- **Sync Frequency:** 15-minute refresh cycles supported
- **SLA Uptime:** 99.9% uptime reported by integration partners
- **Sync Type:** Incremental, hourly sync available
- **Data Volume:** 200+ fields accessible across campaign, ad group, creative, and audience levels

## Best Practices

- Cache tokens for their full 2-hour validity window to reduce authentication overhead
- Implement exponential backoff on HTTP 429 (Too Many Requests) responses
- Use `account_id`, `date_start`, and `date_end` filters to scope report queries and reduce response size
- For bulk data extraction, use incremental syncs rather than full historical pulls

## Contact

For enterprise-level rate limit increases or dedicated API access, contact Choozle support via the Help Center at https://help.choozle.com/
