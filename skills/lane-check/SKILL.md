---
name: lane-check
description: "Use when a parallel agent (a lane, teammate, session or subagent) reports work done, committed, merged or passing, before merging its branch, scoring it, or telling the person it is done; also when its reply quotes gate numbers, break counts or 'evidence already present', and when the person says 'check the lane', 'did it actually' or '/lane-check'."
---

# Lane check

A "lane" here is one agent working in its own git worktree on its own branch.

A lane's reply is its account, not evidence. The incident: a lane merged two branches and reported every gate green and
"the 10 break-test output files were already present and were not re-run since no source files were modified after they
were generated". The output files were from the evening before. The merge had rewritten one of the files they covered
hours later. The gates were real; the break evidence proved nothing about the merged file. It was caught only because
someone looked. This skill makes the looking routine.

## The order: cheap facts first, then the expensive reruns

1. **Where it actually is** (one shell call, in the lane's folder):
   - `git log --oneline -5` and `git status --short | grep -v '^??'`: is HEAD the commit it named? Is the tree clean?
     A dirty tree after "committed" means a change is half in.
   - `pgrep -fl "<test runner or build tool>" | grep <worktree>`: still running anything? Then it is not done, whatever
     it said.
   - Conflict markers: `git grep -nE '^(<<<<<<<|>>>>>>>)'` (and `=======` alone on a line in source files).
2. **Nothing lost** (for a merge): count tests on each parent and on the merge base, with the same command each time
   (for example `git grep -c '<test marker>' "<rev>" -- <source dirs>`). The merge should have parent 1 + parent 2 - base.
   More is fine if the lane says why; fewer means a side was dropped. Compare like with like: a test runner's "N passed"
   covers every package, so it never equals a grep over one directory. Check your ledgers for duplicate rows. In zsh,
   write `git show "${rev}:path"`, never `$rev:path` (`:a` is a zsh modifier).
3. **Evidence is newer than the code it proves.** For every break-list output and gate log it cites, compare the file's
   modification time (`stat -f '%Sm' <file>` on macOS, `stat -c %y` on Linux) with `git log -1 --format=%ci -- <the files
   it covers>`. Older than the last change to those files means stale: rerun. "Already present", "not re-run" and
   "unchanged since" are the words that mean look here.
4. **Its claims, one by one.** Every row or feature it calls carried:
   - the test file exists and has one test per case in the original (count the cases in both);
   - its break list (see "Breaks" below) ran with every line killed: `grep -cE "SURVIV|TIMEOUT"` on the output is 0;
   - a "skipped" or "n/a" has a reason that still holds when you read the original test.
   - **Wired:** for each new public function in the diff (`git diff <base>..HEAD | grep '^+.*pub fn'`, or your
     language's equivalent), grep its name in the source outside test files and its own file. No caller means it is on
     the shelf, not carried. The note must say so, or the work goes back. (A later review found eight modules, around
     8,000 lines, "carried" with no caller.)
   - **Owned:** `git diff --stat <base>..HEAD` names only files the brief said the lane owns, plus the agreed shared
     files.
   - **Old omnibus rows:** a row with fewer named tests than the original has cases is partial, whatever it says.
5. **Your own breaks, then the gate.** Every merge gets breaks you wrote, then the full gate. Write 4-8 breaks aimed at
   what the lane changed, not copies of its list, and put at least one on a call site. A break is a one-line change
   that makes the code wrong, applied by a mutation runner that reruns the tests and reports whether any test failed.
   Then, once per batch of merged lanes, run the full test suite, the release build and your ledger checks. Never say
   "passed" without seeing the number.
6. **See it.** Copy the gated build to a scratch location and run it against throwaway data, never the real data. Drive
   what the lane changed, plus one send, one follow-up and one stop. If the lane itself ran through the product, treat
   its run as a test: every stop, stall, limit or refused tool in that run is a fault until shown otherwise, and each
   fault gets a failing test and a fix.

## What to tell the person
One or two lines per lane: what holds, what didn't, what you are doing about it. Name the lane and its model. If a claim
failed, name the claim and the fact that sank it ("its break evidence predates the merge by 3 hours: rerunning all 46").
Survivors you fixed get named too. A lane is scored by what survived your breaks, not by its reply.

## Signs to stop and look harder
- Round numbers or counts that match the brief's example exactly.
- "All gates passed" with no counts, or counts from a different branch's size.
- Evidence files in someone else's folder, or dated before the lane started.
- A row marked carried whose test file has fewer cases than the original.
- A whole new module whose only users are its own tests.
