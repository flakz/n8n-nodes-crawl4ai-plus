# Changelog

## 5.2.2

### Changed

- **README**: Added "What's New" section at top for npm visibility

## 5.2.1

### Changed

- **README**: Documented Custom (OpenAI-Compatible) provider setup and how it works with litellm

## 5.2.0

### Fixed

- **Custom LLM provider support**: Replaced broken `opencode` and `LiteLLM/Custom` provider options with a single **Custom (OpenAI-Compatible)** option. The previous options failed because litellm validates provider prefixes against its internal registry and rejects unknown providers like `opencode/` and `llm7/` — even when `base_url` is provided.
- **OpenRouter base URL**: Fixed copy-paste bug where OpenRouter was incorrectly using the Ollama URL as its base URL fallback instead of `https://openrouter.ai/api/v1`.

### How the fix works

The Custom option uses litellm's `openai/` provider prefix with a custom `base_url`. litellm recognizes `openai/` as a first-class provider and routes requests to the custom endpoint instead of `api.openai.com`. This works with any OpenAI-compatible API (LLM7, OpenCode, Together AI, Fireworks, etc.).

### Migration

If you were using the **OpenCode** or **LiteLLM/Custom** provider options:
1. Set **LLM Provider** to **Custom (OpenAI-Compatible)**
2. Enter your API's base URL (e.g. `https://api.llm7.ai/v1`)
3. Enter your model name (e.g. `mistral-7b`)
4. Enter your API key (optional)

## 5.1.0

### Added

- **AI Tools node** (`Crawl4aiPlusAiTools`): New node exposing Crawl4AI as AI tools for n8n AI Agent and MCP Trigger. Supports 7 operations: crawl, askQuestion, extractWithLlm, extractWithCss, extractSeo, discoverLinks, healthCheck.
- **Shared SEO helpers** (`nodes/shared/seo-helpers.ts`): Extracted `SEO_FIELDS`, `extractJsonLd()`, `extractHreflang()`, `extractHead()` from `seoExtractor.operation.ts` for reuse across nodes.

## 5.0.1

### Fixed

- **Credential validation**: Added `test` property (health endpoint check) and `icon` (SVG) to credential class, fixing lint errors that blocked publishing
- **Type safety**: Replaced ~55 `any` types across shared code and all operation files with proper types (`unknown`, `Record<string, unknown>`, `IDataObject`, `AxiosResponse`, `Link[]`, etc.)
- **Unused variables**: Removed unused `context` parameter from `parseApiError()`, fixed unused `error` bindings in catch blocks, suppressed interface-required `_nodeOptions` params
- **Stale lint directives**: Removed 9 unused `eslint-disable` comments and fixed `as any` cast in `operations.ts`
- **Cloud support**: Disabled n8n Cloud compatibility checks (node requires axios for Docker REST API communication, inherently incompatible with n8n Cloud)

## 5.0.0

Major rewrite — see CLAUDE.md for full architecture documentation.
