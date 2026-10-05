# bench4: how to serve GLM-5.3-Flash best (and MiniMax-M3 if wanted)

Goal: find the serving configuration that gives the best throughput and latency for `zai-org/GLM-5.3-Flash` (FP8, 328 GB,
MoE 288 experts / 8 active, 45 layers, 1M context, 1 MTP layer) on one 4-GPU host, through smg gRPC mode with the Rust
servicer (the winner of bench3), across SGLang 0.5.20, vLLM nightly and TokenSpeed nightly. All three ship the model and its
MTP head (SGLang `glm5_next` + NextN, vLLM `Glm5Next` + `Glm5NextMTP`, TokenSpeed `glm53_flash` + NextN).

Fit: 328 GB FP8 -> TP4 = 82 GB/GPU weights (plenty of KV), or TP2 x 2 replicas = 164 GB/GPU (DP2 behind smg).
MiniMax-M3-MXFP8: 444 GB -> TP4 = 111 GB/GPU; TP2 x 2 = 222 GB/GPU (tight). All three engines ship it + MTP too.

## Phases (each config: load, warm-up, then the shape list; one config alive at a time)

P0  Baseline, engine defaults at TP4 (`--tensor-parallel-size 4` / `--tp 4`), MTP off. Synthetic length-pinned
    shapes as in bench3 plus long inputs: c1/c8/c32/c128 x 1024->256, c32 x 4096->512, c16 x 16384->1024,
    c8 x 32768->1024, c16 x 512->4096. Establishes per-engine baseline and the long-context behaviour.
P1  Speculative decoding (MTP) on vs off, 1..3 draft tokens where the engine allows, with REAL prompts: acceptance
    depends on predictable text, so synthetic random-word prompts would understate it. Prompt sources already in the
    shared HF cache: ShareGPT (chat) and LongBench-v2 (long context); plus a coding set if available. Natural stops
    (no ignore_eos), max_tokens cap; report output tokens/s, TPOT, acceptance length, at c1/c8/c32/c128.
P2  Parallelism: TP4 vs TP2 x DP2 (two replicas behind smg) vs expert parallelism where supported (vLLM
    `--enable-expert-parallel`, SGLang `--ep-size`, TokenSpeed equivalent), with the best P1 setting.
P3  Knobs on the best P2 layout: max batched tokens / chunked prefill size, CUDA-graph max batch, attention
    backend, FP8 KV cache, prefix caching under a multi-turn workload.

Estimated time: P0 ~1.5 h, P1 ~3 h, P2 ~2.5 h, P3 ~3 h (overnight). Results/scripts on NFS (`~/bench4`,
`~/smg-rerun/bench4`), artifacts pushed to smg-project/artifacts as they land, report in a new smg issue.
Open choices for the user: (a) all three engines or a subset; (b) GLM only or MiniMax too; (c) P1 prompt sets.
