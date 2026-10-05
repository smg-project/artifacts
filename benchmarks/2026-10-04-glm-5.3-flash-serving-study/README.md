# GLM-5.3-Flash serving study: per-configuration results

16 runs, 8 config x shape cells; cells are means over passes. One 4-GPU host, TP4, one replica, served through smg gRPC mode with the Rust servicer. `*` marks cells with failed requests.

## req/s

| shape | vllm-tp4 |
|---|---:|
| c1-i1024-o256 | 0.71 |
| c8-i1024-o256 | 3.35 |
| c8-i32768-o1024 | 0.60 |
| c16-i512-o4096 | 0.43 |
| c16-i16384-o1024 | 1.10 |
| c32-i1024-o256 | 8.31 |
| c32-i4096-o512 | 3.83 |
| c128-i1024-o256 | 19.02 |

## out tok/s

| shape | vllm-tp4 |
|---|---:|
| c1-i1024-o256 | 181 |
| c8-i1024-o256 | 859 |
| c8-i32768-o1024 | 616 |
| c16-i512-o4096 | 1,775 |
| c16-i16384-o1024 | 1,131 |
| c32-i1024-o256 | 2,129 |
| c32-i4096-o512 | 1,961 |
| c128-i1024-o256 | 4,868 |

## TTFT p50 ms

| shape | vllm-tp4 |
|---|---:|
| c1-i1024-o256 | 44 |
| c8-i1024-o256 | 338 |
| c8-i32768-o1024 | 3,031 |
| c16-i512-o4096 | 286 |
| c16-i16384-o1024 | 1,829 |
| c32-i1024-o256 | 593 |
| c32-i4096-o512 | 829 |
| c128-i1024-o256 | 709 |

## TTFT p99 ms

| shape | vllm-tp4 |
|---|---:|
| c1-i1024-o256 | 88 |
| c8-i1024-o256 | 470 |
| c8-i32768-o1024 | 5,822 |
| c16-i512-o4096 | 326 |
| c16-i16384-o1024 | 4,994 |
| c32-i1024-o256 | 1,671 |
| c32-i4096-o512 | 2,331 |
| c128-i1024-o256 | 2,273 |

## TPOT p50 ms

| shape | vllm-tp4 |
|---|---:|
| c1-i1024-o256 | 5.36 |
| c8-i1024-o256 | 7.99 |
| c8-i32768-o1024 | 10.03 |
| c16-i512-o4096 | 8.91 |
| c16-i16384-o1024 | 12.34 |
| c32-i1024-o256 | 12.37 |
| c32-i4096-o512 | 14.66 |
| c128-i1024-o256 | 23.45 |

## e2e p99 ms

| shape | vllm-tp4 |
|---|---:|
| c1-i1024-o256 | 1,454 |
| c8-i1024-o256 | 2,434 |
| c8-i32768-o1024 | 16,084 |
| c16-i512-o4096 | 37,417 |
| c16-i16384-o1024 | 17,862 |
| c32-i1024-o256 | 4,863 |
| c32-i4096-o512 | 9,903 |
| c128-i1024-o256 | 8,281 |

## worker CPU s

| shape | vllm-tp4 |
|---|---:|
| c1-i1024-o256 | 0.6 |
| c8-i1024-o256 | 0.8 |
| c8-i32768-o1024 | 1.0 |
| c16-i512-o4096 | 5.3 |
| c16-i16384-o1024 | 1.9 |
| c32-i1024-o256 | 2.3 |
| c32-i4096-o512 | 2.7 |
| c128-i1024-o256 | 5.7 |

## smg CPU s

| shape | vllm-tp4 |
|---|---:|
| c1-i1024-o256 | 0.4 |
| c8-i1024-o256 | 1.2 |
| c8-i32768-o1024 | 2.5 |
| c16-i512-o4096 | 10.1 |
| c16-i16384-o1024 | 3.8 |
| c32-i1024-o256 | 4.1 |
| c32-i4096-o512 | 4.3 |
| c128-i1024-o256 | 13.3 |

![Requests / s](https://raw.githubusercontent.com/smg-project/artifacts/bench4-live/benchmarks/2026-10-04-glm-5.3-flash-serving-study/charts/req_per_s.png)

![Output tokens / s](https://raw.githubusercontent.com/smg-project/artifacts/bench4-live/benchmarks/2026-10-04-glm-5.3-flash-serving-study/charts/out_tok_per_s.png)

![TTFT p99 (ms)](https://raw.githubusercontent.com/smg-project/artifacts/bench4-live/benchmarks/2026-10-04-glm-5.3-flash-serving-study/charts/ttft_p99_ms.png)

![TPOT p50 (ms)](https://raw.githubusercontent.com/smg-project/artifacts/bench4-live/benchmarks/2026-10-04-glm-5.3-flash-serving-study/charts/tpot_p50_ms.png)
