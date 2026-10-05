# Coverage matrix: vLLM, SGLang, SMG

- vLLM at `138810056093301f4881050fcf2b1786939da387`
- SGLang at `734cf3cf3b9201a5beb104649acd29f05edcd1e5`
- SMG at `8298368e31d3dfb1cc3a35eae5f7c95ba67593b3`
- aliases: `src/bellwether/gaps/aliases.toml`

## Tool-call parsers (vLLM 53, SGLang 42, SMG 26 names; 63 rows)

| row | vLLM | SGLang | SMG | fixtures |
|---|---|---|---|---|
| apertus | apertus (ApertusToolParser) |  |  |  |
| apertus2509 |  | apertus2509 (Apertus2509Detector) |  |  |
| cohere |  |  | cohere (CohereParser) |  |
| cohere_command3 | cohere_command3 (CohereCommand3ToolParser) |  |  |  |
| cohere_command4 | cohere_command4 (CohereCommand4ToolParser) | cohere_command4 (CohereCommand4Detector) |  |  |
| deepseek_v3 | deepseek_v3 (DeepSeekV3ToolParser) | deepseekv3 (DeepSeekV3Detector) | deepseek (DeepSeekParser) |  |
| deepseek_v31 | deepseek_v31 (DeepSeekV31ToolParser) | deepseekv31 (DeepSeekV31Detector) | deepseek31 (DeepSeek31Parser) |  |
| deepseek_v32 | deepseek_v32 (DeepSeekV32EngineToolParser) | deepseekv32 (DeepSeekV32Detector) | deepseek32 (DeepSeekDsmlParser) |  |
| deepseek_v4 | deepseek_v4 (DeepSeekV4EngineToolParser) | deepseekv4 (DeepSeekV4Detector) | deepseek_v4 (DeepSeekDsmlParser) |  |
| deepseek_v41 | deepseek_v41 (DeepSeekV41EngineToolParser) | deepseekv41 (DeepSeekV41Detector) | deepseek_v41 (DeepSeekDsmlParser) |  |
| dots | dots (DotsToolParser) | dots (DotsToolDetector) |  |  |
| ernie45 | ernie45 (Ernie45ToolParser) |  |  |  |
| functiongemma | functiongemma (FunctionGemmaToolParser) |  |  |  |
| gemma4 | gemma4 (Gemma4EngineToolParser) | gemma4 (Gemma4Detector) |  |  |
| gigachat3 | gigachat3 (GigaChat3ToolParser) | gigachat3 (GigaChat3Detector) |  |  |
| gigachat35 |  | gigachat35 (GigaChat35Detector) |  |  |
| glm45 | glm45 (Glm47MoeModelToolParser) | glm (Glm4MoeDetector), glm45 (Glm4MoeDetector) | glm45_moe (Glm4MoeParser) |  |
| glm47 | glm47 (Glm47MoeModelToolParser) | glm47 (Glm47MoeDetector) | glm47_moe (Glm4MoeParser) |  |
| openai | openai (GptOssToolParser) | gpt-oss (GptOssDetector) | harmony (HarmonyDetector) |  |
| granite | granite (GraniteEngineToolParser) |  |  |  |
| granite-20b-fc | granite-20b-fc (Granite20bFCToolParser) |  |  |  |
| granite4 | granite4 (Granite4ToolParser) |  |  |  |
| hermes | hermes (Hermes2ProToolParser) | hermes (HermesDetector), qwen (Qwen25Detector), qwen25 (Qwen25Detector) | qwen (QwenParser) |  |
| hunyuan_a13b | hunyuan_a13b (HunyuanA13BToolParser) |  |  |  |
| hy_v3 | hy_v3 (HYV3ToolParser) |  |  |  |
| hy_v4 | hy_v4 (HYV4ToolParser) | hunyuan (HunyuanDetector) | hy_v4 (HyV4Parser) |  |
| inkling | inkling (InklingEngineToolParser) | inkling (InklingDetector) | inkling (InklingParser) |  |
| internlm | internlm (Internlm2ToolParser) |  |  |  |
| interns1 |  | interns1 (InternlmDetector) |  |  |
| iquest_q1 |  | iquest_q1 (IQuestQ1Detector) |  |  |
| jamba | jamba (JambaToolParser) |  |  |  |
| json |  |  | json (JsonParser) |  |
| k2_horizon | k2_horizon (K2HorizonToolParser) | k2_horizon (K2V3Detector) |  |  |
| kimi_k2 | kimi_k2 (KimiK2ToolParser) | kimi_k2 (KimiK2Detector) | kimik2 (KimiK2Parser) |  |
| kimi_k3 | kimi_k3 (KimiK3ToolParser) | kimi_k3 (KimiK3Detector) | kimi_k3 (KimiK3Parser) |  |
| lfm2 | lfm2 (Lfm2ToolParser) | lfm2 (Lfm2Detector) |  |  |
| ling3 | ling3 (Ling3ToolParser) | ling3 (Ling3Detector) |  |  |
| llama3_json | llama3_json (Llama3JsonToolParser) | llama3 (Llama32Detector) | llama (LlamaParser) |  |
| llama4_json | llama4_json (Llama3JsonToolParser) |  |  |  |
| llama4_pythonic | llama4_pythonic (Llama4PythonicToolParser) |  |  |  |
| longcat | longcat (LongcatFlashToolParser) |  |  |  |
| mimo | mimo (MiMoToolParser) | mimo (MiMoDetector) |  |  |
| minicpm5 | minicpm5 (MiniCPM5XMLToolParser) | minicpm5 (MiniCPM5Detector) |  |  |
| minimax_m2 | minimax_m2 (MinimaxM2ToolParser) | minimax-m2 (MinimaxM2Detector) | minimax_m2 (MinimaxM2Parser) |  |
| minimax_m3 | minimax_m3 (MinimaxM3ToolParser) | minimax-m3 (MinimaxM3Detector) | minimax_m3 (MinimaxM3Parser) |  |
| mistral | mistral (MistralToolParser) | mistral (MistralDetector) | mistral (MistralParser) |  |
| muse_glimmer | muse_glimmer (MuseGlimmerToolParser) | muse (MuseGlimmerDetector) |  |  |
| nanbeige |  | nanbeige (Qwen3CoderDetector) |  |  |
| olmo3 | olmo3 (Olmo3PythonicToolParser) |  |  |  |
| passthrough |  |  | passthrough (PassthroughParser) |  |
| phi4_mini_json | phi4_mini_json (Phi4MiniJsonToolParser) |  |  |  |
| plamo3 | plamo3 (Plamo3EngineToolParser) |  |  |  |
| poolside_v1 | poolside_v1 (PoolsideV1ToolParser) | poolside_v1 (PoolsideV1Detector) |  |  |
| pythonic | pythonic (PythonicToolParser) | pythonic (PythonicDetector) | pythonic (PythonicParser) |  |
| qwen3_coder | qwen3_coder (Qwen3EngineToolParser), qwen3_xml (Qwen3EngineToolParser) | qwen3_coder (Qwen3CoderDetector) | nemotron (QwenXmlParser), qwen_coder (QwenXmlParser), qwen_xml (QwenXmlParser) |  |
| hf | hf (ResponseTemplateToolParser) |  |  |  |
| sarashina |  |  | sarashina (SarashinaParser) |  |
| seed_oss | seed_oss (SeedOssEngineToolParser) |  |  |  |
| spark25 |  | spark25 (Spark25Detector) |  |  |
| step3 | step3 (Step3ToolParser) | step3 (Step3Detector) | step3 (Step3Parser) |  |
| step3p5 | step3p5 (Step3p5ToolParser) | step3p5 (Qwen3CoderDetector) |  |  |
| trinity |  | trinity (TrinityDetector) |  |  |
| xlam | xlam (xLAMToolParser) |  |  |  |

