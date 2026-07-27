### Sergio Peigneux — AI Engineer / Data Scientist

*Construyo primero, prometo después.*

I build backend systems and AI-agent applications in Python — coming from a
5-year Data Science background, now focused on making LLM-based systems
behave predictably: typed contracts, explicit state, and evaluations that
measure a claim instead of assuming it.

---

#### Stack

**Backend & APIs**
![Python](https://img.shields.io/badge/Python-3776AB?logo=python&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-009688?logo=fastapi&logoColor=white)
![Pydantic](https://img.shields.io/badge/Pydantic-E92063?logo=pydantic&logoColor=white)
![pytest](https://img.shields.io/badge/pytest-0A9EDC?logo=pytest&logoColor=white)

**Data**
![Pandas](https://img.shields.io/badge/pandas-150458?logo=pandas&logoColor=white)
![PySpark](https://img.shields.io/badge/PySpark-E25A1C?logo=apachespark&logoColor=white)

**AI / LLM**
![Anthropic](https://img.shields.io/badge/Claude-D97757?logo=claude&logoColor=white)
![Streamlit](https://img.shields.io/badge/Streamlit-FF4B4B?logo=streamlit&logoColor=white)

**Tooling**
![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-2088FF?logo=githubactions&logoColor=white)
![Git](https://img.shields.io/badge/Git-F05032?logo=git&logoColor=white)

---

#### Currently working on

- **[TrainFitter](https://github.com/serpeigd/TrainFitter)** and
  **[Twistify](https://github.com/serpeigd/Twistify)** — both in active
  development, moving phase by phase rather than shipped-and-done.
- Deepening a specific set of AI-engineering topics, in this order of
  priority right now:
  - **Agent architecture** — typed tool contracts, explicit state, bounded
    planning, permissions, retries, human approval.
  - **Context engineering** — loading only the context that's relevant
    when it's needed, instead of stuffing the whole prompt.
  - **Production RAG** — ingestion, chunking, embeddings, hybrid search,
    permission-aware filtering, reranking, citations, evaluation.
  - **Evals & observability** — purpose-built test datasets, traces,
    success rates, latency, cost per task, tool errors, regressions.
  - **Efficient fine-tuning** — SFT + LoRA/QLoRA, DPO/GRPO, only once
    there's real data and a clear metric — not as a first resort.
  - **Inference infrastructure** — vLLM, batching, semantic caching,
    small models for subtasks, routing between models.
  - **Security** — prompt injection, tool isolation, secrets handling,
    per-user authorization, audit trails.

---

#### Featured projects

**[TrainFitter](https://github.com/serpeigd/TrainFitter)**
A multi-agent system that drafts workout and nutrition plans for a personal
trainer's clients, following the trainer's own documented method instead of
generic advice.
*Problem it solves:* the bottleneck in online coaching isn't coaching — it's
the hours spent writing a routine and a diet from scratch per client.
*Stack:* Python, a deterministic rules engine as the free default path, an
optional Anthropic Claude layer, explicit-state orchestration across
routine/diet/validator agents, a Streamlit review panel, pytest, CI on
GitHub Actions.
*Notable design choice:* nothing is ever sent to the client automatically —
every output is a draft, and clinical or injury cases are auto-flagged for
human review.

**[Twistify](https://github.com/serpeigd/Twistify)**
A spoiler-free movie catalogue where the spoiler partition is enforced
server-side, paired with an evaluation harness that measures whether that
promise actually holds.
*Problem it solves:* "spoiler-safe" is usually a UI trick (CSS hiding a
div); here, post-viewing content simply isn't sent to the client until it
declares `seen=true`.
*Stack:* Python 3.12, FastAPI, Pydantic v2, vanilla HTML/CSS/JS on the
frontend, a Claude-based baseline generator, a custom evals harness
(leakage rate, grounded-fact rate, richness) calibrated against planted
spoilers, pytest, CI on GitHub Actions.
*Notable design choice:* the harness reports its own judge's weaknesses
(including a measured `recall = 0.0` case) instead of hiding them.

---

#### Background

5 years studying Data Science, now working with Python, FastAPI, and API
integrations, applied to AI-driven automation. Comfortable across the
full loop of a data problem — from Pandas/PySpark analysis and modeling to
shipping the result as a service — with the AI-agent work above as the
current focus.

---

#### Contact

- GitHub: you're already here — [@serpeigd](https://github.com/serpeigd)
- LinkedIn: [sergio-peigneux](https://www.linkedin.com/in/sergio-peigneux)
