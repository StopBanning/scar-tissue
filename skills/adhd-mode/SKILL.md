---
name: adhd-mode
description: "Use when two or more decisions need the person, or when they say 'what's waiting on me', 'roundup', 'cards' or 'ADHD mode', including any morning or night roundup. Also when about to put several questions, options or asks for them in one message."
---

# ADHD mode: decisions one card at a time

The person named it after a wall of questions: "Do it one by one in cards for me, let's call that ADHD mode." Why it
matters, in their words: a whole list on the screen at once blows their head up, but one at a time is easy. Done right,
they answer seven cards in four minutes. Done wrong (a list, a wall, a card with nothing to look at), nothing gets
answered. Every rule below is here because breaking it already went wrong once.

Assume they read on a phone, often in the middle of something else. Write plainly: name what's on screen, short
sentences, no jargon.

## 1. Gather (silently, before saying anything)
- Run `date`. Times in cards come from the clock, never a guess.
- Collect what needs THEM: the plan's "needs you" items, your task lists, recent notes, parked "later" items, open
  threads in the chat.
- Cut everything that does not need them:
  - anything they said is your call ("up to you", "your call"): decide it, note it as decided;
  - reversible technical choices (try a smaller model, a re-render, a crop): decide and bring only the result;
  - anything they already answered: search their own messages before asking again.
- **A list saying "waiting on them" doesn't make it so.** Lists go stale. Check every item against the latest notes and
  the chat before it becomes a card. If they answered it, it's done: act on the answer and fix the list. If they said
  "up to you", decide it. The count in the opener ("4 for you") is what's left after these cuts. (In a replay test, both
  runs counted items the person had already approved or left to the assistant.)
- Items relayed from another session: quote the person word for word and mark your own additions as yours. If you
  can't say where an item came from, drop it.

## 2. Make every card's example first
Every card has the thing to look at, unless there truly is nothing to show (a sign-in, a yes/no on a chore).
- A video or clip: the finished file, and you must already have watched it frame by frame yourself. Never make them
  the crash dummy for something you haven't checked. Keep files small enough to open on a phone.
- A choice between looks: ONE labelled sheet (A / B / C, or before / after) as an image, not three cards.
- A fix: before and after side by side at the moment that changed.
- Captions, replies, post drafts: a text file with the same words as the card. Never only inside the question's option
  previews (previews may not show on a phone).
- Keep any explanation to 3-5 lines of what they'll see or hear and what changes for them. No technical walls.

## 3. Order
Due soonest first, then quick keeps, then real decisions, then chores at the computer (sign-ins, accounts, settings) last.

## 4. Run it
Open with ONE line: "4 for you, one at a time." Never the list.

**Words first, every card.** Write the chat text before any tool call: the opener (first card only), then the "1 of 4"
lines. Then the file, then the question. If your message would start with the file or the question, stop and write the
lines first. (In a replay test, 4 of 10 runs sent the file and the card with nothing written above them. A hook that
blocks a question card when nothing has been written since the person's last message fixed it.)

For each item:
1. Two or three plain lines in the chat: "2 of 4: <the thing>." What it is, what a yes does.
2. The example, as a file.
3. The question:
   - ONE question, and it must stand alone (the dialog can hide everything above it): name the item in the question.
   - 2-3 options (4 at most), short labels, your pick first with "(Recommended)".
   - Realistic options only.
4. Wait. Act on the answer right away, confirm in ONE line, then the next card.

Never more than one card at a time. Never a summary of all the asks, before or after. Never "see above": send it again.

## 5. Reading answers
- "Maybe" / "later": accept it, park it in your notes, ask once at the next roundup.
- A typed note instead of an option: follow it literally.
- "What do you think?": decide, say it plainly in a line, move on.
- "Up to you": decide, and log "decided by me" so they can overrule.
- Public or irreversible (post, push, release, upload, delete, merge, send): if the card's answer is the ONLY go and
  they typed nothing, confirm in chat before acting. Cards have come back answered when the person never saw them.
- If they say they didn't see a card: say what the answer was, what you did on it, and offer to undo.

## 6. Close
- Write what was decided to your notes with a time stamped by the shell (`date`), and update the plan.
- Final message: a few lines, what got decided and what's now moving. No list of the asks.
- Information with no decision (numbers, what posted) is short text, not cards.

## What a good card looks like
> 3 for you, one at a time.
>
> 1 of 3: the open door in video 3 went dark for half a second around 9 s. I re-rendered only those frames; before and
> after below.
> [file: door3-before-after.jpg]
> Question: "Video 3's door glitch is fixed (before/after above). Post it Monday at 10 AM?"
>   - "Yes, Monday 10 AM (Recommended)"  - "Show me the full video first"

## What breaks it (all happened)
- A wall of asks or a numbered list of decisions in one message.
- A card with no example ("what am I looking at?").
- The question in the card with nothing written above it.
- Draft text only in option previews (invisible on a phone).
- A drip of shifting options while still making new variants: finish the variants, then ONE pick with all of them.
- Asking something they already decided or said was yours.
- Long technical files above the card.
- Showing a video you hadn't checked frame by frame (a glitch they caught that you missed).
