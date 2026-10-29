# Steering: WebApi with Node.js and cache-data

Loads when JavaScript or TypeScript files are in use. Use it for Lambda functions behind API Gateway that are built on `@63klabs/cache-data`.

[View example steering: atlantis-webapi-node-cache-data.md](../../examples/steering/atlantis-webapi-node-cache-data.md)

What it covers:

- An MVC folder layout: `routes/`, `controllers/`, `services/`, `models/`, and `config/`.
- A thin handler that initializes config on cold start and calls `response.finalize()` once.
- Cached data access with `CacheableDataAccess`, plus `endpoint.send()` and `ApiRequest` for HTTP calls.
- Logging with `DebugAndLog` and keeping `template-openapi-spec.yml` up to date.

Use it as a starting point for new API functions. Existing functions that do not follow this layout will not match the rules, so apply them to new code first.
