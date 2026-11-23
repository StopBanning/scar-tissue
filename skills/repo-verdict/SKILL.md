---
name: repo-verdict
description: "Use when the person sends a GitHub repo, crate, package, tool or project link and asks to look into it, whether it is relevant, whether it could be used, or whether it is nonsense; also for 'look into this', 'is this anything', 'could we use this' or '/repo-verdict'."
---

# Repo verdict

The person said they would be sending a lot of links in an ecosystem they don't know well, and wanted to be told when
something is just nonsense, because they are interested and still learning. They also said to ask two questions, not
one: could it go into the product, and could it improve the way the team works? They were "looking for anything." So
every link gets both questions and a straight verdict they can learn from.

The incident that set the checks: a repo led with a benchmark table for a feature that its own README marked "release
binaries only, not in the public build". The feature could not be found in the public code. A claim you cannot find in
the repo is not a feature.

## Gather (read-only, one or two calls; use the `gh` CLI, not a browser)
- `gh api repos/<o>/<r> --jq '{d:.description,s:.stargazers_count,l:.license.spdx_id,p:.pushed_at,lang:.language}'`
- README: `gh api repos/<o>/<r>/readme --jq .content | base64 -d`, skimming past badges. If the license reads
  "NOASSERTION", read the head of the LICENSE file. Layout when it matters: `gh api repos/<o>/<r>/contents --jq '.[].name'`.
- Check the headline claim exists in the public code.
- Already looked at? Search your notes file of past verdicts for the name. If so, say when and what changed since, not a
  fresh essay.

## Judge, against two things
1. **The product:** your own list of what it does or needs (write it once at the top of your notes and reuse it).
2. **The workflow:** token use, agent throughput, verification, build speed and memory use, reviewing agents' work.

Verdict, one of:
- **Relevant**: it touches either list and you could act on it. Say the action (trial it, read file X, a lane later).
- **Interesting, not for us**: good work on a different problem (for example, a library for calling model APIs when the
  project runs agents instead). Say the one idea worth keeping, if any.
- **Skip**: README-only, benchmark bragging from its own tests, "rewrite everything in X", or the headline claim is
  missing from the public code. Say which.

## Rules
- The license decides what may be taken: MIT or Apache means code with attribution; GPL or AGPL means ideas only, never
  code.
- A trial that installs something or changes how agents run needs the person's yes. Never anything that routes your
  agents' sign-ins through a third party (skip a tool whose proxy would).
- Plain words, define the jargon once ("a crate is a Rust library"), and give the why, so the person learns to spot it.
- Numbers (stars, dates, sizes) come from the `gh` call this turn.

## Record
One entry in your notes file per repo: date, stars, license, what it is in a line, the verdict and why.

## Reply shape
Per repo: **Name: verdict.** Two to four lines on what it is and why the verdict, the product angle, the workflow angle.
Several links: relevant ones first. End with any trial worth running as a question.
