---
name: asce-seismic-design-parameters
description: >-
  Retrieve seismic design parameters for a site under ASCE/SEI 7 or ASCE/SEI 41
  from the ASCE Hazard Loads API, choosing a site soil class that is valid for
  the standard edition requested.
api: ASCE Hazard Tool API
base_url: https://api-hazard.asce.org/v1
spec: openapi/asce-amplify-hazard-loads-openapi.yml
operations:
  - GET /seismic
operation_ids:
  - getSeismic
generated: '2026-09-07'
method: generated
source: >-
  Grounded in openapi/asce-amplify-hazard-loads-openapi.yml — the siteClass and
  standardsVersion enums are copied verbatim from the provider's spec — and the
  Hazard Tool API JSON field documentation PDF, Seismic section. operationId
  getSeismic is assigned in overlays/asce-amplify-hazard-loads-overlay.yaml and
  is ours, not ASCE's.
---

# Seismic design parameters

## The one thing that goes wrong

`siteClass` is validated against `standardsVersion`. Sending a soil class that does not exist in the edition you asked for returns an **invalid input** error, and it is the most common failure on this operation. The valid sets are not the same:

| standardsVersion | valid siteClass values |
|---|---|
| `7-10`, `41-17` | `A`, `B`, `C`, `D`, `E`, `F` |
| `7-16` | `A`, `B`, `B-estimated`, `C`, `D`, `D-default`, `E`, `F` |
| `7-22`, `41-23` | `Default`, `A`, `B`, `BC`, `C`, `CD`, `D`, `DE`, `E`, `F` |

`B-estimated` and `D-default` exist only in 7-16 (see ASCE 7-16 Section 11.4.3). `BC`, `CD`, `DE` and `Default` exist only in 7-22 and 41-23. The spec's enum lists every value across every edition, so the spec alone will not stop you sending an invalid combination — the server will.

## Steps

1. **Pick the standard.** `GET /seismic` accepts `7-10`, `7-16`, `7-22`, `41-17` and `41-23`. ASCE 41 editions return seismic data only; there is no ASCE 41 wind, snow or ice.
2. **Pick a site class valid for that edition** from the table above. If a geotechnical report has not established one, 7-16's `D-default` and 7-22's `Default` are the provider's own placeholders — use them deliberately, and record that you did.
3. **Call it.**
   `GET /seismic?lat=&lon=&standardsVersion=&siteClass=&riskLevel=&token=`
   `lat`, `lon`, `standardsVersion` and `siteClass` are required; `riskLevel` (1–4) is optional on this operation.
4. **Read the output against the USGS reference.** ASCE does not restate the seismic field names in its own documentation — it states that "output values are taken from the USGS Seismic Design Web Services" and points at https://earthquake.usgs.gov/ws/designmaps/. Parse against that reference, not against a shape you inferred from one response.
5. **Check the quota.** `requestInfo.currentMonthlyRequestNumber` on the success body, e.g. `"69/1000"`.

## Conventions and failure handling

- Read-only GET. Safe to retry; nothing to reverse; no idempotency key.
- `400 {"code":400,"message":…}` on an invalid soil-class/edition pairing or an out-of-range coordinate.
- `500` covers both a bad key and an exhausted monthly quota — disambiguate with the last known `currentMonthlyRequestNumber`.
- `401 {"code":401,"message":"Token required"}` when `token` is absent.
- Coverage is the contiguous US, Alaska, Hawaii, Puerto Rico, Guam, American Samoa and the US Virgin Islands. A coordinate outside that footprint is not a supported query.

## References

- API documentation: https://www.asce.org/publications-and-news/asce-hazard-tool/api
- Field documentation (PDF), Seismic section: https://www.asce.org/-/media/asce-images-and-files/publications-and-news/hazard-tool/hazard-tool-api-documentation.pdf
- USGS Seismic Design Web Services: https://earthquake.usgs.gov/ws/designmaps/
- Repository: `conventions/asce-amplify-conventions.yml`, `errors/asce-amplify-problem-types.yml`
