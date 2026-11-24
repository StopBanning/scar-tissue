---
name: after-a-freeze
description: "Use when the assistant or the app it runs in froze, hung, restarted or was force quit: a watchdog restarted the assistant, a tool call came back 'interrupted: the session ended', the app stops answering, remotely connected sessions dropped off, or the person says 'frozen', 'stuck', 'restarted' or 'force quit'."
---

# After a freeze

The person watched a quick automatic restart bring things back and asked for it to become a skill. They added that any
sessions connected for remote access (controlling them from a phone, say) must also be woken, because they do not
reconnect on their own.

What happens: a small watchdog script on a timer restarts the assistant when its main log has been silent for four
minutes or more. It saves evidence in a folder for each freeze. The freeze itself is almost always the
computer running short of memory. On a 16 GB machine, too many builds (programs turning code into a runnable app) at
once fill the memory. The computer then spills into swap (slow disk space used as emergency memory), and both the
assistant and the app show about 0 MB in real memory.

## 1. Free the memory first
- `sysctl vm.swapusage` shows how much swap is in use (macOS). `ps -o rss= -p <pid>` shows how much real memory one
  process (a running program) uses.
- Count the builds for each lane (one agent working in its own copy of the code). For each build, run
  `pgrep -f "<build tool> (test|build)"` to list the running ones. Then run `lsof -a -p <pid> -d cwd -Fn` to see which
  folder each one runs in.
- You may have a build gate: a compiler wrapper that lets only a few heavy builds run at once across the whole machine.
  If so, check it is still switched on and read its log. Still keep your own cap on how many lanes build at once. Four
  is a reasonable number. Count your own break runs (test runs that deliberately damage code to see if tests notice) as
  lanes. Stop the newest lanes first, using the lane runner (the tool that starts and stops lanes). If the runner does
  not answer, end those lanes' builds directly with `pkill -TERM -P <build pid>; kill -TERM <build pid>`. Never quit the app yourself: every lane runs
  inside it.

## 2. Wake every remotely connected session
After the assistant restarts, only the session that resumes reconnects. The rest stay off.
- Find which sessions were on. Your session list shows an active flag. Keep a short list of the ones usually on.
- Send each session that is off one line: `Reconnect wake-up after the assistant was restarted at <time>: reply with
  just "ok" and do nothing else.` A session must run one turn before remote access can connect.
- Then switch remote access on for that session. A hook (a small automatic check) may change the call's input. If it
  does, send the call again with exactly the input the hook quotes. Check the session list to confirm each session now
  shows active.
- Update your list whenever the person turns one on or off.

## 2b. Scheduled jobs died with the restart
Scheduled jobs created inside a session live only as long as that session. After a restart, message each session that
keeps jobs. Ask it to list them and recreate them from its saved job file. Check this chat's own list too.

## 3. App frozen or quit
- **Frozen, not quit:** sample its main process with `sample <pid> 2`, which records what the program is doing for two
  seconds. If the main thread is idle, the app is paging back in (loading itself back from disk). Give it a minute
  after you free memory. If the window stays frozen, reload only the window (Cmd+R). Do not quit and reopen the app. On
  one occasion a full restart (the main process got a new pid, its process number) ended every lane. To tell a reload
  from a restart, check the main process's start time with `ps -o lstart= -p <pid>`.
- **Quit (by the person or a crash):** every lane inside it ended. Committed work (changes saved into the code's
  history) is safe in each lane's folder. Reopen the app and wait until its lane runner answers. Then restart the lanes
  as fresh conversations, at most four building at once. Tell each one: "an earlier run stopped when the app was
  quit; read your uncommitted edits first and keep what is right." Do not continue an old conversation: it can land
  back on an account whose plan is used up.

## 4. Tell the person in a few lines
Say what froze and why (give the swap number). Say which sessions are back. Say which lanes you restarted and which
are waiting for room.
