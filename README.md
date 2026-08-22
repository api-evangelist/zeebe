# Zeebe (zeebe)

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

Zeebe is the cloud-native workflow engine that powers Camunda 8, providing scalable, resilient workflow automation and microservices orchestration without relying on a central database, enabling high throughput with horizontal scaling. It implements BPMN 2.0 process execution and provides a REST API for process deployment, instance management, job handling, message correlation, and cluster topology queries.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/zeebe/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/zeebe/refs/heads/main/apis.yml)

## Scope

- **Type:** Index

## Tags

- BPMN
- Camunda
- Cloud Native
- Distributed Systems
- Java
- Microservices
- Process Automation
- Workflow Orchestration

## Timestamps

- **Created:** 2026-03-26
- **Modified:** 2026-05-19

## APIs

### Zeebe REST API

The Zeebe REST API provides programmatic access to the Zeebe workflow engine powering Camunda 8. It enables process deployment, process instance creation and management, job activation and completion, message and signal publishing, incident resolution, user task management, and cluster topology queries.

- **Human URL:** [https://docs.camunda.io/docs/apis-tools/zeebe-api-rest/zeebe-api-rest-overview/](https://docs.camunda.io/docs/apis-tools/zeebe-api-rest/zeebe-api-rest-overview/)
- **Base URL:** `https://{region}.zeebe.camunda.io:443/{clusterId}/v2`

#### Tags

- BPMN
- Camunda
- Cloud Native
- Microservices
- Process Automation
- Workflow Orchestration

#### Properties

- [OpenAPI](https://raw.githubusercontent.com/api-evangelist/zeebe/refs/heads/main/openapi/zeebe-api.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Documentation](https://docs.camunda.io/docs/apis-tools/zeebe-api-rest/zeebe-api-rest-overview/)
- [Postman](https://www.postman.com/camundateam/camunda-8-postman/collection/j0knqwp/zeebe-api-rest) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Spectral  Rules](https://raw.githubusercontent.com/api-evangelist/zeebe/refs/heads/main/rules/zeebe-rules.yml)
- [Examples](https://raw.githubusercontent.com/api-evangelist/zeebe/refs/heads/main/examples/)
- [JSON Schema](https://raw.githubusercontent.com/api-evangelist/zeebe/refs/heads/main/json-schema/) — [JSON Schema](https://json-schema.org/specification)
- [JSON Structure](https://raw.githubusercontent.com/api-evangelist/zeebe/refs/heads/main/json-structure/)
- [JSON-LD](https://raw.githubusercontent.com/api-evangelist/zeebe/refs/heads/main/json-ld/zeebe-context.jsonld) — [JSON-LD](https://www.w3.org/TR/json-ld11/)
- [Vocabulary](https://raw.githubusercontent.com/api-evangelist/zeebe/refs/heads/main/vocabulary/zeebe-vocabulary.yml)
- [Capabilities](https://raw.githubusercontent.com/api-evangelist/zeebe/refs/heads/main/capabilities/)
- [Postman Collection](collections/zeebe-api.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/zeebe-api.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

## Common Properties

- [Website](https://camunda.com/platform/zeebe/)
- [Documentation](https://docs.camunda.io/docs/components/zeebe/zeebe-overview/)
- [Documentation](https://docs.camunda.io/docs/apis-tools/zeebe-api-rest/zeebe-api-rest-overview/)
- [Getting Started](https://docs.camunda.io/docs/guides/)
- [Git Hub](https://github.com/camunda/camunda)
- [Git Hub Org](https://github.com/camunda)
- [Git Hub Org](https://github.com/camunda-community-hub)
- [Pricing](https://camunda.com/pricing/)
- [Blog](https://camunda.com/blog/)
- [Issues](https://github.com/camunda/camunda/issues)
- [SDK](https://github.com/camunda/camunda-bpm-spring-boot-starter)
- [SDK](https://github.com/camunda-community-hub/zeebe-client-csharp)
- [SDK](https://github.com/camunda-community-hub/micronaut-zeebe-client)
- [Changelog](https://github.com/camunda/camunda/releases)
- [Forum](https://forum.camunda.io/)
- [Integrations](https://camunda.com/partners/)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
