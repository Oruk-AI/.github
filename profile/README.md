# oruk

Oruk is a speech lab. We build models for transcription, emotion and speaking-style analysis, with a [hosted API](https://oruk.ai/docs) and [open research](https://oruk.ai/research).

## Speech API

Resonance analyzes prerecorded English audio. One request can return the transcript, 15 emotion scores, 16 speaking-style scores and timed segments. Scores are independent model outputs, not calibrated probabilities of a person's inner state.

```bash
curl https://speech-api.oruk.ai/v1/audio/analysis \
  -H "Authorization: Bearer $ORUK_API_KEY" \
  -F file=@call.wav -F model=oruk-resonance
```

The file API also has separate [transcription, emotion and speaking-style endpoints](https://oruk.ai/docs). The [Realtime preview](https://oruk.ai/docs#realtime) streams transcription in 32 locales and phrase-level emotion over WebSocket. Full emotion and speaking-style analysis uses the English file endpoints.

Plans include audio minutes, measured by the second. Standard self-serve plans have a seven-day trial that requires a card, charges $0 today and can be canceled before the trial ends. Promotional offers have their own terms. See [current plans and allowances](https://oruk.ai/pricing).

- [Python SDK](https://pypi.org/project/oruk/) · [TypeScript SDK](https://www.npmjs.com/package/@oruk-ai/sdk) · [SDK examples](https://oruk.ai/docs/sdks)
- [Try the voice emotion analyzer](https://oruk.ai/tools/voice-emotion-analyzer)
- [Hosted MCP server](https://oruk.ai/docs/mcp)

## Orukeet: local speech recognition

[Orukeet](https://github.com/Oruk-AI/orukeet) is a 25-language speech recognizer built from NVIDIA Parakeet TDT 0.6B v3. It has NeMo, ONNX and native inference exports.

Start with the [tested local-transcription tutorial](https://oruk.ai/guides/orukeet-local-transcription), including native Q8 and sherpa-onnx CPU examples, pinned artifacts and recorded outputs. The [model card](https://huggingface.co/oruk/orukeet) documents the weights, licenses and evaluation limitations. OpenWhispr [1.10.0](https://github.com/OpenWhispr/openwhispr/releases/tag/v1.10.0) includes Orukeet as its recommended local model.

## Benchmarks and research

[oruk-bench](https://github.com/Oruk-AI/oruk-bench) contains the published speech-emotion evaluation toolkit and results. The benchmark's seven-class mapping and multilingual dataset describe its evaluation protocol, not the hosted API's native outputs or language support. Oruk's historical model was evaluated in-distribution; those results do not establish the current API's accuracy on independent audio. Read the [results](https://oruk.ai/benchmarks) and [methodology](https://oruk.ai/benchmarks/methodology) together.

[Research articles](https://oruk.ai/research) · [RSS](https://oruk.ai/rss.xml) · [API scope](https://oruk.ai/capabilities) · [Contact](mailto:access@oruk.ai)
