---
name: use-your-eyes
description: "Use before saying anything visual is ready, fixed, good, posted, loaded or 'looks right' (a video, a render, a scene, a frame, an export, an app screen, a web page, a live post), before calling a reference video understood, and whenever the person says 'use your eyes', 'did you even look', 'actually watch it', 'look at it' or '/use-your-eyes'."
---

# Use your eyes: look at the real thing, as a viewer, before you say it

This skill collects the times the person caught something the assistant would have seen just by looking:
- a computer-drawn flock of birds was called "made", with perfect audio levels, and looked like a toddler drew it;
- a file existed and rendered (was turned into a finished picture), and it had a glitch in it;
- code shown on screen hid the scene behind it;
- captions sat under a platform's own buttons and bars;
- a post the notes said was not up was on the live page;
- a test copy the person could not see working was handed over without anyone watching it.

**The rule:** a number, a PASS line, a file that exists, a note, or another agent's yes is not looking. Before you say
something visual is ready, fixed, good, posted or the same as before, open the real thing. Look at it the way the
person it is for will see it, and write down what you saw in plain words.

## What to look at, by thing

| Thing | Look at | How |
|---|---|---|
| A video or cut you made | every frame at 4 per second, the first second and every cut or drop at full frame rate, the phone-sized view | make a contact sheet (a grid of small frames) with ffmpeg, a free video tool, for example `ffmpeg -i in.mp4 -vf "fps=4,scale=270:-1,tile=8x8" sheet-%02d.png`, then OPEN the images; do the same at full rate for the first second |
| A render or scene | the whole clip as a viewer, then still frames at full size | pull out frames and open them |
| The exact file going out | the EXPORT, not your original (an editor may re-encode it or add audio) | run the same checks on the export |
| A reference video | all of it: 4 per second, full rate at the key moment, until you can say its point in one line | frame sheets, or screenshots over time |
| What is posted, on a grid or in an admin page | the LIVE page, not your notes | open it in a browser; if the platform has an API (a way for programs to read its data), read the captions back through it |
| The app's screen, a feature | the real app doing it, in a hidden or muted copy, with a screenshot | never hand over a copy you haven't watched work |
| A web page or artifact you published | the rendered page at desktop and phone width, in light and dark mode | browser screenshots |

## The look, in order (write each answer in your log line or report)

1. **The first second, as a stranger:** what is on screen, what moves, and would you keep watching? One plain sentence.
2. **The whole frame, shot by shot:** count what is on screen. There should be one subject, at most one line of words,
   and nothing covering the subject. Text must sit inside the platform's safe area, the part its own buttons don't
   cover (for 1080 x 1920 vertical video, roughly x 60..890 and y 270..1630).
3. **Every join, drop and fast move at full frame rate:** look for pops, black or repeated frames, glitches, and text
   that jumps.
4. **Read every word on screen at phone size,** code included. Is it the right text, spelled right?
5. **The end, and the loop back to frame 0.**
6. **Compare it with what it is meant to be:** the card, the person's words, the last item of its kind. Is it better
   on the thing they named?
7. Only then check the numbers (loudness, peak level, PASS lines), as a second check, never the first.

**Is 4 frames a second enough?** For the pass over the whole clip, yes. It shows every shot, every caption, and
anything that lasts more than about a quarter second. It cannot see anything shorter: a one-frame flash, a 4-frame toast
pop (a small message that pops up), a repeated or frozen frame, flicker in AI-made video (things popping in and out
between frames), or whether a hit lands on the beat. So:
- always use 4 per second for the whole thing;
- look at every frame in the first second, at every cut, at the drop, at every fast move and at every text change;
- **for AI-made picture, use 8 per second for the whole clip.** Also run a frame-difference scan to find single-frame
  jumps, then look at every frame around each spot it flags:
  `ffmpeg -i <file> -vf "select='gt(scene,0.08)',showinfo" -f null - 2>&1 | grep -o 'pts_time:[0-9.]*'`
  (lists the moments where the picture changes sharply);
- check claims about landing on the beat against measured beat times, never by eye at 4 per second.

Saying "watched it" with no sentence about what you saw doesn't count. If you can't say what happens at 1.0 s, you
didn't look.

## Red flags: stop and go look

| Thought | Reality |
|---|---|
| "The checker printed PASS" | It measures sound and edges. It never saw the frame. Open the sheets. |
| "The numbers are fine" | The flock had perfect loudness and still looked wrong. |
| "I checked a few frames" | The point of a clip is often in the frames you skipped. |
| "Another reviewer cleared it" | Their yes is input, not a look. |
| "My notes say it's not posted / loaded / set" | Notes go stale after your memory resets. Open the live page. |
| "The file exists" / "it rendered" | Existing isn't watching. |
| "It's the same as the version they approved" | Exports re-encode. Look at the file that goes out. |
| "It's a small change" | Small changes break joins. Look again at the changed part at full rate, and the whole thing at 4 per second. |

## When the person says "use your eyes"

It means you made a claim you hadn't looked at. Don't argue, and don't explain the numbers again. Open the thing now, do
the look above, and tell them in two or three lines what you actually see, including what is wrong. Then fix it, and
look again before you say it's fixed.