Engine names with no SMG counterpart (39): apertus, apertus2509, coherecommand3, coherecommand4, dots, ernie45, functiongemma, gemma4, gigachat3, gigachat35, granite, granite20bfc, granite4, hunyuana13b, hyv3, internlm, interns1, iquestq1, jamba, k2horizon, lfm2, ling3, llama4json, llama4pythonic, longcat, mimo, minicpm5, museglimmer, nanbeige, olmo3, phi4minijson, plamo3, poolsidev1, responsetemplate, seedoss, spark25, step3p5, trinity, xlam

SMG-only names (4): cohere, json, passthrough, sarashina

Only one engine has it (27): apertus, apertus2509, coherecommand3, ernie45, functiongemma, gigachat35, granite, granite20bfc, granite4, hunyuana13b, hyv3, internlm, interns1, iquestq1, jamba, llama4json, llama4pythonic, longcat, nanbeige, olmo3, phi4minijson, plamo3, responsetemplate, seedoss, spark25, trinity, xlam

One implementation behind several rows (alias candidates):
- SGLang `Qwen3CoderDetector`: nanbeige, qwen3xml, step3p5
- SMG `DeepSeekDsmlParser`: deepseekv32, deepseekv4, deepseekv41
- SMG `Glm4MoeParser`: glm45, glm47
- vLLM `Glm47MoeModelToolParser`: glm45, glm47
- vLLM `Llama3JsonToolParser`: llama3json, llama4json

