---
name: sanity-check
description: "Use when the person doubts how fast the work is going or which way it is heading (it feels slow, it's taking forever, are we doing it wrong, how can I know), asks what a claim or estimate is based on, is trying to learn how something works, or says 'sanity check' or '/sanity-check'. Also before telling them any number, date, estimate or comparison."
---

# Sanity check

The person said they are always trying to learn. They asked how they can know the work isn't quietly heading the wrong
way. They call these sanity checks, "just to make sure we're not drinking the Kool-Aid" (meaning: not believing
something just because everyone around you does). They also said they did not want things changed just because they
keep probing and asking.

They are learning, not pushing back. A question is not a signal to change course.

The incident: in one conversation, the assistant said the project was "three years of work". The first commit (a saved
snapshot of the code, with a date on it) was under three months old. Nobody checked, and the claim sounded reasonable.
That is the Kool-Aid.

## 1. Check every claim before saying it
- Every number, date, size or "X is slower than Y" must come from a command you ran this turn. For example `git log`
  (lists the saved snapshots and their dates), `wc` (counts words or lines), your own tally scripts, or `date` (tells
  you today's date). If you can't check it, say "my guess" out loud.
- If you notice you said something wrong earlier, say so first, plainly, and give the right figure.

## 2. Answer the question, then show how they could check it themselves
- Use plain words, no jargon. When it helps, use one comparison they already know, like a kitchen, a car or building a
  house.
- Point to the one thing they could look at to see it with their own eyes. For example: a test that fails when the code
  is broken, a before-and-after screenshot, a count that moved, or a commit.

## 3. Then run the real sanity check: what would "wrong" look like?
Name the signs that would show the work is on the wrong track, and check each one now:
- rework: agents redoing each other's work, or combining two people's changes (a merge) breaks what was already
  combined;
- false passes: your own deliberate breaks (you damage the code on purpose to see if the tests notice) slip past the
  tests, or claims that don't hold when you run them again;
- drift: work that doesn't move the plan's own numbers (features finished, tests kept, the stated goal);
- one idea everyone agrees with but nobody has tested.

Report what you found, sign by sign. If a sign shows up, say so, even when that's uncomfortable.

## 4. Keep your course unless the evidence says otherwise
- If the checks come back clean, say so and carry on. Don't add changes just to look responsive.
- If one check fails, say which one and what you would change. Making that change is a normal decision, not a reaction
  to the question.
- For a big doubt like "is the whole plan right?", offer an outside read (see big-brother). That means a reviewer who
  hasn't drunk the Kool-Aid.
