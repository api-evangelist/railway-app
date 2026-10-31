# Railway

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

Railway is a cloud application deployment platform (PaaS) that builds, deploys, and scales services, databases, and cron jobs from a Git repository or Docker image. Its programmatic surface is a GraphQL-first Public API served at https://backboard.railway.com/graphql/v2 - the same API that powers the Railway dashboard. There is no REST API; all queries and mutations are issued as GraphQL POST requests, and real-time build, deployment, and environment log streams are delivered as GraphQL subscriptions over a WebSocket endpoint at wss://backboard.railway.com/graphql/v2.

**Areas:** Deployment · Platform-as-a-Service · Cloud · Infrastructure · GraphQL · DevOps · Real-Time

## Railway on APIs.io

Everything profiled for Railway is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/railway-app/](https://apis.io/providers/railway-app/)** — or go straight to one of the APIs or properties below.

### APIs (13)

- [Railway Projects API](https://apis.io/apis/railway-app/railway-app-projects-api/) — GraphQL operations for creating, reading, updating, and deleting Railway projects - the top-level container for services and environments. Queries include…
- [Railway Services API](https://apis.io/apis/railway-app/railway-app-services-api/) — GraphQL operations for managing services and their per-environment service instances. Queries include service and serviceInstance; mutations include…
- [Railway Deployments API](https://apis.io/apis/railway-app/railway-app-deployments-api/) — GraphQL operations for triggering and managing deployments. Queries include deployment and deployments; mutations include serviceInstanceDeployV2,…
- [Railway Environments API](https://apis.io/apis/railway-app/railway-app-environments-api/) — GraphQL operations for isolated project environments (for example production and staging). Queries include environment and environments; mutations include…
- [Railway Variables API](https://apis.io/apis/railway-app/railway-app-variables-api/) — GraphQL operations for service and environment configuration variables. Queries include variables; mutations include variableUpsert, variableDelete, and…
- [Railway Volumes API](https://apis.io/apis/railway-app/railway-app-volumes-api/) — GraphQL operations for persistent volumes attached to services. Queries include volume; mutations include volumeCreate, volumeUpdate, volumeDelete, and…
- [Railway Plugins API](https://apis.io/apis/railway-app/railway-app-plugins-api/) — GraphQL operations for legacy plugins (managed database add-ons such as Postgres, MySQL, Redis, and MongoDB). Queries include plugin; mutations include…
- [Railway Custom Domains API](https://apis.io/apis/railway-app/railway-app-custom-domains-api/) — GraphQL operations for attaching custom and Railway-provided domains to a service. Queries include customDomain and domains; mutations include…
- [Railway TCP Proxies API](https://apis.io/apis/railway-app/railway-app-tcp-proxies-api/) — GraphQL operations for exposing a service over raw TCP. Queries include tcpProxies; mutations include tcpProxyCreate and tcpProxyDelete.
- [Railway Usage and Metrics API](https://apis.io/apis/railway-app/railway-app-usage-metrics-api/) — GraphQL operations for reading resource consumption and cost. Queries include usage, estimatedUsage, and metrics for per-service vCPU, memory, network…
- [Railway Teams and Workspaces API](https://apis.io/apis/railway-app/railway-app-teams-api/) — GraphQL operations for the authenticated account, its workspaces, teams, and members. Queries include me, workspace, and workspaces; mutations include…
- [Railway Webhooks API](https://apis.io/apis/railway-app/railway-app-webhooks-api/) — GraphQL operations for project webhooks that notify external URLs of deployment status changes. Queries include projectWebhooks; mutations include…
- [Railway Logs API](https://apis.io/apis/railway-app/railway-app-logs-api/) — GraphQL log surface for builds, deployments, environments, and HTTP traffic. Available both as point-in-time queries (buildLogs, deploymentLogs,…

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [Railway GraphQL Subscriptions (WebSocket)](https://apis.io/asyncapis/railway-app/railway-app-asyncapi/)

#### Event channels (4)

Individual events and webhooks the provider emits.

- [buildLogs](https://apis.io/channels/railway-app/buildlogs/)
- [deploymentLogs](https://apis.io/channels/railway-app/deploymentlogs/)
- [environmentLogs](https://apis.io/channels/railway-app/environmentlogs/)
- [httpLogs](https://apis.io/channels/railway-app/httplogs/)

#### GraphQL (1)

GraphQL schemas.

- [Railway GraphQL Public API](https://apis.io/graphqls/railway-app/railway-app-graphql/)

#### Collections (1)

Postman and Open Collection request collections.

- [Railway GraphQL Public API](https://apis.io/collections/railway-app/open-railway-app/)

#### Governance rules (1)

Spectral rulesets for the provider's contracts.

- [Railway — asyncapi rules](https://apis.io/rules/railway-app/railway-app-asyncapi-spectral-rules/)

#### Security (2)

Authentication, trust centre, and vulnerability disclosure.

- [Railway App Domain Security](https://apis.io/security/railway-app/railway-app-domain-security/)
- [Railway App Trust Center](https://apis.io/security/railway-app/railway-app-trust-center/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Railway App Plans Pricing](https://apis.io/plans/railway-app/railway-app-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Railway App Rate Limits](https://apis.io/rate-limits/railway-app/railway-app-rate-limits/)

#### FinOps (1)

What the API costs to run, by operation.

- [Railway App Finops](https://apis.io/finops/railway-app/railway-app-finops/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://railway.com/)
- [Documentation](https://docs.railway.com)
- [Blog](https://blog.railway.com/rss.xml)
- [GitHub](https://github.com/railwayapp)

## API Evangelist rating

**Kin Score 28.6** — thin · rubric 0.24.0 · scored 2026-10-17

| Facet | Score |
|---|---|
| Discoverability | 71.4 |
| Contract quality | 49.6 |
| Contract governance | 11.4 |
| Operational transparency | 10.5 |
| Developer ergonomics | 19.0 |
| Access clarity | 15.8 |

**Agent readiness 14.7** — agent-aware

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | — |
| Reversibility Documented | — |
| MCP Server | — |
| Auth Clarity | — |
| Idempotency | — |
| Error Semantics | — |
| OpenAPI Examples | — |
| Rate Limit Signal | derived (partial credit) |
| Event Surface Described | derived (partial credit) |
| Agent Skills | — |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |

**Regulatory alignment 10.8** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/railway-app/](https://apis.io/providers/railway-app/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Railway: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/railway-app/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
