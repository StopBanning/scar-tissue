---
name: repo-verdict
description: "Use when the person sends a GitHub repo, crate, package, tool or project link and asks you to look into it, whether it is relevant, whether it could be used, or whether it is nonsense; also for 'look into this', 'is this anything', 'could we use this' or '/repo-verdict'."
---

# Repo verdict

The person said they would be sending a lot of links from a world they don't know well. They wanted to be told when
something is just nonsense, because they are interested and still learning. They also said to ask two questions, not
one: could it go into the product, and could it make the way the team works better? They were "looking for anything."
So every link gets both questions and a straight verdict they can learn from.

The incident that set the checks: a repo led with a table of speed tests for a feature. Its own README marked that
feature "release binaries only, not in the public build" (so the code isn't shared, only the finished program). The
feature could not be found in the public code. A claim you can't find in the repo is not a feature.

## Gather (read-only, one or two calls; use the `gh` command-line tool for GitHub, not a browser)
- `gh api repos/<o>/<r> --jq '{d:.description,s:.stargazers_count,l:.license.spdx_id,p:.pushed_at,lang:.language}'`
  (gets the description, stars, license, last update and language)
- Read the README: `gh api repos/<o>/<r>/readme --jq .content | base64 -d`. Skim past the badges (status pictures). If the license reads "NOASSERTION", read the first lines of the LICENSE file. When the layout
  matters, list the top-level files: `gh api repos/<o>/<r>/contents --jq '.[].name'`.
- Check that the headline claim exists in the public code.
- Already looked at it? Search your notes file of past verdicts for the name. If you find it, say when you looked and
  what has changed since. No fresh essay.

## Judge it against two things
1. **The product:** your own list of what the product does or needs. Write it once at the top of your notes and reuse
   it.
2. **The workflow:** how many tokens (the units AI services charge for) get used, how much work the agents get done,
   checking, build speed and memory use, and reviewing the agents' work.

Give one verdict:
- **Relevant**: it touches either list and you could act on it. Name the action (try it, read a certain file, give it
  to an agent later).
- **Interesting, not for us**: good work on a different problem. For example, a library for calling model APIs (the
  way programs talk to AI services) when the project runs agents instead. Name the one idea worth keeping, if any.
- **Skip**: the repo is README-only, brags about benchmarks (speed tests) it ran itself, says "rewrite everything in X",
  or its headline claim is missing from the public code. Say which.

## Rules
- The license decides what you may take. MIT or Apache means you may use the code if you credit the author. GPL or AGPL
  means you may take ideas only, never code.
- A trial that installs something, or changes how agents run, needs the person's yes. Never try anything that sends your
  agents' sign-ins through a third party. If a tool's proxy (a middleman server) would do that, skip the tool.
- Use plain words. Explain jargon once ("a crate is a Rust library", meaning a bundle of ready-made code). Give the
  reason for your verdict, so the person learns to spot it themselves.
- Numbers (stars, dates, sizes) must come from the `gh` call you made this turn.

## Record
Add one entry per repo to your notes file: date, stars, license, what it is in one line, the verdict, and why.

## Reply shape
For each repo: **Name: verdict.** Then two to four lines on what it is, why you gave that verdict, the product angle and
the workflow angle. With several links, put the relevant ones first. End with any trial worth running, phrased as a
question.
