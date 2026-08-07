### Sergio Peigneux d'Egmont — Data Scientist / AI Engineer

*"Connect the data backwards, invent the future forwards, and stay curious."*

Data Scientist with 3+ years of professional experience in ML, NLP, and data
engineering, now focused on LLM-based agent systems — making them behave
predictably with typed contracts, explicit state, and evaluations that
measure a claim instead of assuming it.

---

#### Stack

**Data science & ML (professional)**
![Python](https://img.shields.io/badge/Python-3776AB?logo=python&logoColor=white)
![SQL](https://img.shields.io/badge/SQL-4479A1?logo=postgresql&logoColor=white)
![PySpark](https://img.shields.io/badge/PySpark-E25A1C?logo=apachespark&logoColor=white)
![pandas](https://img.shields.io/badge/pandas-150458?logo=pandas&logoColor=white)
![scikit--learn](https://img.shields.io/badge/scikit--learn-F7931E?logo=scikitlearn&logoColor=white)
![Azure Databricks](https://img.shields.io/badge/Azure_Databricks-FF3621?logo=databricks&logoColor=white)
![Azure ML](https://img.shields.io/badge/Azure_ML-0078D4?logo=microsoftazure&logoColor=white)

**BI & reporting**
![Power BI](https://img.shields.io/badge/Power_BI-F2C811?logo=powerbi&logoColor=black)
![Tableau](https://img.shields.io/badge/Tableau-E97627?logo=tableau&logoColor=white)

**Backend & AI agents (personal projects)**
![FastAPI](https://img.shields.io/badge/FastAPI-009688?logo=fastapi&logoColor=white)
![Pydantic](https://img.shields.io/badge/Pydantic-E92063?logo=pydantic&logoColor=white)
![pytest](https://img.shields.io/badge/pytest-0A9EDC?logo=pytest&logoColor=white)
![Anthropic](https://img.shields.io/badge/Claude-D97757?logo=claude&logoColor=white)
![Ollama](https://img.shields.io/badge/Ollama-000000?logo=ollama&logoColor=white)
![Streamlit](https://img.shields.io/badge/Streamlit-FF4B4B?logo=streamlit&logoColor=white)

**Tooling**
![Git](https://img.shields.io/badge/Git-F05032?logo=git&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-2088FF?logo=githubactions&logoColor=white)

---

#### Currently working on

- **[TrainFitter](https://github.com/serpeigd/TrainFitter)**,
  **[Twistify](https://github.com/serpeigd/Twistify)**, and
  **[AuraPulse](https://github.com/serpeigd/AuraPulse)** — three portfolio
  projects moving phase by phase rather than shipped-and-done, each covering
  a deliberately different slice of the agent-engineering roadmap: a
  multi-agent pipeline with a human-approval gate (TrainFitter), a
  measured-not-promised safety guarantee with a calibrated eval harness
  (Twistify), and conditional routing / when a graph orchestrator earns its
  complexity over a plain sequential pipeline (AuraPulse).
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
generic advice — now with a live demo, Gmail/Notion integrations, and a
client-facing portal, not just a pipeline.
*Problem it solves:* the bottleneck in online coaching isn't coaching — it's
the hours spent writing a routine and a diet from scratch per client, then
tracking whether the client actually follows it.
*Stack:* Python 3.12, a deterministic rules engine as the free default path
(with an optional Anthropic Claude layer behind the same schema),
explicit-state orchestration across routine/diet/validator agents, a
Streamlit review panel and client portal, Gmail/Notion connectors, a
GitHub Actions cron trigger, pytest, CI.
*Notable design choice:* nothing is ever sent to a client automatically
(one narrow, disclosed exception for the portal's own magic link) — every
plan is a draft, and clinical or injury cases are auto-flagged for human
review by a validator that's deliberately never the LLM path.
*Try it:* [trainfitter.streamlit.app](https://trainfitter.streamlit.app/) — no install, no login, no API key.

**[Twistify](https://github.com/serpeigd/Twistify)**
A spoiler-free movie catalogue where the spoiler partition is enforced
server-side, paired with an evaluation harness that measures whether that
promise actually holds — including the uncomfortable case where the cheap
judge fails.
*Problem it solves:* "spoiler-safe" is usually a UI trick (CSS hiding a
div); here, post-viewing content simply isn't sent to the client until it
declares `seen=true`.
*Stack:* Python 3.12, FastAPI, Pydantic v2, vanilla HTML/CSS/JS on the
frontend, two interchangeable baseline generators (Anthropic paid / Groq
free tier), a custom evals harness (leakage rate, grounded-fact rate,
richness) calibrated against a 7,657-review external human dataset, pytest,
CI.
*Notable design choice:* the harness reports its own judge's weaknesses
(a measured `recall = 0.089` on the best judge so far) instead of hiding
them, and blocks the next milestone (retrieval) until the judge clears a
trust bar.
*Try it:* [twistify.onrender.com](https://twistify.onrender.com) — 8/20 titles fully researched with cited sources, the rest browsable via TMDB.

**[AuraPulse](https://github.com/serpeigd/AuraPulse)**
An agent that reads a restaurant's public reviews and detects recurring
operational inconsistencies (food praised while wait time is consistently
criticized, for example) instead of just reporting aggregate sentiment.
*Problem it solves:* sentiment dashboards tell a business "you're at 4
stars"; this turns the same reviews into a specific, actionable signal
about *what* is quietly degrading.
*Stack:* Python 3.11+, Pydantic v2 schema-first classification, a local
LLM served by Ollama (zero paid API calls anywhere in the project), pandas
for dataset handling, pytest/ruff/mypy in CI.
*Notable design choice:* ground truth is never LLM-generated — a
deterministic fake-review generator validates the pipeline first, and the
free Yelp star rating backs sentiment evals before a single review gets
hand-labeled for aspect extraction.
*Status:* Hito 0 (classification → aggregation → reporting) done and
evaluated end-to-end; Hito 1's first slice has since shipped too —
LLM-free routing, draft-reply generation, and deterministic escalation
flagging, still with no orchestration framework until the `if/elif`
routing genuinely stops being legible.

---

#### Background

Bachelor in Data Science, University of Valencia. 3+ years of professional
experience:

- **IVIRMA Global** — ML demand forecasting in Python, NLP/sentiment
  analysis on unstructured text, end-to-end ETL and ML pipelines with SQL,
  PySpark, and Azure Databricks; model evaluation, A/B testing, and
  hyperparameter tuning with Azure ML; Power BI/Tableau dashboards for
  stakeholder reporting.
- **SDG Group** — ETL workflow development and datamart design/validation
  for a banking client, using SQL and PowerCenter.
- **University of Valencia (NLP project)** — NLP-based data anonymization
  and text-preprocessing pipelines, with automated ETL and data-governance
  workflows for privacy-sensitive data.

Comfortable across the full loop of a data problem — from analysis and
modeling to shipping a result as a service — with the AI-agent work above
as the current, self-directed focus.

---

#### Contact

- GitHub: you're already here — [@serpeigd](https://github.com/serpeigd)
- LinkedIn: [sergio-peigneux](https://www.linkedin.com/in/sergio-peigneux)
