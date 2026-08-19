---
name: Pull Choozle campaign performance
description: >-
  Walk a Choozle account's campaign and ad group structure, then pull daily
  performance rows for a date range and assemble them into a complete time
  series. Covers the filter exclusivity rules and the sparse-row trap.
api: openapi/choozle-reports-api-openapi.yml
operations:
  - getAuthorizationToken
  - listAccounts
  - getReports
generated: '2026-08-13'
method: generated
source: https://app.choozle.com/apidoc/api_data.json
---

# Pull Choozle campaign performance

The Choozle Reporting API is read-only and has exactly three operations. This is
the main flow: find the account, then pull its numbers.

## 1. Get a token

Run the **Authenticate to the Choozle Reporting API** skill
(`skills/choozle-authenticate.md`) to get a `token` valid for two hours, and send
it as a `token` request header on both calls below.

## 2. `listAccounts` — discover the structure

`GET https://app.choozle.com/api/accounts`

Returns the whole tree in one document — there is no pagination and no way to
fetch a single account by id:

```json
{ "accounts": [ { "id": "1", "name": "Acme", "account_state": "A",
  "campaigns": [ { "id": "15", "name": "June2014", "start_date": "2014-06-20",
    "end_date": "2014-07-31", "archived": "N",
    "ad_groups": [ { "id": "154", "name": "Ad Category", "status": "E" } ] } ] } ] }
```

Use this to resolve a human-supplied account or campaign **name** to the numeric
id the reports call needs. Do not ask the user for an `account_id` you could
have looked up here.

Read the enums rather than guessing at them:

- `account_state` — `A` Active, `I` Inactive (error with account), `C`
  Cancelled, `P` Paused.
- `archived` — `Y` or `N` on a campaign.
- ad group `status` — `I` Incomplete, `U` Unapproved, `E` Enabled, `D` Disabled,
  `S` Scheduled, `W` Error, `O` Over Ad Group's Budget, `B` Over Ad Group's
  Daily Budget, `C` Campaign Over Budget, `A` Campaign Over Daily Budget.

The last four are budget-exhaustion states, and `C` and `A` describe the parent
**campaign**, not the ad group. If a user asks why an ad group stopped
delivering, this field usually answers it — check it before pulling reports.

Ids come back as JSON strings of digits. Keep them as strings; do not round-trip
them through an integer type.

## 3. `getReports` — pull the numbers

`GET https://app.choozle.com/api/reports`

| Parameter | Required | Notes |
|---|---|---|
| `account_id` | yes | The only required filter |
| `date_start` | no | ISO date, inclusive |
| `date_end` | no | ISO date, inclusive |
| `campaign_id` | no | Cannot be combined with `campaign_status` |
| `campaign_status` | no | One of `all`, `active`, `inactive`, `archived`. Cannot be combined with `campaign_id` |
| `ad_group_id` | no | One or more ids, comma separated. Cannot be combined with `campaign_id` or `campaign_status` |

**The three narrowing filters are mutually exclusive.** Pick exactly one of
`campaign_id`, `campaign_status`, `ad_group_id` per call. Choozle documents no
error for violating this, so a bad combination may return something plausible
rather than failing — validate before you send, not after.

Open-ended ranges work: `date_start` alone returns everything on and after that
date; `date_end` alone returns everything on and before it. Always send both
unless the user explicitly asked for an open range — an unbounded pull on a
large account returns an unbounded array.

Example, quoted from the provider's knowledge base:

```
GET https://app.choozle.com/api/reports?account_id=85&date_start=2017-12-11&date_end=2017-12-11&ad_group_id=42506,42507,42508,41194
```

## 4. Read the rows correctly

One row per **active ad group per day**:

```json
[ { "date": "2014-12-02", "account_id": "1", "account_name": "Acme",
    "campaign_id": "15", "campaign_name": "Campaign 1",
    "ad_group_id": "154", "ad_group_name": "Ad Group 1",
    "advertiser_cost": 0, "impressions_bid_on": 0, "impressions_won": 3,
    "win": 0, "clicks": 0, "conversions": 0,
    "cpm": 0, "cpc": 0, "ctr": 0, "cpa": 0 } ]
```

Two things to get right:

- **Rows are sparse.** "If no reports were recorded for an ad group on a
  particular day, that report is omitted." A missing row means no activity, not
  a gap in the data. If you are building a daily series or charting a trend,
  fill missing days with zeros yourself — otherwise a paused week silently
  compresses and every rate you compute is wrong.
- **Spend is `advertiser_cost`.** There is no `spend` field. Volume is split
  into `impressions_bid_on` (auction attempts) and `impressions_won` (delivered);
  there is no single `impressions` field. Report the names the API actually
  returns.

To roll up to campaign or account level, aggregate the ad group rows yourself —
the API returns no pre-aggregated totals. Sum the counts and costs, then
recompute `ctr`, `cpc`, `cpm` and `cpa` from the summed values. Never average the
per-row rates; that weights a 10-impression day the same as a 10-million-
impression day.

## 5. Long pulls

There are no rate limits published and no rate-limit headers returned, so you
have no runtime budget signal. Be conservative:

- Cache the token for its full two hours; re-authenticate when it expires
  mid-job rather than per call.
- Chunk wide date ranges into bounded windows — the response is unpaginated, so
  a year across a large account is a single enormous array.
- There is no `Retry-After` and no documented 429. Treat any unexpected status
  as a stop-and-report, and back off exponentially before retrying.

## Errors

Every documented failure is a 401 with `{"error": "..."}`. If you get 404 with an
HTML body you have hit an unrouted path — check the endpoint spelling, and note
the auth endpoint is `/api/auth`, not `/api/authorization`.

See `errors/choozle-problem-types.yml`, `conventions/choozle-conventions.yml` and
`data-model/choozle-data-model.yml`.
