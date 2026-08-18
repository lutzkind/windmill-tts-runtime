# windmill-tts-runtime

Private self-hosted multilingual TTS runtime for Windmill.

The runtime uses the CPU build of Speaches and exposes the OpenAI-compatible `/v1/audio/speech` endpoint on the private Windmill Docker network. It preloads:

- `speaches-ai/Kokoro-82M-v1.0-ONNX` for English speech.
- `speaches-ai/piper-de_DE-thorsten-high` for native German speech.

Models are cached in a persistent Docker volume. No managed TTS API is required.
