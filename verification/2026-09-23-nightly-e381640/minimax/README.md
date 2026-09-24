# MiniMax-Provider-Verifier · MiniMax-M3 behind SMG `nightly-20260923-e381640` (prefill/decode mode)

Official verifier from [MiniMax-AI/MiniMax-Provider-Verifier](https://github.com/MiniMax-AI/MiniMax-Provider-Verifier),
run 2026-09-23/24 against an SMG gateway in gRPC prefill/decode mode (`--pd-disaggregation`) in front of two vLLM gRPC
servicers (one prefill, one decode) connected with NIXL.

## Stack

| Component | Version |
|---|---|
| SMG router image | `ghcr.io/smg-project/smg:nightly-20260923-e381640@sha256:a2efb8e5f671eca1e69935ff712a69e88e461089963c3d34eb44a315daf5cc8c` (main `e38164038`) |
| Router flags | `--policy cache_aware --tool-call-parser minimax_m3 --reasoning-parser minimax_m3 --pd-disaggregation --prefill grpc://… --decode grpc://…` (plus the per-run flags listed below) |
| Engines | vLLM `0.29.1rc1.dev347+gdee37d891` (`vllm/vllm-openai:nightly@sha256:dea7fa04…`), TP4 per leg, `NixlConnector` (prefill `kv_producer`, decode `kv_consumer`) |
| Servicer | `smg-grpc-servicer` 0.12.0 on both legs, redis media sidecar available (`SMG_VLLM_MM_PROCESSOR=redis`, `SMG_VLLM_MM_MAX_ITEMS=200`, `SMG_VLLM_MM_MAX_ITEM_BYTES=256 MiB`) |
| Model | MiniMax-M3 MXFP8 checkpoint served as `MiniMax-M3` |

## Official pass@10 (`run_batch_sequential.sh`, 10 loops × 102 cases, 5 workers)

Averages over the 10 loops, compared with the vendor's own baseline shipped in the repository (`output-dir/MiniMax-M3`):

| Metric | SMG + vLLM (this run) | MiniMax official baseline |
|---|---|---|
| Query-Success-Rate | 1.000 | 1.000 |
| ToolCalls-Match-Rate | 0.981 | 0.988 |
| ToolCalls-Trigger-Similarity | 0.995 | — |
| ToolCalls-Schema-Accuracy | 0.982 | 0.989 |
| Error-Only-Reasoning-Rate | 0.000 | 0.000 |
| Language-Following-Success-Rate | 1.000 | 1.000 |
| Scenario-Check-Pass-Rate | 0.800 (8 of 10 loops) | 1.000 |

The scenario check is a single case that asks the model to repeat a nested tool schema in its original property order;
the deployed checkpoint returns the properties key-sorted in some loops. The gateway was shown to forward the schema in
request order (prefix-cache proof), so that gap is engine/model-side.

## Format-check suites (`m3_format_check`)

Three router configurations were run, all on the same image and engines:

- **A, engine-side media, defaults**: media decoded by the redis sidecar next to each engine; no API key; default health probe (5 s timeout, 3 failures).
- **B, engine-side media, probe workaround**: as A with `--health-check-timeout-secs 120 --health-failure-threshold 10`.
- **C, router-side media**: `--mm-processing router` (the gateway decodes and preprocesses media itself), `--api-key` set, same probe workaround as B.

| Suite | A | B | C | What the remaining failures are |
|---|---|---|---|---|
| text | 152 pass / 4 fail | — | **156 pass / 0 fail** (5 skipped) | A's four: two no-API-key tests (no key configured), `tool_choice=required` argument value taken from the schema description (intermittent, gateway constraint path), one thinking multiturn without reasoning (model, intermittent) |
| image | 108 / 2 | — | **109 / 1** | C: 200 images at the spec maximum time out at the verifier's 300 s client limit (a 1 GB preprocessed payload). A also failed the tiny-image upscale monotonicity check, which vLLM's MiniMax processor gets wrong and the gateway's own processor gets right |
| stream | 10 / 0 | — | 10 / 0 | — |
| video | 77 / 11 | 85 / 3 | 85 / 3 | A: all 11 are 503 `no_available_workers` after the gateway lost its connection to the prefill engine (see below). B: 20- and 30-minute videos exceed the sidecar's 512 MiB result limit and the verifier's 600 s timeout; one image-plus-video case returned an empty completion once (passes on rerun). C: 10-, 20- and 30-minute videos exceed the verifier's 600 s timeout with router-side payloads of 0.4–1.4 GB |

### The video outage in configuration A

The engine's gRPC server closed the router's connection with `Too many pings` while a long video request was in flight.
The router sends HTTP/2 keepalive pings every 30 s; grpc-core servers reject pings closer than 5 minutes apart when no
data is flowing unless the server relaxes that, and vLLM's gRPC launcher tries to but passes the option under a name
grpc-core does not recognise (`grpc.http2.min_recv_ping_interval_without_data_ms`; the real name has no `recv`). The
router multiplexes its health probes over the same connection, so the probes failed with it, the prefill leg was marked
unhealthy, and every later test received 503. The engine itself answered an independent health prober throughout.
Two fixes follow: the launcher option name in vLLM, and a dedicated probe connection in the SMG gateway.

## Files

- `pass10/metrics_report.json`, `pass10/comparison_report.json` — the verifier's aggregated report and its comparison with the vendor baseline
- `pass10/loop_NN/smg-pd_summary.json`, `pass10/loop_NN/batch_report.json` — per-loop summaries
- `pass10/verify_single_run_summary.json` — the single `verify.py` run that preceded the batch (102/102)
- `format-check/junit-{text,image,stream}.xml` — configuration A
- `format-check/junit-video.default-health-probe.xml` — configuration A; `format-check/junit-video.health-timeout-120.xml` — configuration B
- `format-check/junit-{text,image,video}.router-side-media.xml` — configuration C
- `images.txt` — image digests, engine versions and media-sidecar settings read from the running pods
