# windmill-tts-runtime

Private self-hosted multilingual TTS runtime for Windmill.

The runtime uses the CPU build of Speaches and exposes the OpenAI-compatible `/v1/audio/speech` endpoint on the private Windmill Docker network. It preloads:

- `speaches-ai/Kokoro-82M-v1.0-ONNX` for English speech.
- `speaches-ai/piper-de_DE-thorsten-high` for native German speech.

Models are cached in a persistent Docker volume. No managed TTS API is required.

## Deployment identity

- Canonical repository: `lutzkind/windmill-tts-runtime` (this repository) — source of truth.
- Compose service: `kokoro-tts`, internal port `8880`, external network `windmill`.
- Live Coolify name: **`windmill-self-hosted-tts`**. The running Coolify-managed app still carries
  `coolify.resourceName=windmill-self-hosted-tts` and
  `coolify.serviceName=windmill-self-hosted-tts`, a legacy name inherited from the superseded
  `lutzkind/windmill-self-hosted-tts` repository.
- Verified 2026-09-19: that live container runs this repository's pinned Speaches image digest and
  the exact `UVICORN_PORT`/`ENABLE_UI`/`LOG_LEVEL`/`TTS_MODEL_TTL`/`PRELOAD_MODELS` environment, so
  the mismatch is naming-only.
- Canonical mapping: `windmill-self-hosted-tts` (Coolify app) → `kokoro-tts` (service) →
  `lutzkind/windmill-tts-runtime` (repository). Treat the legacy Coolify name as this application
  until the Coolify resource is renamed; renaming it is a Coolify-side action and is not performed
  by repository changes.
- Do not copy the legacy name into new repository names, config, docs, or app names.
