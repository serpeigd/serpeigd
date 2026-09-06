# CLAUDE.md — serpeigd (GitHub profile repo)

This repo is the special `serpeigd/serpeigd` GitHub profile repo: `README.md` renders
directly on `github.com/serpeigd`. `PROFILE_IMPROVEMENTS.md` is a running set of notes
on portfolio gaps and priorities, based on direct inspection of the other project
repos — not invented, and updated (append, don't rewrite history) rather than replaced
each pass.

## Standing conventions

- All repo content (README, notes, commit messages) is written in English. Chat with
  the user stays in Spanish.
- No CI is configured here (it's a static README + a notes file, nothing to test) —
  don't add one speculatively.
- **Keep it short (2026-08-13, explicit request in chat).** Too much text, too much
  explaining. Lead with the answer or the change; give reasoning only where it would
  change a decision. Don't recap work already visible in the diff, don't restate the
  question before answering it, and don't close with a summing-up line. Applies to
  chat, commit messages and PR bodies. Reference docs (README, this file) can be
  longer, but only where the length earns it.
- Keep the featured-projects section honest and current: pull status/stack directly
  from each project repo's own README/CLAUDE.md rather than guessing or letting a
  description go stale after a project repo changes.
- **This repo is public — only public repos belong in it (added 2026-08-13, explicit
  decision in chat).** Every file here is publicly readable: `README.md` renders on
  the profile page, and `PROFILE_IMPROVEMENTS.md` and this file are just as visible.
  **None of them may name, describe, or link a private repo — not even as an example
  of what to exclude.** Before writing about a project anywhere in this repo, check
  its actual visibility via the API; don't assume from memory. Private repos are
  tracked in their own repo's `CLAUDE.md`, which is private with them.
  - This is a real correction, not a hypothetical: the 2026-08-13 doc-sync run added
    a private repo to Featured projects, the project owner removed it and asked that
    it stay out, and the same run then leaked it twice more — into
    `PROFILE_IMPROVEMENTS.md`, and again into this file while writing up the lesson.
  - **Recurred again 2026-08-23, in a different spot**: the 2026-08-18 pass's own
    process notes in `PROFILE_IMPROVEMENTS.md` named the private repo, linked its
    PR, and described its app features (bet types, reactions, admin actions) while
    writing up how that sync run went — not Featured Projects this time, but the
    rule covers the whole file, not just that section. Caught and redacted
    2026-08-23 (repo referred to only as "the private repo in scope," no name/link/
    feature detail). The rule isn't just "don't feature it" — it's "don't write
    anything identifying about it here at all," including in a retrospective note
    about the sync process itself.
  - **Being in scope for the sync task and being featured here are separate things.**
    A private repo's own README still gets maintained by the recurring run. That is
    not a reason to surface it on the profile. Each excluded repo says so in its own
    `CLAUDE.md`, so read those before deciding what belongs on the profile.

## Run-summary format for the scheduled cross-repo sync (added 2026-08-30, explicit request in chat)

The final summary of a cross-repo documentation-sync run — both the chat reply and
the push notification sent when the run finishes — must be **short and visual, in
Spanish**, readable at a glance. Not prose paragraphs (the previous default): a
compact bullet list or mini-table, one line per repo with an emoji/word verdict
(no changes / merged / open, needs you), then a short "needs your attention" list
for anything urgent (a leaked secret/path, broken CI, a PR nobody can merge). Full
detail already lives in each repo's own PR body and in this repo's
`PROFILE_IMPROVEMENTS.md` — the run summary should point there, not repeat it.
This is specifically about the *summary delivered to Sergio when the task runs*,
not about this file's or the README's own writing style, which stays under the
"keep it short" convention above (English, prose is fine there).

**Give this summary every time the task finishes, not only in the push
notification (added 2026-09-06, explicit request in chat).** The chat reply at
the end of a run must carry the same short/visual/Spanish summary described
above — repo-by-repo verdicts, then a "needs your attention" list — so it's clear
at a glance what happened even without opening the notification.

## Scheduled documentation-sync runs (added 2026-08-07, explicit decision in chat)

Standing authorization to merge doc-only PRs from the recurring cross-repo
documentation-sync task yourself, without waiting for approval — there's no CI gate
here, so "safe to merge" just means the content is accurate against the other repos'
current state. That scheduled run lands on a fresh randomly-named branch every time,
so an unmerged PR from a previous run is never reused automatically. Before opening a
new one, check for another open PR titled starting "docs: sync" — if found, fold any
still-valid unique content from it into the new one, merge the more complete/accurate
PR, and close the other with a comment linking to the merged one. Don't leave two open
at once.

**Default across all 8 repos is now automatic merge (added 2026-09-06, explicit
decision in chat).** Previously only the repos with a standing-authorization clause
in their own `CLAUDE.md` were merged automatically, and the rest (WayWin,
FlightsDelay) were always left open for manual review even when the change was a
routine, verified documentation fix. Sergio's own instruction: merge automatically
unless something genuinely needs his review. That standing-authorization clause has
since been added to every repo in scope (WayWin and FlightsDelay's own `CLAUDE.md`
now carry it too), so **every repo's doc-sync PR merges automatically by default**
going forward. Reserve manual review (leave the PR open, flag it clearly in the
run summary) only for a PR that:
- touches anything beyond documentation — even a one-line code fix, which this task
  is never supposed to make in the first place (see "docs-sync stays docs-only"
  below);
- encodes an ambiguous decision with more than one reasonable reading (the same bar
  used for a discovered code defect: don't decide it silently, flag it);
- has a merge conflict, a failing CI check (on a repo where CI actually runs on
  doc changes), or any other mechanical reason it isn't cleanly mergeable; or
- the sync agent itself is unsure and says so.
A routine "fixed a stale number/status/feature list, verified against the code" PR —
the overwhelming majority of what this task produces — does not meet that bar and
should merge without waiting.

## How to run the cross-repo sync (learned 2026-08-13, first full sweep of all 7 repos)

That pass found doc-vs-code drift in five of six project repos, so treat drift as
the default expectation, not the exception. The pattern is always the same:
**a feature ships and the README keeps describing the design it replaced.**
Twistify still said retrieval hadn't started after Milestone 1 finished;
TrackerAID was two phases behind; TrainFitter carried a limitation the code had
already fixed; AuraPulse contradicted itself about being deployed.

What that pass learned about doing it well:

- **Verify against the working tree, not the changelog.** Commit messages and a
  repo's own `CLAUDE.md` Status section are leads, not evidence — and they drift
  in both directions. TrainFitter's `CLAUDE.md` was current while its README was
  stale; elsewhere the reverse. Read the actual module before writing about it.
- **Never "correct" a number you can't reproduce.** TravelPlanner's README claims
  245 tests; counting `def test_` gives 213, because parametrized cases inflate
  the collected count. `pytest` is not installed in the scheduled-run environment,
  so the honest move was leaving it alone. A confident wrong number is worse than
  an unverified right one.
- **CI is the check, not a local run.** Nothing is installed in this container by
  default. Say so in the PR rather than implying tests were run.
- **Check repo visibility before writing about a repo anywhere public.** Two of
  eight repos are private. That pass wrote a private one into this repo's public
  files and had to walk it back — then nearly did it again while writing up the
  lesson. Both `README.md` and `PROFILE_IMPROVEMENTS.md` are public, and so is
  this file. Private repos get discussed in their own `CLAUDE.md`, never here,
  not even as an example.
- **A defect found while writing docs is not yours to silently fix.** That pass
  surfaced two real ones — one of them TravelPlanner's devcontainer pinning a
  Python older than the package requires. Both had more than one reasonable fix,
  so both were documented, flagged to Sergio, and left alone. Docs-sync stays
  docs-only.
- **Rebase before assuming a docs branch still applies.** TravelPlanner gained
  two commits on `main` mid-sweep and the PR hit a merge conflict.
- **Standing authorization to merge is per-repo and written down** — check the
  repo's own `CLAUDE.md` before merging, since a one-off "merge it" in chat is not
  a general permission and doesn't carry to the next run. As of 2026-09-06 every
  repo in scope grants it (see the note above), so this is now about confirming the
  authorization is still there and current, not about which repos have it.
- **Never push private data, local file-system paths, session IDs, or any other
  sensitive/internal info into a GitHub repo — public or private (2026-08-17,
  explicit rule from Sergio after a real leak).** The 2026-08-16 sweep's PR
  footers used the attribution line `_Generated by [Claude Code](https://claude.ai/code/session_...)_`
  instead of the plain `https://claude.ai/code` link the convention actually
  specifies — a session-tracking identifier leaked into 5 PR bodies (4 public
  repos plus one private repo) before being caught and fixed the next day.
  Before finishing any push/commit/PR/comment, re-read it for: local paths
  (`/home/user/...`), session or environment identifiers, anything the task
  prompt itself never asked to be written down. If something already went out,
  fix it in place (edit the PR body/file, amend if unpushed) rather than
  leaving it live — don't just avoid it going forward.
  - **Root cause finally identified, 2026-09-06: the GitHub MCP tool itself
    injects this footer.** `mcp__github__create_pull_request` appends
    `_Generated by [Claude Code](https://claude.ai/code/session_...)_` to
    whatever body text is sent — every prior "fix" (2026-08-16, twice on
    2026-08-18, 2026-08-23, 2026-08-30) was catching the symptom after the
    fact, not a body-text mistake by the agent each time. **Standing habit
    going forward: immediately after every `create_pull_request` call, read
    the PR back and strip this footer with `update_pull_request` before doing
    anything else with that PR** (merging, further edits) — don't trust the
    body text you sent to be what actually got posted.
