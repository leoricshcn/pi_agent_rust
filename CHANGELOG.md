# Changelog

All notable changes to **pi_agent_rust** are documented here.

Versions marked **Release** have published binaries on GitHub. Versions marked
**Tag-only** exist as git tags without a GitHub Release (no downloadable
binaries). Versions marked **Draft** have an unpublished draft release.

Repository: <https://github.com/Dicklesworthstone/pi_agent_rust>

---

## [Unreleased] (after v0.1.9)

105 commits since v0.1.9 (2026-03-12 through 2026-03-21).

### New Model Definitions

- Add built-in model entries for GPT-5.2 Codex, Gemini 2.5 Pro CLI, and Gemini 3 Flash ([`43ddc6f`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/43ddc6f0305fcc22dc574d90dc725572e00a9d29)).

### Auth & Configuration

- Support `$ENV:` prefix in `auth.json` for env-var-backed API keys ([`266be4c`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/266be4c4774949bc707c2095e6d57ee36d6940dc)).
- Fix OAuth callback protocol violations, including RFC 6749 Section 4.1.3 `redirect_uri` compliance ([`d264bb8`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/d264bb8e31d5e04a89f20b606b7e9ca8ee2865d6)).
- Random-port OAuth callback server, viewport scroll clipping fix ([`bda35a4`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/bda35a46ed328c58128fe8da4ed2b892e729822b)).
- Async Kimi OAuth flow, theme picker caching, session index offloading ([`943085f`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/943085f6fe3e1c6e5d2c89e5c8bc2e254c8a5bab)).

### Security & Reliability (fail-closed hardening)

- Fail closed on invalid extension manifests, package manifests, and hostcall reactor configs ([`028be33`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/028be3308e81ede7a793dbc98d1db26c2560b3e8), [`ebffa82`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/ebffa82ff9378c7fac14d95c0c5f4e1f8d03d6da), [`7b0a0b6`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/7b0a0b67e67067061948f03b3d382f3fe199f3d6)).
- Cap `randomBytes` native hostcall to prevent OOM-based DoS; use `sync_channel` for RPC stdout backpressure ([`c5afccf`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/c5afccf553d4bc2ce1da6f93cb6100ecc58cb1d0)).
- Prevent DoS vectors via unbounded thread creation and indefinite stream blocking ([`a7ecaa3`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/a7ecaa306caeeb7e4aff76a653c9ec7ee3ffbd59)).
- Cap WASM `extract_bytes` pre-allocation to prevent OOM on large arrays ([`95d4128`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/95d4128d7a5887683e488d5a91a18d043095224c)).
- Share WASM virtual files via `Arc` to fix OOM from cloning ([`61b400b`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/61b400b9f86decc6b66a069dc8ecded87f712dba)).

### Session & Extension Stability

- Prune stale session index rows when project directories disappear ([`d8bc4f4`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/d8bc4f44337ea00d8ec1bafef96472d43ca0704c)).
- Harden SessionStoreV2 newline-heal rebuild path ([`0ee28af`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/0ee28af45a60ce72860200821bbccfa3fa5c2c88)).
- Fix exec wrapper double-buffering that lost stdout/stderr on close ([`fc1f91f`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/fc1f91fd0ec61b28dac0b01c6e0b9cf7a4c2c476)).
- Normalize hosted git SSH provenance refs and repository shorthands ([`53f80eb`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/53f80eb30bc56c93d02f83ebfb8c8ba2b3157473)).
- Resolve O(N^2) string concatenations in polyfills and WASM memory cloning ([`ec1dfeb`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/ec1dfeba2f0e22ef5dc2a549ee8dfcbd4f213fa7)).

### Tools & Interactive

- Enable grep/find/ls by default; document all 8 built-in tools ([`7fc5cc5`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/7fc5cc520458993a0f4c6858da6c14c7753f5d97)).
- Embed changelog into compiled binary ([`c3385cb`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/c3385cb0eb87cdab45252be3156ae0f8607f8d03)).
- Expand extension stress testing, tool dispatch, and tree view ([`fcf99ca`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/fcf99cad08e3021c96998ded5d02be91e3e57565)).
- Allow empty keybinding overrides to unbind defaults ([`60d63a6`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/60d63a678302e72a463f06e553e08987904312ab)).

### Providers

- Avoid duplicating first string stream delta ([`c354a0c`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/c354a0ccf2b426139c0156ed273d966e1dfec2da)).
- Honor native adapter defaults and sync session connector channel ([`e65dcad`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/e65dcadc6034d6b79d0bec4345fff6b39ec6c08b)).
- Handle `cannot_be_a_base` URLs gracefully in all provider URL normalizers ([`8ad4f90`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/8ad4f90e71a165314ea0cb77434b7e161c8d53cf)).

### HTTP Stack

