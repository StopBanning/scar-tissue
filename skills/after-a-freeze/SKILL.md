---
name: after-a-freeze
description: "Use when the assistant or the app it runs in froze, hung, restarted or was force quit: a watchdog restarted the assistant, a tool call came back 'interrupted: the session ended', the app stops answering, remotely connected sessions dropped off, or the person says 'frozen', 'stuck', 'restarted' or 'force quit'."
---

# After a freeze

The person watched a quick automatic restart bring things back and asked for it to become a skill, adding that any
sessions that had been connected for remote access also had to be woken, because they do not reconnect on their own.

What happens: a small watchdog script on a timer restarts the assistant when its main log has been silent for four or
more minutes, and saves evidence in a folder per freeze. The freeze itself is almost always memory pressure: on a
16 GB machine, too many compiles at once push the assistant and the app into swap, and both show about 0 MB resident.

## 1. Free the memory first
- `sysctl vm.swapusage` (macOS); the resident size of the two apps: `ps -o rss= -p <pid>`.
- Count builds by lane: for each `pgrep -f "<build tool> (test|build)"`, read its working directory with
  `lsof -a -p <pid> -d cwd -Fn`.
- If you run a build gate (a compiler wrapper that lets only a few heavy compiles run at once machine-wide), check it is
  still set and read its log. Still keep a cap on lanes building (four is a reasonable number), and count your own break
  runs as lanes. Stop the newest lanes first through the lane runner. If the runner does not answer, end those lanes'
  build trees directly (`pkill -TERM -P <build pid>; kill -TERM <build pid>`). Never quit the app yourself: every lane
  runs inside it.

## 2. Wake every remotely connected session
After an assistant restart only the session that resumes reconnects. The rest stay off.
- Find which were on (your session list shows an active flag), and keep a short list of the ones that are usually on.
- For each that is off, send it one line: `Reconnect wake-up after the assistant was restarted at <time>: reply with
  just "ok" and do nothing else.` A session must run a turn before remote access can connect.
- Then switch remote access on for that session. If a hook changes the call's input, send the call again with exactly the
  input it quotes. Confirm with the session list that each shows active.
- Update your list when the person turns one on or off.

## 2b. Scheduled jobs died with the restart
Scheduled jobs created inside a session live only in that session. After a restart, message each session that keeps jobs
and ask it to list and recreate them from its saved job file; check this chat's own list too.

## 3. App frozen or quit
- Frozen, not quit: sample its main process (`sample <pid> 2`). An idle main thread means it is paging back in: give it a
  minute after memory is freed. If the window stays frozen, reload only the window (Cmd+R) and do not quit and reopen:
  on one occasion a full restart (new main pid) ended every lane. Tell a reload from a restart by the main process's
  start time (`ps -o lstart= -p <pid>`).
- Quit (by the person or a crash): every lane in it ended; committed work is safe in each folder. Reopen the app, wait
  until its lane runner answers, then restart the lanes as fresh conversations, at most four building, each told: "an
  earlier run stopped when the app was quit; read your uncommitted edits first and keep what is right." Continuing an
  old conversation can land on an account whose plan is spent: start fresh ones.

## 4. Tell the person in a few lines
What froze and why (the swap number), which sessions are back, which lanes were restarted and which wait for room.
