# Railway (railway-app)

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
