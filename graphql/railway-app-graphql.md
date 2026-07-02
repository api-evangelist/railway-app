# Railway GraphQL Public API

Railway is a cloud application deployment platform (PaaS). Its entire programmatic surface is a **GraphQL API** - there is no REST API. The Public API is the same API that powers the Railway dashboard, and it lets you integrate Railway into CI/CD pipelines and other automation.

**HTTP endpoint (queries + mutations):** `https://backboard.railway.com/graphql/v2`
**WebSocket endpoint (subscriptions):** `wss://backboard.railway.com/graphql/v2`
**Documentation:** https://docs.railway.com/reference/public-api
**GraphQL overview:** https://docs.railway.com/integrations/api/graphql-overview

## Authentication

All requests are authenticated with a token created in the Railway dashboard. There are three token scopes:

| Token type | Scope | Header |
| --- | --- | --- |
| Account token | All resources across every workspace you belong to | `Authorization: Bearer <TOKEN>` |
| Workspace token | A single workspace | `Authorization: Bearer <TOKEN>` |
| Project token | A single project environment | `Project-Access-Token: <TOKEN>` |
| OAuth access token | User-granted permissions | `Authorization: Bearer <TOKEN>` |

## Transport reality

This is a GraphQL-first API. Every operation is an HTTP `POST` to the single `/graphql/v2` endpoint with a JSON body of the form `{ "query": "...", "variables": { ... } }`. Real-time log streams (build, deployment, environment) are delivered as **GraphQL subscriptions over WebSocket** (`graphql-ws`/`graphql-transport-ws`) at the `wss://` endpoint - this is how `railway logs` streams in the CLI and how tools like `railway-chord` egress logs.

## Example query - current user

```graphql
query {
  me {
    id
    name
    email
  }
}
```

## Example query - project with services

```graphql
query project($id: String!) {
  project(id: $id) {
    id
    name
    services {
      edges {
        node {
          id
          name
        }
      }
    }
    environments {
      edges {
        node {
          id
          name
        }
      }
    }
  }
}
```

## Example mutation - create a project

```graphql
mutation projectCreate($input: ProjectCreateInput!) {
  projectCreate(input: $input) {
    id
    name
  }
}
```

## Example mutation - deploy a service instance

```graphql
mutation serviceInstanceDeployV2($serviceId: String!, $environmentId: String!) {
  serviceInstanceDeployV2(serviceId: $serviceId, environmentId: $environmentId)
}
```

## Example mutation - upsert a variable

```graphql
mutation variableUpsert($input: VariableUpsertInput!) {
  variableUpsert(input: $input)
}
```

## Example subscription - stream deployment logs (WebSocket)

```graphql
subscription deploymentLogs($deploymentId: String!) {
  deploymentLogs(deploymentId: $deploymentId) {
    timestamp
    message
    severity
  }
}
```

## curl example

```bash
curl -X POST https://backboard.railway.com/graphql/v2 \
  -H "Authorization: Bearer $RAILWAY_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"query":"query { me { id name email } }"}'
```

- SDL schema fragment: [railway-app-schema.graphql](railway-app-schema.graphql)
- Repository: https://github.com/api-evangelist/railway-app
