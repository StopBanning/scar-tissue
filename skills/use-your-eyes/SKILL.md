---
name: use-your-eyes
description: "Use before saying anything visual is ready, fixed, good, posted, loaded or 'looks right' (a video, a render, a scene, a frame, an export, an app screen, a web page, a live post), before calling a reference video understood, and whenever the person says 'use your eyes', 'did you even look', 'actually watch it', 'look at it' or '/use-your-eyes'."
---

# Use your eyes: look at the real thing, as a viewer, before you say it

This skill pulls together the times the person caught something the assistant would have seen by looking:
- a rendered flock of birds called "made", with perfect audio levels, that looked like a toddler drew it;
- an asset that existed and rendered, with a glitch in it;
- code shown on screen that hid the scene behind it;
- captions placed under a platform's own UI bar;
- a post the notes said was not up, which was on the live page;
- a test copy the person could not see working, handed over unwatched.

**The rule:** a number, a PASS line, a file that exists, a note or another agent's yes is not looking. Before saying
something visual is ready, fixed, good, posted or the same as before, open the real thing and look at it the way the
person it is for will see it, and write down what you saw in plain words.

## What to look at, by thing

| Thing | Look at | How |
|---|---|---|
| A video or cut you made | every frame at 4 per second, the first second and every cut or drop at full frame rate, the phone-sized view | extract a contact sheet with ffmpeg (for example `ffmpeg -i in.mp4 -vf "fps=4,scale=270:-1,tile=8x8" sheet-%02d.png`), then OPEN the images; do the same at full rate for the first second |
| A render or scene | the whole clip as a viewer, then still frames at full size | extract frames, open them |
| The exact file going out | the EXPORT, not your master (an editor may re-encode it or add audio) | run the same checks on the export |
| A reference video | all of it: 4 per second, full rate at the key moment, until you can say its point in one line | frame sheets, or screenshots over time |
| What is posted, on a grid or in an admin page | the LIVE page, not your notes | open it in a browser; read captions back through the platform's API if it has one |
| The app's screen, a feature | the real app doing it, in a hidden or muted copy, with a screenshot | never hand over a copy you haven't watched work |
| A web page or artifact you published | the rendered page at desktop and phone width, light and dark | browser screenshots |

## The look, in order (write each answer down in your log line or report)

1. **The first second as a stranger:** what is on screen, what moves, would you keep watching? One plain sentence.
2. **The whole frame, shot by shot:** count what is on screen. One subject, at most one line of words, nothing covering
   the subject, text inside the platform's safe area (for 1080 x 1920 vertical video, roughly x 60..890 and y 270..1630).
3. **Every join, drop and fast move at full frame rate:** pops, black or repeated frames, glitches, text jumping.
4. **Read every word on screen at phone size,** including code: is it the right text, spelled right?
5. **The end, and the loop back to frame 0.**
6. **Compare with what it is meant to be:** the card, the person's words, the last item of its kind. Is it better on the
   thing they named?
7. Only then the numbers (loudness, peak, PASS lines), as a second check, never the first.

**Is 4 frames a second enough?** For the whole-clip pass, yes: it shows every shot, every caption and anything that lasts
more than about a quarter second. It cannot see what is shorter: a one-frame flash, a 4-frame toast pop, a repeated or
frozen frame, AI-video flicker (things popping in and out between frames), or whether a hit lands on the beat. So:
- 4 per second for the whole thing, always;
- every frame at the first second, every cut, the drop, every fast move and every text change;
- **AI-made picture: 8 per second for the whole clip**, plus a frame-difference scan to find single-frame jumps, then
  every frame at each spot it flags:
  `ffmpeg -i <file> -vf "select='gt(scene,0.08)',showinfo" -f null - 2>&1 | grep -o 'pts_time:[0-9.]*'`;
- claims about landing on the beat get checked against measured beat times, never by eye at 4 per second.

Saying "watched it" with no sentence about what you saw doesn't count. If you can't say what happens at 1.0 s, you
didn't look.

## Red flags: stop and go look

| Thought | Reality |
|---|---|
| "The checker printed PASS" | It measures sound and edges. It never saw the frame. Open the sheets. |
| "The numbers are fine" | The flock had perfect loudness and looked wrong. |
| "I checked a few frames" | The point of a clip is often in the frames you skipped. |
| "Another reviewer cleared it" | Their yes is input, not a look. |
| "My notes say it's not posted / loaded / set" | Notes go stale after a context reset. Open the live page. |
| "The file exists" / "it rendered" | Existing isn't watching. |
| "It's the same as the version they approved" | Exports re-encode. Look at the file that goes out. |
| "It's a small change" | Small changes break joins. Re-look at the changed part at full rate and the whole thing at 4 per second. |

## When the person says "use your eyes"

It means you made a claim you hadn't looked at. Don't argue and don't re-explain the numbers: open the thing now, do the
look above, and tell them in two or three lines what you actually see, including what is wrong. Then fix it, and look
again before saying so.
