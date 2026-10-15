# CS 789 — Assignment 6: Build a SOC Copilot

**UNLV · AI-Powered Cyber Attacks and Defenses · Fall 2026 · Prof. Yoohwan Kim**

You build the core of a **product**: an AI copilot that answers SOC analysts' questions from a knowledge graph of
real IDS/SIEM alerts, follows a guardrailed policy, remembers the conversation, and runs as a web app with
dashboards. **A7 continues it** (n8n automation, an uncensored model, your own dashboards) — keep `my_a6.py`.

* **Part A** — complete the SOC **ontology** (OWL/Turtle) and a **SHACL** shape
* **Part B** — build the **LlamaIndex** property graph from 37,808 alerts; extract facts from analysts' notes with an LLM
* **Part C** — a KG retriever under a **token budget**, a **guardrailed system prompt**, **three LLMs** compared
* **Part D** — **LangChain memory** stored in **SQLite**, with your own history policy
* **Part E** — launch the **SOC Copilot web app** (dashboards + your chat + KG explorer), run its acceptance test,
  and export your copilot to `my_a6.py` for A7

The handout is `CS 789 A6.docx` / `.pdf` on WebCampus. This README is the "how do I start" sheet.

## Start on Google Colab (recommended)

1. Open **https://colab.research.google.com/github/unlv-cs789-f26/A6/blob/main/A6_SOC_Copilot.ipynb**
2. *Runtime → Change runtime type →* **L4 GPU** → *Save*.
3. *File → Save a copy in Drive*.
4. Run cell 0.1. It clones this repo into `/content/A6`, installs the packages, installs vLLM into its own
   environment and starts **Qwen3-4B-Instruct-2507** on port 8000 (about 6 minutes the first time).

No paid API is needed. Gemini is optional (a free key from aistudio.google.com in Colab 🔑 Secrets as `GEMINI_API_KEY`).
The web app (port 8080) opens through Colab's own https proxy link that the notebook prints.

## Start on your own computer (Linux or WSL2, NVIDIA GPU ≥ 16 GB)

```bash
git clone https://github.com/unlv-cs789-f26/A6.git
cd A6
./start.sh --vllm         # makes .venv, installs packages and vLLM, checks the machine, opens Jupyter Lab
./start.sh --check        # only the environment check
```
Windows without WSL2: `start.bat` sets up a venv so you can read the notebook, but vLLM needs Linux.

## Files

| file | what it is |
|---|---|
| `A6_SOC_Copilot.ipynb` | the assignment notebook — 🛠️ build cells (with AI prompts), ✅ checks, ✍️ questions |
| `soc6/` | the fixed harness: data, ontology tools, KG helpers, LLM servers, scoring, web app. **Do not edit.** |
| `ontology/soc.ttl`, `ontology/shapes.ttl` | the ontology and SHACL shapes you complete in Part A |
| `data/` | the alerts (history and live feed), host inventory, staff, exercise windows, ATT&CK techniques |
| `notes/` | analysts' shift-handover notes for LLM extraction (Part B); you add `my_note.md` |
| `questions.yaml`, `dialogue.yaml` | the 22 evaluation questions (Part C) and the 10-turn conversation (Part D) |
| `install_vllm.sh` | vLLM installer used by the notebook |
| `PROMPTS.md` | how to use Claude in Chrome / Gemini in Chrome / Gemini in Colab, and prompt patterns |
| `start.sh` / `start.bat` / `check_environment.py` | local start-up and checks |

Results you measure are appended to `results/results.jsonl`; conversations are stored in `conversations.db`;
E.4 writes `my_a6.py`, the starting point of A7.

## Data and credit

Alerts: **AIT Alert Data Set** — M. Landauer, F. Skopik, M. Wurzenberger, Zenodo 2023,
doi:[10.5281/zenodo.8263181](https://doi.org/10.5281/zenodo.8263181), CC BY 4.0. See `data/DATASET.md` for what was
changed. The host inventory, staff, roles and phone numbers are invented for the lab.

## Submission

One PDF on WebCampus: the filled-in handout followed by this notebook printed with its outputs
(*File → Print → Save as PDF*).
