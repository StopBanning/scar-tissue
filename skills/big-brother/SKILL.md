---
name: big-brother
description: "Use when stuck on a problem after two failed tries, unable to explain a result, or going in circles; before every release; or when the person says 'big brother', '/big-brother', 'big brother brainstorm' or 'call in big brother'."
---

# /big-brother: a second pair of eyes that isn't you

The person asked for a command to use when there is an issue the assistant can't figure out, or when a sweep finds issues
it can't see, calling in a stronger or fresher reviewer. They said they wished they had used it early on.

Why it exists: the two worst misses of one month were not bugs anyone was stuck on. They were gaps nobody looked for:
- every detection improvement of the month lived on the export side only, and the live view was untouched for weeks;
- a finished split-and-rebuild sat on the main branch for days while the public app stayed on the release before it,
  and the build on the person's own machine had been packaged without the splitter's model. (The first telling of this
  was itself wrong, because the release it blamed had never held the splitter. The first review run caught that.)
Both are seen only from the whole project, by eyes that don't share your assumptions.

## When to call it
- **Stuck mode:** `/big-brother <problem>`. Call it yourself when you have tried twice and can't explain why, or when the
  same bug comes back. The person calls it when they think you are going in circles.
- **Sweep mode:** `/big-brother` with no problem. Also before every release (add it to the release runbook as step 0),
  and after any big feature lands.
- **Brainstorm mode:** `/big-brother brainstorm`. A look back at how the work has gone lately, then a plan for what is
  next, picked with the person. See "Brainstorm mode" below. Good every week or two, or when things feel stuck or
  scattered.
- **Permission:** the person typing `/big-brother` is their OK. When you want to call it on your own, ask them first in
  one line, since it costs extra usage. Never call it just to feel safer about something you can check yourself in a few
  tool calls.

## Who the big brother is
- **When this chat itself is on the stronger model:** you are the big brother. Do the look yourself, from the record, as
  if you had no history: reread the files rather than trusting what you remember, and go looking for where your own
  earlier calls were wrong. Call nobody else unless asked. Never assume another model's usage is available; the person
  names who gets called.
- **Big runs = one long-lived reviewer session** on the stronger model that the person can open, watch and talk to. It
  reads the files itself and writes reports to a review folder; you verify every finding and do the work. Steps: write a
  handoff file with the jobs in order; compact this chat first; start the session fresh with no worktree; set its model
  before its first real turn (or start it with a short "wait for the go" prompt, switch, then send the go). Reuse the same
  session for later runs while its context holds.
- **Quick second looks mid-work = an advisor tool**, if your setup has one that sees the whole conversation. Read the
  files into the chat first, then call it. If the person can't see the advisor's answer in their app, show it to them in
  a few lines right after each call, then what you are doing about it. Log each call.
- **Big brother keeps its context; blind brother has none.** Big brother is the one long-lived session (history: sweeps,
  plan check-ins, stuck problems, "are we repeating ourselves"). Never restart it while its context holds.
- **Blind brother = a fresh session every time**, given only the file under review (and its caption, which a stranger
  sees too) and a short brief. It must not read plans, logs, concept files, memory or this skill: not knowing what you
  meant is the point. (A sound was meant to be muffled. The author knew that and heard "as designed". A stranger heard
  nothing.) Its job: the night-before look at each deliverable, written as a stranger's answers. Use a cheaper model
  for a plain fresh-eyes look and the stronger one when the look needs real reasoning (a release-level item, a new
  format, a disagreement to settle). Archive it yourself as soon as its report is read and its verdict logged. Archive,
  never delete. Never reuse one: a second look would not be blind.
- **The nightly order:** blind brother looks first, then big brother reads the blind answer beside the plan and history
  (it catches what only context shows: a caption that says "on the drop" when there is no drop), then you fix what either
  finds, then the person sees the result if the file changed.
- Use whatever session mechanism you already have, not an ad hoc subagent, unless the person has said subagents are fine.

## 1. The brief (the most important step)
Write it to `<repo>/review/<date>-<slug>.md`, then read it and the files it names into the conversation before calling
the advisor.
- **Stuck mode:** the symptom (exact error, numbers, what the person saw), how to reproduce it, what you tried and what
  each try showed, what you have ruled out and how, the files and commits involved.
- **Sweep mode:** what the project is (one paragraph), what you tell people it does (README, release notes, recent
  posts), and the questions: what is claimed but not shipped? What is built but never wired in? What do the tests not
  run? What breaks for a stranger on a clean machine?
- **Facts first, your theory labelled.** The reviewer sees your reasoning anyway; mark what is measured and what you
  suspect, and ask it to look for where you are wrong, not to confirm you.
- Rules for the reviewer: read-only, no pushes, merges, releases or installs, no touching the person's running apps,
  never a real camera or microphone.
- Ask for: findings ranked most severe first, each with file:line evidence, what it would check next, and how sure it is.

## 2. Verify every claim yourself
A confident answer isn't proof. Open the source before stating a fact.
- For each finding: open the file at the line, run the check, reproduce it. Mark it CONFIRMED, WRONG or UNSURE.
- Only confirmed findings go to the person or into code. Wrong ones get logged too (they tell you when to trust whom).

## 3. Tell the person, plainly
A few lines: what it found, which findings are real, what changes for them, and what you are doing about each one. If it
found nothing, say so in one line. That is a result too. A fix that needs a decision goes to them as one short question.

## 4. Log it
Append to `<repo>/review/LOG.md`, one line per run: date, mode, who was called, the problem, findings confirmed and wrong,
and **did it help** (yes / no / partly, and why). After ten runs, read the log and adjust who gets called for what.

## Brainstorm mode: `/big-brother brainstorm`
The person's idea: have the strong model write a full overview of how things have gone recently, then use the team's
skills to build a plan from it. A mixture of review and planning.

1. **The look back.** The strong model does it. If this chat is on it, that is you, reading everything fresh. When a
   separate session is called instead, the brief gives facts and paths, no theory: the current plan, the backlog, the
   metrics and roundups, the work logs, past review reports, the memory folder, the skills (how you work), and `git log`.
   Rules: read-only except its report; never open credentials or tokens; never read session transcripts whole. Ask for:
   - **How things have gone lately:** what worked (with the numbers), what didn't, what you keep repeating, what you are
     not seeing.
   - **How you work:** which skills and habits helped, which cost time, and anything missing.
   - **2-3 directions for the next stretch:** for each, the why, what it would take, the risk, and what it means for the
     person's time.
   - Every claim with its evidence (file, line or number). Report to `<repo>/review/<date>-overview.md`.
2. **Verify** (step 2 above): check every number against the source or a fresh readback, and mark findings CONFIRMED,
   WRONG or UNSURE.
3. **Brainstorm with the person, one short card at a time:** a few lines with the overview's headline, then one question
   at a time. First, what matters most this stretch (the why). Then the directions as one question, your pick first.
   Then the one or two details that change the plan most. Each question has its example above it (a number, a frame, a
   file).
4. **Write the plan** (`<repo>/plans/<date>.md`): what you are doing, why, the order, and what you are NOT doing. It does
   not have to be short. Write it so a session with no context could execute from it: every step with its files, its
   checks, and what done looks like. What the person reads stays short (the cards and a few lines); the plan itself is as
   long as the work needs. One question for their OK, then slot it into your backlog.
5. **Log it:** what it found, what the person picked, and later, whether the plan held up.
