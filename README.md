# Columbia Sportswear (columbia-sportswear)

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

Columbia Sportswear is a global designer, marketer, and distributor of outdoor, active, and everyday lifestyle apparel, footwear, accessories, and equipment under the Columbia, Mountain Hardwear, SOREL, and prAna brands. Columbia Sportswear Digital runs a partner-facing API estate on Microsoft Azure API Management: a developer portal at columbia.developer.azure-api.net and a production gateway on Columbia's own domain at api.columbia.com. Exactly one API product is documented anonymously — ContentHub External, a read-only product-imagery service with a published OpenAPI 3.0.1 contract — and every other product on the portal requires sign-in. Access is a partner arrangement rather than a developer program: subscriptions require Columbia's approval, portal terms restrict use to Columbia employees and to vendors serving Columbia under agreement, and no price, rate limit, SLA or status page is published. The company also exchanges traditional EDI documents (POs, ASNs, invoices) with retail trading partners through providers like TrueCommerce and eZCom.

**URL:** [Visit APIs.json URL](https://raw.githubusercontent.com/api-evangelist/columbia-sportswear/refs/heads/main/apis.yml)

## Scope

- **Type:** Index
- **Position:** Consuming
- **Access:** 3rd-Party

## Tags

- Apparel
- B2B
- Consumer Management
- Content Management
- Digital Asset Management
- Footwear
- Fortune 1000
- Outdoor
- Partner APIs
- Product Imagery
- Retail

## Timestamps

- **Created:** 2025-03-23
- **Modified:** 2026-09-05

## APIs

### Columbia Sportswear Digital Developer Portal

Columbia Sportswear's partner-facing API platform, hosted on Microsoft Azure API Management. The portal at columbia.developer.azure-api.net lists API products, offers a try-it console, and takes subscription requests; the production gateway answers on Columbia's own domain at api.columbia.com. Anonymously, the portal publishes one product — ContentHub External — and everything else requires sign-in. Every subscription requires Columbia's approval before a key is issued. The legacy portal endpoint at columbia.portal.azure-api.net has been retired and now returns HTTP 503; this record was repointed at the live portal on 2026-09-05.

**Human URL:** [https://columbia.developer.azure-api.net/](https://columbia.developer.azure-api.net/)
**Base URL:** `https://api.columbia.com/`

#### Properties

- [Developer Portal](https://columbia.developer.azure-api.net/)
- [API Reference](https://columbia.developer.azure-api.net/apis)
- [Documentation](https://columbia.developer.azure-api.net/products)
- [Sign Up](https://columbia.developer.azure-api.net/signup)

### Content Hub External API

Columbia Sportswear's ContentHub image service for external customers. A read-only API with two GET operations: look up product imagery ("seasonal assets") for a single 10-digit material number, or page through assets in bulk over a modified-on date range with Skip/Take paging capped at a Take of 1000. Authentication is an Azure API Management subscription key on every call. The OpenAPI 3.0.1 contract in this repository was exported from Columbia's own API Management instance and declares `servers[]` `https://api.columbia.com/ContentHubExternal` — Columbia's own domain.

**Human URL:** [Portal API detail](https://columbia.developer.azure-api.net/api-details#api=4cad0e39673846b186038d3113e5a4ab)
**Base URL:** `https://api.columbia.com/ContentHubExternal`

#### Properties

- [OpenAPI](openapi/columbia-sportswear-content-hub-external-openapi.json) — [OpenAPI specification](https://spec.openapis.org/oas/latest.html)
- [Error Catalog](errors/columbia-sportswear-problem-types.yml)
- [Conformance](conformance/columbia-sportswear-conformance.yml)
- [Data Model](data-model/columbia-sportswear-data-model.yml)

## Artifacts in this repository

| Artifact | File | Method |
|---|---|---|
| OpenAPI (harvested, verbatim) | `openapi/_original/columbia-sportswear-content-hub-external-openapi.json` | harvested |
| OpenAPI (registered) | `openapi/columbia-sportswear-content-hub-external-openapi.json` | harvested |
| OpenAPI Overlay | `overlays/columbia-sportswear-content-hub-external-overlay.yaml` | generated |
| Authentication | `authentication/columbia-sportswear-authentication.yml` | derived |
| Conventions (idempotency + reversibility) | `conventions/columbia-sportswear-conventions.yml` | derived |
| Error catalog | `errors/columbia-sportswear-problem-types.yml` | derived |
| Conformance | `conformance/columbia-sportswear-conformance.yml` | derived |
| Data model | `data-model/columbia-sportswear-data-model.yml` | derived |
| Lifecycle | `lifecycle/columbia-sportswear-lifecycle.yml` | probed |
| Plans / pricing | `plans/columbia-sportswear-plans-pricing.yml` | probed |
| Rate limits | `rate-limits/columbia-sportswear-rate-limits.yml` | probed |
| Domain security | `security/columbia-sportswear-domain-security.yml` | probed |
| Well-known probe (all 404 — a recorded absence) | `well-known/columbia-sportswear-well-known.yml` | probed |
| Packages / SDKs | `packages/columbia-sportswear-packages.yml` | searched |
| MCP (candidate — no server exists) | `mcp/columbia-sportswear-mcp.yml` | derived |
| Agent Skill | `skills/columbia-sportswear-product-imagery-sync.md` | generated |
| llms.txt | `llms/columbia-sportswear-llms.txt` | generated |
| Vocabulary | `vocabulary/columbia-sportswear-vocabulary.yml` | generated |

**Not published by Columbia Sportswear**, each probed and recorded as absent rather than assumed: client SDK, CLI, MCP server, A2A agent card, AsyncAPI or webhook catalog, status page, changelog, deprecation policy, published rate limits, sandbox, `security.txt`, trust centre, and any `/.well-known/` discovery document on any host.

## Common Properties

- [Website](https://www.columbia.com/)
- [Corporate](https://www.columbiasportswear.com/)
- [Developer Portal](https://columbia.developer.azure-api.net/)
- [API Reference](https://columbia.developer.azure-api.net/apis)
- [Sign Up](https://columbia.developer.azure-api.net/signup)
- [Support](https://help.columbia.com/s/)
- [GitHub Organization](https://github.com/columbiasportswear)
- [LinkedIn](https://www.linkedin.com/company/columbia-sportswear)
- [Privacy Policy](https://www.columbia.com/t/legal/privacy-policy/)
- [Terms of Use](https://www.columbia.com/t/legal/terms-of-use/)
- [Investor Relations](https://investor.columbia.com/)
- [Mountain Hardwear](https://www.mountainhardwear.com/)
- [SOREL](https://www.sorel.com/)
- [prAna](https://www.prana.com/)

## Maintainers

**FN:** Kin Lane

**Email:** kin@apievangelist.com