- Harden Transfer-Encoding aggregation, reject unsupported transfer-coding chains ([`b613709`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/b613709f6d5d878313f78e68bec9163353dad19a), [`184a2a6`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/184a2a6e8bf331d2d950b19e7d4fcaad3ff3e22c)).
- Tolerate bare-LF line endings in chunked transfer encoding ([`d1e7166`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/d1e71664d0603089cc5fc4a6210abf0efb3cddaf)).
- Drop caller-supplied `Transfer-Encoding` header ([`b3625e2`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/b3625e256e264a35947c7772c0fce7cf62aebaba)).

### Performance

- Batch session entry inserts in chunks of 200 for SQLite ([`86368c2`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/86368c203f9f400d0ab7f217b99a9a0b641cf4a9)).
- Skip resource resolution when all categories disabled; deduplicate cached extension entries ([`996dcf3`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/996dcf3c63f0b6b0aa9d70e467b27b344d186119)).

### CI

- Harden ARM64 Linux release build ([`aef5fb8`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/aef5fb8323bac64ede978fbccf9f7bcd08b54b97)).
- Remove submodules boolean that broke checkout in all build jobs ([`7bee5ed`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/7bee5edc70e63a008f824b724859af96e7a85b49)).

---

## [v0.1.9](https://github.com/Dicklesworthstone/pi_agent_rust/releases/tag/v0.1.9) -- 2026-03-12 (Release)

348 commits. Largest release to date, spanning 12 days of multi-agent development.

### Asupersync Migration (Epic bd-xdcrh)

- Migrate compaction worker from `std` threads to asupersync runtime ([`009c97b`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/009c97ba43ce4c7a1ed0c3e8eff6d67a07e7d6f9)).
- Propagate asupersync `Cx` through RPC, agent, interactive, and session layers ([`d3211c9`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/d3211c97e0fd8c02f6d3c0a85c4da4bca4a8e68b)).
- Migrate `Session` save-path metadata and `GrepTool` `fs::metadata` to async filesystem ([`8179452`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/8179452679050c7cdec9f8dbb16b50df9e5e1fe4), [`2a36d88`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/2a36d88286fda6cf30d11a6f0e59d8a62cf2a58a)).
- Add binary body support to fetch shim; expand asupersync coverage in tools/resources/package_manager ([`2edd6c8`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/2edd6c84c9eb2d0cb0aea8f6aca0da8e4b5d520c)).

### Session Store & Persistence

- V2 sidecar staleness detection with JSONL rehydration fallback and cross-format chain hash verification ([`7d0cc00`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/7d0cc0002cffb6a09c7c87c38ea3f4e958a36fa3)).
- Atomic sidecar rebuild with staging/backup swap and trash-based deletion ([`e578369`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/e578369234cdac3f6e42c3e90c93f5b0ad4a1ddc)).
- Honor SQLite WAL sidecars in metadata and deletion ([`5239849`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/5239849c46b05c71e5c79f4b54a72b4e98c6e43b)).
- Cache segment file descriptors, guard shutdown flush, filter session-index files ([`e9aad24`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/e9aad2408a7316b5b447cb7baf5b3aa924aee480)).
- Heal missing-newline JSONL frames instead of truncating segment data ([`217e253`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/217e253ca1bc2e34057db821b7fe01340963ad84)).
- Preserve existing session name when upsert value is null ([`dd62452`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/dd6245265b8d463ac174d21c30c1e6d0fa80cf69)).

### Interactive TUI

- Custom extension overlay rendering, input capture, and lifecycle management ([`da1669e`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/da1669e41df10830d8d39f8362c78a84bd13161c)).
- Custom UI hostcall for extension-driven interactive overlays ([`dd5d450`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/dd5d4503aa891b74ba9c642784f4dee8d28ce3d4)).
- Preserve scroll offset across viewport content updates ([`178408c`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/178408cf8bd53182ca175c4f3ce2df90c2378741)).
- Scope tmux mouse-wheel override to current pane; traverse parent dirs for git HEAD ([`60fe95e`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/60fe95ee70bbeff1f00be8c2fd01e9ff2fbf8b70)).
- Pause terminal UI before launching external editor ([`0d19b81`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/0d19b8181720ec4e9016890207320c4f9c86091d)).
- Handle agent-busy state gracefully in tree navigation and branch picker ([`66e2c89`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/66e2c89b447f986eaccf295fa3a25dfc3b845ae6)).

### Security Hardening

