# ClipForge — web interface

The live site: **https://zorvayatechnologyes.github.io/clipforge-site/**

This repo holds only the static front-end. Paste a YouTube stream link, get the
funny / interesting moments back as vertical 1080x1920 clips with burned-in
captions.

## Why it needs an engine

Browsers cannot run ffmpeg or Whisper, so the page talks to a small server
(the "engine") that does the downloading, transcription, ranking and rendering.
Open the site and you will see an **Engine** box at the top — point it at an
engine and the page comes alive.

## Getting an engine

**On your own machine** (free, private, nothing leaves the laptop):

```bash
# needs Python 3.10+ and ffmpeg on PATH
python -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
python -m clipforge serve        # http://127.0.0.1:8000
```

Then open the live site and press **Connect** with `http://127.0.0.1:8000`.
Browsers exempt `localhost` from mixed-content blocking, so an HTTPS page can
call a local HTTP engine — this works.

**Hosted** (so it works from your phone): deploy the engine's Docker image to
Render, Railway, Fly.io or any VPS, then paste that HTTPS address into the
Engine box. The engine needs at least 2 GB RAM and a persistent disk; free tiers
will not survive a render.

## Engine settings worth knowing

| variable | default | meaning |
|---|---|---|
| `CLIPFORGE_ALLOWED_ORIGINS` | `*` | set to `https://zorvayatechnologyes.github.io` to allow only this site |
| `CLIPFORGE_WHISPER_MODEL` | `small` | `tiny` for speed, `large-v3` for accuracy |
| `CLIPFORGE_MAX_CLIPS` | `6` | clips per job |
| `CLIPFORGE_USE_LLM` | `true` | use a local Ollama model for smarter picks |

## Legal

Downloading and re-uploading someone else's stream can breach YouTube's Terms of
Service and the creator's copyright. Use it on your own streams or material you
have permission to reuse.
