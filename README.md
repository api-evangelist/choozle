# Choozle

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

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