- Path traversal guards in EditTool and WriteTool ([`4390667`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/4390667e3a878cb62238ec27b95c110c4d5eac37)).
- Scope extension filesystem access by extension ID; harden path traversal controls ([`4d6ab94`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/4d6ab94a48b7d2a4c99b2c3ff85f97d2c8b40e2e)).
- Thread `extension_id` through `FsConnector` for per-extension policy ([`4b6f268`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/4b6f26844f11f8aa97fcd2076fb4e8189281b852)).
- Eliminate TOCTOU race in device ID file creation ([`dfdafd7`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/dfdafd701fc4c18060bf5a74ea4d91f8de46ea7d)).
- TOCTOU path traversal fix in extension module resolver ([`930c9c1`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/930c9c170a8e38dd1fca54878a2322b21dc22d4d)).
- Make `auth.json` write crash-safe by padding before truncation ([`2ca7a37`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/2ca7a37abc5943719e155d4809f89ac039d7213e)).
- Enforce `READ_TOOL_MAX_BYTES` limit in extension host file reads ([`0b6c1a6`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/0b6c1a64255497b4405cd60de35a0dc7f011e22e)).

### HTTP Stack

- Validate Content-Length headers; reject malformed or conflicting values per RFC 9110 ([`c25efc6`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/c25efc65d9e4b01bb70ed8a8fd2c3674f85b630c)).
- Handle coalesced Content-Length headers per RFC 9110 ([`4dbd0d4`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/4dbd0d43de5457de62a022db1937d869eb800643)).
- Treat 1xx/204/205/304 responses as empty-body per RFC 9110 ([`6e6c123`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/6e6c12344fd00f9313c7ae537f670d07ccecf243)).
- `write_all_with_retry` to handle transient `Ok(0)` from TLS transports ([`7722a14`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/7722a148d471003863ee3b9049dfa7e3c26d9df5)).

### Providers

- Parse cached token count from OpenAI streaming responses ([`e70b2a4`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/e70b2a4dda46cc06b2d8c69dbb5723ccb491c3b0)).
- Normalize bare official OpenAI/Cohere origins to `/v1` endpoints; always persist thinking level ([`7145c6e`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/7145c6eab3e3a7d99f1b036a6a349b5754da5c0b)).
- Force temperature to 1.0 when Anthropic extended thinking is enabled ([`a6e008a`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/a6e008aabcd9138402f2e736012ff93d72a1fe2d)).
- Atomicize model/thinking-level management with session header sync and deduplication ([`720dc56`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/720dc56a1d6c53a0a5f9cffe59e5fba81c48f4f3)).
- Local OAuth callback server for browser redirect capture ([`bf3ac72`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/bf3ac726b705350a9d49dbc3a703328d8e8b7765)).

### Permissions & Extensions

- Stabilize JSON serialization order for deterministic permission diffs ([`3537b9c`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/3537b9cf9cff6c0e3b23c11ae71a93e7a8be89f0)).
- Schema version validation and timestamp-aware permission expiry checking ([`42b2c7d`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/42b2c7d9bc7cf0b4e3a7b3f5ab18cc0f23b33a3d)).
- Preserve runtime IDs for extension permission cache ([`08922e4`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/08922e45a7e29f4b5e2aab22b09fb6c0f70d3b5a)).
- Replace hand-rolled semver parser with `semver` crate for correct pre-release ordering ([`add7336`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/add73369e9be0bec93eb4acb0ba78d6b56a8d1b8)).
- Extract `safe_canonicalize` to deduplicate path validation ([`6cd8211`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/6cd82114eb26bf3c7a24a56c16b21d76b20e1cdb)).

### VCR Test Infrastructure

- Redact sensitive form bodies and normalized text request bodies in cassettes ([`7d929dd`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/7d929dd4ec0b15b14dfe3ef3f6e2e3a4cbbbe73e), [`ae24ad4`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/ae24ad4c8a8a7f21c74e854b5e6e88e4f8f2b6fb)).
- Distinguish absent vs explicitly-unset env var overrides in test helpers ([`421ad64`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/421ad641b1f31d8b6b42d3e6e1baeef97c93a1e0)).
- Recover poisoned env override lookups ([`babd3cd`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/babd3cde7fd3a2a72ee23cf7f89ae9bd2a7b9ef5)).
- Fail closed on zero-baseline telemetry ([`eae5a87`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/eae5a877e7f1c21f6e03e74dbbdce88d84d6a2e0)).

### Performance

- Cache canonicalized extension roots; eliminate redundant `safe_canonicalize()` calls on every path check ([`4811dda`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/4811ddad23e5698e25152fe271705dfa2d6c4afe), [`7ebe734`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/7ebe734aff802d659ef8b91169f8b3365a2fb98e)).
- Genericize model table rendering to avoid intermediate allocations ([`89e6637`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/89e66376b65d6db8b3f6eff70fb1c07e18d0fc4e)).

### Bug Fixes

