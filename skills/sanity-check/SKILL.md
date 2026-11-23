---
name: sanity-check
description: "Use when the person doubts the pace or the direction of anything (it feels slow, it's taking forever, are we doing it wrong, how can I know), asks what a claim or estimate is based on, is trying to learn how something works, or says 'sanity check' or '/sanity-check'. Also before telling them any number, date, estimate or comparison."
---

# Sanity check

The person said they are always trying to learn, and asked how they can know the work is not just going off in the wrong
direction. They call these sanity checks, "just to make sure we're not drinking the Kool-Aid". They also said they did
not want things changed just because they keep probing and asking.

They are learning, not pushing back. A question is not a signal to change course.

The incident: in the same conversation the assistant said the project was "three years of work". The first commit was
under three months old. Nobody checked, and it sounded reasonable. That is the Kool-Aid.

## 1. Check every claim before saying it
- Every number, date, size or "X is slower than Y" comes from a command run this turn: `git log`, `wc`, your ledger
  scripts, `date`. If it can't be checked, say "my guess" out loud.
- When you find you said something wrong earlier, say so first, plainly, with the right figure.

## 2. Answer the question asked, then show how they could check it themselves
- Plain words, no jargon, one comparison they already know (a kitchen, a car, a house build) when it helps.
- Give them the one thing they could look at to see it with their own eyes: a test that fails when the code is broken, a
  before/after screenshot, a count that moved, a commit.

## 3. Then the actual sanity check: what would "wrong" look like?
Name the signs that would show the work is on the wrong track, and check each one now:
- rework: agents redoing each other's work, merges that break what was merged before;
- false passes: your own deliberate breaks getting past the tests, claims that don't survive a rerun;
- drift: work that doesn't move the plan's own numbers (features done, tests carried, the stated goal);
- one idea everyone agrees with but nobody tested.
Report what was found, sign by sign. A sign that shows up gets said, even when that's uncomfortable.

## 4. Keep course unless the evidence says otherwise
- If the checks come back clean, say so and carry on. Don't add changes just to look responsive.
- If one fails, say which and what you would change. Making the change is a normal decision, not a reaction to the
  question.
- For a big "is the whole plan right?" doubt, offer an outside read (see big-brother): a reviewer who hasn't drunk the
  Kool-Aid.
