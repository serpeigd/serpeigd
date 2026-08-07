# GitHub profile & portfolio — improvement notes

Based on a direct inspection of the local repos (`TrainFitter`, `Twistify`,
`AuraPulse`) and the public state of `github.com/serpeigd`. Nothing below is
invented — every point ties to something observed in the code, git history, or
GitHub API response.

> **Update (2026-08-06 doc-sync pass):** a third public repo, `AuraPulse`, now
> exists (Hito 0 in progress — classification → aggregation → reporting
> pipeline, free/local via Ollama) and has been added to the profile README's
> "Currently working on" and "Featured projects" sections. Several items below
> that were open at the time this file was first written are now resolved —
> marked inline rather than deleted, so the history of what was flagged stays
> visible. The three project repos' own `README.md`s got a full doc-sync pass
> the same day; see each repo's `docs/DESIGN.md` (AuraPulse), `docs/decisiones.md`
> (TrainFitter), or `docs/DESIGN.md` (Twistify) for their own change logs.

> **Update (2026-08-07 doc-sync pass):** two corrections and one process
> finding from today's run:
> 1. The line above calling AuraPulse "Hito 0 in progress" was already stale
>    — Hito 0 finished and Hito 1's first slice (LLM-free routing, draft-reply
>    generation, deterministic escalation flagging) has since shipped on
>    `main`. Fixed in the profile README's AuraPulse status line; leaving this
>    note rather than rewriting the line above, per this file's own
>    append-don't-rewrite convention.
> 2. Each project repo got a second documentation-sync pass today (badges,
>    screenshots, Configuration/Limitations/FAQ sections, staleness fixes) —
>    see AuraPulse [#11](https://github.com/serpeigd/AuraPulse/pull/11),
>    TrainFitter [#2](https://github.com/serpeigd/TrainFitter/pull/2), and
>    Twistify [#8](https://github.com/serpeigd/Twistify/pull/8) (all draft
>    PRs, not yet merged).
> 3. **Process gap, flagged for manual attention, not fixed here:** this
>    scheduled task runs on a fresh branch name each time
>    (`claude/<slug>-<random>`), so an unmerged draft PR from one run is
>    never reused by the next — it just opens another one from scratch.
>    Every one of the four repos now has **two** open draft "sync docs" PRs
>    covering near-identical ground (yesterday's `*-sy7lxb` branches and
>    today's `*-vwudox` branches: AuraPulse #10 & #11, TrainFitter #1 & #2,
>    Twistify #7 & #8, and this repo's own #1 plus whatever branch today's
>    push lands on). None of this session's agents were told about the
>    older PRs going in, so they didn't dedupe against them. Recommend
>    reviewing and merging one PR per repo, closing its sibling, before the
>    next scheduled run adds a third.

## Repos to pin

Three public project repos now exist (plus this profile repo itself). All
three are reasonable pin candidates — no scratch/test repo has shown up yet
to crowd them out. The "same skill twice" gap flagged below is now partially
closed by AuraPulse, which demonstrates conditional routing / local-LLM
classification rather than repeating TrainFitter's or Twistify's shape.

## Quality improvements — TrainFitter

| Item | Status | Recommendation |
|---|---|---|
| README | ✅ Strong — grown substantially since this note was written (live demo, Gmail/Notion, client portal, inbox automation all now documented) | No change needed |
| Tests | ✅ 245 tests passing (`tests/test_*.py`), covers rule engines, validator, orchestrator, connectors (mocked network), PDF round-trips | No change needed |
| CI | ✅ `ci.yml`, badge in README | No change needed |
| `.env.example` | ✅ Present and complete against every env var actually read in code | No change needed |
| `.gitignore` | ✅ `.venv` and secrets properly excluded (verified: 0 tracked files under `.venv`) | No change needed |
| **LICENSE** | ✅ Resolved — MIT license added, badge in README | — |
| **Docker** | ❌ Still no Dockerfile | Add one — see rationale below (still open) |

## Quality improvements — Twistify

| Item | Status | Recommendation |
|---|---|---|
| README | ✅ Strong — clear differentiation ("not another movie CRUD"), screenshots, honest status table, now also documents the live deploy and full judge-calibration results | No change needed |
| Tests | ✅ `tests/test_metrics.py` (8 tests), CI green | No change needed |
| CI | ✅ `tests.yml`, badge in README, plus a release badge (`v1.0.0`) | No change needed |
| `.gitignore` | ✅ Correct — verified no `__pycache__`/`.pytest_cache` tracked | No change needed |
| **`.env.example`** | ❌ Still missing — README's Configuration table documents every env var in prose, but there's no copy-pasteable template | Add one (still open) |
| **LICENSE** | ❌ Still missing (README says "no license defined yet — ask first") | Add one, even a restrictive one — an explicit license reads as more finished than a note asking people to ask (still open) |
| **Unpushed commits** | ✅ Resolved — `main` is fully in English, repo is current | — |
| **Docker** | ❌ Still no Dockerfile, despite being a FastAPI app with no database — the easiest repo of the three to containerize | Add one — see rationale below (still open) |

## Quality improvements — AuraPulse

| Item | Status | Recommendation |
|---|---|---|
| README | ✅ Strong — features, architecture diagram, tech stack, honest limitations section with real eval numbers | No change needed |
| Tests | ✅ 63 passing (`pytest -q`) | No change needed |
| CI | ✅ `ci.yml` runs pytest + ruff + mypy, badge in README | No change needed |
| `ruff` / `mypy` | ✅ Both clean (`All checks passed!` / `no issues found in 19 source files`) | No change needed |
| `.env.example` | ✅ Present (documents `OLLAMA_HOST`/`OLLAMA_MODEL`, both optional) | No change needed |
| **LICENSE** | ✅ Present (MIT) | — |
| **Docker** | ❌ No Dockerfile — lower priority here than for Twistify/TrainFitter since the project depends on a local Ollama server anyway, so a container wouldn't be self-contained without also bundling/documenting Ollama | Optional — a `docker-compose.yml` pairing an app container with an `ollama/ollama` service would be the honest way to do this, not a plain Dockerfile |
| **End-to-end classification script** | ❌ No script classifies the full review subset and writes `data/processed/classified_reviews.jsonl` yet — `generate_report.py` is only demonstrable via `--demo` today | Add one to close out Hito 0 (flagged by the repo's own doc-sync pass, not by this file originally) |

## Why Docker matters here specifically

You listed Docker and deployment as target skills, but neither public repo
demonstrates it. Twistify is a small FastAPI + vanilla JS app with no database —
it's a same-day job to add a `Dockerfile` (and optionally a one-line
`docker-compose.yml` for the `ANTHROPIC_API_KEY` env var) and mention it in the
"Try it in 2 minutes" section. This closes the single biggest gap between what
your resume claims and what a recruiter can click through and verify.

## New portfolio projects worth building

Your three existing repos all show a closely related skill: building an
LLM-agent app with a rules/eval layer (AuraPulse adds a genuinely different
angle — local-model classification and conditional routing — but it's still
"agent app," not the classic ML/data side of your CV). A hiring manager
scanning your profile for 60 seconds still sees one shape three times.
Prioritized suggestions, in order of how much they'd diversify your
portfolio relative to effort:

1. **A visible data-analysis project (Pandas/PySpark/ML).** Your CV shows real
   PySpark/Azure Databricks/Azure ML experience from IVIRMA Global and SQL/ETL
   work from SDG Group — but that code is proprietary and can't be public. Right
   now nothing in your GitHub shows this side of your work at all; both public
   repos are backend/agent apps. A focused public project (EDA + feature
   engineering + a baseline forecasting or NLP model on a public dataset, with a
   PySpark step to justify the tool) would be the highest-leverage addition,
   since it's real, substantial experience with zero public evidence.
2. **A minimal production-RAG project.** You're already studying this
   (ingestion → chunking → embeddings → hybrid search → reranking → citations →
   eval) — turning it into a small working repo, even over a narrow document set,
   converts "learning" into "shipped," and is a natural extension of the evals
   discipline you already show in Twistify.
3. **Containerized deployment reference.** Could be as simple as taking TrainFitter
   or Twistify and adding Docker + a one-command deploy (Fly.io/Railway/Render free
   tier), documented in a short `docs/deployment.md`. Directly demonstrates the
   "Docker and despliegue de servicios" interest you listed, with near-zero new
   code.
4. **A generalized evals/observability mini-tool.** Twistify already has a
   calibrated evals harness (leakage/grounding/richness). Extracting the reusable
   part (a small library or CLI: "run N test cases against a generator, calibrate a
   judge, report drift over time") as its own repo would read as a genuine niche
   specialty rather than a one-off feature.
5. **Optional, higher effort:** a small agent-security demo — a tool-calling agent
   with typed permissions and a prompt-injection test suite (attack cases +
   pass/fail). Directly matches the "Security" item in your current-learning list
   and is a differentiator few candidates show.

## General quality checklist

- [x] Add a `LICENSE` to `TrainFitter` — done (MIT).
- [ ] Add a `LICENSE` to `Twistify` (MIT is the standard default for
      portfolio code; keep "ask first" wording only if you genuinely want to
      restrict reuse — but an explicit restrictive license still reads better
      than no license at all). **Still open.**
- [x] Push Twistify's pending commits (English translation) — done, `main`
      is fully in English.
- [ ] Add `.env.example` to Twistify (TrainFitter and AuraPulse both already
      have one — good pattern, just replicate it). **Still open.**
- [ ] Add a `Dockerfile` to at least Twistify (simplest target — FastAPI, no
      database), ideally TrainFitter too. AuraPulse is a special case (see
      its own table above — `docker-compose.yml` pairing with an Ollama
      service, not a plain Dockerfile). **Still open.**
- [x] Create the `serpeigd/serpeigd` special repo on GitHub and push this
      folder's `README.md` to it — done, this repo exists and the README is
      kept in sync here.
- [ ] Build the Pandas/PySpark data project (see above) — closes the biggest
      credibility gap between your stated background and your visible repos.
      **Still open**, still the single highest-leverage addition.
- [x] AuraPulse became the third solid repo — revisit pinning if a fourth,
      unrelated-shape project shows up; for now all three project repos are
      correctly pinned.
- [ ] Close out AuraPulse's Hito 0 by adding the end-to-end classification
      script that writes `data/processed/classified_reviews.jsonl` (see its
      own table above) — the one piece stopping `generate_report.py` from
      being demonstrable against real data, not just `--demo`.

## Priority x effort

| Priority | Effort | Item | Status |
|---|---|---|---|
| High | Low | Push Twistify's pending commits | ✅ Done |
| High | Low | Publish this README to `serpeigd/serpeigd` | ✅ Done |
| High | Low | Add LICENSE to TrainFitter | ✅ Done |
| High | Low | Add LICENSE to Twistify | Still open |
| High | Medium | Add `Dockerfile` to Twistify | Still open |
| High | Medium | Add `.env.example` to Twistify | Still open |
| High | Low | Close out AuraPulse Hito 0 (full-dataset classification script) | Still open |
| High | High | Build the Pandas/PySpark data-analysis project | Still open |
| Medium | Medium | Add Dockerfile (or `docker-compose.yml`) to TrainFitter / AuraPulse | Still open |
| Medium | High | Build the production-RAG project | Still open |
| Low | Medium | Extract Twistify's evals harness into a standalone tool | Still open |
| Low | High | Agent-security demo project | Still open |
