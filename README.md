# Justt

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

Justt is an AI-native chargeback management and dispute-representment platform for high-volume merchants. Its Dynamic Arguments engine assembles evidence-backed representment packages for card disputes across 30+ payment service providers (Stripe, Adyen, PayPal, Braintree, Checkout.com, Worldpay, Chase Paymentech, Nuvei and others), and it also handles pre-chargeback alerts from Ethoca, Verifi CDRN and RDR. Justt publishes a public developer portal at developers.justt.ai with three OpenAPI definitions — a REST API for chargebacks, transactions, evidence, files, merchants and integrations; a Pre-Chargeback Alerts API; and an OpenAPI 3.1 webhook-events specification covering eleven signed event types — plus an RFC 9727 /.well-known/api-catalog, an llms.txt documentation index, a sandbox environment, and a Vanta-hosted trust center.

**Areas:** Company · Payments · Chargebacks · Disputes · Fraud Prevention · Risk Management · Financial Services · E-Commerce · Artificial Intelligence · Webhook

## Justt on APIs.io

Everything profiled for Justt is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/justt/](https://apis.io/providers/justt/)** — or go straight to one of the APIs or properties below.

### APIs (9)

- [Justt Chargebacks API](https://apis.io/apis/justt/justt-chargebacks-api/) — The Chargebacks API from Justt — 4 operation(s) for chargebacks.
- [Justt Data Subjects API](https://apis.io/apis/justt/justt-data-subjects-api/) — The Data Subjects API from Justt — 1 operation(s) for data subjects.
- [Justt Evidence API](https://apis.io/apis/justt/justt-evidence-api/) — The Evidence API from Justt — 2 operation(s) for evidence.
- [Justt Files API](https://apis.io/apis/justt/justt-files-api/) — The Files API from Justt — 1 operation(s) for files.
- [Justt Integrations API](https://apis.io/apis/justt/justt-integrations-api/) — The Integrations API from Justt — 2 operation(s) for integrations.
- [Justt Merchants API](https://apis.io/apis/justt/justt-merchants-api/) — The Merchants API from Justt — 2 operation(s) for merchants.
- [Justt Pre-chargeback Alerts API](https://apis.io/apis/justt/justt-pre-chargeback-alerts-api/) — The Pre-chargeback Alerts API from Justt — 3 operation(s) for pre-chargeback alerts.
- [Justt Sandbox API](https://apis.io/apis/justt/justt-sandbox-api/) — The Sandbox API from Justt — 1 operation(s) for sandbox.
- [Justt Transactions API](https://apis.io/apis/justt/justt-transactions-api/) — The Transactions API from Justt — 1 operation(s) for transactions.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### Arazzo workflows (4)

Multi-step workflows that chain operations into a business task.

- [Work a Justt pre-chargeback alert to a reported outcome](https://apis.io/arazzos/justt/justt-alert-to-outcome/)
- [Drive a chargeback through its lifecycle in the Justt sandbox](https://apis.io/arazzos/justt/justt-sandbox-lifecycle/)
- [Submit evidence for a Justt chargeback](https://apis.io/arazzos/justt/justt-submit-evidence/)
- [Triage Justt chargebacks and set the representment decision](https://apis.io/arazzos/justt/justt-triage-and-decide/)

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [Justt Webhook Events](https://apis.io/asyncapis/justt/justt-webhook-events/)

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [justt-wordpress-mcp](https://apis.io/servers/justt/justt-wordpress-mcp/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Justt Agentic Access](https://apis.io/agentic-access/justt/justt-agentic-access/)

#### Overlays (3)

OpenAPI overlays, including conversational phrasing for each operation.

- [Justt Pre Chargeback Alerts Overlay](https://apis.io/overlays/justt/justt-pre-chargeback-alerts-overlay/)
- [Justt Rest Api Overlay](https://apis.io/overlays/justt/justt-rest-api-overlay/)
- [Justt Webhook Events Overlay](https://apis.io/overlays/justt/justt-webhook-events-overlay/)

#### Security (3)

Authentication, trust centre, and vulnerability disclosure.

- [Justt Authentication](https://apis.io/security/justt/justt-authentication/)
- [Justt Domain Security](https://apis.io/security/justt/justt-domain-security/)
- [Justt Trust Center](https://apis.io/security/justt/justt-trust-center/)

#### OAuth scopes (1)

The permissions the API asks for.

- [Justt Scopes](https://apis.io/scopes/justt/justt-scopes/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Justt Plans Pricing](https://apis.io/plans/justt/justt-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Justt Rate Limits](https://apis.io/rate-limits/justt/justt-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://justt.ai/)
- [Documentation](https://developers.justt.ai/docs/getting-started)
- [Getting started](https://developers.justt.ai/docs/getting-started)
- [API reference](https://developers.justt.ai/reference)
- [Support](https://developers.justt.ai/docs/contact-us)
- [Blog](https://justt.ai/blog/)
- [Compliance](https://trust.justt.ai/)
- [Trust centre](https://trust.justt.ai/)
- [Terms of service](https://justt.ai/terms-of-use/)
- [Privacy policy](https://justt.ai/privacy-policy/)
- [Status](https://status.justt.ai/)

## API Evangelist rating

**Kin Score 52.3** — developing · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 75.0 |
| Contract quality | 56.4 |
| Contract governance | 18.2 |
| Operational transparency | 48.7 |
| Developer ergonomics | 49.4 |
| Access clarity | 43.4 |

**Agent readiness 52.9** — agent-ready (gated down from agent-native)

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | — |
| MCP Server | platform (partial credit) |
| Auth Clarity | served (partial credit) |
| Idempotency | — |
| Error Semantics | verified |
| OpenAPI Examples | partial |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | yes |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | yes |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | served (partial credit) |
| Protected Resource Metadata | verified |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | paginated |
| Operation Distinctiveness | distinct |

**Regulatory alignment 33.3** — Payments

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/justt/](https://apis.io/providers/justt/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Justt: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/justt/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
