# Make Claude Code call your name when it needs you 🔊

> **macOS only** — this uses Apple's built-in `say` text-to-speech engine, which ships with every Mac.

Tired of missing the moment Claude Code stops and waits for your input? Replace the default chime with your Mac addressing you like JARVIS addresses Tony Stark — **"[put your name] … your input is required"** — spoken aloud in a calm British voice, with a natural pause after your name.

- ✅ Zero tokens — runs 100% locally, no API call, no model involved
- ✅ Zero dependencies — uses macOS's built-in `say` command
- ✅ Works offline, free, instant

> **Note:** Claude Code does *not* do this by default — out of the box you get, at most, a terminal bell. This hook is something you add yourself, and it takes under a minute.

## Setup (macOS)

Open `~/.claude/settings.json` and add the `hooks` block below (create it if it doesn't exist). Replace `[put your name]` with your own name:

```jsonc
{
  "hooks": {
    // Fires in a plain terminal when Claude needs your input
    "Notification": [
      {
        "hooks": [
          {
            "type": "command",
            "command": "say -v Daniel \"[put your name] [[slnc 400]] your input is required\" 2>/dev/null || true"
          }
        ]
      }
    ],
    // FOR VS CODE USERS — the Notification hook above doesn't fire in the VS Code
    // extension. PermissionRequest catches every prompt where Claude asks to run a
    // tool it needs your approval for (Bash, WebFetch, Edit, Write, …) and speaks
    // only when you've tabbed away from VS Code. Delete it if you only use the terminal.
    "PermissionRequest": [
      {
        "hooks": [
          {
            "type": "command",
            "command": "front=$(lsappinfo info -only name \"$(lsappinfo front)\" 2>/dev/null | sed -E 's/.*\"LSDisplayName\"=\"([^\"]*)\".*/\\1/'); case \"$front\" in Code|iTerm2|Terminal) : ;; *) say -v Daniel \"[put your name] [[slnc 400]] your input is required, sir\" 2>/dev/null ;; esac; true"
          }
        ]
      }
    ],
    // ALSO FOR VS CODE — plan approvals (ExitPlanMode) and multiple-choice prompts
    // (AskUserQuestion) aren't permission dialogs, so PermissionRequest skips them.
    // This block covers those two. Same "only when away" guard.
    "PreToolUse": [
      {
        "matcher": "AskUserQuestion|ExitPlanMode",
        "hooks": [
          {
            "type": "command",
            "command": "front=$(lsappinfo info -only name \"$(lsappinfo front)\" 2>/dev/null | sed -E 's/.*\"LSDisplayName\"=\"([^\"]*)\".*/\\1/'); case \"$front\" in Code|iTerm2|Terminal) : ;; *) say -v Daniel \"[put your name] [[slnc 400]] your input is required, sir\" 2>/dev/null ;; esac; true"
          }
        ]
      }
    ]
  }
}
```

That's it — the next session will speak whenever Claude needs your input. Terminal-only users can drop the `PreToolUse` block; VS Code users should keep both.

> **Why `PreToolUse` for VS Code?** In the VS Code extension the `Notification` event doesn't fire, so the terminal hook stays silent there. The two moments Claude explicitly waits on you are *tools*: `AskUserQuestion` (a multiple-choice prompt) and `ExitPlanMode` (a plan presented for approval). Matching `PreToolUse` to both (`AskUserQuestion|ExitPlanMode`) plays the alert the instant either appears — the moment your input is needed. Add more tool names to the matcher to alert on other actions too.

What the pieces mean:

| Part | What it does |
|---|---|
| `-v Daniel` | The voice. **Daniel** is Apple's British male voice — the JARVIS feel. Drop this flag to use your Mac's default voice. |
| `[[slnc 400]]` | 400 ms of silence after your name — the dramatic pause. |
| `2>/dev/null \|\| true` | Keeps the hook silent-and-harmless if `say` ever fails. |

Test it in any terminal before committing:

```bash
say -v Daniel "Tony [[slnc 400]] your input is required"
```

## How it works

```
Claude needs your input
        │
        ▼
Claude Code (the local CLI) fires a "Notification" event
        │
        ▼
It checks ~/.claude/settings.json for matching hooks
        │
        ▼
Runs your shell command locally:  say -v Daniel "[put your name] [[slnc 400]] your input is required"
        │
        ▼
macOS text-to-speech speaks it — on-device, offline, free
```

The model never sees the hook fire. A `"type": "command"` hook is pure shell between the CLI and your OS — **zero token cost, forever**.

## Customize

| Want | Change |
|---|---|
| Different pause length | `[[slnc 400]]` is milliseconds of silence — try `250` (snappier) or `600` (dramatic) |
| Different voice | `say -v Samantha "..."` — list all voices with `say -v '?'` |
| Different phrase | Anything you like: `"Boss, your turn"`, `"Code's ready for review"` |
| Test it first | Just run the `say` command in any terminal |

## Get creative 🎨

Your Mac's `say` engine has dozens of voices and languages built in. Run `say -v '?'` to see what's installed, then try these:

### Speak your language
Make it feel like home — `say` supports voices for 40+ languages (download more in System Settings → Accessibility → Spoken Content):

```bash
say -v Lekha "[put your name], एक मिनट"          # Hindi
say -v Kyoko "[put your name], お願いします"       # Japanese
say -v Mónica "[put your name], un segundo"     # Spanish
say -v Amélie "[put your name], une seconde"    # French
say -v Tingting "[put your name], 请稍等"         # Mandarin
say -v Yuna "[put your name], 잠시만요"           # Korean
say -v Milena "[put your name], секунду"        # Russian
```

### Pick a persona
```bash
say -v Daniel "Sir, the build is complete"                     # 🦾 full JARVIS mode
say -v Daniel "Pardon the interruption, sir"                   # 🎩 polite British butler
say -v Zarvox "Human input required"                           # 🤖 sci-fi robot / HAL 9000
say -v Whisper "[put your name]... it is time"                 # 👻 dramatic whisper
say -v "Good News" "Your code is ready"                        # 🎵 it literally sings
say -v Cellos "Claude needs you"                               # 🎻 sung over a cello line
say "This is the final boarding call for [put your name]"      # ✈️ airport announcement
say "Box box box"                                              # 🏎️ F1 pit-wall radio
say "Player one, your move"                                    # 🎮 arcade vibes
say "Come with me if you want to compile"                      # 🦿 you'll be back
```

(The novelty voices like Zarvox, Whisper, Good News, and Cellos may need a one-time download in System Settings → Spoken Content.)

### Different sounds for different events
Hooks fire on more than just `Notification`. Give each event its own audio identity:

```json
{
  "hooks": {
    "Notification": [
      { "hooks": [{ "type": "command", "command": "say -v Daniel \"[put your name] [[slnc 400]] your input is required\" 2>/dev/null || true" }] }
    ],
    "Stop": [
      { "hooks": [{ "type": "command", "command": "say -v \"Good News\" \"All done\" 2>/dev/null || true" }] }
    ]
  }
}
```

Now "your input is required" means *waiting on you*, and a sung "All done" means *task finished* — you can tell them apart from across the room.

### Prefer a chime over a voice?
macOS ships with classic system sounds too:

```bash
ls /System/Library/Sounds          # Glass, Ping, Submarine, Hero, Funk...
afplay /System/Library/Sounds/Submarine.aiff
```

## Manage it later

Type `/hooks` inside any Claude Code session to review, edit, or disable hooks.

---

*Built with Claude Code itself — I asked it where the notification sound came from, and it rewired its own alert.*
