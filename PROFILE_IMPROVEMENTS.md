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

> **Update (2026-08-09 doc-sync pass):** all four repos' CLAUDE.md files were
> updated (2026-08-07, in a prior session) with a standing dedupe/self-merge
> rule for exactly the gap flagged above — before opening a new "docs: sync"
> PR, check for an existing open one and fold/merge/close rather than
> stacking a third. Confirmed working this run: every repo had **zero** open
> PRs before this pass started (AuraPulse's #12/#13/#14-worth of PRs,
> TrainFitter's #1-#3, Twistify's #1-#9, this repo's #1-#3 are all
> merged/closed) — the duplication problem from 2026-08-07 is resolved, not
> just documented. This pass reset each project repo's designated branch
> from its base first (per the same CLAUDE.md convention, since each
> branch's prior content had already been merged), then ran a focused,
> docs-only review per repo:
> - **AuraPulse** [#14](https://github.com/serpeigd/AuraPulse/pull/14)
>   (merged): found and fixed a real doc/code mismatch — `.env` isn't
>   actually auto-loaded (`python-dotenv` is a listed dependency that's
>   never imported/called anywhere; config is read via plain
>   `os.environ.get(...)`). README and `.env.example` wrongly implied
>   copying `.env.example` → `.env` was sufficient. See the new row added to
>   this file's AuraPulse table below.
> - **TrainFitter** [#4](https://github.com/serpeigd/TrainFitter/pull/4)
>   (merged): `docs/arquitectura.md` and `docs/highlights.md` had drifted
>   behind the most recent feature commit (client roster + trend charts,
>   `ad22bc8`) — fixed, and `docs/highlights.md` gained entry #12. Flagged
>   for manual attention: `CLAUDE.md` itself still says highlights.md is
>   "11 decisions, 1 page" — now stale at 12, left untouched since
>   `CLAUDE.md` was out of this run's docs-only scope.
> - **Twistify** [#10](https://github.com/serpeigd/Twistify/pull/10)
>   (merged): `docs/DESIGN.md` D14 still described best-of-3 draft
>   generation as "not implemented" two commits after it actually shipped
>   and was confirmed working live — fixed. Also fixed a stale count (7→8
>   researched titles) and a wrong tech-stack claim (README credited
>   Anthropic Claude for research-assist drafting; the code only ever calls
>   Groq). Flagged, not fixed (out of file-scope): the `v1.0.0` GitHub
>   Release notes are stale, and `evals/results/substring_calibration.json`
>   has a leftover Spanish `"nota"` field from before the English-only pass.
>
> This file's profile-README edits (TrainFitter/Twistify/AuraPulse featured
> blurbs) are additive — see the "recent improvement" lines added to each
> project's card — not a rewrite of the existing status prose, which was
> re-verified accurate.

> **Update (2026-08-11 doc-sync pass):** a fourth public repo, `TrackerAID`,
> has appeared since the last pass (F0 done, F1 — field-coverage
> measurement, gold-set labeling, BM25 baseline + IR eval harness — in
> progress) and has been added to the profile README's "Currently working
> on" and "Featured projects" sections, plus its own quality table below.
> This is a genuinely different shape from the other three: it's the first
> project with a real IR-retrieval-eval discipline (precision/recall/nDCG/MRR
> against a hand-labeled gold set) and the first to use real orchestration
> tooling (n8n) outside pure Python — it substantially starts closing the
> "production-RAG project" and "toolset diversification" gaps flagged in
> this file's "New portfolio projects worth building" section below (see the
> inline note added there). It does not yet close the still-fully-open
> "visible Pandas/PySpark data-analysis project" gap — TrackerAID's stack is
> retrieval/IR, not the classic ML/ETL side of the CV.
>
> This run also found and fixed one real doc/code mismatch in each of the
> other three repos (small, targeted — most of each README was already
> accurate): AuraPulse's "Tests and checks" section was missing `app/` from
> its `ruff`/`mypy` commands even though CI already lints/type-checks that
> directory (merged, [#21](https://github.com/serpeigd/AuraPulse/pull/21));
> TrainFitter's "never sends automatically" section undercounted its own
> `gmail.send` exceptions (two documented, three in code) and split out the
> `motor="llm"` optional-install step (PR
> [#5](https://github.com/serpeigd/TrainFitter/pull/5), pending CI at the
> time of this pass); Twistify's README picked up the mobile off-canvas
> drawer, the `/api/search` browse tier, and a couple of stale install notes
> (merged, [#11](https://github.com/serpeigd/Twistify/pull/11)).
>
> **Process note:** this run's four project-repo sync agents each hit the
> session's API usage limit mid-task (a capacity issue, not a task failure)
> and had to be resumed manually rather than autonomously; TrainFitter's and
> TrackerAID's README edits were already fully drafted by the time their
> agent was interrupted; and were committed/pushed/PR'd to completion
> instead of redone from scratch — no lost work, just a slower path than
> usual.

## Repos to pin

Four public project repos now exist (plus this profile repo itself). All
four are reasonable pin candidates — no scratch/test repo has shown up yet
to crowd them out. The "same skill twice" gap flagged below is now further
closed by TrackerAID (retrieval/IR-eval + real orchestration tooling) on
top of AuraPulse's earlier conditional-routing/local-LLM angle — a
recruiter scanning the pinned repos now sees four distinct shapes, not one
repeated three or four times.

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
| **`.env` auto-loading** | ❌ `python-dotenv` is a listed dependency but never imported/called anywhere — a `.env` file does nothing by itself, config must be real exported shell env vars. Docs now say this accurately (flagged 2026-08-09) | Either wire in `load_dotenv()` at the scripts' entry points, or drop the dependency if `.env` support isn't actually wanted — small code fix, **still open** |

## Quality improvements — TrackerAID

| Item | Status | Recommendation |
|---|---|---|
| README | ✅ Substantially expanded this pass — repo structure, F1 script usage, a `.env.example`-cross-checked config table, and a limitations section, on top of the architecture/roadmap/privacy sections that already existed | No change needed |
| Tests | ✅ Unit tests for the BDNS client (mocked via `respx`), the BM25 retriever, and IR metrics (`tests/test_*.py`), plus an `integration` marker for a real-API smoke test excluded from default CI | No change needed |
| CI | ✅ `ci.yml` runs `ruff check` + `pytest --cov`, badge in README, green on `main` | No change needed |
| `mypy` | ❌ Not configured (unlike TrainFitter/AuraPulse) — no type-checking step in CI | Optional — add once the codebase is past early-F1 churn; low priority while `extraction/` is still a placeholder |
| `.env.example` | ✅ Present, and now fully cross-referenced against what `config.py` actually reads vs. what's a future-phase placeholder | No change needed |
| **LICENSE** | ✅ Present (MIT) from the start — ahead of Twistify here | — |
| **Docker** | ❌ No Dockerfile — reasonable at this stage (F1, no deployed service yet; Postgres/Supabase and n8n are still unused placeholders per `.env.example`) | Revisit once F3 (n8n + FastAPI in production) actually ships — premature before then |
| **Gold-set labeling** | ❌ 450 candidates generated with heuristic relevance, 0 hand-reviewed — the eval harness runs but the real ablation table it exists to produce isn't published yet | This is F1's own next step per the repo's roadmap, not a documentation gap — flagged here only for visibility |

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
   > **2026-08-11 note:** TrackerAID (see "Repos to pin" above) has since started
   > covering this ground from the retrieval/eval side — BM25 baseline, IR
   > metrics against a gold set, hybrid/reranker stages still on its own
   > roadmap (F1→). It's ingestion+ranking over structured grant records, not
   > embeddings-over-documents RAG, so this item isn't fully closed — but the
   > gap is narrower than when this list was first written.
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
      correctly pinned. **2026-08-11: the fourth showed up** — see next item.
- [ ] Close out AuraPulse's Hito 0 by adding the end-to-end classification
      script that writes `data/processed/classified_reviews.jsonl` (see its
      own table above) — the one piece stopping `generate_report.py` from
      being demonstrable against real data, not just `--demo`.
- [x] TrackerAID appeared as a fourth project repo (2026-08-11) —
      added to the profile README's "Currently working on" and "Featured
      projects" sections and given its own quality table above; all four
      project repos are now correctly pin-candidate quality (CI, tests,
      LICENSE, `.env.example` all present on each).

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
| Low | Medium | Hand-review TrackerAID's 450 gold-set candidates (`relevance` column) to unlock the real ablation table | Still open — tracked as F1 on TrackerAID's own roadmap, not a documentation gap |

---

## Update (2026-08-13 doc-sync pass)

**TravelPlanner** — a ranking system with a grounding check the LLM can't talk
past, a measured price-model MAE, a golden-set eval and `mypy --strict` — had
never been covered by this file and is now in the profile README's "Featured
projects", making five public projects there.

Scope note: this file lives in a **public** repo, so it only ever discusses
public repos. Private repos are tracked in their own repo's `CLAUDE.md`, not
here — see the standing convention in this repo's `CLAUDE.md`.

### Doc-vs-code drift found this pass

Documentation had fallen behind the code in five of the six project repos —
worth recording because the pattern is consistent: **features get built and
the README keeps describing the design they replaced.**

| Repo | What the docs still claimed | Reality |
|---|---|---|
| Twistify | Judge calibration in progress, retrieval "hasn't started" | Six judges tried and closed as unsolved; Milestone 1 complete at 20/20 titles |
| TrackerAID | "F2 in progress", F3 not started | F2 done (91.3% deadline coverage), F3 pipeline/API/n8n running |
| TrainFitter | Forwarded checklists not picked up by the adherence scan | Fixed — only the trainer's own sent copy is excluded now |
| AuraPulse | "The Streamlit app isn't deployed anywhere yet" | Deployed and live; contradicted its own Status section |

### A real defect surfaced by writing the docs

Not a documentation problem — something that only became visible when the
README's claims were checked against the tree.

- [ ] **TravelPlanner: the devcontainer can't build.** `.devcontainer/`
      pins `python:1-3.11-bookworm` while `pyproject.toml` declares
      `requires-python = ">=3.12"` (matching CI, ruff and mypy), so the
      Codespaces install step fails. Fix is either bumping the image or
      lowering the floor — the second means re-auditing 3.12-only constructs
      in `src/`.

### Licensing, now stated everywhere

Every project README gained an explicit copyright and legal notice this pass —
previously most had a one-line License section or none at all. The four repos
with a `LICENSE` file (AuraPulse, TrackerAID, TrainFitter, TravelPlanner) now
also spell out what MIT does *not* cover: the Yelp dataset's own terms, the
Booking.com fixture, BDNS public-sector reuse conditions, and the health-data
obligations that come with running TrainFitter on real clients.

- [ ] **Twistify still has no `LICENSE` file.** Its README now states
      copyright is reserved by default, which is accurate and better than
      silence — but picking a licence is still an open decision, and "all
      rights reserved" on a portfolio repo discourages exactly the
      reading-and-learning it exists to invite. **Still open since the first
      pass.**
- [ ] **The `LICENSE` copyright holder is inconsistent** across the four repos
      that have one: `serpeigd`, `Sergio`, `Sergio Peigneux d'Egmont`, and
      `Sergio (@serpeigd)`. Harmless legally, sloppy on a portfolio. Left
      untouched this pass — the request was scoped to READMEs.

### Housekeeping

- [ ] **TrackerAID PR #1** ("docs: sync README with F1 retrieval eval
      pipeline…", opened 11 Aug) is still open and now superseded. Its still-
      valid content was folded into this pass's PR and updated; it was not
      closed automatically because TrackerAID, unlike the other repos, has no
      `CLAUDE.md` granting standing authorization to merge or close doc PRs.

## Update (2026-08-16 doc-sync pass)

Verified all 5 public repos (AuraPulse, TrainFitter, Twistify, TrackerAID,
TravelPlanner) against their current READMEs/CLAUDE.md. Twistify and
TravelPlanner needed no changes — already accurate. One stale claim found
and fixed in this repo's own `README.md`: TrainFitter's card still said
"a trainer-facing client roster," but that per-client roster table was
removed in favor of an anonymized fleet-level dashboard (per TrainFitter's
own `CLAUDE.md` — "'Clients' is now the dashboard *only*... the per-client
roster table... is gone"). Fixed to "a fleet-level client dashboard."

Three real, out-of-scope-to-fix-here gaps surfaced while verifying:

- [ ] **TrackerAID has no ADR for its F3 decisions.** `docs/adr/` has only
      0001–0004 (architecture-decision-records convention, single-source
      BDNS, logic-in-Python-not-n8n, free deadline extraction), but F3
      (Supabase ingestion pipeline, FastAPI API, n8n scaffold) is
      substantially built with no ADR documenting those choices — a real
      gap against the repo's own stated convention of ADR-ing every
      architectural call.
- [ ] **TrackerAID's `sql/001_init_schema.sql` has a stale comment.** Line 1
      says "Se aplicará vía Supabase (migraciones) en F4," but F3 already
      applies this schema via Supabase (`pipeline.py`/`storage.py` per the
      current README) — the comment describes a design that shipped a
      phase earlier than it says.
- [ ] **AuraPulse's GitHub repo description metadata is stale**, confirmed
      live via the GitHub API: "Detects recurring operational
      inconsistencies in restaurant reviews and turns them into actionable
      product-improvement signal. Zero-cost, local-LLM pipeline (portfolio
      project, Hito 0 in progress)." Hito 0 is done and Hito 1 has shipped
      substantial work (routing, draft-reply generation, escalation
      flagging, a LangGraph reject/regenerate loop, a live Streamlit demo)
      per the repo's own README. Not a file this doc-sync task can edit —
      flagged here for Sergio to update by hand in the repo's GitHub
      settings. **Still stale as of the 2026-08-17 pass below.**

## Update (2026-08-17 doc-sync pass)

Verified all public project repos (AuraPulse, TrainFitter, Twistify,
TrackerAID, TravelPlanner) against their current working trees. AuraPulse,
TrackerAID and TravelPlanner needed no doc changes — already accurate.
Two real drift fixes landed:

- **Twistify** [#14](https://github.com/serpeigd/Twistify/pull/14) (merged):
  `docs/DESIGN.md`'s own "Pending"/"Open questions" sections still described
  Milestone 1 as in-progress ("just needs a live run") even though D16,
  later in the same file, documents it as fully run and closed (20/20
  titles, judge iteration ended for good). The file was internally
  contradicting itself — fixed both sections to match D16's conclusion.
- **TrainFitter** [#9](https://github.com/serpeigd/TrainFitter/pull/9)
  (merged): `docs/arquitectura.md` still described the "Clients" tab as a
  per-client roster table with a low-adherence warning flag
  (`_etiqueta_atencion()`); both were removed from `ui/app.py` in favor of
  an anonymized fleet-level dashboard. Fixed to match — the profile
  README's own TrainFitter card already said "fleet-level client
  dashboard" (see the 2026-08-16 entry above), so no README change was
  needed here, just the architecture doc catching up.

No change to this repo's `README.md` this pass — every claim in the five
featured-project cards was checked against the linked repo's current working
tree and still holds.

### Two real gaps surfaced, not fixed (docs-sync stays docs-only)

- ⚠️ **TravelPlanner has a committed file exposing Sergio's local Windows
  username.** `zz_HOWTOLOCAL.txt` (added in commit `608c530`) is tracked in
  that **public** repo and its entire content is a literal local path:
  `C:\Users\sergi\venvs\TravenPlanner\Scripts\streamlit.exe run ...`. This
  is the exact class of leak this repo's own `CLAUDE.md` was updated
  (2026-08-17) to guard against for Claude-authored commits — this instance
  predates any Claude session and is a personal scratch file, not something
  this task's docs-only mandate covers fixing, but it's live on a public
  repo right now and worth Sergio's own attention (delete, gitignore, or
  leave — more than one reasonable call).
- [ ] **TrainFitter's devcontainer also drifts from its Python target** —
  `.devcontainer/devcontainer.json` pins 3.11 while CI/`pyproject.toml`
  target 3.12. Lower severity than TravelPlanner's equivalent, already-known
  issue above (no `requires-python` floor here, so a Codespace likely still
  installs), but the same category of gap and previously undocumented.

### Housekeeping: session IDs found leaking in three of this repo's own historical PR bodies

While checking for an existing open "docs: sync" PR (none was open — the
last four are all merged/closed, nothing to fold), PRs
[#4](https://github.com/serpeigd/serpeigd/pull/4),
[#5](https://github.com/serpeigd/serpeigd/pull/5) and
[#6](https://github.com/serpeigd/serpeigd/pull/6) (2026-08-09 through
2026-08-13, all merged) turned out to still carry the
`_Generated by [Claude Code](https://claude.ai/code/session_...)_` footer
with a real session ID baked in — the same leak class the 2026-08-17 rule
above was written to close, just three earlier, previously-unnoticed
instances of it. Per that rule ("fix it in place... rather than leaving it
live"), edited all three PR bodies in place to the plain
`https://claude.ai/code` footer; no other content changed.

## Update (2026-08-18 doc-sync pass)

A sixth public repo, **FlightsDelay** (flight-delay-arrival prediction over
13.9M BTS flights, explicit leakage contract, DuckDB-vs-Spark benchmark),
confirmed public via the GitHub API and added to the profile README's
"Currently working on" and "Featured projects" sections, plus two new
`Data stores & orchestration` badges (DuckDB, MLflow) for a genuinely new
tech surface. Repo visibility re-verified for all 8 repos in scope via the
API rather than assumed from memory — **WayWin stays confirmed private**
and correctly absent from every public file here.

Per-repo sync results: AuraPulse and TrainFitter needed no doc changes
(re-verified against their working trees). Twistify
([#15](https://github.com/serpeigd/Twistify/pull/15), merged): a real
README inaccuracy — "26 tests"/"26/26 passing" in four places, but running
`pytest` with only CI's own installed deps gives 18 passed + 2 skipped
(two test files `importorskip` optional deps CI never installs). TrackerAID
([#6](https://github.com/serpeigd/TrackerAID/pull/6), merged): two real
*code* gaps found and documented (not fixed, per this task's docs-only
mandate) — `extraction/llm_ollama.py` ignores the `OLLAMA_URL`/`OLLAMA_MODEL`
env vars its own README documented as configurable (hardcoded constants
instead), and `pipeline.py` (F3) doesn't actually filter ingested grants by
`abierto` yet, though `docs/gold-labeling-criteria.md` said it did.
TravelPlanner: no doc changes needed; the `zz_HOWTOLOCAL.txt` local-path
leak flagged 2026-08-17 is **still present**, and a new small one found —
`evaluation/scenarios.py`'s docstring says "ten requests," `GOLDEN_SET`
actually holds 11 (matches the README's correct "11/11," only the source
docstring undercounts).

WayWin (private, no PR merge authorization documented in its `CLAUDE.md`):
found and folded two competing "docs: sync" PRs into one
([#5](https://github.com/serpeigd/WayWin/pull/5), left open as draft) —
the older PR (#4) had already independently renamed "viaje"→"plan"
throughout and documented number-based bets, reactions, reopening, activity
history and admin bulk-points that this pass's own first draft had missed;
verified both against the code and merged the accurate parts of each rather
than picking one blind. FlightsDelay: a PR (#1) already existed from an
earlier attempt this same pass — left open as draft (no merge authorization
there either).

**New instance of the session-ID leak, caught and fixed in place**: two PR
bodies opened *during this same pass* — Twistify #15 (already merged into
`main` by the time this was caught) and FlightsDelay #1 — used the
`_Generated by [Claude Code](https://claude.ai/code/session_...)_` footer
with a real session ID, the exact same mistake the 2026-08-17 entry above
documents fixing three instances of. Edited both PR bodies in place to the
plain `https://claude.ai/code` footer. This is the second time this leak
class has recurred after being "fixed" — worth Sergio's attention as a
process gap (the rule lives in every repo's `CLAUDE.md`, but a background
sync agent still produced it twice more), not just a one-off correction.
