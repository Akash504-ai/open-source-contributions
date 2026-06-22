# Open Source Contributions — Akash Santra

## [Strapi](https://strapi.io)

- Fixed RBAC authorization failures in `countDraftRelations` by implementing permission-aware populate handling, restoring correct entity-level access checks and preventing incorrect 403/UI errors.  
  PR: [#25977](https://github.com/strapi/strapi/pull/25977)

- Fixed OpenAPI route generation for plugins by correctly handling `router.prefix` and route-level prefixes, ensuring accurate API documentation paths.  
  PR: [#25616](https://github.com/strapi/strapi/pull/25616)

---

## [Supabase](https://supabase.com)

- Added validation requiring `replica_identity_index` when PostgreSQL `REPLICA IDENTITY` is configured as `INDEX`, preventing invalid SQL generation in `pg-meta`.  
  PR: [#45019](https://github.com/supabase/supabase/pull/45019)

- Fixed cross-schema index collisions in `pg-meta` by including schema-qualified joins for `pg_indexes`, ensuring accurate index metadata retrieval when duplicate index names exist across schemas.  
  PR: [#45374](https://github.com/supabase/supabase/pull/45374)

- Improved Supabase documentation by adding React quickstart error handling examples and standardizing Docker-related terminology across setup guides.  
  PR: [#45320](https://github.com/supabase/supabase/pull/45320)

  ---

## [Hugging Face Diffusers](https://huggingface.co/docs/diffusers/index)

- Fixed profiling decorator instance leakage in LTX2 pipelines by rebinding unbound methods correctly, preserving isolation across deep-copied components and preventing shared state bugs.  
  PR: [#13471](https://github.com/huggingface/diffusers/pull/13471)

---

## [Haystack (deepset-ai)](https://haystack.deepset.ai)

- Fixed malformed NVIDIA structured-output payload generation by correcting nested `extra_body` handling and migrating to `response_format`, restoring reliable JSON responses and test stability.  
  PR: [#3058](https://github.com/deepset-ai/haystack-core-integrations/pull/3058)

---

## [Future AGI](https://futureagi.com/)

- Fixed an authentication security flaw where revoked or expired API keys could still authenticate successfully. Added active-state validation in the API key authentication flow and comprehensive regression tests covering revoked and expired key scenarios, preventing unauthorized access and future regressions.

  PR: [#621](https://github.com/future-agi/future-agi/pull/621#event-26468550098)

---

## [Cal.com](https://cal.com)

- Fixed negative wait-time values in rate-limit error messages by clamping expired reset timestamps, improving API reliability and UX.  
  PR: [#28765](https://github.com/calcom/cal.com/pull/28765)

- Improved documentation clarity, grammar, formatting, and onboarding consistency across Cal.com/Cal.diy setup guides and README references, enhancing developer experience and readability.  
  PRs: [#28832](https://github.com/calcom/cal.com/pull/28832), [#29005](https://github.com/calcom/cal.diy/pull/29005)

- Fixed Event Type URL prefix alignment issues in the setup UI, improving visual consistency and interface polish.  
  PR: [#29000](https://github.com/calcom/cal.diy/pull/29000)

---

## [Mastra](https://mastra.ai)

* Implemented MCP server instruction forwarding into Agent system prompts, enabling Agents to automatically consume server-provided guidance with configurable opt-in controls, truncation limits, deterministic ordering, and comprehensive test coverage.

  PR: [#17155](https://github.com/mastra-ai/mastra/pull/17155#event-26159981593)

* Prevented indefinite e2e test hangs by adding timeout watchdogs and improved process cleanup/error handling for dev server startup flows.
  PR: [#14955](https://github.com/mastra-ai/mastra/pull/14955)

* Fixed PostgreSQL `jsonb` persistence failures by sanitizing invalid JSON escape sequences before workflow snapshot storage.
  PR: [#14692](https://github.com/mastra-ai/mastra/pull/14692)

* Added contiguous trimming mode to `TokenLimiterProcessor` to preserve conversational continuity and avoid fragmented LLM context windows.
  PR: [#14801](https://github.com/mastra-ai/mastra/pull/14801)

* Introduced configurable `minMessages` support for delayed title generation, improving title quality and reducing unnecessary LLM calls.
  PR: [#14778](https://github.com/mastra-ai/mastra/pull/14778)

* Fixed multipart upload handling in the Fastify adapter by properly resuming oversized file streams, preventing hanging requests and adding multipart integration tests.
  PR: [#15796](https://github.com/mastra-ai/mastra/pull/15796)

* Standardized adapter APIs around `registeredTools`, eliminating cross-adapter inconsistencies and preventing naming collisions with request payloads.
  PR: [#15635](https://github.com/mastra-ai/mastra/pull/15635)

* Added `tools` compatibility support to the Express adapter while preserving backward compatibility with existing `registeredTools` integrations.
  PR: [#15632](https://github.com/mastra-ai/mastra/pull/15632)

* Added test coverage for prefill error detection in PrefillErrorHandler, validating retry behavior for recognized plain Error instances and preventing future regressions.

  PR: [#18028](https://github.com/mastra-ai/mastra/pull/18028)

* Improved Mastra documentation consistency, formatting, grammar, CLI guidance, and Markdown/Vale setup instructions across README and contributor docs.
  PRs: [#15854](https://github.com/mastra-ai/mastra/pull/15854), [#15900](https://github.com/mastra-ai/mastra/pull/15900)

* Fixed OpenTelemetry export handling for `RAG_EMBEDDING` spans by mapping them to GenAI semantic conventions, exporting model/provider/usage metadata, preserving embedding-specific attributes, and enabling accurate embedding observability in downstream tools such as Langfuse.

  PR: [#17917](https://github.com/mastra-ai/mastra/pull/17917)

* Fixed semantic recall threshold handling in `Memory.recall()`, ensuring `semanticRecall.threshold` is consistently applied to vector search results and aligned with processor-based recall behavior. Added targeted regression tests covering filtering and threshold boundary conditions.

  PR: [#18211](https://github.com/mastra-ai/mastra/pull/18211)

* Added `listToolsWithErrors()` to MCPClient, enabling tool discovery with structured per-server error reporting while preserving backward compatibility with existing `listTools()` behavior. Included documentation and comprehensive test coverage for partial failures, retries, reconnect handling, and duplicate tool names.

  PR: [#18030](https://github.com/mastra-ai/mastra/pull/18030)
  
---

## [PostHog](https://posthog.com)

- Added missing DMARC TXT records to Domain Connect email verification templates, enabling successful automatic DNS configuration and fixing email verification failures for providers like Vercel and Cloudflare.  
  PR: [#54159](https://github.com/PostHog/posthog/pull/54159)

---

## [conda-forge](https://conda-forge.org)

- Fixed Windows `UnicodeDecodeError` issues in sidebar JSON parsing by explicitly enforcing UTF-8 encoding for documentation scripts.  
  PR: [#2800](https://github.com/conda-forge/conda-forge.github.io/pull/2800)

- Fixed UTF-8 decoding failures in documentation builds on Windows, improving cross-platform CI reliability.  
  PR: [#2799](https://github.com/conda-forge/conda-forge.github.io/pull/2799)

---

## [GeomScale / volesti](https://github.com/GeomScale/volesti)

- Improved build and execution documentation for the `hpolytope-volume` example with clearer CMake workflows and setup guidance.  
  PR: [#376](https://github.com/GeomScale/volesti/pull/376)
