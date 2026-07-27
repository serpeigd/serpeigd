# GitHub profile & portfolio — improvement notes

Based on a direct inspection of both local repos (`TrainFitter`, `Twistify`) and the
public state of `github.com/serpeigd` (2 public repos, both already pinned, no
profile README until now). Nothing below is invented — every point ties to something
observed in the code, git history, or GitHub API response.

## Repos to pin

You only have two public repos, and both are already pinned — nothing to change there.
That said, it means your entire public portfolio is "LLM agent app with an eval
harness," twice. Good depth, no breadth. See "New portfolio projects" below for the
gap this creates.

## Quality improvements — TrainFitter

| Item | Status | Recommendation |
|---|---|---|
| README | ✅ Strong — problem framing, usage, structure, honest "what's not done yet" section | No change needed |
| Tests | ✅ 6 test files (`tests/test_*.py`), real coverage of routine/diet/validator/orchestrator | No change needed |
| CI | ✅ `ci.yml`, badge in README | No change needed |
| `.env.example` | ✅ Present, documents `ANTHROPIC_API_KEY` | No change needed |
| `.gitignore` | ✅ `.venv` and secrets properly excluded (verified: 0 tracked files under `.venv`) | No change needed |
| **LICENSE** | ❌ Missing | Add one (see checklist) |
| **Docker** | ❌ No Dockerfile | Add one — see rationale below |

## Quality improvements — Twistify

| Item | Status | Recommendation |
|---|---|---|
| README | ✅ Strong — clear differentiation ("not another movie CRUD"), screenshots, honest status table | No change needed |
| Tests | ✅ `tests/test_metrics.py`, CI green | No change needed |
| CI | ✅ `tests.yml`, badge in README | No change needed |
| `.gitignore` | ✅ Correct — verified no `__pycache__`/`.pytest_cache` tracked | No change needed |
| **`.env.example`** | ❌ Missing (README references `ANTHROPIC_API_KEY` usage indirectly but gives no template) | Add one |
| **LICENSE** | ❌ Missing (README says "no license defined yet — ask first") | Add one, even a restrictive one — an explicit license reads as more finished than a note asking people to ask |
| **Unpushed commits** | ⚠️ 4 local commits ahead of `origin/main` (English translation of UI/docs) | Push them — right now the public repo is still in Spanish while your target roles are English-speaking |
| **Docker** | ❌ No Dockerfile, despite being a FastAPI app — the easiest of your two repos to containerize | Add one — see rationale below |

## Why Docker matters here specifically

You listed Docker and deployment as target skills, but neither public repo
demonstrates it. Twistify is a small FastAPI + vanilla JS app with no database —
it's a same-day job to add a `Dockerfile` (and optionally a one-line
`docker-compose.yml` for the `ANTHROPIC_API_KEY` env var) and mention it in the
"Try it in 2 minutes" section. This closes the single biggest gap between what
your resume claims and what a recruiter can click through and verify.

## New portfolio projects worth building

Your two existing repos both show the same skill: building an LLM-agent app with a
rules/eval layer. That's a real and valuable skill, but a hiring manager scanning
your profile for 60 seconds sees one thing twice. Prioritized suggestions, in order
of how much they'd diversify your portfolio relative to effort:

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

- [ ] Add a `LICENSE` to both `TrainFitter` and `Twistify` (MIT is the standard
      default for portfolio code; keep "ask first" wording only if you genuinely
      want to restrict reuse — but an explicit restrictive license still reads
      better than no license at all).
- [ ] Push Twistify's 4 pending commits (English translation) so the public repo
      matches what recruiters will actually read.
- [ ] Add `.env.example` to Twistify (TrainFitter already has one — good
      pattern, just replicate it).
- [ ] Add a `Dockerfile` to at least Twistify (simplest target), ideally both.
- [ ] Create the `serpeigd/serpeigd` special repo on GitHub and push this
      folder's `README.md` to it — that's the only way GitHub renders a README
      on the profile page itself (`github.com/serpeigd`) instead of just inside a
      normal repo.
- [ ] Build the Pandas/PySpark data project (see above) — closes the biggest
      credibility gap between your stated background and your visible repos.
- [ ] Once you have 3+ solid repos, revisit the pinned selection — right now
      pinning both existing repos is correct by default (you only have two), but
      don't let a future repo like a scratch/test one crowd them out.

## Priority x effort

| Priority | Effort | Item |
|---|---|---|
| High | Low | Push Twistify's 4 pending commits |
| High | Low | Publish this README to `serpeigd/serpeigd` |
| High | Low | Add LICENSE to both repos |
| High | Medium | Add `Dockerfile` to Twistify |
| High | Medium | Add `.env.example` to Twistify |
| High | High | Build the Pandas/PySpark data-analysis project |
| Medium | Medium | Add Dockerfile to TrainFitter |
| Medium | High | Build the production-RAG project |
| Low | Medium | Extract Twistify's evals harness into a standalone tool |
| Low | High | Agent-security demo project |
