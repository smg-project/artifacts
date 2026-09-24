# Kimi-Vendor-Verifier · Kimi-K3 (NVFP4) behind SMG `nightly-20260923-e381640`

Official conformance suites from [MoonshotAI/Kimi-Vendor-Verifier](https://github.com/MoonshotAI/Kimi-Vendor-Verifier)
(checkout `66092cf`, 2026-09-17), run 2026-09-23 against an SMG gateway in gRPC mode in front of a vLLM gRPC servicer.

## Stack

| Component | Version |
|---|---|
| SMG router image | `ghcr.io/smg-project/smg:nightly-20260923-e381640@sha256:a2efb8e5f671eca1e69935ff712a69e88e461089963c3d34eb44a315daf5cc8c` (main `e38164038`) |
| Router flags | `--policy cache_aware --tool-call-parser kimi_k3 --reasoning-parser kimi_k3`, router-side media processing (default) |
| Engine | vLLM `0.29.1rc1.dev347+gdee37d891` (`vllm/vllm-openai:nightly@sha256:dea7fa04…`), TP8, 2 replicas |
| Servicer | `smg-grpc-servicer` 0.12.0 (gRPC), `SMG_VLLM_MM_PROCESSOR=inprocess` available, unused by these suites |
| Model | Kimi-K3 NVFP4 checkpoint served as `kimi-k3-nvfp4` |

## Results

| Suite | Invocation | Result |
|---|---|---|
| `tests/params` | defaults | 18 passed |
| `tests/k3_features` | defaults | 108 passed, 18 skipped (skips are the suite's own vision/beam gates) |
| `tests/prompt_tokens` | defaults | 59 passed (prompt_tokens match the vendor's counts for every case) |
| `tests/tool_call_json_schema` | `THINK_MODE=opensource --thinking -n 4` (thinking on via `chat_template_kwargs`) | 404 passed, 4 failed on the first pass; all 4 pass on three consecutive reruns |

The four first-pass failures (`TestEnforcerCases:2`, `TestAnyOf:2`, `TestReferences:2`, `TestReferences:16`) all ended
with `finish_reason=length` at the suite's 2048-token budget: the model's reasoning consumed the budget before the tool
call. They are sampling variance, not schema violations; `tool-call-schema-report.retry-{1,2,3}.json` record the reruns.

Note on thinking mode: with Kimi's `thinking: {"type": "disabled"}` the model answers in prose instead of calling the
forced tool in roughly half of the cases, on every gateway build tested (including the previous nightly). That is
tracked separately and is not part of this report's headline numbers.

## Files

- `junit-params.xml`, `junit-k3_features.xml`, `junit-prompt_tokens.xml`, `junit-tool_call_json_schema.xml` — pytest JUnit output per suite
- `tool-call-schema-report.json` — the verifier's own per-case report (`--tool-json-report`), 408 cases, mode and thinking flags in the header
- `tool-call-schema-report.retry-{1,2,3}.json` — reruns of the four first-pass failures
- `router-image.txt` — image digests and engine versions as read from the running pods
