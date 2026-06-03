# Make Claude Code call your name when it needs you 🔊

> **macOS only** — this uses Apple's built-in `say` text-to-speech engine, which ships with every Mac.

Tired of missing the moment Claude Code stops and waits for your input? Replace the default chime with your Mac literally saying **"<your name>, need a second"** — spoken aloud, with a natural pause after your name.

- ✅ Zero tokens — runs 100% locally, no API call, no model involved
- ✅ Zero dependencies — uses macOS's built-in `say` command
- ✅ Works offline, free, instant

> **Note:** Claude Code does *not* do this by default — out of the box you get, at most, a terminal bell. This hook is something you add yourself, and it takes under a minute.

## Setup (macOS)

Open `~/.claude/settings.json` and add a `Notification` hook (create the `hooks` block if it doesn't exist):

```json
{
  "hooks": {
    "Notification": [
      {
        "hooks": [
          {
            "type": "command",
            "command": "say \"Surya [[slnc 400]] need a second\" 2>/dev/null || true"
          }
        ]
      }
    ]
  }
}
```

Replace `Surya` with your own name. That's it — the next session will speak whenever Claude needs your input.

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
Runs your shell command locally:  say "Surya [[slnc 400]] need a second"
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
say -v Lekha "सूर्या, एक मिनट"             # Hindi
say -v Kyoko "スーリヤさん、お願いします"      # Japanese
say -v Mónica "Surya, un segundo"        # Spanish
say -v Amélie "Surya, une seconde"       # French
say -v Tingting "Surya, 请稍等"            # Mandarin
say -v Yuna "Surya, 잠시만요"              # Korean
say -v Milena "Сурья, секунду"           # Russian
```

### Pick a persona
```bash
say -v Zarvox "Human input required"                 # 🤖 sci-fi robot
say -v Whisper "Surya... it is time"                 # 👻 dramatic whisper
say -v "Good News" "Your code is ready"              # 🎵 it literally sings
say -v Cellos "Claude needs you"                     # 🎻 sung over a cello line
say "This is the final boarding call for Surya"      # ✈️ airport announcement
say "Box box box"                                    # 🏎️ F1 pit-wall radio
say "Player one, your move"                          # 🎮 arcade vibes
say "Sir, your code awaits"                          # 🎩 personal butler
```

(The novelty voices like Zarvox, Whisper, Good News, and Cellos may need a one-time download in System Settings → Spoken Content.)

### Different sounds for different events
Hooks fire on more than just `Notification`. Give each event its own audio identity:

```json
{
  "hooks": {
    "Notification": [
      { "hooks": [{ "type": "command", "command": "say \"Surya [[slnc 400]] need a second\" 2>/dev/null || true" }] }
    ],
    "Stop": [
      { "hooks": [{ "type": "command", "command": "say -v \"Good News\" \"All done\" 2>/dev/null || true" }] }
    ]
  }
}
```

Now "need a second" means *waiting on you*, and a sung "All done" means *task finished* — you can tell them apart from across the room.

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
