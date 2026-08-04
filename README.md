# Railway (railway-app)

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
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Railway is a cloud application deployment platform (PaaS) that builds, deploys, and scales services, databases, and cron jobs from a Git repository or Docker image. Its programmatic surface is a **GraphQL-first Public API** served at `https://backboard.railway.com/graphql/v2` - the same API that powers the Railway dashboard. **There is no REST API.** All queries and mutations are GraphQL POST requests, and real-time build, deployment, and environment log streams are delivered as **GraphQL subscriptions over WebSocket** at `wss://backboard.railway.com/graphql/v2`.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/railway-app/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/railway-app/refs/heads/main/apis.yml)

## Transport reality

- **GraphQL over HTTP** (`https://backboard.railway.com/graphql/v2`) - every query and mutation is an HTTP `POST` with a JSON body `{ "query": "...", "variables": { ... } }`.
- **GraphQL subscriptions over WebSocket** (`wss://backboard.railway.com/graphql/v2`) - real-time log streaming using the `graphql-transport-ws` / `graphql-ws` subprotocol. This is what `railway logs` streams from.
- **No REST** - Railway does not publish a REST API, so this repository intentionally contains **no** `openapi/` directory. The GraphQL surface is documented in [`graphql/railway-app-schema.graphql`](graphql/railway-app-schema.graphql) and [`graphql/railway-app-graphql.md`](graphql/railway-app-graphql.md).

## Authentication

| Token type | Scope | Header |
| --- | --- | --- |
| Account token | All resources across every workspace | `Authorization: Bearer <TOKEN>` |
| Workspace token | A single workspace | `Authorization: Bearer <TOKEN>` |
| Project token | A single project environment | `Project-Access-Token: <TOKEN>` |
| OAuth access token | User-granted permissions | `Authorization: Bearer <TOKEN>` |

## Tags

- Deployment
- PaaS
- Cloud
- Infrastructure
- GraphQL
- DevOps

## Timestamps

- **Created:** 2026-07-02
- **Modified:** 2026-07-02

## APIs

Each "API" below is a logical grouping of GraphQL operations against the single `/graphql/v2` endpoint.

### Railway Projects API

GraphQL operations for creating, reading, updating, and deleting projects. Queries: `project`, `projects`. Mutations: `projectCreate`, `projectUpdate`, `projectDelete`.

### Railway Services API

Manage services and per-environment service instances. Queries: `service`, `serviceInstance`. Mutations: `serviceCreate`, `serviceUpdate`, `serviceInstanceUpdate`, `serviceConnect`, `serviceDisconnect`, `serviceDelete`.

### Railway Deployments API

Trigger and manage deployments. Queries: `deployment`, `deployments`. Mutations: `serviceInstanceDeployV2`, `serviceInstanceRedeploy`, `deploymentRedeploy`, `deploymentRestart`, `deploymentStop`, `deploymentCancel`, `deploymentRemove`.

### Railway Environments API

Isolated project environments. Queries: `environment`, `environments`. Mutations: `environmentCreate`, `environmentDelete`, `environmentPatchCommitStage`.

### Railway Variables API

Service and environment configuration variables. Query: `variables`. Mutations: `variableUpsert`, `variableDelete`, `variableCollectionUpsert`.

### Railway Volumes API

Persistent volumes. Query: `volume`. Mutations: `volumeCreate`, `volumeUpdate`, `volumeDelete`, `volumeInstanceUpdate`.

### Railway Plugins API

Managed database add-ons (Postgres, MySQL, Redis, MongoDB). Query: `plugin`. Mutations: `pluginCreate`, `pluginUpdate`, `pluginRestart`, `pluginDelete`.

### Railway Custom Domains API

Attach custom and Railway-provided domains. Queries: `customDomain`, `domains`. Mutations: `customDomainCreate`, `customDomainDelete`, `serviceDomainCreate`.

### Railway TCP Proxies API

Expose a service over raw TCP. Query: `tcpProxies`. Mutations: `tcpProxyCreate`, `tcpProxyDelete`.

### Railway Usage and Metrics API

Read resource consumption and cost. Queries: `usage`, `estimatedUsage`, `metrics`.

### Railway Teams and Workspaces API

The authenticated account, its workspaces, teams, and members. Queries: `me`, `workspace`, `workspaces`. Mutations: `workspaceUpdate`, `teamMemberInvite`.

### Railway Webhooks API

Project webhooks for deployment status changes. Query: `projectWebhooks`. Mutations: `webhookCreate`, `webhookUpdate`, `webhookDelete`.

### Railway Logs API

Build, deployment, environment, and HTTP logs as both point-in-time queries (`buildLogs`, `deploymentLogs`, `environmentLogs`, `httpLogs`) and real-time GraphQL subscriptions over WebSocket. Modeled additionally as AsyncAPI at [`asyncapi/railway-app-asyncapi.yml`](asyncapi/railway-app-asyncapi.yml).

## Rate limits

The GraphQL Public API is rate limited per plan (requests per hour / requests per second): Trial 100 RPH, Hobby 1,000 RPH / 10 RPS, Pro 10,000 RPH / 50 RPS, Enterprise custom. Responses carry `X-RateLimit-*` headers; throttled requests return HTTP 429 with `Retry-After`. See [`rate-limits/railway-app-rate-limits.yml`](rate-limits/railway-app-rate-limits.yml).

## Pricing

Flat monthly subscription plus usage-based, per-second billing for vCPU (~$20/vCPU/mo), memory (~$10/GB/mo), network egress ($0.05/GB), and volume storage (~$0.15/GB/mo). Plans: Trial ($5 credit), Hobby ($5/mo), Pro ($20/seat/mo), Enterprise (custom). See [`plans/railway-app-plans-pricing.yml`](plans/railway-app-plans-pricing.yml) and [`finops/railway-app-finops.yml`](finops/railway-app-finops.yml).

## Common Properties

- [GitHub Organization](https://github.com/railwayapp)
- [LinkedIn](https://www.linkedin.com/company/railwayapp)
- [Website](https://railway.com/)
- [Documentation](https://docs.railway.com)
- [Plans](plans/railway-app-plans-pricing.yml)
- [Rate Limits](rate-limits/railway-app-rate-limits.yml)
- [Fin Ops](finops/railway-app-finops.yml)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
