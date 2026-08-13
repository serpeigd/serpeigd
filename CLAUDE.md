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
- Keep the featured-projects section honest and current: pull status/stack directly
  from each project repo's own README/CLAUDE.md rather than guessing or letting a
  description go stale after a project repo changes.
- **This repo is public — only public repos belong in it (added 2026-08-13, explicit
  decision in chat).** `README.md` renders on the profile page and
  `PROFILE_IMPROVEMENTS.md` is publicly readable too, so *neither* file may name,
  describe, or link a private repo. Before adding a project to either file, check
  it's actually public. Track private repos in their own repo's `CLAUDE.md` instead.
  - **`WayWin` is private and stays out of both files.** The 2026-08-13 doc-sync run
    added it to Featured projects; the project owner removed it and asked that it
    stay out while keeping WayWin's own README maintained. Don't re-add it on a
    later pass just because the repo is in scope for the sync task — being synced
    and being featured are separate things.

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