## Reasoning parsers (vLLM 37, SGLang 34, SMG 21 names; 49 rows)

| row | vLLM | SGLang | SMG | fixtures |
|---|---|---|---|---|
| apertus2509 |  | apertus2509 (Apertus2509Detector) |  |  |
| base |  |  | base (BaseReasoningParser) |  |
| cohere_cmd |  |  | cohere_cmd (CohereCmdParser) |  |
| cohere_command3 | cohere_command3 (CohereCommand3ReasoningParser) |  |  |  |
| cohere_command4 | cohere_command4 (CohereCommand4ReasoningParser) | cohere_command4 (CohereCommand4Detector) |  |  |
| deepseek_r1 | deepseek_r1 (DeepSeekR1ReasoningParser) | deepseek-r1 (DeepSeekR1Detector) | deepseek_r1 (DeepSeekR1Parser) |  |
| deepseek_v3 | deepseek_v3 (DeepSeekV3ReasoningParser) | deepseek-v3 (_DeepSeekV3Detector) |  |  |
| deepseek_v31 |  |  | deepseek_v31 (BaseReasoningParser) |  |
| deepseek_v4 | deepseek_v4 (DeepSeekV4ParserReasoningAdapter) | deepseek-v4 (DeepSeekV4Detector) | deepseek_v4 (BaseReasoningParser) |  |
| deepseek_v41 | deepseek_v41 (DeepSeekV41ParserReasoningAdapter) | deepseek-v41 (DeepSeekV41ReasoningDetector) | deepseek_v41 (DeepSeekV41Parser) |  |
| dots |  | dots (Qwen3Detector) |  |  |
| ernie45 | ernie45 (Ernie45ReasoningParser) |  |  |  |
| gemma4 | gemma4 (Gemma4ParserReasoningAdapter) | gemma4 (Gemma4Detector) |  |  |
| gigachat35 |  | gigachat35 (DeepSeekR1Detector) |  |  |
| glm45 | glm45 (Glm47MoeParserReasoningAdapter), glm47 (Glm47MoeParserReasoningAdapter) | glm45 (Glm45Detector) | glm45 (Glm45Parser) |  |
| openai_gptoss | openai_gptoss (GptOssReasoningParser) | gpt-oss (GptOssDetector) | harmony (HarmonyDetector) |  |
| granite | granite (GraniteReasoningParser) |  |  |  |
| granite_thinking_parser | granite_thinking_parser (GraniteThinkingParserReasoningAdapter) | granite_thinking_parser (GraniteThinkingDetector) |  |  |
| holo2 | holo2 (DeepSeekV3ReasoningWithThinkingParser) |  |  |  |
| hunyuan_a13b | hunyuan_a13b (HunyuanA13BReasoningParser) |  |  |  |
| hy_v3 | hy_v3 (HYV3ReasoningParser) |  |  |  |
| hy_v4 | hy_v4 (HYV4ReasoningParser) | hunyuan (HunyuanDetector) | hy_v4 (HyV4Parser) |  |
| inkling | inkling (InklingParserReasoningAdapter) | inkling (InklingDetector) | inkling (InklingParser) |  |
| interns1 |  | interns1 (Qwen3Detector) |  |  |
| iquest_q1 |  | iquest_q1 (IQuestQ1ReasoningDetector) |  |  |
| k2_horizon | k2_horizon (K2HorizonReasoningParser) | k2_horizon (K2V3Detector) |  |  |
| kimi |  | kimi (KimiDetector) | kimi (KimiParser) |  |
| kimi_k2 | kimi_k2 (KimiK2ReasoningParser) | kimi_k2 (KimiK2Detector) | kimi_thinking (BaseReasoningParser) |  |
| kimi_k25 |  |  | kimi_k25 (BaseReasoningParser) |  |
| kimi_k3 | kimi_k3 (KimiK3ReasoningParser) | kimi_k3 (KimiK3Detector) | kimi_k3 (KimiK3Parser) |  |
| ling3 | ling3 (Ling3ParserReasoningAdapter) | ling3 (Ling3Detector) |  |  |
| mimo | mimo (MiMoParserReasoningAdapter) | mimo (_MimoDetector) |  |  |
| minimax_m2_append_think | minimax_m2_append_think (MiniMaxM2AppendThinkReasoningParser) | minimax-append-think (MiniMaxAppendThinkDetector) |  |  |
| minimax_m2 | minimax_m2 (MiniMaxM2ReasoningParser) | minimax (Qwen3Detector) | minimax (MiniMaxParser) |  |
| minimax_m3 | minimax_m3 (MiniMaxM3ReasoningParser) | minimax-m3 (MiniMaxM3Detector) | minimax_m3 (MinimaxM3Parser) |  |
| mistral | mistral (MistralParserReasoningAdapter) | mistral (MistralDetector) |  |  |
| muse_glimmer | muse_glimmer (MuseGlimmerReasoningParser) | muse (MuseGlimmerDetector) |  |  |
| nanbeige |  | nanbeige (Qwen3Detector) |  |  |
| nemotron_v3 | nemotron_v3 (NemotronV3ParserReasoningAdapter) | nemotron_3 (Nemotron3Detector) | nano_v3 (NanoV3Parser) |  |
| olmo3 | olmo3 (Olmo3ReasoningParser) |  |  |  |
| passthrough |  |  | passthrough (PassthroughParser) |  |
| plamo3 | plamo3 (Plamo3ParserReasoningAdapter) |  |  |  |
| poolside_v1 | poolside_v1 (PoolsideV1ReasoningParser) | poolside_v1 (_PoolsideV1Detector) |  |  |
| qwen3 | qwen3 (Qwen3ParserReasoningAdapter) | qwen3 (Qwen3Detector) | qwen3 (Qwen3Parser) |  |
| qwen3-thinking |  | qwen3-thinking (Qwen3Detector) | qwen3_thinking (QwenThinkingParser) |  |
| hf | hf (ResponseTemplateReasoningParser) |  |  |  |
| seed_oss | seed_oss (SeedOssParserReasoningAdapter) |  |  |  |
| step3 | step3 (Step3ReasoningParser) | step3 (DeepSeekR1Detector) | step3 (Step3Parser) |  |
| step3p5 | step3p5 (Step3p5ParserReasoningAdapter) | step3p5 (DeepSeekR1Detector) |  |  |