- Prevent panic on `fill_buf` error during segment recovery ([`1953deb`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/1953debc56e5148f9b0ec268ddff703e46039efe)).
- Resolve RwLock poison panic, fix theme syntax error, fix `revert_last_user_message` context duplication ([`e119767`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/e11976e739ebd9573320433b3b341c0e2e4d7261)).
- Replace mutex `.unwrap()` / `.expect()` with poison-resilient recovery across codebase ([`9ff39b0`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/9ff39b0fb09dff8f531e9c285c3d3e725440ba49)).
- Scheduler timer ID allocation rewrite with uniform wrap-around and exhaustion detection ([`923a05e`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/923a05e02402b1085565665ba86623dab18fb1e9)).
- Cycle detection in process tree traversal to prevent stack overflow ([`6aead21`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/6aead21fd6f2619f8e92dc9631a7ea257e13f539)).
- SSE: reset event state on empty lines without data to prevent stale field leakage ([`80bf530`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/80bf530baf4838ed1027b12005dd13123b7ec015)).
- Persist messages before error propagation to prevent data loss on failures ([`b3cac70`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/b3cac706b4b100b3ff57375751f325cde696bdad)).
- Send `UiShutdown` event to unblock async bridge after TUI exits ([`bc645f0`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/bc645f03dbb6b6c28f02c5f2bbb06f1fdd14c5c5)).

### CI

- Use `macos-15-intel` runner for x86_64 Darwin builds (deprecation of `macos-13`) ([`11c8e6a`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/11c8e6aea625f9cf04dbe1c47257f61f89392b0b)).

---

## [v0.1.8](https://github.com/Dicklesworthstone/pi_agent_rust/releases/tag/v0.1.8) -- 2026-02-28 (Release)

144 commits. Major feature release: HashlineEditTool, image support in tool results, per-model reasoning detection, and a security hardening pass.

### New Tools

- **HashlineEditTool**: Line-addressed file editing tool with hashline output mode, enabled in default tool set ([`0b1baad`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/0b1baada82ffe79e59eea12e57b77dc8e4dea18f), [`72d8125`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/72d8125dd7ff71b0314d879df56df3a0ba1511d3), [`c947acc`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/c947accc9adbf249ab62119edbdb64f04fc346b5)).
- GrepTool hashline output mode for line-hash-addressed references ([`72d8125`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/72d8125dd7ff71b0314d879df56df3a0ba1511d3)).

### Provider Enhancements

- Support image content in tool results for Azure and Bedrock ([`35ed28b`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/35ed28ba7299550799511caf9a6cd97151c59e24)).
- Per-model reasoning detection for DeepSeek, Mistral, Llama, Claude 3 variants, Gemini variants, QwQ ([`06595fe`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/06595fea7e1a9f3ee4c8d0f10be5d6d7bd6c1ddc), [`0189ed4`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/0189ed4897ccbd7ebceb1b85f4a2d48a2e1cd17f)).
- Consolidated `model_is_reasoning` function replacing scattered checks ([`b88817b`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/b88817ba73e6fa9c6908da9d781efe66840f65b2)).
- Canonical provider preference and deterministic model sorting ([`f799a7b`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/f799a7b1b0d8a88f2b29ceae0e3e2d7d4f3f11d2)).
- Accumulate streaming tool call deltas instead of overwriting ([`3df7373`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/3df7373cbf102b1f53aaf9cd86435c83b22ea6fd)).
- `--hide-cwd-in-prompt` CLI flag ([`37f8361`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/37f83618f29cb0cc8f3a18dcbf6b7e6c7a4dc5a6)).

### Security

- `0o600` permissions on migrated `auth.json` and session files ([`4dafcd9`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/4dafcd9565e466d044e9d16b6bdd7f8d0b285842), [`6ec4ac2`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/6ec4ac22f3b911a8488172952a506cdf901adb73)).
- Shared file locks for auth reads ([`6ec4ac2`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/6ec4ac22f3b911a8488172952a506cdf901adb73)).
- Prevent zero-filled output on `getrandom` failure in crypto shim ([`96f8187`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/96f818729009493c2fcb8fbcd5d52cbcf0c43fb4)).
- Use `subarray` for `Buffer.slice` and `getrandom` for crypto randomness ([`6cdfbbe`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/6cdfbbe1bd56bd7185b7ddab7dc8452c3a0791ee)).

### Tools & Editor

- `sync_all()` before atomic renames for crash safety ([`eaa63b3`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/eaa63b3c28913cd692818a79645c51a1d3888669)).
- Canonicalize file paths in EditTool/WriteTool; harden GrepTool match iteration ([`e6c7fdb`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/e6c7fdb9c1b9f5c3aac5e0c7a6d7a70c2e79d3be)).
- CRLF idempotency fix, redundant counter removal, div-by-zero guard in tool output ([`ba6df5e`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/ba6df5e9cc3db0ce59f2da3cbac5d938a43a3b0a)).
- Find `rg` binary helper; respect workspace `.gitignore` in grep/find ([`12cce2e`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/12cce2ed517093932d1c2627b03d006c673a83c2)).
- Size-limited read in EditTool; guard ReadTool image scaling against division-by-zero ([`8561fc2`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/8561fc2e4a97f6b8a7a34d6e4218f87a2ebc7d91), [`cf69a47`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/cf69a474ddcf7feb7bf69bfb3b8b90c34c8e4e65)).

