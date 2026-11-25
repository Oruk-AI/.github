# oruk

Oruk, Inc. builds speech AI APIs for transcription, vocal emotion and speaking-style analysis. Use Spectra-2 for recorded speech in 25 languages, Realtime for live transcription in 32 locales, and model-specific endpoints for expression scores, speaker turns and synthetic-speech detection.

[Choose a model](https://oruk.ai/models#model-comparison) · [Speech emotion recognition API](https://oruk.ai/speech-emotion-recognition-api) · [API quickstart](https://oruk.ai/docs/quickstart) · [Pricing](https://oruk.ai/pricing)

For hosted transcription, start with the [Orukeet hosted model](https://oruk.ai/models/orukeet) and [API quickstart](https://oruk.ai/docs/quickstart). For vocal delivery, read [what paralinguistics measures](https://oruk.ai/what-is-paralinguistics), listen to the [voice emotion analyzer](https://oruk.ai/tools/voice-emotion-analyzer), or integrate the [speech emotion recognition API](https://oruk.ai/speech-emotion-recognition-api).

## Build with the speech API

| Model | Use it for | Access and scope |
| --- | --- | --- |
| [Fourier 2B](https://oruk.ai/models#model-comparison) (`oruk-fourier-2b`) | English batch transcription (`POST /v1/audio/transcriptions`), up to 30 MiB and 60 minutes per request | Preview; `$0.0080/min` (shared speech-understanding allowance); serves pinned [open weights](https://huggingface.co/oruk/oruk-fourier-2b) |
| [Spectra-2](https://oruk.ai/docs/models/spectra-2) | 25-language transcription plus 15 emotion and 16 speaking-style scores | Stable; short recordings; scores cover the whole clip |
| [Resonance 1](https://oruk.ai/docs/quickstart) | English transcription, timed emotion/style scores and optional speaker turns | Stable file API |
| [Resonance 2](https://oruk.ai/docs/models/resonance-2) | 31 continuous expression scores and six signed axes, without a transcript | Preview; new organizations need separate approval |
| [Realtime](https://oruk.ai/docs#realtime) | Live transcript tokens in 32 locales and phrase-level emotion events | WebSocket preview |
| [Orukeet hosted](https://oruk.ai/models/orukeet) | English dictation and short recordings, with optional emotion and diarization | Preview; separate Orukeet subscription allowance |
| [OrukZero](https://oruk.ai/synthetic-speech-detection-api) | Human-or-synthetic English speech detection | Free for active accounts, including free/trial accounts, with approved API access and a valid key |

The [complete model matrix](https://oruk.ai/models#model-comparison) also covers legacy Fourier, Proficiency, language support, streaming behavior and allowance pools. Transcription language support does not establish equal emotion accuracy in every language. Expression scores describe how speech sounds, not a person's inner state; OrukZero's uncalibrated scores are review signals, not proof.

### First request

Keep your API key on your server. For English transcription with `oruk-fourier-2b` (`POST /v1/audio/transcriptions`, `$0.0080/min`):

```bash
curl --fail-with-body --connect-timeout 10 --max-time 120 \
  https://speech-api.oruk.ai/v1/audio/transcriptions \
  -H "Authorization: Bearer $ORUK_API_KEY" \
  -H "X-Request-ID: $(uuidgen)" \
  -F model=oruk-fourier-2b \
  -F language=en \
  -F file=@call.wav
```

For transcription plus vocal emotion and speaking-style analysis with `oruk-resonance`:

```bash
curl --fail-with-body --connect-timeout 10 --max-time 120 \
  https://speech-api.oruk.ai/v1/audio/analysis \
  -H "Authorization: Bearer $ORUK_API_KEY" \
  -H "X-Request-ID: $(uuidgen)" \
  -F model=oruk-resonance \
  -F file=@call.wav
```

For supplied audio, saved JSON output and error handling, follow the [Python, Node.js and cURL quickstart](https://oruk.ai/docs/quickstart). Existing Hume users can start with the [contract comparison](https://oruk.ai/compare/hume-expression-measurement-alternative) and [native implementation guide](https://oruk.ai/docs/hume-migration); Oruk is not a drop-in Hume protocol or TTS replacement.

- [Python SDK](https://pypi.org/project/oruk/) · [TypeScript SDK](https://www.npmjs.com/package/@oruk-ai/sdk) · [Verified SDK installs and examples](https://oruk.ai/docs/sdks)
- [Hosted MCP server](https://oruk.ai/docs/mcp) · [Pipecat speech integration](https://oruk.ai/integrations/pipecat)
- [Public API examples](https://github.com/Oruk-AI/speech-api-examples) · [Try your audio](https://oruk.ai/tools/voice-emotion-analyzer)

Plans start at $9/month (Hobby), $49/month (Builder) and $199/month (Production). Speech understanding minutes and Orukeet's task-valued allowance are separate; optional Orukeet tasks consume its allowance at their published rates. Standard self-serve trials last seven days, require a card and renew as the selected paid plan unless canceled. Promotional terms may differ. [Compare current allowances and spending limits](https://oruk.ai/pricing).

## Orukeet: local speech recognition

[Orukeet](https://github.com/Oruk-AI/orukeet) is a 25-language speech recognizer built from NVIDIA Parakeet TDT 0.6B v3. It has NeMo, ONNX and native inference exports. The downloadable model is distinct from the English-only hosted preview.

Start with the [tested local-transcription tutorial](https://oruk.ai/guides/orukeet-local-transcription), including native Q8 and sherpa-onnx CPU examples, pinned artifacts and recorded outputs. The [model card](https://huggingface.co/oruk/orukeet) documents the weights, licenses and evaluation limitations. OpenWhispr [1.10.0](https://github.com/OpenWhispr/openwhispr/releases/tag/v1.10.0) includes Orukeet as its recommended local model.

## Fourier 2B: open-weight and hosted English ASR

[Oruk Fourier 2B](https://huggingface.co/oruk/oruk-fourier-2b) (`oruk/oruk-fourier-2b`, 2.04B parameters) is an English-specialized Qwen3-ASR fine-tune available both as open weights (`transformers >= 5.21`, vLLM, llama.cpp Q8 GGUF, MLX 8-bit, sherpa-onnx INT8) and on Oruk's hosted self-serve API (`POST https://speech-api.oruk.ai/v1/audio/transcriptions`, `model=oruk-fourier-2b`, `$0.0080/min`).

- **Hugging Face Open ASR Leaderboard (`v1.16.3`, merged in [`open_asr_leaderboard#298`](https://github.com/huggingface/open_asr_leaderboard/pull/298)):** **#7 / 68 overall** and **#1 single-model open-weights** (**5.52%** 9-dataset average WER at **254× RTFx** on H200 BF16; **4.95%** 7-split public English mean vs. **5.75%** base `Qwen/Qwen3-ASR-1.7B-hf` with Fourier's default 3-beam config vs. greedy base — AMI-Cleaned `6.73%` vs. `8.31%`, VoxPopuli-AA `1.46%` vs. `2.85%`, SPGISpeech `1.87%` vs. `2.57%`, GigaSpeech-Cleaned `6.50%` vs. `7.22%`, Earnings22-Cleaned-AA `5.61%` vs. `5.84%`, URGENT2024 `9.03%` vs. `9.93%`, Voice Arena Monsoon `3.42%` vs. `3.50%`).
- **Additional verified English benchmarks (`oruk/oruk-fourier-2b@8c2a8871`):**
  - Open ASR English Long-Form (`10/10` splits, 320 h): **10.92% avg WER** @ `202×` RTFx ([`open_asr_leaderboard#304`](https://github.com/huggingface/open_asr_leaderboard/pull/304))
  - SpeechColab GigaSpeechBench (`20/20` English splits, matched greedy vLLM): **#1/16** English Accents (`12.73%`), **#1/16** Vertical-Domain (`6.09%`), **#3/16** Hotword B-WER (`13.50%`), **#1/17** `OLD-EN` (`13.42%`) ([`GigaSpeechBench#14`](https://github.com/SpeechColab/GigaSpeechBench/pull/14))
  - MERaLiON AudioBench `ASR-English` (`12/12` datasets, greedy vLLM): **6.33% mean WER (#2/35)** ([`AudioBench-Leaderboard#2`](https://huggingface.co/spaces/MERaLiON/AudioBench-Leaderboard/discussions/2))
  - Omi Health Medical PriMock57 (`55` consultations): **8.57% WER (#4/43)**, **3.02% Canonical M-WER (#8/43)** ([`medical-STT-eval#6`](https://github.com/Omi-Health/medical-STT-eval/pull/6))
- **Ecosystem & local guides:** Works with [`pipecat-oruk`](https://github.com/Oruk-AI/pipecat-oruk), [`speech-api-examples`](https://github.com/Oruk-AI/speech-api-examples), [`fourier-blender`](https://github.com/Oruk-AI/fourier-blender), [`fourier-anki`](https://github.com/Oruk-AI/fourier-anki), [Buzz](https://github.com/chidiwilliams/buzz), [OpenWhisper](https://github.com/Knuckles92/OpenWhisper), [audio.cpp](https://github.com/0xShug0/audio.cpp), [VocaPhone](https://github.com/VocaHQ/vocaphone), [lmms-eval](https://github.com/EvolvingLMMs-Lab/lmms-eval), [pyVideoTrans](https://github.com/jianchang512/pyvideotrans), plus the [8-bit GGUF setup guide](https://huggingface.co/oruk/oruk-fourier-2b/blob/main/examples/handy-gguf/README.md) and [Hex guide](https://huggingface.co/oruk/oruk-fourier-2b/blob/main/examples/hex/README.md).

The open weights are [CC BY-NC 4.0](https://creativecommons.org/licenses/by-nc/4.0/). Oruk also permits [local workplace dictation in Hex](https://huggingface.co/oruk/oruk-fourier-2b#hex-local-workplace-dictation). Other commercial uses and self-hosted API serving require a separate Oruk license, or use Oruk's commercial hosted API at [speech-api.oruk.ai](https://oruk.ai/pricing).

## Benchmarks and research

[oruk-bench](https://github.com/Oruk-AI/oruk-bench) contains the published speech-emotion evaluation toolkit and results. The benchmark's seven-class mapping and multilingual dataset describe its evaluation protocol, not the hosted API's native outputs or language support. Oruk's historical model was evaluated in-distribution; those results do not establish the current API's accuracy on independent audio. Read the [results](https://oruk.ai/benchmarks) and [methodology](https://oruk.ai/benchmarks/methodology) together.

[Listen to six recorded Resonance 2 examples](https://oruk.ai/research/resonance-2), including mistakes, and inspect the model/calibration revisions and all 546 predictions from the September 17 acted-emotion diagnostic. Training overlap has not been audited; the diagnostic is not an independent held-out evaluation.

[Research articles](https://oruk.ai/research) · [RSS](https://oruk.ai/rss.xml) · [Company facts](https://oruk.ai/company#facts) · [Contact](mailto:access@oruk.ai)

