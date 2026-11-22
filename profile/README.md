# oruk

Oruk, Inc. builds speech AI APIs for transcription, vocal emotion and speaking-style analysis. Use Spectra-2 for recorded speech in 25 languages, Realtime for live transcription in 32 locales, and model-specific endpoints for expression scores, speaker turns and synthetic-speech detection.

[Choose a model](https://oruk.ai/models#model-comparison) · [Speech emotion recognition API](https://oruk.ai/speech-emotion-recognition-api) · [API quickstart](https://oruk.ai/docs/quickstart) · [Pricing](https://oruk.ai/pricing)

For hosted transcription, start with the [Orukeet hosted model](https://oruk.ai/models/orukeet) and [API quickstart](https://oruk.ai/docs/quickstart). For vocal delivery, read [what paralinguistics measures](https://oruk.ai/what-is-paralinguistics), listen to the [voice emotion analyzer](https://oruk.ai/tools/voice-emotion-analyzer), or integrate the [speech emotion recognition API](https://oruk.ai/speech-emotion-recognition-api).

## Build with the speech API

| Model | Use it for | Access and scope |
| --- | --- | --- |
| [Spectra-2](https://oruk.ai/docs/models/spectra-2) | 25-language transcription plus 15 emotion and 16 speaking-style scores | Stable; short recordings; scores cover the whole clip |
| [Resonance 1](https://oruk.ai/docs/quickstart) | English transcription, timed emotion/style scores and optional speaker turns | Stable file API |
| [Resonance 2](https://oruk.ai/docs/models/resonance-2) | 31 continuous expression scores and six signed axes, without a transcript | Preview; new organizations need separate approval |
| [Realtime](https://oruk.ai/docs#realtime) | Live transcript tokens in 32 locales and phrase-level emotion events | WebSocket preview |
| [Orukeet hosted](https://oruk.ai/models/orukeet) | English dictation and short recordings, with optional emotion and diarization | Preview; separate Orukeet subscription allowance |
| [OrukZero](https://oruk.ai/synthetic-speech-detection-api) | Human-or-synthetic English speech detection | Free for active accounts, including free/trial accounts, with approved API access and a valid key |

The [complete model matrix](https://oruk.ai/models#model-comparison) also covers Fourier and Proficiency, language support, streaming behavior and allowance pools. Transcription language support does not establish equal emotion accuracy in every language. Expression scores describe how speech sounds, not a person's inner state; OrukZero's uncalibrated scores are review signals, not proof.

### First request

Keep your API key on your server. This request uses one local English recording and available subscription or trial usage:

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

## Fourier 2B for local English transcription

[Fourier 2B](https://huggingface.co/oruk/oruk-fourier-2b) transcribes short English recordings with the native Qwen3-ASR backend in Transformers. The model card includes a Python example. The weights are [CC BY-NC 4.0](https://creativecommons.org/licenses/by-nc/4.0/). Commercial use and hosted or API serving require a separate Oruk license.

## Benchmarks and research

[oruk-bench](https://github.com/Oruk-AI/oruk-bench) contains the published speech-emotion evaluation toolkit and results. The benchmark's seven-class mapping and multilingual dataset describe its evaluation protocol, not the hosted API's native outputs or language support. Oruk's historical model was evaluated in-distribution; those results do not establish the current API's accuracy on independent audio. Read the [results](https://oruk.ai/benchmarks) and [methodology](https://oruk.ai/benchmarks/methodology) together.

[Listen to six recorded Resonance 2 examples](https://oruk.ai/research/resonance-2), including mistakes, and inspect the model/calibration revisions and all 546 predictions from the September 17 acted-emotion diagnostic. Training overlap has not been audited; the diagnostic is not an independent held-out evaluation.

[Research articles](https://oruk.ai/research) · [RSS](https://oruk.ai/rss.xml) · [Company facts](https://oruk.ai/company#facts) · [Contact](mailto:access@oruk.ai)

