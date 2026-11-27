---
name: be-curious
description: "Use when about to say something can't be done, isn't supported, is gated, needs a workaround or 'only the official app can do it', especially when the reason comes from memory, an old note or a past attempt; also when the person says 'be curious', 'is that still true', 'are we sure', 'that was a while ago' or '/be-curious'."
---

# Be curious

The person put it this way: "We just think that something's impossible and we go, oh, yep, but as time goes by, these
models get better and better. We just figure out how to do things. So always be curious."

The incident: the app could not show one AI company's cloud sessions inside its own window, and needed a hand-made
setup for each project before it could use another company's cloud. Both facts came from notes written two months
earlier. The person asked to look again. Twenty minutes of re-testing the current versions found a new, hidden
(experimental) option: one agent's "hands" (the part that runs commands) can live on any computer while its "head"
stays in the app, with every step shown live. A test connection worked first try. The other company's help text had
also changed. Both "can't"s had been true once, then repeated as facts long after.

## The rule

A "can't" is a measurement with a date and a version number, never a permanent fact. Before saying it, or acting on
it, climb the ladder below until something works or every step is done. Then say which steps were done.

## The ladder (stop as soon as you find a way)

1. **Date the old claim.** Where does the "can't" come from: a note, an old error message, a guess? When was it
   measured, and on which version? Check the version installed now (`<tool> --version`). For tools that change every
   week (AI coding agents and the services behind them), a claim more than a week old is unverified.
2. **Read today's surface.** The tool's help (`--help`) and the help of every subcommand. Look for experimental
   switches: a feature list, an `--experimental` flag, a way to print the tool's full protocol (the exact list of
   requests a program can send it). Read the release notes and the maker's documentation.
3. **If the maker's own app can do it, there is a way.** Find out how it does it: read the app's bundled code (many
   desktop apps are web pages packed in a wrapper, and the code can be unpacked and searched), watch its network
   requests, or read its protocol.
4. **Look inside with study tools.** Open reverse-engineering tools exist that inspect programs, desktop apps and
   websites locally and explain what they do, with evidence for each conclusion. Use them from a scratch folder, and
   never let one install itself into other programs' settings.
5. **Try it once, small and real.** The smallest test that answers yes or no: in a scratch folder, with a throwaway
   password or token, and costing nothing. If it would cost money or use up the person's quota, ask first.
6. **Ask outside.** A web search for the exact error or feature name, the tool's issue tracker, or a second reviewer
   who doesn't share your assumptions.

## Saying what you found

- "Measured today on <tool> <version>: works / doesn't / partly", with the test that shows it (the command and what
  it printed).
- Update the note that held the old claim, with today's date and version. Never leave an undated "can't" behind.
- If it still can't be done, name the steps you did and the one thing that would change the answer: a switch that may
  ship, an account restriction, a reset time.

## Where curiosity stops

- A gate on the person's account ("not enabled for your account") is reported, never worked around.
- Never read, copy or share anyone's passwords or sign-in tokens.
- Spending money, paid requests or the person's usage needs a yes first.

## Signs an old opinion is talking

"We tried that." "It's not supported." "The API doesn't allow it." "Only the official app can." "That needs a
workaround." A note with no version on it. Each of these means: climb the ladder first.

## How it was tested

Two runs without the skill and two with it, each given a dated "can't" note and the person's question. Without it,
both runs already doubted the note (a date invites doubt), and one would have spent a real paid cloud task without
asking. With it, both plans went to the hidden switches and the maker's own app code, which is where the real answer
was, and both waited for a yes before spending. The skill's value is how deep it digs and the spending guard, not the
first doubt. Not tested: a "can't" buried inside an unrelated task, where nothing prompts the doubt.

Related: big-brother (a second reviewer), repo-verdict.
