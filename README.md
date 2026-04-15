# Open Source Contributions – Akash Santra

## Strapi

### 1. RBAC Fix in `countDraftRelations`
**PR:** https://github.com/strapi/strapi/pull/25977  
**Status:** Merged

**Problem**  
`countDraftRelations` used `populate: {}`, preventing RBAC conditions (e.g., "same as creator", "same role") from evaluating correctly. This caused incorrect 403 errors and UI failures.

**Solution**  
- Replaced static populate with RBAC-aware populate using `populate-builder`
- Integrated `permissionChecker.sanitizedQuery` to derive permission-based query
- Aligned logic with existing controllers (`findOne`, `update`)

**Impact**  
- Fixed incorrect authorization failures  
- Eliminated user-facing errors in content manager  
- Restored correct RBAC behavior in production workflows  

**Tests Added**  
- Verified populate is derived from permission query  
- Covered:
  - Successful flow
  - Full permission denial (403)
  - Entity not found (404)
  - Entity-level RBAC failure
  - Cases where entity loading is skipped  

### 2. OpenAPI Plugin Route Prefix Fix
**PR:** https://github.com/strapi/strapi/pull/25616  
**Status:** Merged

**Problem**  
OpenAPI generator ignored `router.prefix`, causing plugin routes (e.g., upload) to be generated under incorrect paths (`/` instead of `/upload`).

**Solution**  
- Merged `router.prefix` with `route.path`
- Respected `config.prefix` at route level when present
- Normalized paths to prevent duplicate/trailing slashes
- Improved type safety using `Core.Router`

**Impact**  
- Corrected OpenAPI specifications for plugin routes  
- Ensured accurate API documentation generation  
- Prevented incorrect endpoint mapping in downstream usage  

**Tests Added**  
- Router prefix handling  
- Route-level prefix override  
- Mixed prefix scenarios  
- No-prefix edge cases

---

## Hugging Face Diffusers

### 1. Profiling Decorator Instance Isolation Fix
**PR:** https://github.com/huggingface/diffusers/pull/13471  
**Status:** Merged

**Problem**  
Profiling decorators were wrapping bound methods, capturing the original `self` instance inside the closure. When components (e.g., schedulers) were deep-copied, the wrapped methods still referenced the original instance, causing shared state and incorrect behavior.

**Solution**  
- Extracted the underlying function using `__func__`
- Applied the decorator to the unbound function
- Rebound the method to the instance using `__get__`
- Scoped the fix specifically to LTX2 pipelines to keep the change minimal and safe

**Impact**  
- Preserved instance isolation across deep-copied components  
- Prevented shared state bugs in multi-component pipelines  
- Avoided potential runtime inconsistencies in profiling workflows  

**Validation**  
- Verified using deepcopy-based test to ensure isolated state per instance  
- Ensured no class-level modifications or side effects

---

## Haystack (deepset-ai)

### 1. NVIDIA Structured Output Syntax Fix
**PR:** https://github.com/deepset-ai/haystack-core-integrations/pull/3058  
**Status:** Merged

**Problem**  
The `guided_json` schema was incorrectly nested inside `generation_kwargs["extra_body"]`, producing malformed payloads like:

{
  "extra_body": {
    "extra_body": {
      "guided_json": {...}
    }
  }
}

This caused the NVIDIA API to ignore the schema and return non-JSON output, leading to `JSONDecodeError` in tests.

**Solution**  
- Flattened nested `extra_body` before API calls  
- Migrated from deprecated `guided_json` to the newer `response_format` schema  
- Applied fix consistently in both `run` and `run_async`  
- Used explicit parent class calls instead of `super()` to avoid decorator-related issues  

**Impact**  
- Restored correct structured JSON output from NVIDIA models  
- Fixed failing integration tests and improved reliability  
- Ensured compatibility with updated NVIDIA API standards  

**Validation**  
- Ran full NVIDIA integration test suite:  
  - 180 tests passed  
  - 17 skipped (expected live tests)  
- Verified correct JSON parsing from model responses

---

## Cal.com

### 1. Rate Limit Negative Wait Time Fix
**PR:** https://github.com/calcom/cal.com/pull/28765  
**Status:** Merged

**Problem**  
Rate limit error messages could display negative wait times when the reset timestamp was already in the past, resulting in incorrect outputs like:

"Rate limit exceeded. Try again in -5 seconds."

**Solution**  
- Clamped computed wait time to a minimum of 0  
- Ensured consistent and user-friendly error messaging  

**Impact**  
- Eliminated incorrect negative values in error messages  
- Improved API reliability and user experience  
- Prevented confusion in rate limit handling  

**Validation**  
- Simulated rate limiter response with expired reset timestamp  
- Verified error message always shows non-negative values  

### 2. Documentation Improvements
**PR:** https://github.com/calcom/cal.com/pull/28832  
**Status:** Merged

