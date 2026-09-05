---
name: columbia-sportswear-product-imagery-sync
description: >-
  Retrieve Columbia Sportswear product imagery ("seasonal assets") from the Content
  Hub External API — either for one 10-digit material number or as an incremental
  bulk sync over a modified-on window — using an Azure API Management subscription
  key.
api: Content Hub External API
provider: Columbia Sportswear
base_url: https://api.columbia.com/ContentHubExternal
operations:
  - get-api-external-image-getseasonalassets-materialnumber-materialnumber
  - get-api-external-image-getseasonalassetsbulk
generated: '2026-09-05'
method: generated
source: openapi/columbia-sportswear-content-hub-external-openapi.json
---

# Sync Columbia product imagery

Columbia's Content Hub External API is a **read-only** image-lookup service. There
are exactly two operations and both are `GET`. Nothing in this skill can change
state at Columbia, so there is no rollback to plan and no idempotency key to send.

## Before you start

You need an Azure API Management subscription key. Columbia does not self-serve
these: request a subscription to the **ContentHub External** product at
<https://columbia.developer.azure-api.net/products>, and a Columbia administrator
must approve it. The portal's terms restrict access to Columbia employees and to
employees of vendors providing services to Columbia under agreement — if you are
neither, stop here.

Send the key on **every** request, as either:

- the `Ocp-Apim-Subscription-Key` request header (preferred), or
- the `subscription-key` query parameter (avoid — it lands in logs and referrers).

Without it the gateway answers `401` with
`WWW-Authenticate: AzureApiManagementKey` and the body
`{ "statusCode": 401, "message": "Access denied due to missing subscription key. ..." }`.

## Flow A — imagery for one product

Operation: `get-api-external-image-getseasonalassets-materialnumber-materialnumber`
(`GET /api/external/image/GetSeasonalAssets`).

1. Resolve the product to Columbia's **10-digit material number**. This is a
   Columbia-internal identifier, not a GTIN — you need a mapping table. Example:
   `1442362613`.
2. Call with `MaterialNumber` as a required query parameter.
3. Optionally narrow with `Perspective` (e.g. `f`), `SubType` (e.g. `On Model`),
   and the `ModifiedOnStartRange` / `ModifiedOnEndRange` date-time pair.
4. On `400` the message is `Material Number is required` — you omitted the
   parameter or sent it empty. Do not retry without fixing the request.

```
GET /api/external/image/GetSeasonalAssets?MaterialNumber=1442362613&SubType=On%20Model
Host: api.columbia.com
Ocp-Apim-Subscription-Key: <your key>
```

## Flow B — incremental bulk sync

Operation: `get-api-external-image-getseasonalassetsbulk`
(`GET /api/external/image/GetSeasonalAssetsBulk`).

1. Track a high-water mark — the last `ModifiedOn` timestamp you successfully
   ingested.
2. Call with `ModifiedOnStartRange` set to that high-water mark and
   `ModifiedOnEndRange` set to now. This date-range filter is the only incremental
   mechanism the API offers.
3. Page with `Skip` (default `0`) and `Take` (default `100`). **`Take` above 1000
   is rejected** with `400 Maximum Take size is 1000`. Use `Take=1000` and advance
   `Skip` by 1000 each call.
4. Advance the high-water mark only after the whole page set is committed.

```
GET /api/external/image/GetSeasonalAssetsBulk?ModifiedOnStartRange=2026-08-01T00:00:00Z&ModifiedOnEndRange=2026-09-01T00:00:00Z&Skip=0&Take=1000
Host: api.columbia.com
Ocp-Apim-Subscription-Key: <your key>
```

## Things the contract does not tell you

Plan around these — they are real gaps in Columbia's published contract, not
omissions in this skill:

- **No response schema.** Neither `200` declares a media type, schema or example.
  You cannot know the asset representation, the field that carries the image URL,
  or the paging envelope until you call it with a live key. Do not hard-code a
  shape from documentation; discover it and pin it in your own tests.
- **No total count or last-page signal is documented.** Treat a page shorter than
  `Take` as the end, and verify that assumption on first integration.
- **`Perspective` and `SubType` are not enumerated.** The only values Columbia
  publishes are the examples `f` and `On Model`.
- **No rate limits are published** and no `RateLimit-*` or `Retry-After` header was
  observed. Throttle yourself conservatively, back off exponentially on `429` and
  `503`, and treat the bulk endpoint as the one most likely to be limited.
- **No request-id header is documented.** The gateway returns Azure's `x-azure-ref`
  on errors; capture it, but expect no Columbia support process that reads it.

## Error handling

| Status | Meaning | What to do |
|---|---|---|
| `400` | `Material Number is required` or `Maximum Take size is 1000` | Fix the request. Never retry unchanged. |
| `401` | Missing or invalid subscription key | Check the key and that the subscription is approved and active. Do not retry in a loop. |
| `500` | `Unexpected Exception` | Retry with exponential backoff. No error code or correlation reference is published. |

Errors come back as `{ "statusCode": <int>, "message": "<string>" }`. This is the
Azure API Management envelope, not RFC 9457 `application/problem+json` — do not
parse for `type`, `title` or `detail`.

## Access note

Unauthorised callers are limited to Product Shot imagery older than a configured
season. Columbia does not publish what that season threshold is, so if your result
set looks unexpectedly thin or stale, confirm your subscription's entitlement with
Columbia before assuming the data is missing.
