---
name: big-brother
description: "Use when stuck on a problem after two failed tries, unable to explain a result, or going in circles; before every release; or when the person says 'big brother', '/big-brother', 'big brother brainstorm' or 'call in big brother'."
---

# /big-brother: a second pair of eyes that isn't you

The person asked for a command to use when you can't figure out a problem. It also covers a sweep (a broad check of the
whole project) that finds issues you can't see. Either way, it calls in a stronger or fresher reviewer. They said they
wished they had used it early on.

Why it exists: the two worst misses of one month were not bugs anyone was stuck on. They were gaps nobody looked for:
- Every improvement to detection that month went into the export side only. The live view stayed untouched for weeks.
- A finished split-and-rebuild sat on the main branch (the main line of work in the code's history) for days. The public
  app stayed on the release before it. The build on the person's own machine had also been packaged without the
  splitter's model. (The first telling of this was itself wrong, because the release it blamed had never held the
  splitter. The first review run caught that.)

Only someone looking at the whole project can see gaps like these. They need eyes that don't share your assumptions.

## When to call it
- **Stuck mode:** `/big-brother <problem>`. Call it yourself when you have tried twice and can't explain why, or when
  the same bug comes back. The person calls it when they think you are going in circles.
- **Sweep mode:** `/big-brother` with no problem. Also use it before every release (add it to the release checklist as
  step 0), and after any big feature lands.
- **Brainstorm mode:** `/big-brother brainstorm`. It looks back at how the work has gone lately, then makes a plan for
  what comes next, picked together with the person. See "Brainstorm mode" below. It is good every week or two, or when
  things feel stuck or scattered.
- **Permission:** when the person types `/big-brother`, that is their OK. When you want to call it on your own, ask
  them first in one line, since it costs extra usage. Never call it just to feel safer about something you can check
  yourself in a few tool calls.

## Who the big brother is
- **When this chat is already on the stronger model:** you are the big brother. Do the look yourself, from the record,
  as if you had no history. Reread the files instead of trusting your memory. Go looking for where your own earlier
  calls were wrong. Call nobody else unless asked. Never assume another model's usage is available. The person names
  who gets called.
- **Big runs = one long-lived reviewer session** on the stronger model. The person can open it, watch it and talk to
  it. It reads the files itself and writes reports to a review folder. You check every finding and do the work. The
  steps:
  1. Write a handoff file (a note with the jobs, in order).
  2. Compact this chat first (shrink its history so it has room).
  3. Start the reviewer session fresh, with no worktree (a separate working copy of the code).
  4. Set its model before its first real turn. Or start it with a short "wait for the go" prompt, switch the model,
     then send the go.

  Reuse the same session for later runs while its context holds (while it still remembers the earlier work).
- **Quick second looks mid-work = an advisor tool**, if your setup has one that sees the whole conversation. Read the
  files into the chat first, then call it. If the person can't see the advisor's answer in their app, show it to them
  in a few lines right after each call. Then tell them what you are doing about it. Log each call.
- **Big brother keeps its context; blind brother has none.** Big brother is the one long-lived session. Its history
  covers sweeps, plan check-ins, stuck problems and "are we repeating ourselves". Never restart it while its context
  holds.
- **Blind brother = a fresh session every time.** Give it only the file under review (plus its caption, which a
  stranger sees too) and a short brief. It must not read plans, logs, concept files, memory or this skill. Not knowing
  what you meant is the point. (One sound was meant to be muffled. The author knew that and heard "as designed". A
  stranger heard nothing.) Its job is the night-before look at each finished piece, written as a stranger's answers.
  Use a cheaper model for a plain fresh-eyes look. Use the stronger one when the look needs real reasoning: a
  release-level item, a new format, a disagreement to settle. Archive the session yourself as soon as you have read
  its report and logged its verdict. Archive it, never delete it. Never reuse one: a second look would not be blind.
- **The nightly order:**
  1. Blind brother looks first.
  2. Big brother reads the blind answer next to the plan and history. It catches what only context shows, such as a
     caption that says "on the drop" when there is no drop.
  3. You fix what either one finds.
  4. The person sees the result if the file changed.
