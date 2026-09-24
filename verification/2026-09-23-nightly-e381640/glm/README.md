# providers-verifier (z.ai golden set) · GLM-5.3-Flash behind SMG `nightly-20260923-e381640`

[providers-verifier](https://github.com/smg-project/providers-verifier) replays a golden set recorded against z.ai's
own GLM-5.3-Flash endpoint (634 cases: parameter matrix, media with exact prompt-token counts, long context, tool
battery, the 424-case tool-schema set, thinking and formatting probes) against a target and compares every response
with the vendor's. Run 2026-09-23 with 3 repeats per case (1,902 runs), concurrency 4, `--separate-reasoning`.

## Stack

| Component | Version |
|---|---|
| SMG router image | `ghcr.io/smg-project/smg:nightly-20260923-e381640@sha256:a2efb8e5f671eca1e69935ff712a69e88e461089963c3d34eb44a315daf5cc8c` (main `e38164038`) |
| Router flags | `--policy cache_aware --tool-call-parser glm47_moe --reasoning-parser glm45`, router-side media processing |
| Engine | vLLM `0.29.1rc1.dev347+gdee37d891` (`vllm/vllm-openai:nightly@sha256:dea7fa04…`), TP8, 1M context, `--limit-mm-per-prompt {"image":64,"video":4}` |
| Servicer | `smg-grpc-servicer` 0.12.0, redis media sidecar available (`SMG_VLLM_MM_PROCESSOR=redis`) |
| Model | GLM-5.3-Flash FP8 checkpoint served as `glm-5.3-flash` |
| providers-verifier | `7ca2162` |

## Results

| Metric | Value | Threshold |
|---|---|---|
| prompt_tokens_match_rate | 1.000 | 1.0 |
| query_success_rate | 0.913 | 1.0 |
| tool_trigger_match_rate | 0.443 | 0.98 |
| tool_schema_accuracy (of triggered calls) | 0.974 | 0.98 |
| think_leak_rate | 0.647 | 0.0 |
| error_only_reasoning_rate | 0.026 | 0.0 |
| language_following_rate | 0.500 | 0.4 |
| scenario_check_pass_rate | 0.000 | 1.0 |

Pass rate by category (share of runs matching the vendor on every check): error 100%, streaming 100%, structured
83%, vendor 78%, thinking 67%, media 62%, text 58%, params 43%, vision 33%, tools 13%, tool_battery 7%,
tool_schema 0%, longctx 0%. Every category is equal to or better than the 2026-09-22 run on the previous nightly
except `structured` (5 of 6 runs instead of 6 of 6).

## What the failures are

- **Requests SMG or the engine rejects (400) where z.ai answers 200**, 129 runs: 16/32/64 images per request and two
  videos (the model spec's per-request caps of 10 images / 1 video, not the engine's limits); one image plus one video
  (duplicate `patches_per_image` tensor key); `.bmp` input; a 12 s video whose 90,280 embedding tokens exceed the
  engine's encoder cache; `top_p` above 1.0, `tool_choice` naming an unknown function, a non-object `json_schema` and
  `stream_options` without `stream` (SMG validates these, z.ai accepts them); and 18 strict tool schemas the engine
  refuses to compile (`Invalid grammar specification: 'triggers'`). Seven streamed tool-schema cases end with an engine
  error mid-stream.
- **Tool calling**: on this deployment the model mostly reasons at length and then answers in prose or runs out of
  tokens instead of emitting `<tool_call>`, for both the natural tool battery and the forced-call schema set. The
  rendered prompt has been shown byte-identical to the reference chat template, so this is being investigated on the
  engine/model side rather than in the gateway. `think_leak_rate` is dominated by the same runs.
- **Long context**: the four needle cases (32k to 1M tokens) are served but answered wrong or refused, where z.ai answers
  all four on token-identical prompts.
- **Media that is accepted** matches z.ai on prompt tokens in 100% of cases and on content in most.

## Files

- `pv-verify-report.json` — the verifier's full report: metrics, thresholds, per-case checks, and the target's response next to the vendor's golden summary for every run
- `junit-pv-verify.xml` — one JUnit case per golden case
- `images.txt` — image digests, engine versions, media settings and router arguments read from the running pods
