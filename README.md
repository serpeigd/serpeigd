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

**Data stores & orchestration (personal projects)**
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?logo=postgresql&logoColor=white)
![Supabase](https://img.shields.io/badge/Supabase-3FCF8E?logo=supabase&logoColor=white)
![DuckDB](https://img.shields.io/badge/DuckDB-FFF000?logo=duckdb&logoColor=black)
![Docker](https://img.shields.io/badge/Docker-2496ED?logo=docker&logoColor=white)
![n8n](https://img.shields.io/badge/n8n-EA4B71?logo=n8n&logoColor=white)
![LangGraph](https://img.shields.io/badge/LangGraph-1C3C3C?logo=langchain&logoColor=white)
![MLflow](https://img.shields.io/badge/MLflow-0194E2?logo=mlflow&logoColor=white)

**Tooling**
![Git](https://img.shields.io/badge/Git-F05032?logo=git&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-2088FF?logo=githubactions&logoColor=white)
![Ruff](https://img.shields.io/badge/Ruff-D7FF64?logo=ruff&logoColor=black)
![mypy](https://img.shields.io/badge/mypy-2A6DB2?logo=python&logoColor=white)

---

#### Currently working on

- **[TrainFitter](https://github.com/serpeigd/TrainFitter)**,
  **[Twistify](https://github.com/serpeigd/Twistify)**,
  **[AuraPulse](https://github.com/serpeigd/AuraPulse)**,
  **[TrackerAID](https://github.com/serpeigd/TrackerAID)**,
  **[TravelPlanner](https://github.com/serpeigd/TravelPlanner)**, and
  **[FlightsDelay](https://github.com/serpeigd/FlightsDelay)** — six
  portfolio projects moving phase by phase rather than shipped-and-done,
  each covering a deliberately different slice of the roadmap: a
  multi-agent pipeline with a human-approval gate (TrainFitter), a
  measured-not-promised safety guarantee with a calibrated eval harness
  (Twistify), conditional routing / when a graph orchestrator earns its
  complexity over a plain sequential pipeline (AuraPulse), a retrieval
  system with proper IR-eval discipline plus real orchestration tooling —
  n8n, Supabase, a local LLM (TrackerAID), a ranking system where the LLM
  is explicitly a component rather than the system, held to a grounding
  check it cannot talk its way past (TravelPlanner), and a classical
  ML/data-engineering piece — a 13.9M-row leakage contract, DuckDB vs.
  Spark benchmarked rather than assumed (FlightsDelay).
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
generic advice — now with a live demo, Gmail/Notion integrations, a
client-facing portal, and a fleet-level client dashboard, not just a
pipeline.
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
*Recent improvement:* clients can now favourite a meal or an exercise from
their own portal and have it *bias* — never pin — what gets generated next
week, dropped silently the moment a new injury or allergy makes it unsafe.
Verified statistically against the live workspace rather than eyeballed: a
liked exercise reappeared in ~74% of 30 regenerations.
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
*Notable design choice:* six different spoiler judges were built and
measured; none proved trustworthy enough to report a leakage rate, and the
project says so rather than shipping the flattering number. The default
judge stays the one with a *known* `recall = 0.0` — because missing things
is a bounded failure, and confidently flagging non-leaks isn't.
*Recent improvement:* Milestone 1 (Wikipedia retrieval restricted to a
GREEN-tier corpus that never even constructs the plot section as a source)
took grounded-fact rate from 0.0 to 1.0 across all 20 titles — and hand-
reading every one of them found three real leaks no judge had caught, via
two distinct mechanisms. Both results are published, not just the good one.
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
evaluated end-to-end; Hito 1 shipped too — LLM-free routing, draft-reply
generation, deterministic escalation flagging, and a Streamlit demo
deployed publicly.
*Recent improvement:* the project's central question finally got a
concrete answer, and it came out **both ways in the same codebase**.
Routing between three known outcomes stays a plain `if/elif` — a framework
would buy nothing there. But the draft reject/regenerate loop has to pause
indefinitely between clicks and survive the reviewer closing the browser,
which a Python loop can't do: that one earned LangGraph, and nothing else
in the project did.

**[TrackerAID](https://github.com/serpeigd/TrackerAID)**
A weekly semantic radar for Spanish public-grant announcements (BDNS, the
national subsidy registry), ranked by fit for each user's business profile
— the newest of the four projects, and the first built with a
retrieval/IR-evaluation discipline from day one rather than bolted on
afterward.
*Problem it solves:* relevant grants for freelancers and small businesses
get published constantly but sit buried in a generic government feed;
nobody has time to check by hand every week.
*Stack:* Python, FastAPI, a BM25 retrieval baseline with a proper IR eval
harness (precision/recall/nDCG/MRR) against a hand-labeled gold set,
Postgres/pgvector on Supabase (from F1 on), n8n for weekly orchestration,
Resend for email — the same "logic lives in tested Python, orchestration
tools never hold business logic" discipline as the rest of the portfolio
(see [ADR-0003](https://github.com/serpeigd/TrackerAID/blob/main/docs/adr/0003-logica-en-python-no-en-n8n.md)).
*Notable design choice:* the retrieval-quality claim is held to the same
bar AuraPulse holds its sentiment/aspect claims to — never asserted without
a labeled denominator; the eval script explicitly flags when it's still
running on provisional heuristic labels instead of a human-reviewed gold
set.
*Status:* F0–F2 done, F3 in progress. The gold set is complete (443 of 450
pairs hand-confirmed) and the BM25 baseline has real numbers against it —
`MRR = 1.00`, `precision@20 = 0.95`, but `recall@20 = 0.153`, which is
stated as the weak number to beat rather than buried under the two good
ones. Deadline extraction (F2) resolves 91.3% of announcements through a
three-tier cascade — structured field, then regex, then a **local** LLM via
Ollama — at zero API cost, and leaves the remaining 8.7% explicitly
unresolved instead of guessing. F3 has the ingestion pipeline, a FastAPI
service and the n8n cron scaffold running.

**[TravelPlanner](https://github.com/serpeigd/TravelPlanner)**
A trip-recommendation system built to be defended rather than demoed: it
ranks real accommodation and activity candidates with an explainable score,
enforces hard constraints in deterministic code, and only then lets an LLM
describe the result.
*Problem it solves:* recommendation demos are easy to make impressive and
hard to justify — this one is built so every number in the output can be
traced to a rule, a model coefficient, or a retrieved fact.
*Stack:* Python 3.12, FastAPI, a hedonic price model (scikit-learn), a
reproducible evaluation harness, Streamlit, `mypy --strict`, ruff, pytest
in CI.
*Notable design choice:* the explanation step is **structurally unable to
invent a fact** — a grounding check verifies every figure in the generated
text against the retrieved data, and the one class of error it still can't
catch (claim-level misattribution) is documented as a known blind spot
rather than left for a reader to discover.
*Measured, not asserted:* price-model MAE €40.85 against €73.32 for the
best baseline (a 44% cut), 11/11 golden-set scenarios passing, 100% budget
compliance, zero hard-constraint violations.

**[FlightsDelay](https://github.com/serpeigd/FlightsDelay)**
Predicts whether a US domestic flight arrives 15+ minutes late over 13.9M
BTS flights (2023-2024), built around a single question: does the model
know something it wouldn't know yet at the moment a passenger actually asks?
*Problem it solves:* a leakage bug is the easiest way to make a delay model
look great and be useless — most of the obviously predictive columns in the
source feed are recorded *after* the outcome they're predicting.
*Stack:* Python 3.12, an explicit leakage contract (every column tagged with
when its value becomes known, features assembled by filtering on that
instead of hand-picked lists), DuckDB and Spark benchmarked head-to-head,
Delta Lake, MLflow, Streamlit, pytest/ruff/`mypy --strict` in CI.
*Notable design choice:* the same label, data, models and split, run twice —
once with an inference-time cutoff and once without — turn a single PR-AUC
number into a measured leakage gap (0.343 vs. 0.938) instead of one
optimistic score.
*Measured, not asserted:* DuckDB beats Spark at every scale tested on this
workload (13.8x-2.5x depending on operation, narrowing but never crossing
as data grows 24x) — a documented, benchmarked case *against* reaching for
the bigger engine by default.
*Try it:* [flightsdelay-demo.streamlit.app](https://flightsdelay-demo.streamlit.app/).

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
