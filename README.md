# Open Source Contributions — Akash Santra

## [Strapi](https://strapi.io)

- Fixed RBAC authorization failures in `countDraftRelations` by implementing permission-aware populate handling, restoring correct entity-level access checks and preventing incorrect 403/UI errors.  
  PR: [#25977](https://github.com/strapi/strapi/pull/25977)

- Fixed OpenAPI route generation for plugins by correctly handling `router.prefix` and route-level prefixes, ensuring accurate API documentation paths.  
  PR: [#25616](https://github.com/strapi/strapi/pull/25616)

---

## [Hugging Face Diffusers](https://huggingface.co/docs/diffusers/index)

- Fixed profiling decorator instance leakage in LTX2 pipelines by rebinding unbound methods correctly, preserving isolation across deep-copied components and preventing shared state bugs.  
  PR: [#13471](https://github.com/huggingface/diffusers/pull/13471)

---

## [Haystack (deepset-ai)](https://haystack.deepset.ai)

- Fixed malformed NVIDIA structured-output payload generation by correcting nested `extra_body` handling and migrating to `response_format`, restoring reliable JSON responses and test stability.  
  PR: [#3058](https://github.com/deepset-ai/haystack-core-integrations/pull/3058)

---

## [Cal.com](https://cal.com)

- Fixed negative wait-time values in rate-limit error messages by clamping expired reset timestamps, improving API reliability and UX.  
  PR: [#28765](https://github.com/calcom/cal.com/pull/28765)

- Improved Cal.com documentation clarity, formatting, and onboarding consistency across setup guides and environment configuration references.  
  PR: [#28832](https://github.com/calcom/cal.com/pull/28832)

- Fixed Event Type URL prefix alignment issues in the setup UI, improving visual consistency and interface polish.  
  PR: [#29000](https://github.com/calcom/cal.diy/pull/29000)

---

## [Mastra](https://mastra.ai)

- Prevented indefinite e2e test hangs by adding timeout watchdogs and improved process cleanup/error handling for dev server startup flows.  
  PR: [#14955](https://github.com/mastra-ai/mastra/pull/14955)

- Fixed PostgreSQL `jsonb` persistence failures by sanitizing invalid JSON escape sequences before workflow snapshot storage.  
  PR: [#14692](https://github.com/mastra-ai/mastra/pull/14692)

- Added contiguous trimming mode to `TokenLimiterProcessor` to preserve conversational continuity and avoid fragmented LLM context windows.  
  PR: [#14801](https://github.com/mastra-ai/mastra/pull/14801)

- Introduced configurable `minMessages` support for delayed title generation, improving title quality and reducing unnecessary LLM calls.  
  PR: [#14778](https://github.com/mastra-ai/mastra/pull/14778)

- Standardized adapter APIs around `registeredTools`, eliminating cross-adapter inconsistencies and preventing naming collisions with request payloads.  
  PR: [#15635](https://github.com/mastra-ai/mastra/pull/15635)

- Reverted Express adapter regression to maintain consistent `registeredTools` behavior across all framework adapters.  
  PR: [#15650](https://github.com/mastra-ai/mastra/pull/15650)

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
