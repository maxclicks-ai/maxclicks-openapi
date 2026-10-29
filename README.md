# maxclicks-openapi

The official [OpenAPI 3.1](https://spec.openapis.org/oas/v3.1.0) specification for the [maxclicks](https://maxclicks.ai) Public API v1.

`openapi.yaml` is the single source of truth for the public REST contract: every endpoint, request and response shape, error, and rate limit. It is the reference behind the official SDKs and the developer docs.

## Contents

- [`openapi.yaml`](openapi.yaml) : the specification (source of truth, hand maintained against the API server).

## Using it

```bash
npm install

npm run lint         # validate the spec (Redocly)
npm run bundle       # bundle to dist/openapi.yaml
npm run bundle:json  # bundle to dist/openapi.json
npm run preview      # interactive reference docs
npm run build-docs   # static reference docs to dist/index.html
```

Point any OpenAPI tool at `openapi.yaml`: generate a client, import into Postman or Insomnia, or render reference docs.

## The API in one screen

- Base URL: `https://api.maxclicks.ai/v1` (production), `https://api-stage.maxclicks.ai/v1` (staging).
- Auth: `Authorization: Bearer <api_key or OAuth access token>` on every endpoint except the public form and email actions. OAuth clients discover the authorization server at `https://api.maxclicks.ai/.well-known/oauth-authorization-server` (dynamic registration, PKCE S256).
- Success envelope: `{ "data": ... }` (plus an optional `warnings` array). Lists add `pagination`.
- Error envelope: `{ "error": { "type", "code", "message" } }`.
- Pagination: `limit` (default 50, max 200) and `offset` (default 0, max 10000).
- Rate limits, per API key: 100 reads/second, 25 writes/second.

## Keeping it accurate

The spec is hand maintained to match the API server (`server/src/modules/Server/Public/v1`). When an endpoint, field, error code, or limit changes there, update `openapi.yaml` in the same change and re run `npm run lint`.

## License

MIT
