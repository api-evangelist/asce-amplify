# ASCE Amplify (asce-amplify)

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

ASCE Amplify is a platform created by the American Society of Civil Engineers (ASCE) that provides civil engineering data and advocacy tools. The platform includes the ASCE Hazard Tool API, which provides a simple interface to query locations in the United States for environmental hazard data by geographic location. The Hazard Tool API covers seismic, wind, snow, ice, flood, and other environmental hazard loads used in structural design per ASCE standards. ASCE Amplify also supports advocacy, connecting civil engineers with elected officials to advocate for infrastructure investment and sustainable practices.

**URL:** [Visit APIs.json URL](https://raw.githubusercontent.com/api-evangelist/asce-amplify/refs/heads/main/apis.yml)

**Run:** [Capabilities Using Naftiko](https://github.com/naftiko/fleet?utm_source=api-evangelist&utm_medium=readme&utm_campaign=company-api-evangelist&utm_content=repo)

## Tags:

 - Civil Engineering, Hazard Data, Engineering Standards, Infrastructure

## Timestamps

- **Created:** 2025-02-17
- **Modified:** 2026-04-19

## APIs

### ASCE Hazard Tool API
The ASCE Hazard Tool API provides a simple interface to query locations in the United States for environmental hazard data by geographic location. It provides site-specific hazard values used in structural engineering design including seismic ground motion parameters, wind speeds, snow loads, ice loads, and flood data in accordance with ASCE 7 and related standards. Access requires an ASCE membership or license.

**Human URL:** [https://amplify.asce.org/api](https://amplify.asce.org/api)

#### Tags:

 - Civil Engineering, Hazard Data, Seismic, Wind, Snow, Structural Engineering

#### Properties

- [Documentation](https://amplify.asce.org/api)
- [Authentication](https://amplify.asce.org/api)

## Common Properties

- [ASCE Amplify Platform](https://amplify.asce.org/)
- [ASCE Website](https://www.asce.org/)

## Features

| Name | Description |
|------|-------------|
| Geographic Hazard Lookup | Query any US location by latitude and longitude or address to retrieve site-specific environmental hazard values for structural design, including ASCE 7 seismic, wind, snow, and ice parameters. |
| ASCE 7 Seismic Parameters | Retrieve seismic design parameters including Ss, S1, SMS, SM1, SDS, SD1, and spectral acceleration values per ASCE 7 for any US location. |
| Wind Speed Data | Access design wind speed values for various risk categories and exposure categories per ASCE 7 for structural wind load calculations. |
| Snow and Ice Load Data | Retrieve ground snow load values and ice storm data for design of roof structures and overhead transmission lines per ASCE 7. |
| Civil Engineer Advocacy | Tools for ASCE members to contact elected officials and advocate for infrastructure funding, engineering standards, and professional issues. |

## Use Cases

| Name | Description |
|------|-------------|
| Structural Design | Structural engineers use the ASCE Hazard Tool API to obtain site-specific hazard parameters for building and infrastructure design in compliance with ASCE 7 and building codes. |
| Site Assessment | Civil engineers perform preliminary site assessments for new construction projects by querying multiple locations for hazard comparisons. |
| Software Integration | Structural engineering software vendors integrate the ASCE Hazard Tool API to automatically populate design parameters based on project location. |

## Integrations

| Name | Description |
|------|-------------|
| ASCE 7 Standards | API values directly correspond to ASCE 7 Minimum Design Loads for Buildings and Other Structures, the primary reference standard for US structural engineering. |
| IBC Building Codes | Hazard parameters from the API align with International Building Code requirements that reference ASCE 7 for environmental load design values. |

## Maintainers

**FN:** Kin Lane

**Email:** kin@apievangelist.com
