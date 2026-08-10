# Smart B-roll Placement Detector

A small full-stack assignment app that reads a vlog transcript, proposes visually showable B-roll placements, explains each choice, and lets the user reject suggestions locally in the UI.

## Run Locally

From a fresh clone, run the backend and frontend in two terminals:

```bash
cd backend
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
uvicorn app.main:app --reload
```

```bash
cd frontend
npm install
npm run dev
```

Open the Vite URL, usually [http://127.0.0.1:5173](http://127.0.0.1:5173). The frontend loads `frontend/public/transcript.json` and posts it to `http://127.0.0.1:8000/detect`.

## Detector

The detector is intentionally rule-based and explainable. It excludes direct-to-camera moments such as `welcome back`, `subscribe`, `thanks for watching`, `see you next time`, and `like and subscribe`, then filters weak abstract/reflection-heavy lines containing terms like `feel`, `believer`, `worth it`, and `stress`. Remaining candidates are scored with weighted visual keywords: places/scenes are worth 3 points per hit, while objects and actions are worth 2 points per hit. Placements snap to full transcript segment boundaries, are capped at 40% total video coverage, and must keep at least a 3 second gap from other accepted placements.

For the included 60 second sample transcript, the 40% cap allows up to 24 seconds of B-roll. The expected selected moments are:

- `13.5-19.0`: road, pine forests, valley
- `22.5-28.0`: roasting Ethiopian beans by entrance
- `31.5-37.0`: pour-over, wooden deck, river
- `41.0-46.5`: old town, streets, vintage shops

## Tests

Run backend unit tests with:

```bash
cd backend
PYTHONPATH=. python3 -m unittest discover -s tests
```

The tests cover greeting/CTA/sign-off exclusions, abstract segment exclusions, visual selection, the 40% coverage cap, segment boundary preservation, the 3 second minimum gap, and the expected sample placements.

Manual UI checks:

- App loads the transcript.
- Suggestions appear highlighted.
- Reasons are visible next to highlighted segments.
- Rejecting a suggestion updates accepted count and total coverage.

## What I'd Do With More Time

I would add better local NLP, embeddings for visual concreteness, transcript-level pacing, shot variety constraints, and optional LLM or frame analysis when a paid/API workflow is allowed. I would also add frontend component tests and a small import flow for arbitrary transcript files.

## AI Tools Disclosure

Codex/AI assistance was used for planning and implementation.
