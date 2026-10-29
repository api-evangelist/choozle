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
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Choozle is a Denver-based self-service demand-side platform (DSP) for programmatic digital advertising across Display, Connected TV, Video, Audio, Native, DOOH, Search and Social, with buying routed through The Trade Desk and Amazon DSP. Its public developer surface is a single read-only product, the Choozle Outbound Reporting API: three operations that exchange an HMAC-SHA256 signature for a two-hour token, return the account/campaign/ad group tree, and return daily per-ad-group performance rows. Campaign, audience, creative and deal management are performed in the web application only — no public API writes to them. Keys are issued by support ticket rather than self-service.

**Areas:** Digital Advertising · Programmatic Advertising · DSP · Advertising Reporting · Campaign Reporting · Display Advertising · Connected TV · CTV · Video Advertising · Native Advertising · Digital Out Of Home · Reporting

## Choozle on APIs.io

Everything profiled for Choozle is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/choozle/](https://apis.io/providers/choozle/)** — or go straight to one of the APIs or properties below.

### APIs (2)

- [Choozle Authorization API](https://apis.io/apis/choozle/choozle-authorization-api/) — The token exchange. POST an API profile email, an ISO 8601 timestamp within five minutes of server time, and an HMAC-SHA256 hex signature to receive a token…
- [Choozle Reporting API](https://apis.io/apis/choozle/choozle-reporting-api/) — Account structure and campaign performance reporting.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [choozle](https://apis.io/servers/choozle/choozle/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Choozle Agentic Access](https://apis.io/agentic-access/choozle/choozle-agentic-access/)

#### JSON Schema (2)

The data models the API reads and writes.

- [AuthorizationRequest](https://apis.io/schemas/choozle/authorization-request/)
- [ReportRow](https://apis.io/schemas/choozle/report-row/)

#### Examples (3)

Example requests and responses.

- [Get Reports](https://apis.io/examples/choozle/get-reports/)
- [Get Token](https://apis.io/examples/choozle/get-token/)
- [List Accounts](https://apis.io/examples/choozle/list-accounts/)

#### Collections (3)

Postman and Open Collection request collections.

- [Choozle Reporting Accounts API](https://apis.io/collections/choozle/open-choozle-accounts-api/)
- [Choozle Reporting Authorization API](https://apis.io/collections/choozle/open-choozle-authorization-api/)
- [Choozle Reporting Reports API](https://apis.io/collections/choozle/open-choozle-reports-api/)

#### Overlays (3)

OpenAPI overlays, including conversational phrasing for each operation.

- [Choozle Accounts Api Overlay](https://apis.io/overlays/choozle/choozle-accounts-api-overlay/)
- [Choozle Authorization Api Overlay](https://apis.io/overlays/choozle/choozle-authorization-api-overlay/)
- [Choozle Reports Api Overlay](https://apis.io/overlays/choozle/choozle-reports-api-overlay/)

#### Governance rules (1)

Spectral rulesets for the provider's contracts.

- [Choozle — jsonschema rules](https://apis.io/rules/choozle/choozle-jsonschema-spectral-rules/)

#### Security (2)

Authentication, trust centre, and vulnerability disclosure.

- [Choozle Authentication](https://apis.io/security/choozle/choozle-authentication/)
- [Choozle Domain Security](https://apis.io/security/choozle/choozle-domain-security/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Choozle Plans Pricing](https://apis.io/plans/choozle/choozle-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Choozle Rate Limits](https://apis.io/rate-limits/choozle/choozle-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://choozle.com/)
- [Documentation](https://help.choozle.com/)
- [Getting started](https://help.choozle.com/connecting-to-choozles-reporting-api)
- [API reference](https://app.choozle.com/apidoc/)
- [Pricing](https://choozle.com/managed-self-service/)
- [Support](https://help.choozle.com/)
- [Blog](https://choozle.com/blog/)
- [Compliance](https://choozle.com/data-processing-agreement/)
- [Terms of service](https://choozle.com/terms-of-service/)
- [Privacy policy](https://choozle.com/privacy-policy/)
- [GitHub](https://github.com/choozle)

## API Evangelist rating

**Kin Score 41.9** — developing · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 71.4 |
| Contract quality | 60.0 |
| Contract governance | 41.7 |
| Operational transparency | 2.6 |
| Developer ergonomics | 47.0 |
| Access clarity | 27.6 |

**Agent readiness 31.8** — agent-ready

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | — |
| MCP Server | — |
| Auth Clarity | bearer (partial credit) |
| Idempotency | — |
| Error Semantics | verified |
| OpenAPI Examples | verified |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | — |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | — |
| Operation Distinctiveness | distinct |

**Regulatory alignment 16.7** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/choozle/](https://apis.io/providers/choozle/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Choozle: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/choozle/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
