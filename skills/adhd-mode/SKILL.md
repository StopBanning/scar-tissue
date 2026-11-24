---
name: adhd-mode
description: "Use when two or more decisions need the person, or when they say 'what's waiting on me', 'roundup', 'cards' or 'ADHD mode', including any morning or night roundup. Also when you are about to put several questions, options or asks for them in one message."
---

# ADHD mode: decisions one card at a time

The person named it after getting a wall of questions: "Do it one by one in cards for me, let's call that ADHD mode."
Their reason: a whole list on the screen at once overwhelms them, but one at a time is easy. Done right, they answer
seven cards in four minutes. Done wrong (a list, a wall of text, a card with nothing to look at), nothing gets
answered. Every rule below exists because breaking it already went wrong once.

Assume they read on a phone, often in the middle of something else. Write plainly: name what's on screen, use short
sentences, skip the jargon.

## 1. Gather (quietly, before you say anything)
- Run `date` (prints the current date and time). Times in cards come from the clock, never from a guess.
- Collect what needs THEM: the plan's "needs you" items, your task lists, recent notes, parked "later" items, and open
  threads in the chat.
- Cut everything that does not need them:
  - anything they said is your call ("up to you", "your call"): decide it and note that you decided;
  - small choices that are easy to undo (try a smaller model, a re-render, a crop): decide, and bring them only the
    result;
  - anything they already answered: search their own messages before asking again.
- **A list that says "waiting on them" doesn't make it so.** Lists go stale. Check every item against the latest notes
  and the chat before it becomes a card. If they answered it, it's done: act on the answer and fix the list. If they
  said "up to you", decide it. The count in your opening line ("4 for you") is what's left after these cuts. (In a
  replay test, both runs counted items the person had already approved or left to the assistant.)
- Items passed along from another session: quote the person word for word, and mark anything you added as yours. If you
  can't say where an item came from, drop it.

## 2. Make every card's example first
Every card has something to look at, unless there truly is nothing to show (a sign-in, a yes/no on a chore).
- A video or clip: the finished file, and you must already have watched it frame by frame yourself. Never make them
  the crash-test dummy for something you haven't checked. Keep files small enough to open on a phone.
- A choice between looks: ONE labelled sheet (A / B / C, or before / after) as a single image, not three cards.
- A fix: before and after side by side, at the moment that changed.
- Captions, replies, post drafts: a text file with the same words as the card. Never put them only in the question's
  option previews (previews may not show on a phone).
- Keep any explanation to 3-5 lines on what they will see or hear and what changes for them. No technical walls.

## 3. Order
Put what is due soonest first. Then quick keep-or-drop items, then real decisions. Put chores at the computer (sign-ins,
accounts, settings) last.

## 4. Run it
Open with ONE line: "4 for you, one at a time." Never show the list.

**Words first, every card.** Write the chat text before any tool call: the opening line (first card only), then the "1
of 4" lines. After that, send the file, then the question. If your message would start with the file or the question,
stop and write the lines first. (In a replay test, 4 of 10 runs sent the file and the card with nothing written above
them. A hook, which is an automatic check that runs on its own, fixed it: it blocks a question card when you haven't
written anything since the person's last message.)

For each item:
1. Write two or three plain lines in the chat: "2 of 4: <the thing>." Say what it is and what a yes does.
2. Send the example, as a file.
3. Ask the question:
   - ONE question. It must stand alone, because the dialog can hide everything above it, so name the item in the
     question.
   - 2-3 options (4 at most) with short labels. Put your pick first, marked "(Recommended)".
   - Offer only realistic options.
4. Wait. Act on the answer right away, confirm in ONE line, then send the next card.

Never show more than one card at a time. Never send a summary of all the asks, before or after. Never write "see
above": send it again.

## 5. Reading answers
- "Maybe" or "later": accept it, park it in your notes, and ask once more at the next roundup.
- A typed note instead of an option: follow it literally.
- "What do you think?": decide, say your choice plainly in one line, and move on.
- "Up to you": decide, and log "decided by me" so they can overrule you.
- Public or can't be undone (post, push, release, upload, delete, merge, send): if the card's answer is the ONLY go-ahead
  and they typed nothing, confirm in chat before acting. Cards have come back answered when the person never saw them.
- If they say they didn't see a card: tell them what the answer was and what you did with it, and offer to undo it.

## 6. Close
- Write what was decided into your notes, with a time stamp from the shell (`date`), and update the plan.
- Final message: a few lines on what got decided and what is now moving. No list of the asks.
- Information with no decision in it (numbers, what got posted) is short text, not cards.

## What a good card looks like
> 3 for you, one at a time.
>
> 1 of 3: the open door in video 3 went dark for half a second around 9 s. I re-rendered only those frames; before and
> after below.
> [file: door3-before-after.jpg]
> Question: "Video 3's door glitch is fixed (before/after above). Post it Monday at 10 AM?"
>   - "Yes, Monday 10 AM (Recommended)"  - "Show me the full video first"

## What breaks it (all of these happened)
- A wall of asks, or a numbered list of decisions in one message.
- A card with no example ("what am I looking at?").
- The question in the card with nothing written above it.
- Draft text that appears only in option previews (invisible on a phone).
- A drip of shifting options while you are still making new versions: finish the versions first, then ask ONE question
  with all of them.
- Asking something they already decided, or said was yours.
- Long technical files above the card.
- Showing a video you hadn't checked frame by frame (they caught a glitch you missed).
