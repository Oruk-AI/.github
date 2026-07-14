# oruk

**oruk is a speech lab.** We build audio models that transcribe words and
classify emotion and speaking style from the same signal — served through the
[oruk Speech API](https://oruk.ai).

## What the API does

- **English transcription** — `POST /v1/audio/transcriptions`
- **Calibrated multilabel emotion** (15 labels) — `POST /v1/audio/emotions`
- **Speaking-style classification** (16 labels) — `POST /v1/audio/styles`
- **Unified analysis** (transcript + labels + segments) — `POST /v1/audio/analysis`

File-based REST API for prerecorded audio, priced per second. New accounts
include $5 in trial credit — no card required.

```bash
curl https://speech-api.oruk.ai/v1/audio/analysis \
  -H "Authorization: Bearer $ORUK_API_KEY" \
  -F file=@call.wav -F model=oruk-resonance
```

## Measured, not marketed

We benchmark in the open: [speech-emotion-bench](https://oruk.ai/benchmarks)
scores 64 systems — commercial APIs, audio LLMs, open models — on 64,384
held-out clips with one identical pipeline, with downloadable results and a
[published methodology](https://oruk.ai/benchmarks/methodology) that states
its caveats plainly.

## Links

- [Documentation & playground](https://oruk.ai/docs)
- [Python SDK on PyPI](https://pypi.org/project/oruk/) (`pip install oruk`)
- [Pricing](https://oruk.ai/pricing) · [Capabilities & scope](https://oruk.ai/capabilities)
- [Research notes](https://oruk.ai/research) ([RSS](https://oruk.ai/rss.xml))
- Contact: access@oruk.ai