**Changes**  
- Fixed grammar and formatting issues across documentation  
- Improved clarity in setup instructions  
- Standardized naming (e.g., Cal.com)  
- Enhanced readability of `.env` references  

**Impact**  
- Improved developer onboarding experience  
- Increased clarity and consistency in documentation  

**Validation**  
- Reviewed updated documentation files for correctness and readability

---

## Mastra (mastra-ai)

### 1. Prevent E2E Dev Server Hang
**PR:** https://github.com/mastra-ai/mastra/pull/14955  
**Status:** Merged

**Problem**  
Dev server startup in e2e tests relied only on stdout/stderr signals. If the server failed silently, tests could hang indefinitely.

**Solution**  
- Added timeout fallback (watchdog timer)  
- Ensured proper cleanup on resolve/reject  
- Improved error detection logic  
- Used explicit `SIGTERM` for process termination  

**Impact**  
- Eliminated infinite test hangs  
- Improved reliability of CI pipelines  
- Ensured deterministic test behavior  

### 2. PostgreSQL JSON Escape Sanitization
**PR:** https://github.com/mastra-ai/mastra/pull/14692  
**Status:** Merged

**Problem**  
Invalid JSON escape sequences (e.g., `\v`, `\k`, `\u0000`) caused PostgreSQL `jsonb` operations to fail when storing workflow snapshots.

**Solution**  
- Escaped invalid backslash sequences safely  
- Removed problematic null/unicode sequences  
- Preserved valid JSON content  

**Impact**  
- Prevented database write failures  
- Improved reliability of workflow persistence  
- Ensured compatibility with PostgreSQL JSON parsing  

**Tests Added**  
- Verified sanitization preserves valid escapes  
- Ensured null characters are removed before persistence  

### 3. Contiguous Trimming Mode for TokenLimiterProcessor
**PR:** https://github.com/mastra-ai/mastra/pull/14801  
**Status:** Merged

**Problem**  
Default token trimming strategy ("best-fit") could skip messages, breaking conversational continuity.

**Solution**  
- Added new `trimMode: "contiguous"` option  
- Stops at first message exceeding token budget  
- Preserves continuous suffix of conversation  

**Impact**  
- Improved LLM context consistency  
- Avoided fragmented conversation history  
- Gave developers control over trimming strategy  

### 4. `minMessages` Option for Title Generation
**PR:** https://github.com/mastra-ai/mastra/pull/14778  
**Status:** Merged

**Problem**  
Titles were generated on the first message, often resulting in generic or duplicate titles.

**Solution**  
- Introduced `minMessages` configuration  
- Delays title generation until threshold is met  
- Applied across modern and legacy agent flows  

**Impact**  
- Improved quality of generated titles  
- Reduced unnecessary LLM calls  
- Enhanced user experience in chat workflows  

## conda-forge

### 1. Fix UnicodeDecodeError in Sidebar JSON Parsing
**PR:** https://github.com/conda-forge/conda-forge.github.io/pull/2800  
**Status:** Merged

**Problem**  
Reading `_sidebar*.json` files without specifying encoding caused `UnicodeDecodeError` on Windows due to default `cp1252` encoding, while files were UTF-8 encoded.

**Solution**  
- Explicitly set file encoding to UTF-8 when reading sidebar JSON files  

**Impact**  
- Ensured consistent cross-platform behavior  
- Prevented decoding errors in CI and local environments  
- Improved reliability of documentation scripts  

**Validation**  
- Verified `.ci_scripts/check_sidebars.py` runs without errors on Windows  

### 2. Fix UnicodeDecodeError in Documentation Build
**PR:** https://github.com/conda-forge/conda-forge.github.io/pull/2799  
**Status:** Merged

**Problem**  
CFEP markdown files encoded in UTF-8 caused decoding errors during documentation builds on Windows due to default `cp1252` encoding.

**Solution**  
- Explicitly specified UTF-8 encoding when reading CFEP files  

**Impact**  
- Fixed documentation build failures on Windows  
- Improved developer experience across platforms  
- Ensured consistent encoding handling in CI scripts  

**Validation**  
- Verified `.ci_scripts/update_docs` runs successfully after fix

---

## GeomScale (volesti)

### 1. Improve Build and Run Instructions for hpolytope-volume Example
**PR:** https://github.com/GeomScale/volesti/pull/376  
**Status:** Merged

**Problem**  
Build and run instructions for the `hpolytope-volume` example were unclear and required manual configuration, making it difficult for new users to get started.

**Solution**  
- Added explanation of the example’s purpose  
- Updated build process to use recommended out-of-source CMake workflow  
- Documented optional configuration for local `lp_solve` installation  
- Provided clear steps to run the example after compilation  

**Impact**  
- Improved developer onboarding experience  
- Reduced setup complexity for first-time users  
- Aligned documentation with best practices  

**Validation**  
- Verified build and execution steps work with updated instructions

---
