---
name: lane-brief
description: "Use when about to start, restart or carry over a parallel agent (a lane working in its own copy of the code): a new brief, a lane that stopped when the app closed or its plan ran out, a lane moving to another model, or when the person says 'start a lane', 'spin up lanes', 'restart them' or '/lane-brief'."
---

# Lane brief

A "lane" here is one agent working in its own worktree (a separate working copy of the code) on its own branch (a
separate line of work in the code's history).

The incident: every lane start over two days was retyped by hand, and each retype dropped something. One lane went out
on "account default" for its model, and the person said to pick a model on purpose. Early briefs had no title, so the
sidebar showed ten rows that all began "You are picking up a lane...". A restarted lane nearly edited over a mutation
run its stopped predecessor had left going. (A mutation run, also called a break run, deliberately damages lines of code
to see whether the tests notice.) That run was still breaking lines in the folder. This is the brief, whole, so nothing
drops.

## Before starting it (one shell call)
- Run `date`. Run `git -C <worktree> log --oneline -1` to see the latest commit (a saved change in the code's history).
  Run `git -C <worktree> status --short | grep -v '^??'` to list changed files that are not new. Count the dirty files
  (ones with unsaved changes).
- Run `pgrep -fl <mutation runner> | grep <worktree>`. A stopped lane can leave its break run going, and this finds
  any such run. Note it in the brief. Never start a second lane on a folder whose break run is still changing files,
  unless the brief says to wait for it.
- Usage: check what the runtime's plan has left. A runtime is the tool that runs the agent. If one runtime's weekly
  usage is above about 70%, run one lane on it at most. An account near its short-window cap will stop mid-task. Start
  it anyway only if the long window has room, and expect a restart after the reset.
- Build load: decide a cap on how many builds run at the same time. Count your own merge runs and break runs against
  it. (A merge joins one branch into another.) Four heavy builds at once on one machine is a reasonable ceiling for a
  laptop-class box.
- Files: list the files and folders this lane owns. Check that no running lane's brief lists any of them. Grep (search)
  the other handoff files for each one. Two lanes never own the same file. Shared files (a module index, a ledger) are
  touched only by adding lines. (Two lanes once each wrote the same new file from scratch.)

## Starting the conversation, every time
- Set the runtime and an explicit model. Set the effort level too where the runtime takes one. Never use "account
  default".
- Run it in an autonomous mode if your runner has one. If your runner cannot set the working folder as a parameter, the
  brief names the folder instead.
- A stopped lane that was on an account with a spent plan gets a fresh conversation, not a "continue". A continued
  conversation can land back on the account that ran out.

## The brief (fill in the angle brackets; keep every numbered line)

```
<Name> lane: <what, in five words> (<folder>).

You are picking up a lane that stopped part-way <when the app was closed | when its plan ran out> / You are starting a lane.
Work in <worktree> (branch <branch>, HEAD <short hash>). Do not switch branches or start another worktree.

1. Read <worktree>/<handoff file> in full: that is your brief. <Items already done or skipped, and why.>
1a. You own: <files and folders>. Do not edit anything else except to add a line to the shared index and rows to the ledgers. If the work needs a file you do not own, stop and say so. Other lanes are working on: <areas>.
2. Before you edit anything, run `git status` and `git diff`. <N files have uncommitted edits from an earlier run: build on what is right; do not redo it. | The folder should be clean apart from handoff files.>
3. CAREFUL: a mutation run (<mutation runner>) may have been killed mid-way, leaving a deliberately broken line in a file. Compare each changed hunk with the break lists under <scratch>/evidence/ (each entry is `path|||old ==> new`) and put back any hunk that matches a break's `new` side. <If a mutation run from an earlier run is still going here (pid N), wait for it to finish before editing.>
4. For each item: one test per case in the original, each with a `// case:` comment; the code is CALLED from the product, not only from tests: name the call site (file:line, outside test files) for every new public function, or write "on the shelf: <what will call it>" in the ledger note; one break must be on the call site (remove or bypass the call) and must be caught; a break list in <scratch>/evidence/<lane>/<item>.entries, run with your mutation runner; every break caught (a break that only stops the build proves nothing). Then run your ledger checks, and commit that item alone. Stage files by name, never `git add -A`, never handoff files or tool config folders, never --no-verify.
5. Use your own build output folder (<scratch>/target-<name>) and a low job count; put a timeout on every build command and run one build command at a time. Compiles may wait for a slot; that is normal.
6. Before you stop, run the test suite for the package you changed. Do not run the release tests or the release build: the merge and CI run them.
7. Never push. Reply with: the HEAD commit, `git status --short`, the test pass count and exit code as you saw them, each item's break counts, each new public function's call site, and anything left unfinished. A step that was blocked is not a pass.
```

Optional lines, only when they apply. One is a command-wrapper line, if you are trialling one. Never put a wrapper in
front of the mutation runner or the ledger scripts. The other is a known stale note ("a helper may already exist in
<file>: check first").

## After starting it
- Read the first reply once after about 15 seconds. "Working" is fine. A limit or setup error means you should start
  it elsewhere now.
- Add one update line to the current state note. Include the lane, the folder, the conversation id, the runtime and
  model, and why.
- Tell the person the lane by its name and model, never by "account default".
