# Voice alert not working? Troubleshoot it (macOS + VS Code) 🔧

If you set up the [voice alert](voice-alert.md) and hear **nothing** — especially inside the **VS Code extension** — use this logged version. It writes a line to `~/.claude/voice-alert.log` on every fire, telling you *exactly* why it did (or didn't) speak.

> **macOS only.** Uses the built-in `say` command and `lsappinfo`.

## Why it often fails in VS Code

The plain `Notification` hook **doesn't fire inside the VS Code extension** (it works fine in a bare terminal). The fix is a focus-aware `Stop` hook that speaks only when you've tabbed *away* from VS Code. But that hook depends on the `VSCODE_PID` environment variable being present — and a few setups, an un-restarted editor, or a missing voice can all cause silence. The log below tells you which one.

## 1. Install the logged hooks

Open `~/.claude/settings.json` (create it if missing) and add this `hooks` block inside the top-level `{ }`. **Replace `[put your name]` (it appears twice) with your name.**

```json
{
  "hooks": {
    "Notification": [
      {
        "hooks": [
          {
            "type": "command",
            "command": "echo \"$(date '+%F %T') [Notification] fired\" >> \"$HOME/.claude/voice-alert.log\"; say -v Daniel \"[put your name] [[slnc 400]] your input is required, sir\" 2>>\"$HOME/.claude/voice-alert.log\" || true"
          }
        ]
      }
    ],
    "Stop": [
      {
        "hooks": [
          {
            "type": "command",
            "command": "L=\"$HOME/.claude/voice-alert.log\"; ts=$(date '+%F %T'); front=$(lsappinfo info -only name \"$(lsappinfo front)\" 2>/dev/null | sed -E 's/.*\"LSDisplayName\"=\"([^\"]*)\".*/\\1/'); if [ -z \"$VSCODE_PID\" ]; then echo \"$ts [Stop] fired; VSCODE_PID empty -> skip (not a VS Code session)\" >> \"$L\"; exit 0; fi; case \"$front\" in Code|iTerm2|Terminal) echo \"$ts [Stop] fired; VSCODE_PID=$VSCODE_PID front=[$front] -> SILENT (editor focused)\" >> \"$L\";; *) say -v Daniel \"[put your name] [[slnc 400]] your input is required, sir\" 2>>\"$L\"; echo \"$ts [Stop] fired; VSCODE_PID=$VSCODE_PID front=[$front] -> SPOKE (say rc=$?)\" >> \"$L\";; esac; true"
          }
        ]
      }
    ]
  }
}
```

> Already have keys in the file? Just add the `"hooks"` key alongside them — don't paste a second `{ }`. Keep the JSON valid.

## 2. Fully quit and reopen VS Code

The hook config only reloads on restart. Quit VS Code completely (⌘Q), then reopen it.

## 3. Trigger it

In a Claude Code session, send any short message, then **immediately click into Chrome (or any non-VS-Code app) and wait ~5 seconds.** You should hear *"…your input is required, sir."*

## 4. Read the log

Open the VS Code integrated terminal and run:

```bash
cat ~/.claude/voice-alert.log
```

Match the most recent line to the table:

| Log line | Meaning & fix |
|---|---|
| `… -> SPOKE (say rc=0)` | ✅ **Working.** You just have to be tabbed away from VS Code to hear it. |
| `VSCODE_PID empty -> skip` | The hook can't tell it's inside VS Code. `VSCODE_PID` isn't reaching the hook's shell — see [fix below](#fix-vscode_pid-empty). |
| `… -> SILENT (editor focused)` | Working as designed, but VS Code was the focused window. Tab away to Chrome and retry. |
| `SPOKE (say rc=1)` (non-zero) | Hook fires but `say` failed — the **Daniel voice isn't installed**. System Settings → Accessibility → Spoken Content → System Voice → manage → add **Daniel** (English UK). |
| **(no file / empty)** | The hook never fired → settings.json wasn't saved, JSON is invalid, or VS Code wasn't restarted. Recheck steps 1–2. |

## Fix: `VSCODE_PID empty`

If the log says `VSCODE_PID empty`, the gate is bailing out. Swap the **first part** of the `Stop` command's gate from relying on `VSCODE_PID` to detecting any Claude-in-an-app session — replace:

```
if [ -z "$VSCODE_PID" ]; then echo "$ts [Stop] fired; VSCODE_PID empty -> skip (not a VS Code session)" >> "$L"; exit 0; fi;
```

with a version that drops the gate entirely and relies purely on the focused-app check:

```
# (no VSCODE_PID gate — decide solely by which app is focused)
```

i.e. delete that whole `if … fi;` clause. The `case "$front"` block already stays silent when VS Code/terminal is focused and speaks otherwise, so the gate is only an optimization — removing it makes the alert work even when `VSCODE_PID` isn't exported.

> Trade-off: without the gate, the `Stop` hook also runs in plain-terminal sessions. That's harmless (it stays silent while the terminal is focused), but if you *also* use the `Notification` hook in the terminal you may get a double alert there. If you only use VS Code, removing the gate is the simplest fix.

## Clean up the log later

The log grows by one line per turn. Delete it anytime:

```bash
rm ~/.claude/voice-alert.log
```

To go back to the silent (non-logging) version, use the hooks from the main [voice-alert.md](voice-alert.md) tip.

## Manage hooks

Type `/hooks` inside any Claude Code session to review or disable hooks.