- Use whatever session mechanism you already have. Do not use an ad hoc subagent (a helper agent you spin up on the
  spot), unless the person has said subagents are fine.

## 1. The brief (the most important step)
Write it to `<repo>/review/<date>-<slug>.md`. Then read it, and the files it names, into the conversation before you
call the advisor.
- **Stuck mode:** write the symptom (the exact error, the numbers, what the person saw). Add how to reproduce it, what
  you tried and what each try showed, and what you have ruled out and how. List the files and commits involved. (A
  commit is a saved change in the code's history.)
- **Sweep mode:** write what the project is (one paragraph). Add what you tell people it does (README, release notes,
  recent posts). Then ask the questions. What is claimed but not shipped? What is built but never wired in? What do the
  tests not run? What breaks for a stranger on a clean machine?
- **Facts first, your theory labelled.** The reviewer sees your reasoning anyway. Mark what is measured and what you
  only suspect. Ask it to look for where you are wrong, not to confirm you.
- Rules for the reviewer: read-only. No pushes (sending work to the shared online copy), merges (joining one branch
  into another), releases or installs. No touching the person's running apps. Never use a real camera or microphone.
- Ask for findings ranked most severe first. Each one needs file:line evidence (the file and line number), what the
  reviewer would check next, and how sure it is.

## 2. Verify every claim yourself
A confident answer isn't proof. Open the source before you state a fact.
- For each finding: open the file at that line, run the check, reproduce it. Mark it CONFIRMED, WRONG or UNSURE.
- Only confirmed findings go to the person or into code. Log the wrong ones too. They tell you when to trust whom.

## 3. Tell the person, plainly
Write a few lines: what it found, which findings are real, what changes for them, and what you are doing about each
one. If it found nothing, say so in one line. That is a result too. If a fix needs a decision, ask the person one short
question.

## 4. Log it
Append to `<repo>/review/LOG.md`, one line per run. Include the date, the mode, who was called, the problem, how many
findings were confirmed and how many wrong, and **did it help** (yes / no / partly, and why). After ten runs, read the
log and adjust who gets called for what.

## Brainstorm mode: `/big-brother brainstorm`
The person's idea: have the strong model write a full overview of how things have gone recently. Then use the team's
skills to build a plan from it. It mixes review and planning.

1. **The look back.** The strong model does it. If this chat is on it, that is you, reading everything fresh. If you
   call a separate session instead, the brief gives facts and paths, with no theory. Point it to the current plan, the
   backlog, the metrics and roundups, the work logs, past review reports, the memory folder, the skills (how you
   work), and `git log` (the list of past changes). Rules: read-only except for its report. Never open credentials or
   tokens. Never read session transcripts whole. Ask for:
   - **How things have gone lately:** what worked (with the numbers), what didn't, what you keep repeating, what you
     are not seeing.
   - **How you work:** which skills and habits helped, which cost time, and anything missing.
   - **2-3 directions for the next stretch:** for each, the why, what it would take, the risk, and what it means for
     the person's time.
   - Every claim comes with its evidence (a file, a line or a number). The report goes to
     `<repo>/review/<date>-overview.md`.
2. **Verify** (step 2 above). Check every number against its source or a fresh readback. Mark findings CONFIRMED,
   WRONG or UNSURE.
3. **Brainstorm with the person, one short card at a time.** Start with a few lines giving the overview's headline.
   Then ask one question at a time:
   1. What matters most this stretch (the why).
   2. The directions, as one question, with your pick first.
   3. The one or two details that change the plan most.

   Put an example above each question (a number, a frame, a file).
4. **Write the plan** (`<repo>/plans/<date>.md`). Say what you are doing, why, the order, and what you are NOT doing.
   It does not have to be short. Write it so a session with no context could carry it out. Give every step its files,
   its checks, and what done looks like. What the person reads stays short (the cards and a few lines). The plan itself
   is as long as the work needs. Ask one question for their OK, then slot it into your backlog.
5. **Log it:** what it found, what the person picked, and later, whether the plan held up.
