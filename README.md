# scar-tissue

Seven Claude Code skills. Each one exists because something went wrong once, and each opens with that incident. The
rule in the skill is the scar that formed over it.

These skills came from building an open-source desktop app called Locust, where several agents worked in parallel
git worktrees ("lanes"). Elsewhere in this repo, that project is just "the app". Adapt the commands to your own tools.

| Skill | What it does | Incident it came from |
|---|---|---|
| [lane-check](skills/lane-check) | Checks an agent's "done" report against facts before you merge or repeat it | Break evidence reported as current was hours older than the merge |
| [lane-brief](skills/lane-brief) | A complete brief for starting or restarting a parallel agent | Hand-retyped briefs dropped the model, the title and a leftover mutation run |
| [sanity-check](skills/sanity-check) | Verifies claims and checks for wrong direction without changing course on a whim | "Three years of work" for a project under three months old |
| [use-your-eyes](skills/use-your-eyes) | Look at the real visual output before calling it ready | Perfect numbers, wrong-looking render |
| [big-brother](skills/big-brother) | Calls in a fresh or stronger reviewer when stuck, before releases, and for planning | Two gaps nobody looked for sat unseen for weeks |
| [repo-verdict](skills/repo-verdict) | A straight verdict on a repo link, for the product and for the workflow | A README benchmark for a feature missing from the public code |
| [after-a-freeze](skills/after-a-freeze) | Recovery steps after the assistant or app freezes or restarts | Out-of-memory freezes from too many parallel builds |

## Install

Copy a skill folder into your skills directory:

```
cp -r skills/lane-check ~/.claude/skills/
```

Each skill is one `SKILL.md`. Start new sessions afterwards so they are picked up.

## License

MIT. See the `LICENSE` file.
