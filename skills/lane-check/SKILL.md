---
name: lane-check
description: "Use when a parallel agent (a lane, teammate, session or subagent) reports work done, committed, merged or passing, before merging its branch, scoring it, or telling the person it is done; also when its reply quotes gate numbers, break counts or 'evidence already present', and when the person says 'check the lane', 'did it actually' or '/lane-check'."
---

# Lane check

A "lane" here is one agent working in its own worktree (a separate working copy of the code) on its own branch (a
separate line of work in the code's history).

A lane's reply is its own account of what it did. It is not evidence. The incident: a lane merged two branches (joined
them into one) and reported every gate green. A gate is a check that must pass before work moves on. It also said "the
10 break-test output files were already present and were not re-run since no source files were modified after they were
generated". The output files were from the evening before. The merge had rewritten one of the files they covered,
hours later. The gates were real. The break evidence proved nothing about the merged file. (A break test deliberately
damages one line of code to see whether the tests notice.) Someone caught it only because they looked. This skill makes
the looking routine.

## The order: cheap facts first, then the expensive reruns

1. **Where it actually is** (one shell call, in the lane's folder):
   - Run `git log --oneline -5` and `git status --short | grep -v '^??'`. Is HEAD (the latest commit, a saved change)
     the commit it named? Is the tree clean? A dirty tree after "committed" means a change is only half in.
   - Run `pgrep -fl "<test runner or build tool>" | grep <worktree>`. This lists programs still running in that
     folder. If it is still running anything, it is not done, whatever it said.
   - Look for conflict markers (leftover signs of a merge that went wrong). Run
     `git grep -nE '^(<<<<<<<|>>>>>>>)'`. Also look for `=======` alone on a line in source files.
2. **Nothing lost** (for a merge): count the tests on each parent (the two branches that were joined) and on the merge
   base (the point where they split). Use the same command each time, for example
   `git grep -c '<test marker>' "<rev>" -- <source dirs>`. The merge should have parent 1 + parent 2 - base. More is
   fine if the lane says why. Fewer means a side was dropped. Compare like with like. A test runner's "N passed"
   covers every package, so it never equals a grep over one directory. Check your ledgers for duplicate rows. In zsh,
   write `git show "${rev}:path"`, never `$rev:path` (`:a` is a zsh modifier, so the shorter form breaks).
3. **Evidence is newer than the code it proves.** For every break-list output and gate log it cites, compare the
   file's modification time with the last change to the code it covers. Get the file's time with
   `stat -f '%Sm' <file>` on macOS or `stat -c %y` on Linux. Get the code's time with
   `git log -1 --format=%ci -- <the files it covers>`. Evidence older than the last change to those files is stale:
   rerun it. "Already present", "not re-run" and "unchanged since" are the words that tell you to look here.
4. **Its claims, one by one.** Check every row or feature it calls carried:
   - The test file exists and has one test per case in the original. Count the cases in both.
   - Its break list (see "Breaks" below) ran with every line killed. `grep -cE "SURVIV|TIMEOUT"` on the output gives 0.
   - A "skipped" or "n/a" has a reason that still holds when you read the original test.
   - **Wired:** for each new public function in the diff, grep its name in the source outside test files and outside
     its own file. Find them with `git diff <base>..HEAD | grep '^+.*pub fn'`, or your language's equivalent. No caller
     means it is on the shelf, not carried. The note must say so, or the work goes back. (A later review found eight
     modules, around 8,000 lines, "carried" with no caller.)
   - **Owned:** `git diff --stat <base>..HEAD` names only files the brief said the lane owns, plus the agreed shared
     files.
   - **Old omnibus rows:** a row with fewer named tests than the original has cases is partial, whatever it says.
5. **Your own breaks, then the gate.** Every merge gets breaks you wrote, then the full gate. Write 4-8 breaks aimed at
   what the lane changed, not copies of its list. Put at least one on a call site. A break is a one-line change that
   makes the code wrong. A mutation runner applies it, reruns the tests and reports whether any test failed. Then,
   once per batch of merged lanes, run the full test suite, the release build and your ledger checks. Never say
   "passed" without seeing the number.
6. **See it.** Copy the gated build to a scratch location and run it against throwaway data, never the real data. Drive
   what the lane changed, plus one send, one follow-up and one stop. If the lane itself ran through the product, treat
   its run as a test. Every stop, stall, limit or refused tool in that run is a fault until shown otherwise. Each fault
   gets a failing test and a fix.

## What to tell the person
Write one or two lines per lane: what holds, what didn't, and what you are doing about it. Name the lane and its
model. If a claim failed, name the claim and the fact that sank it ("its break evidence predates the merge by 3 hours:
rerunning all 46"). Name the survivors you fixed too. A survivor is a break the tests failed to catch. A lane is scored
by what survived your breaks, not by its reply.

## Signs to stop and look harder
- Round numbers, or counts that match the brief's example exactly.
- "All gates passed" with no counts, or counts from a different branch's size.
- Evidence files in someone else's folder, or dated before the lane started.
- A row marked carried whose test file has fewer cases than the original.
- A whole new module whose only users are its own tests.
