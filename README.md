# WanAPIs (wanapis)

Developer-focused AI API gateway with an OpenAI-compatible endpoint. One API key gives access to GPT, Claude, Gemini, DeepSeek, image, video, and audio models behind a single unified surface — with a model marketplace (345+ models, 13+ vendors), usage logs, quota management, transparent metering, multi-channel routing, and failover.

**APIs.yml:** [apis.yml](apis.yml)

## Type
- **x-type:** company
- **submitted via:** [api-search/network#34](https://github.com/api-search/network/issues/34)

## APIs
- **WanAPIs Unified AI API** — `https://api.wanapis.com/v1` — OpenAI-compatible REST gateway aggregating GPT, Claude, Gemini, DeepSeek, plus image/video/audio model providers. [Docs](https://wanapis.com/docs) · [Model Marketplace](https://wanapis.com/model) · [Pricing](https://wanapis.com/pricing)

## Tags
LLM Gateway, AI API Gateway, OpenAI Compatible, Model Marketplace, LLM, GPT, Claude, Gemini, DeepSeek, Image Generation, Video Generation, Audio, Multimodal, Routing, Failover

## Common Properties
- [Website](https://wanapis.com/)
- [Documentation](https://wanapis.com/docs)
- [Model Marketplace](https://wanapis.com/model)
- [Pricing](https://wanapis.com/pricing)

## Artifacts

WanAPIs does not publish a machine-readable OpenAPI. `https://api.wanapis.com/openapi.json` returns the admin dashboard HTML. The artifacts below were hand-authored by API Evangelist from `https://wanapis.com/docs`, `https://wanapis.com/model`, and `https://wanapis.com/pricing`. They model the OpenAI-compatible surface that WanAPIs actually exposes plus the WanAPIs-native Responses and async task endpoints.

### OpenAPI
- [`openapi/wanapis-openapi.yml`](openapi/wanapis-openapi.yml) — OpenAPI 3.1 covering `/chat/completions`, `/responses`, `/completions`, `/embeddings`, `/images/generations`, `/images/edits`, `/audio/speech`, `/audio/transcriptions`, `/audio/translations`, `/models`, `/models/{model}`, `/tasks/{task_id}`. Bearer auth.

### Naftiko Capabilities
One self-contained capability per resource family. Each binds `WANAPIS_API_KEY`, consumes the upstream WanAPIs HTTP surface, and exposes both REST (`/v1/...`) and MCP adapters.
- [`capabilities/wanapis-chat.yaml`](capabilities/wanapis-chat.yaml)
- [`capabilities/wanapis-responses.yaml`](capabilities/wanapis-responses.yaml)
- [`capabilities/wanapis-completions.yaml`](capabilities/wanapis-completions.yaml)
- [`capabilities/wanapis-embeddings.yaml`](capabilities/wanapis-embeddings.yaml)
- [`capabilities/wanapis-images.yaml`](capabilities/wanapis-images.yaml)
- [`capabilities/wanapis-audio.yaml`](capabilities/wanapis-audio.yaml)
- [`capabilities/wanapis-models.yaml`](capabilities/wanapis-models.yaml)
- [`capabilities/wanapis-tasks.yaml`](capabilities/wanapis-tasks.yaml)

### JSON Schema
- [`json-schema/wanapis-chatcompletionrequest-schema.json`](json-schema/wanapis-chatcompletionrequest-schema.json)
- [`json-schema/wanapis-chatcompletionresponse-schema.json`](json-schema/wanapis-chatcompletionresponse-schema.json)
- [`json-schema/wanapis-chatmessage-schema.json`](json-schema/wanapis-chatmessage-schema.json)
- [`json-schema/wanapis-embeddingrequest-schema.json`](json-schema/wanapis-embeddingrequest-schema.json)
- [`json-schema/wanapis-imagerequest-schema.json`](json-schema/wanapis-imagerequest-schema.json)

### JSON-LD
- [`json-ld/wanapis-context.jsonld`](json-ld/wanapis-context.jsonld) — schema.org-aligned context for Model, Provider, Channel, ChatCompletion, Embedding, ImageGeneration, Task, Quota, etc.

### Examples
- [`examples/wanapis-chat-completion-example.json`](examples/wanapis-chat-completion-example.json) — chat completion against `claude-opus-4-7`.
- [`examples/wanapis-embedding-example.json`](examples/wanapis-embedding-example.json) — multi-input embedding call.
- [`examples/wanapis-image-generation-example.json`](examples/wanapis-image-generation-example.json) — DALL·E-3 image generation.

### Governance
- [`rules/wanapis-rules.yml`](rules/wanapis-rules.yml) — Spectral ruleset (OAS 3.1) enforcing base URL, bearer auth, operationId casing, and OpenAI-compatible request shape conventions.
- [`vocabulary/wanapis-vocabulary.yml`](vocabulary/wanapis-vocabulary.yml) — domain vocabulary (Gateway, Provider, Model, Channel, Quota, Failover, Metering, Task, Webhook Callback, ...).

### Commercial
- [`plans/wanapis-plans-pricing.yml`](plans/wanapis-plans-pricing.yml) — pay-as-you-go per-model token pricing, $0.20 welcome credit. `reconciled: false` — rates change per upstream vendor.
- [`rate-limits/wanapis-rate-limits.yml`](rate-limits/wanapis-rate-limits.yml) — 429/503 guidance and quota model. `reconciled: false`.
- [`finops/wanapis-finops.yml`](finops/wanapis-finops.yml) — FOCUS 1.3-aligned FinOps view with per-model token meters, cache-hit, image, audio, balance-topup, and request-count meters.

## Notes
- WanAPIs is OpenAI-compatible: any official OpenAI SDK works by setting `base_url=https://api.wanapis.com/v1` and `api_key=<wanapis_key>`.
- All inference endpoints use `Authorization: Bearer <wanapis_api_key>`.
- Long-running image/video/audio jobs may return a `task_id`; poll `/tasks/{task_id}` or configure a webhook callback.
- Per-model pricing is dynamic. Always reconcile against [https://wanapis.com/pricing](https://wanapis.com/pricing) before billing decisions.

## Timestamps
- **Created:** 2026-05-27
- **Modified:** 2026-05-27

## Maintainers
- **Kin Lane** — kin@apievangelist.com