Engine names with no SMG counterpart (28): apertus2509, coherecommand3, coherecommand4, deepseekv3, dots, ernie45, gemma4, gigachat35, granite, granitethinkingparser, holo2, hunyuana13b, hyv3, interns1, iquestq1, k2horizon, ling3, mimo, minimaxappendthink, mistral, museglimmer, nanbeige, olmo3, plamo3, poolsidev1, responsetemplate, seedoss, step3p5

SMG-only names (5): base, coherecmd, deepseekv31, kimik25, passthrough

Only one engine has it (18): apertus2509, coherecommand3, dots, ernie45, gigachat35, granite, holo2, hunyuana13b, hyv3, interns1, iquestq1, kimi, nanbeige, olmo3, plamo3, qwen3thinking, responsetemplate, seedoss

One implementation behind several rows (alias candidates):
- SGLang `DeepSeekR1Detector`: deepseekr1, gigachat35, step3, step3p5
- SGLang `Qwen3Detector`: dots, interns1, minimaxm2, nanbeige, qwen3, qwen3thinking
- SMG `BaseReasoningParser`: base, deepseekv31, deepseekv4, kimik2, kimik25

## Renderers (vLLM 10, SGLang 2, SMG 6 names; 11 rows)

| row | vLLM | SGLang | SMG | fixtures |
|---|---|---|---|---|
| cohere | cohere (CohereRenderer) |  |  |  |
| deepseek_v32 | deepseek_v32 (DeepseekV32Renderer) |  | deepseek_v32 (Renderer::DeepseekV32) |  |
| deepseek_v4 | deepseek_v4 (DeepseekV4Renderer) |  | deepseek_v4 (Renderer::DeepseekV4) |  |
| deepseek_v41 | deepseek_v41 (DeepseekV4Renderer) |  | deepseek_v41 (Renderer::DeepseekV41) |  |
| hf | hf (HfRenderer) | hf (jinja chat template) | jinja (Renderer::Jinja) |  |
| inkling | inkling (InklingRenderer) | inkling (InklingTextTokenizer) |  |  |
| kimi_audio | kimi_audio (HfRenderer) |  |  |  |
| kimi_k25_tools |  |  | kimi_k25_tools (encoders::kimi_k25_tools) |  |
| kimi_k3 | kimi_k3 (KimiK3Renderer) |  | kimi_k3_xtml (encoders::kimi_k3_xtml) |  |
| mistral | mistral (MistralRenderer) |  |  |  |
| terratorch | terratorch (TerratorchRenderer) |  |  |  |

