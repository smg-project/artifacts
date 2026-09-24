# Vendor verifier runs · SMG `nightly-20260923-e381640`

Raw reports from the official vendor conformance suites, run on 2026-09-23/24 against the SMG router image
`ghcr.io/smg-project/smg:nightly-20260923-e381640` (main `e38164038`), digest
`sha256:a2efb8e5f671eca1e69935ff712a69e88e461089963c3d34eb44a315daf5cc8c`. Every run uses SMG in gRPC mode in front
of `smg-grpc-servicer` 0.12.0 on vLLM `0.29.1rc1.dev347+gdee37d891`. Each subfolder has its own README with the
stack, the exact invocation, the numbers and the list of failing cases.

| Folder | Model | Verifier | Headline |
|---|---|---|---|
| [`kimi/`](kimi/) | Kimi-K3 NVFP4, TP8 | [Kimi-Vendor-Verifier](https://github.com/MoonshotAI/Kimi-Vendor-Verifier) | params 18/18 · k3_features 108 pass / 18 skip · prompt_tokens 59/59 · tool_call_json_schema 404/408 (4 length-budget flakes pass on rerun) |
| [`minimax/`](minimax/) | MiniMax-M3 MXFP8, prefill/decode pair over NIXL | [MiniMax-Provider-Verifier](https://github.com/MiniMax-AI/MiniMax-Provider-Verifier) | pass@10: query success 1.000, tool-call match 0.981 (vendor baseline 0.988), schema accuracy 0.982 (0.989); format checks with router-side media: text 156/156, image 109/110, stream 10/10, video 85/88 (long videos exceed the verifier's timeout) |
| [`glm/`](glm/) | GLM-5.3-Flash FP8, TP8, 1M context | [providers-verifier](https://github.com/smg-project/providers-verifier) (z.ai golden set) | prompt_tokens match 1.000 · query success 0.913 · media 62% · tool calling far below the vendor (tool_battery 7%, tool_schema 0%) — see the folder README for the breakdown |

Conventions: `junit-*.xml` are pytest JUnit files; the JSON files are the verifiers' own reports; `images.txt` /
`router-image.txt` record the image digests and versions read from the running pods at the time of the run. Model
outputs inside the reports are the models' own responses to the vendors' public test prompts.
