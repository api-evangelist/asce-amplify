---
name: asce-site-hazard-lookup
description: >-
  Retrieve the full set of ASCE 7 environmental design hazard values for a
  building site in the United States — wind, snow, ice, rain, flood, tornado and
  tsunami — from the ASCE Hazard Loads API, and read the results without
  mistaking a sentinel value for data.
api: ASCE Hazard Tool API
base_url: https://api-hazard.asce.org/v1
spec: openapi/asce-amplify-hazard-loads-openapi.yml
operations:
  - GET /wind
  - GET /snow
  - GET /ice
  - GET /rain
  - GET /flood
  - GET /tornado
  - GET /tsunami
operation_ids:
  - getWind
  - getSnow
  - getIce
  - getRain
  - getFlood
  - getTornado
  - getTsunami
generated: '2026-09-07'
method: generated
source: >-
  Grounded in openapi/asce-amplify-hazard-loads-openapi.yml (paths and parameter
  enums verbatim) and the Hazard Tool API JSON field documentation PDF. The
  provider's spec carries no operationIds; the ids above are the ones assigned in
  overlays/asce-amplify-hazard-loads-overlay.yaml and are ours, not ASCE's.
---

# Site hazard lookup (ASCE 7)

## What you need before you start

- An API key issued by ASCE to your company through the ASCE Hazard Tool Account Manager. It goes in the `token` query parameter — there is no header form.
- The site latitude and longitude in decimal degrees. The API covers the contiguous US, Alaska, Hawaii, Puerto Rico, Guam, American Samoa and the US Virgin Islands. There is no address geocoder in the API.
- The ASCE/SEI 7 edition your project is designed to: `7-10`, `7-16` or `7-22`.
- The Risk Category (1–4).

## Steps

1. **Fix the inputs once.** `lat`, `lon`, `standardsVersion` and `riskLevel` are the same for every call in this flow. Getting the edition wrong changes the response *shape*, not just the numbers.
2. **Call each hazard you need.** They are separate operations; there is no combined endpoint.
   - `GET /wind?lat=&lon=&standardsVersion=&riskLevel=&token=` — `standardsVersion` and `riskLevel` are both required.
   - `GET /snow?lat=&lon=&standardsVersion=&riskLevel=&token=` — both required.
   - `GET /ice?lat=&lon=&standardsVersion=&token=` — `riskLevel` is optional here.
   - `GET /rain?lat=&lon=&token=` — no edition parameter; NOAA Atlas 14 is not edition-scoped.
   - `GET /flood?lat=&lon=&token=` — no edition parameter; FEMA NFHL is not edition-scoped.
   - `GET /tsunami?lat=&lon=&standardsVersion=&token=` — accepts `7-10`, `7-16`, `7-22`.
   - `GET /tornado?lat=&lon=&standardsVersion=7-22&riskLevel=&token=` — the only accepted edition is `7-22`.
3. **Read the quota off each response.** `requestInfo.currentMonthlyRequestNumber` is a string like `"69/1000"`. This is the only place your remaining allowance appears — there are no rate-limit headers. A seven-hazard site lookup spends seven of your thousand monthly requests.
4. **Interpret the sentinels before you use any number.**
   - `flood.features.attributes.STATIC_BFE` of `-9999` means the base flood elevation is not applicable. It is not an elevation.
   - Snow `Display_1` / `DisplaySI` reading `"Case Study"`, or an Alaska `Notes` field reading `"Case Study"`, means a site-specific study is required. When it appears the load value is `0`, and `0` means N/A, never a zero snow load.
   - `tornado.isRiskLevelApplicable` means the Risk Category was I or II and no tornado data was returned. That is correct behaviour, not an error.
   - An empty `tsunami.features` means the site is outside the mapped tsunami design zone (or you asked for `7-10`).
   - `snow` `"See Details"` (7-16) means the site is outside Tables 7.2-1 to 7.2-8 and the Authority Having Jurisdiction must be consulted.
5. **Branch on the edition when parsing.** For snow, 7-10 and 7-16 return `snowResults.features.attributes.Display_1`; 7-22 returns `snowResults.riskCategoryXX`; 7-22 in Alaska returns `snowResults.attributes.ValueXX`. For ice, 7-10/7-16 return `attributes.ice_load`; 7-22 returns `riskCategoryXX`. Write the parser per edition, not per hazard.

## Conventions and failure handling

- **Read-only.** Every operation is a GET. Nothing you call here changes state, so there is no idempotency key to send and nothing to reverse. Retrying a failed call is always safe.
- **Errors** are a bare JSON envelope `{"code": …, "message": …}` — not RFC 9457 problem+json. `400` is invalid input; `500` is a missing/invalid key **or** an exhausted monthly quota; an anonymous call returns `401 {"code":401,"message":"Token required"}`. Because a single `500` covers two very different causes, check `currentMonthlyRequestNumber` from your last successful response before assuming your key is bad.
- **Do not log raw responses.** `requestInfo.url` echoes back the full request URL including your `token`.
- **Quota exhaustion is not a 429.** Do not build a Retry-After backoff for it — there is no header and no reset signal. Ask ASCE for a higher limit at https://www.asce.org/publications-and-news/asce-hazard-tool/request-a-quote.

## References

- API documentation: https://www.asce.org/publications-and-news/asce-hazard-tool/api
- Field documentation (PDF): https://www.asce.org/-/media/asce-images-and-files/publications-and-news/hazard-tool/hazard-tool-api-documentation.pdf
- Interactive reference: https://api-hazard.asce.org/docs
- Repository: `conventions/asce-amplify-conventions.yml`, `errors/asce-amplify-problem-types.yml`, `data-model/asce-amplify-data-model.yml`