Engine names with no SMG counterpart (5): cohere, inkling, kimiaudio, mistral, terratorch

SMG-only names (1): kimik25tools

Only one engine has it (8): cohere, deepseekv32, deepseekv4, deepseekv41, kimiaudio, kimik3, mistral, terratorch

One implementation behind several rows (alias candidates):
- vLLM `DeepseekV4Renderer`: deepseekv4, deepseekv41
- vLLM `HfRenderer`: hf, kimiaudio

## Tokenizer modes (vLLM 9, SGLang 3, SMG 2 names; 10 rows)

| row | vLLM | SGLang | SMG | fixtures |
|---|---|---|---|---|
| cohere | cohere (CachedHfTokenizer) |  |  |  |
| deepseek_v32 | deepseek_v32 (DeepseekV32Tokenizer) |  |  |  |
| deepseek_v4 | deepseek_v4 (DeepseekV4Tokenizer) |  |  |  |
| deepseek_v41 | deepseek_v41 (DeepseekV41Tokenizer) |  |  |  |
| hf | hf (CachedHfTokenizer) | hf (transformers tokenizer) | huggingface (TokenizerType::HuggingFace) |  |
| inkling | inkling (CachedHfTokenizer) | inkling (InklingTokenizer) |  |  |
| kimi_audio | kimi_audio (KimiAudioTokenizer) |  |  |  |
| kimi_k3 | kimi_k3 (CachedHfTokenizer) |  |  |  |
| mistral | mistral (MistralTokenizer) |  |  |  |
| tiktoken |  | tiktoken (TiktokenProcessor) | tiktoken (TokenizerType::Tiktoken) |  |

Engine names with no SMG counterpart (8): cohere, deepseekv32, deepseekv4, deepseekv41, inkling, kimiaudio, kimik3, mistral

SMG-only names (0): none

Only one engine has it (8): cohere, deepseekv32, deepseekv4, deepseekv41, kimiaudio, kimik3, mistral, tiktoken

One implementation behind several rows (alias candidates):
- vLLM `CachedHfTokenizer`: cohere, hf, inkling, kimik3
