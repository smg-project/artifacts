# bellwether coverage matrix · 2026-10-05

The first run of `bellwether gaps` (M1): which tool-call parsers, reasoning parsers, renderers and tokenizer
modes vLLM and SGLang register, mapped onto SMG's, so that every row without an SMG column is a parser to
write. `gaps.md` is the matrix as printed; `gaps.json` is the same data, canonical JSON.

## Sources

| System | Read at | How |
|---|---|---|
| vLLM | `138810056093301f4881050fcf2b1786939da387` | registry tables fetched at that commit (`vllm/tool_parsers/__init__.py`, `vllm/reasoning/__init__.py`, `vllm/renderers/registry.py`, `vllm/tokenizers/registry.py`) |
| SGLang | `734cf3cf3b9201a5beb104649acd29f05edcd1e5` | name lists, class maps and the native renderer and tokenizer modules fetched at that commit |
| SMG | `8298368e31d3dfb1cc3a35eae5f7c95ba67593b3` (main) | `register_parser` calls in the two factories, the renderer enum and the tokenizer types, read from the checkout |

Generated with [smg-project/bellwether](https://github.com/smg-project/bellwether) at `e0786ea5` (main after PR #3):

```bash
bellwether gaps --vllm-ref 138810056093301f4881050fcf2b1786939da387 \
                --sglang-ref 734cf3cf3b9201a5beb104649acd29f05edcd1e5 \
                --smg-src <smg checkout at 8298368e> --format markdown --out gaps.md
```

The reader uses `ast` and regular expressions only; no engine is imported. Names that differ across systems
for one format are merged through `src/bellwether/gaps/aliases.toml` in that commit, where every entry
states its evidence; the alias candidates at the end of each section come from one implementation class
registered under several names.

## Headline

| Kind | vLLM | SGLang | SMG | rows | engine-only | SMG-only | engines differ |
|---|---|---|---|---|---|---|---|
| Tool-call parsers | 53 | 42 | 26 | 63 | 39 | 4 | 27 |
| Reasoning parsers | 37 | 34 | 21 | 49 | 28 | 5 | 18 |
| Renderers | 10 | 2 | 6 | 11 | 5 | 1 | 8 |
| Tokenizer modes | 9 | 3 | 2 | 10 | 8 | 0 | 8 |

"engine-only" rows are formats at least one engine serves and SMG does not: the backlog for M6. "SMG-only"
rows are formats SMG serves that neither engine registers under a name the alias table knows. The
reconciliation of this matrix against the hand-made survey of 2026-10-04 (Appendix A) is in the body of
bellwether PR #3; the alias decisions left open there (SMG `cohere` vs. `cohere_command3/4`, SMG
`deepseek_v31` vs. the engines' `deepseek_v3`) are unchanged here.

No fixtures existed on `main` at this run, so the `fixtures` column is empty throughout; the first render
fixtures (Qwen3-8B, DeepSeek-R1) are bellwether PR #4.
