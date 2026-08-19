---
name: Authenticate to the Choozle Reporting API
description: >-
  Exchange a Choozle API profile email and private key for a two-hour access
  token using the HMAC-SHA256 handshake, and attach it correctly to reporting
  calls. Do this first — every other Choozle skill depends on it.
api: openapi/choozle-authorization-api-openapi.yml
operations:
  - getAuthorizationToken
generated: '2026-08-13'
method: generated
source: https://help.choozle.com/connecting-to-choozles-reporting-api
---

# Authenticate to the Choozle Reporting API

Choozle does not accept a static API key. You sign a request with a private key,
get back an opaque token, and use that token for two hours.

## Before you start

You need two things, and neither is self-service:

1. An **API profile** — an ORG admin or advertiser admin creates one inside the
   Choozle application. An "API Only" profile has full read access to account
   data through the API but cannot log into the website, which is the correct
   choice for an agent.
2. The **API secret key** — the system generates it when the profile is created,
   but it is only released by submitting a ticket through the Choozle Customer
   Portal. There is no key page and no key-management endpoint. If you do not
   have the key, stop and tell the user to raise that ticket; there is no way to
   proceed and no sandbox to fall back on.

## Steps

### 1. Build the timestamp

Take the current time as an **ISO 8601 datetime with an offset**, for example
`2015-05-04T11:34:02-06:00`.

It must be within **five minutes** of Choozle's server time. If the handshake
fails and everything else looks right, check the caller's clock before checking
the signature.

### 2. Compute the signature

Concatenate the `email` and `timestamp` values exactly as you will submit them,
then HMAC-SHA256 that string keyed with the API private key.

Emit the digest as **lowercase hexadecimal**. Uppercase hex fails. Base64 fails.
This is the provider's own first-listed troubleshooting issue, so check it first
when the handshake returns 401.

### 3. Call `getAuthorizationToken`

`POST https://app.choozle.com/api/auth`

- `Content-Type: application/x-www-form-urlencoded`
- Put `email`, `timestamp` and `signature` in the **request body**. Not in
  headers — Choozle documents header placement as a common failure.

A success returns:

```json
{ "token": "<opaque token>" }
```

### 4. Attach the token to every reporting call

Send it as a **`token` request header**:

```
token: <opaque token>
```

It is a custom header, not `Authorization: Bearer`. If you are using a generated
client or a standard bearer-auth helper, override it explicitly — otherwise you
will get `Unauthorized - No Token Found in request` while believing you sent a
credential.

### 5. Cache and refresh

The token is valid **two hours from creation**. There is no refresh token.

Cache it for its full life rather than re-authenticating per call, and set your
own expiry a few minutes early so a long report pull does not die mid-run. When
it expires, run this skill again from step 1.

## Errors

All of these come back as HTTP 401 with a bare `{"error": "..."}` body.

| Body | Cause | Fix |
|---|---|---|
| `Request incomplete` | Missing or unverifiable `email` / `timestamp` / `signature` | Check hex casing, then body-vs-header placement, then clock skew |
| `Unauthorized - No Token Found in request` | No `token` header on a reporting call | Send the custom `token` header |
| `Unauthorized - Token is expired` | Token older than two hours | Re-run the handshake |
| `Unauthorized - Request token is expired.` | Same condition, different wording from `/reports` | Re-run the handshake |

Note the last two: the accounts and reports endpoints word the identical
condition differently, including the trailing period. Match on the HTTP status
and the substring `expired`, not on the full string.

## Do not

- Do not send the private key on a reporting request. It only ever feeds the
  HMAC.
- Do not log the token or the signature.
- Do not retry a 401 with the same signature — nothing about it will change.
  Recompute the timestamp and signature first.

See `authentication/choozle-authentication.yml` for the full auth profile and
`conventions/choozle-conventions.yml` for the cross-cutting rules.
