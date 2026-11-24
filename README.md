# scar-tissue

Eight rulebooks for an AI assistant, each written right after something went wrong.

## What this is, in plain words

[Claude Code](https://claude.com/claude-code) is an AI assistant that works on a computer: it reads and writes files,
runs programs, and can direct other AI agents. You can give it **skills**, short instruction sheets it reads when a
certain situation comes up, like a checklist a pilot pulls out for a specific emergency.

Every skill here exists because a mistake happened once. Each one starts with the story of that mistake, then gives the
rules that stop it happening again. The mistake is the wound; the rule is the scar tissue. Hence the name.

They came from building an open-source desktop app called Locust, where one assistant ran several AI agents at once,
each building a different piece of the app in its own copy of the code (a "lane"). The skills call it "the app".

## The eight skills

| Skill | What it makes the assistant do | The mistake behind it |
|---|---|---|
| [adhd-mode](skills/adhd-mode) | Bring decisions to a person one at a time, each with something to look at | A screen full of questions, read on a phone, that nobody could answer |
| [sanity-check](skills/sanity-check) | Check every number before saying it, and show the person how to check it too | The assistant called a project "three years of work". It was under three months old |
| [use-your-eyes](skills/use-your-eyes) | Actually look at a picture, video or screen before calling it ready | Every measurement said perfect; the picture looked wrong |
| [lane-check](skills/lane-check) | Check an agent's "I'm done, it all passes" against the facts before trusting it | An agent's proof was hours older than the code it claimed to prove |
| [lane-brief](skills/lane-brief) | Give a new agent a complete set of instructions, the same way every time | Instructions retyped by hand kept leaving out something important |
| [big-brother](skills/big-brother) | Ask a fresh, stronger reviewer for help when stuck, and before every release | Two gaps sat unnoticed for weeks because nobody thought to look |
| [repo-verdict](skills/repo-verdict) | Give a straight answer on a project someone links: useful, interesting, or skip | A project bragged about a speed-up that wasn't in its public code |
| [after-a-freeze](skills/after-a-freeze) | Recover cleanly after the computer runs out of memory and things freeze | Too many programs building at once froze the whole machine |

## Using one

You need Claude Code. Copy a skill's folder into your skills folder, then start a new session:

```
cp -r skills/sanity-check ~/.claude/skills/
```

Each skill is a single `SKILL.md` file written in plain text, so you can read one before you use it. Some name commands
or tools from the Locust project: swap in your own.

## License

MIT: free to use, change and share. See the `LICENSE` file.
