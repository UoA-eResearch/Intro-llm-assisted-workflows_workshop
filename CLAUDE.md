# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

Materials for an "Intro to LLM Workflows" workshop (University of Auckland, 2026-08-14) aimed at researchers using LLMs as research instruments. This is a teaching-materials directory, not a software project — there is no build, lint, or test tooling, and it is not a git repository. Files live in OneDrive-synced storage.

## Workshop format and the two-workshop series

This workshop (2026-08-14) is the **first of two**:

1. **This workshop — demonstration.** Mostly PowerPoint slides, with a ~20-minute flip to a live notebook demo of how to use LLMs programmatically. Participants watch; they do not code.
2. **Second workshop (October 2026) — hands-on.** Participants code along and are shown in detail how to implement these tools. Its notebooks are largely already written and will stay mostly unchanged.

`code/example_embeddings.ipynb` is **from the second workshop** and sits here only as a style reference: the demo script for this workshop should follow the same logic and grammar (structure, tone, exercise flow) so the two workshops feel continuous. **Do not edit `example_embeddings.ipynb`** — work on it will begin closer to the October workshop.

## Layout

- `code/`
  - `intro_llms_new.ipynb` — the demo notebook for this workshop, currently being written (empty as of init). This is the file to develop.
  - `example_embeddings.ipynb` — "Notebook 02 — LLMs as Research Instruments" from the second workshop. Reference only; leave unchanged.
  - `old_script.ipynb` — a previous workshop iteration using local HuggingFace `transformers` (Qwen2.5-3B, 4-bit quantization). Reference material only; the new material does not follow this approach.
- `slides/` — PowerPoint decks: the old presentation and the working copy for this workshop.
- `reading/` — PDF papers referenced by the workshop. Not currently exhaustive and will continue to grow.

## API setup for the demo notebook

The demo runs in **local Jupyter** (not Colab) and calls a **University of Auckland–hosted, OpenAI-compatible endpoint** using the `openai` Python client with a custom `base_url` and API key:

```python
from openai import OpenAI

client = OpenAI(
    base_url="<UNIVERSITY_ENDPOINT_URL>",   # TODO: fill in
    api_key=os.environ["UOA_LLM_API_KEY"],  # key via env var, never hard-coded
)
TEXT_MODEL = "<MODEL_NAME>"                 # TODO: fill in
```

The endpoint URL and model name are placeholders until confirmed. Keep the API key out of all committed/saved files.

Note: `example_embeddings.ipynb` currently uses the Groq API with Colab Secrets. The plan is for the second workshop to also move to the university endpoint eventually, but that migration happens later — for now only this workshop's demo script uses the setup above.

## Notebook conventions (style to follow, from the second workshop)

- Markdown cells explain a concept, then short lettered exercises (a, b, c…) with one API call per code cell, followed by a reflection cell ("What did you notice?") and a closing "What you accomplished" summary table that names what comes next.
- A single setup cell at the top installs dependencies, loads the API key, creates the client, and defines model-name constants.
- Worked examples use New Zealand legislation (Privacy Act 2020 as a well-documented source, Impounding Act 1955 as an obscure one) — keep examples NZ/research-relevant.
- Methodological stance taught throughout: `temperature=0` for coding/extraction (reproducibility), higher temperature only for exploration; always give the model real source data rather than relying on its implicit knowledge.
- Since this workshop is a demo, the notebook should read well when projected and run top-to-bottom without audience interaction — exercises become "watch this" moments rather than fill-in-the-blank tasks.