### Session & Agent

- Populate error message metadata; include thinking in response detection ([`5834f24`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/5834f24ea2b524acbeddc56520f522234cab485a)).
- Simplify session name handling; improve edit overlap detection ([`052a01f`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/052a01f6d6dc1002a3654aef5d432323f4c70f3c)).
- Graceful error recovery during stream event processing ([`888c614`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/888c6144e7e7a3d4f3087e0c16f0c8c2db476f06)).
- Handle transient `WriteZero` errors in SSE streaming (closes #12) ([`5360d79`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/5360d798d2f86a86ec89fc4fb989f58c0c13b6a4)).
- Handle EINTR across all streaming read loops ([`b25cd30`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/b25cd30a3d40f4b0e72c7c49e4ab7adb74e282d0)).
- `WriteZero` retry for Anthropic provider; reduce idle worker threads ([`012f0f6`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/012f0f67ddb40c87dd19cc0e50cdd9d29cce7c47)).

### Performance

- Preserve string buffer capacity by replacing `mem::take` with `clone+clear` ([`2927bbd`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/2927bbd0cd4ff0f441a03dfa861717877395d6dc)).
- TUI diff prefix parser rewritten with explicit byte-walking for correctness ([`d80d5b4`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/d80d5b4f44bc7eb1ba390a6c4320f15cc66eef5e)).

### CI

- Split clippy into per-target-kind gates to avoid rch timeout ([`d12a83a`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/d12a83ae8c5bdab41fceed1f4b38e0f0e2e7dfc5)).

---

## [v0.1.7](https://github.com/Dicklesworthstone/pi_agent_rust/releases/tag/v0.1.7) -- 2026-02-22 (Draft release)

19 commits. Focused on streaming markdown rendering, crates.io publishing, and CI repair.

### Streaming Markdown

- Intelligent format detection for streaming markdown rendering ([`57fe905`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/57fe905a94a2ca378f4d8e81ba9b380effafdfc5)).
- Streaming markdown fence stabilization for live rendering ([`8903571`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/8903571dca2cce22609f1b21ac59ab6235c69d36)).

### Core Hardening

- Harden agent dispatch, SSE streaming, provider selection, and risk scoring ([`0513a80`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/0513a805dc496ce892d8f4f4389f261f74fa6244)).
- Optimize streaming renderer hot path and session serialization ([`c5d8ae6`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/c5d8ae6e56e18ef7f32a85d598dd8486c1dbf5a4)).
- Session index snapshot update with borrowed parameters ([`c0e86a8`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/c0e86a83cde988a28a563a041698db5d8a47146b)).
- Harden abort handling, UTF-8 safety, IO guards, and extension streaming ([`ee12566`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/ee12566c698f13f75fafcf3995b0aa19a3eebb50)).

### CI & Publishing

- Include `docs/wit/extension.wit` in crate package for crates.io ([`5bffab9`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/5bffab9e715fcaa4ec2053b21c2da3e7b8db7e50)).
- Repair release workflow: stub missing submodule, use ARM macOS runner ([`3357e30`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/3357e3067e9a286c9926c1bb8e785a8f7e397f38)).
- Remove local `charmed-bubbletea` patch that broke CI builds ([`9673414`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/9673414da3ac904aac69e9e5d21662d1c0c8f5c8)).
- Fix `PROXY_ARGS` unbound variable error on bash < 4.4 in installer ([`f9f1c3d`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/f9f1c3d36eb0cdb68fa8516ab561f532a78edcc4)).

---

## [v0.1.6](https://github.com/Dicklesworthstone/pi_agent_rust/releases/tag/v0.1.6) -- 2026-02-21 (Release)

1 commit. Hotfix release for OpenAI provider lifetime regression.

- Fix OpenAI provider lifetime issue introduced in v0.1.5 ([`9dd3b3b`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/9dd3b3b4cd2031e4cc9d9238e33d9fe76f326d9a)).

---

## [v0.1.5](https://github.com/Dicklesworthstone/pi_agent_rust/commit/c22199d0c8dc0f204ef1ff38f68d8507237cbfa4) -- 2026-02-20 (Tag-only)

16 commits. Performance-focused release: allocation elimination, streaming UI overhaul, and memory leak fixes.

### Performance

- Eliminate unnecessary heap allocations across providers, session store, and diff generation ([`606fccb`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/606fccb41b6c2eb4bae3835c3e8270887ef7591c)).
- Eliminate redundant deep clones in agent loop and provider streams ([`e9c108c`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/e9c108ca169f59bb5a298ecdae9f2db8c6772a6e)).
- Eliminate intermediate allocations in resource loading; fix `Arc<str>` test sites ([`6b7caaf`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/6b7caaf38582a4b1ea1ed6d1f7f7899ac88ae487)).
- Reduce allocations across agent core, model catalog, and tool output paths ([`96fec6d`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/96fec6d4379efb5b9590f7d3cae2523adff48249)).
- Fix message ordering in agent loop; pre-allocate session vectors ([`2831682`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/283168272500fe945becf7cfec9281891add32d2)).

### UI & Streaming

- Overhaul UI streaming pipeline to eliminate flicker and improve responsiveness ([`9ff9de8`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/9ff9de8c336ac80f5252a9709a7717519ab282db)).
- Harden streaming UI paths; reduce model-list churn ([`8ae9022`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/8ae9022fe89f4f3410b2de348ef36cc446d803a4)).

### Bug Fixes

- Eliminate memory leak in Azure provider role name handling ([`7216f86`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/7216f865c4d6caf0a37dfff6f998c091f7f4d08e)).
- Prevent XML injection in file tag name attributes ([`e9623a0`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/e9623a0ff93243b0e4659c6b95cf1a3b3caf3524)).
- Fix potential deadlock: drop mutex guard before async channel send ([`0211bbd`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/0211bbda0534425a013d3a7e5de40e5b16a95c96)).
- Fix scheduler `has_pending` false positive; clean up session parsing ([`f176d20`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/f176d20a4b5b58db7eeb08bdc23b9a8482e31b94)).

### Features

- Fast-path `config --show` and `--json` output when no packages installed ([`829dcbc`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/829dcbc3470967d823d383a2c2b40355d826a3e5)).
- Synchronous package resource resolution for config fast paths ([`695ad17`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/695ad17e19b8d35c63eb5a280c623207dc24dd9d)).

---

## [v0.1.4](https://github.com/Dicklesworthstone/pi_agent_rust/releases/tag/v0.1.4) -- 2026-02-20 (Release)

13 commits. Security-focused release with deep hardening across extensions, providers, and the hostcall subsystem.

### Security Hardening

- **Path traversal prevention**: `safe_canonicalize()` with symlink-aware ancestor resolution; module resolution enforces scope monotonicity within extension roots.
- **Command obfuscation normalization**: `normalize_command_for_classification()` strips `${ifs}`, backslash-escaped whitespace before dangerous command classification.
- **OOM guards**: depth limits on recursive JSON hashing (128), `MAX_MODULE_SOURCE_BYTES` (1 GB), `MAX_JOBS_PER_TICK` (10,000), SSE buffer limits (10 MB total / 100 MB per-event).
- **Fast-lane policy enforcement**: extension dispatcher fast-lane runs capability policy checks before executing hostcalls.
- **Atomic file permissions**: auth storage uses `OpenOptions::mode(0o600)`.

### Provider Improvements

- Zero-copy OpenAI serialization via lifetime-parameterized borrows ([`f518bb0`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/f518bb07dfc0e60e26f3e29a75a6c4c79b2e5fc4)).
- Empty base URL handling: all normalizers return canonical defaults for empty/whitespace input.
- Gemini/Vertex: unknown part types silently skipped; `ThinkingEnd` events emitted for open thinking blocks.

### Agent Loop & RPC

- Multi-source message fetchers (Vec-based) enabling RPC + extensions to both queue messages ([`355d7e9`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/355d7e9d93d3ca8a19e2de62f9c18e3a2dac84e0)).
- Queue bounds: `MAX_RPC_PENDING_MESSAGES` (128), `MAX_UI_PENDING_REQUESTS` (64).
- Error persistence fix: `max_tool_iterations` error synced to in-memory transcript.

### Session Persistence

- Batched index updates grouped by `sessions_root` for amortized DB access ([`1df017d`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/1df017db40b2c95f47c0e70dc4e5c9c0c68e4fde)).
- `Box<RawValue>` frames to avoid re-serializing payloads.
- Partial hydration tracking via `v2_message_count_offset`.

### Hostcall System

- Log-sinking batch planner with global request ordering ([`9792cf6`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/9792cf6f6c09f8c2a93de5c5b1d85be6c5e50d12)).
- Generation-keyed ghost cache: O(log n) replacing O(n) VecDeque scans.
- FIFO VecDeque scheduler replacing BinaryHeap for monotone-sequence macrotask queue.

### Tools

- Correct trailing-newline truncation semantics (`"a\n"` = 1 line, not 2).
- `BASH_FILE_LIMIT_BYTES` (100 MB) DoS guard.

### Installer

- Remove auto-hook installation for Claude Code/Gemini CLI; idempotent cleanup of prior hooks ([`d2ffdbb`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/d2ffdbb6a30fee54ebc09a9c8bc6cfe9a3b5e18b)).

---

## [v0.1.3](https://github.com/Dicklesworthstone/pi_agent_rust/releases/tag/v0.1.3) -- 2026-02-19 (Release)

13 commits. Extension runtime restoration, security scoring, and conformance overhaul.

### Extensions

- Re-enable JS/TS extension runtime alongside native-rust descriptors ([`ee78a58`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/ee78a581f7e2ac3e82b3a22f8e5c3cba15ce8af5)).
- Recognize JS/TS files as valid extension entry points ([`e9f3c9e`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/e9f3c9ea0fe449989bcda8f6e27aff15beec7b26)).

### Security

- Argument-aware runtime risk scoring with DCG integration and heredoc AST analysis ([`ad26a4f`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/ad26a4f9b7f6a47d87dbdbf9c6aab96c2b6a0c13)).

### Testing & Conformance

- Overhaul scenario harness with setup merging, shared context, and parity improvements ([`93ac8d9`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/93ac8d9f10fa8d5f8bb4f9b73d49e9a7de1b0a2e)).
- Add `normalize_anthropic_base` unit tests and proptest ([`374f8e6`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/374f8e6a41e8d4d23e2d06dc3c55d0fb375ee80c)).
- `ext_release_binary_e2e` tool for live-provider extension validation ([`409742e`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/409742e5ec8aab97b0c5da30a59eb49f78d33cfa)).

### Other

- `codex-spark` registry entry and `xhigh` thinking support ([`cef709c`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/cef709cc36d75af42eddf1ecce44c2da8c64b57a)).
- Make default HTTP request timeout env-configurable with explicit no-timeout mode ([`74e8f1f`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/74e8f1f1bd45dac58e1c893b87c1f3ef2aecb03b)).
- Bump `asupersync` to 0.2.5; add `ast-grep` for heredoc AST analysis ([`dd2e1f8`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/dd2e1f88f5bf97c1b6bafb4afe1c97c44b9c1e5e)).

---

## [v0.1.2](https://github.com/Dicklesworthstone/pi_agent_rust/releases/tag/v0.1.2) -- 2026-02-18 (Release)

First published GitHub Release with downloadable binaries. ~1,839 commits since v0.1.0 representing a massive development sprint.

### Provider Overhaul

- **OpenAI Codex**: full provider support -- `instructions` field, `store`, `tool_choice`, `parallel_tool_calls`, thinking level via `reasoning.effort`, tolerate missing Content-Type in streaming ([`27bdebc`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/27bdebc43406046e37e705ce9a35f1bceae96e7b), [`0485fb4`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/0485fb4b6ee56de0d1e8a08e9c0e3f9379020c0a)).
- **Kimi Code OAuth**: full support, credential resolution overhaul ([`8671312`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/8671312a9cbb0cc1e84b62c5bdb2dcdefc82dde6)).
- **Google Gemini CLI / Antigravity / Copilot / GitLab**: native OAuth providers ([`14e5016`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/14e5016d99e5dfe3a21f6d19a7be5dce1ea7cb1e), [`663ec51`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/663ec510c40be5b67d0bd66cebb14f2aa74b6987)).
- Case-insensitive provider matching; convenience aliases for Kimi, Vercel, Azure ([`2581af0`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/2581af0e7f3e8bc149b89aca5ee00e5d5b3c86fb)).
- Model selector filters to show only credential-configured providers ([`14e5016`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/14e5016d99e5dfe3a21f6d19a7be5dce1ea7cb1e)).

### Auth System

- OAuth CSRF validation, bearer token marking, gcloud project discovery, Windows home dirs ([`63265e5`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/63265e5d1afdfe55e7e81f3c5ce7d5c0ae4b55b6)).
- Anthropic base URL normalization, OAuth bearer lane, Windows home dir ([`efba9c8`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/efba9c83f52a6ee0e88ffdc86bd41a4fa71c6487)).
- Keyless model support and credential resolution overhaul ([`705f692`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/705f6929b80e8e39e3e6ef3d455ee3a8e2f1a95f)).

### Extension Runtime

- Migrate extension runtime from QuickJS/JS to native Rust ([`c5f9cd9`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/c5f9cd95a1d4e5c3b5a9c0b18d1feca5c5ec5f1d)).
- Node.js builtin compatibility overlay system and expanded builtin shims ([`c07fa74`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/c07fa74b8bf7049b32ff0df0c3bdddd5d8f8b12b)).
- NUMA-aware slab pool and replay trace recording for hostcall reactor ([`60bdc96`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/60bdc960b3f89e0cc0e0feb8cb2ab8fce5e6ec6c)).

### Performance

- Allocation-free hostcall dispatch and zero-copy tool execution ([`53e65ea`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/53e65ea723cffaa8cae7e7e8bea78cb3bc3a29c5)).
- Enum-based session hostcall dispatch replacing string matching ([`db80d77`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/db80d77f81b85aabf78db78abc56265e77685f7e)).
- Session save hotpath and tree traversal optimization ([`3b309aa`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/3b309aa6b05fa85efea97e0c3b94ecb78e6bc06c)).
- Reduce clone allocations in parent-chain tree walks ([`2881f0f`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/2881f0f6f99e48267e74e14cf3baadd3e5dd3bbb)).

### Installer

- Offline tarball mode, proxy support, and agent hook management ([`be404aa`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/be404aa4efd508db1bf9fb34d9b5e7cddb5fa6b6)).
- Handle missing `SHA256SUMS`; prioritize archive candidates ([`7cc84de`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/7cc84de8cc03bb3cf48ec5eeb2f1ced0e0c93434)).
- DSR-style asset naming; reorder candidates to try DSR names first ([`746ddc5`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/746ddc54f75b37c3e95eb2d3f2dbbb753f8b42db)).

### Session & Interactive

- Session migration command, credential pruning, and pipe-aware print mode ([`522d1c5`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/522d1c5a0e7d6b7cfb1855da1ceff42327e8f47e)).
- Clipboard migration to `arboard`; Copilot/GitLab OAuth providers in interactive mode ([`663ec51`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/663ec510c40be5b67d0bd66cebb14f2aa74b6987)).

### CI & Benchmarks

- Bun-killer release gate enforcing `rust_vs_bun_ratio <= 0.33` ([`f45916d`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/f45916d34bdc2b8baaa3f3d45f7e27fca8f94cc9)).
- 224/224 conformance milestone achieved ([`ae655b5`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/ae655b5108f03bc6b8b21a2cc89d0fb43ad9db31)).
- FrankenNode mission contracts, claim gating, and full conformance/compatibility test harnesses ([`5e79f92`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/5e79f922c9e92d68e1b1f6ad05c23f26a7a83aee)).

---

## [v0.1.0](https://github.com/Dicklesworthstone/pi_agent_rust/commit/f8980ad6c92bc5daeeb534d25d7ae0653db19101) -- 2026-02-17 (Tag-only)

First tagged version. ~1,809 commits since project inception on 2026-02-02. This tag captures the initial fully-functional Rust port.

### Core Architecture

- From-scratch Rust port of [Pi Agent](https://github.com/badlogic/pi) (TypeScript) by Mario Zechner.
- Built on two purpose-built libraries:
  - **asupersync**: structured concurrency async runtime with built-in HTTP, TLS, and SQLite.
  - **rich_rust**: Rust port of Python's Rich library for terminal output.
- Single binary, no runtime dependencies.

### Provider Support (initial)

- Anthropic (Claude), OpenAI (GPT), Google (Gemini/Vertex), Azure OpenAI, AWS Bedrock, Cohere, Mistral, DeepSeek, Groq, OpenRouter, Fireworks, Together AI, Perplexity.

### Features at v0.1.0

- Interactive TUI with streaming markdown rendering.
- RPC mode for programmatic control via stdin/stdout JSON protocol.
- Session persistence (JSONL format) with branching and tree navigation.
- Package manager for extensions with NPM registry integration.
- 8 built-in tools: BashTool, ReadTool, EditTool, WriteTool, GrepTool, GlobTool, FetchTool, ListTool.
- Extension system with QuickJS runtime and WASM/native-Rust engine selection.
- Hostcall ABI with capability manifests.
- SSE streaming adapter for provider communication.
- Keybinding system with configurable bindings (`~/.pi/agent/keybindings.json`).
- Autocomplete for commands, prompts, skills, files, and paths.
- Session picker with SQLite-backed index.
- Security: risk scoring for bash commands, extension sandboxing.
- Benchmark suite with startup, memory, and streaming budgets.
- `install.sh` curl-pipe installer with platform detection.

---

## Release Matrix

| Version | Date | Type | Commits | Binary Assets |
|---------|------|------|---------|---------------|
| v0.1.0 | 2026-02-17 | Tag-only | ~1,809 | -- |
| v0.1.2 | 2026-02-18 | **Release** | ~1,839 | 8 |
| v0.1.3 | 2026-02-19 | **Release** | 13 | 7 |
| v0.1.4 | 2026-02-20 | **Release** | 13 | 5 |
| v0.1.5 | 2026-02-20 | Tag-only | 16 | -- |
| v0.1.6 | 2026-02-21 | **Release** | 1 | 5 |
| v0.1.7 | 2026-02-22 | Draft | 19 | -- |
| v0.1.8 | 2026-02-28 | **Release** | 144 | 13 |
| v0.1.9 | 2026-03-12 | **Release** | 348 | 13 |

> Note: v0.1.1 was a version bump in code only (commit [`86be39e`](https://github.com/Dicklesworthstone/pi_agent_rust/commit/86be39e0e1a7bea53ff8b9a2dbb8073e4e27ca05)) and was never tagged or released.
