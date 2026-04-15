# Walker Application Launcher

Walker is a fast Wayland-native application launcher (powered by the Elephant backend).

## Global Shortcuts (GNOME)
- **Activate Walker:** `Super + Space` (as configured in GNOME Shortcuts)
- **Close:** `Escape`
- **Toggle (Open/Close):** `Super + Space` (pressing again while open will close it)

## Providers and Prefixes
Use these prefixes at the start of your search to trigger specific modules:

| Prefix | Module | Example | Description |
| :--- | :--- | :--- | :--- |
| `=` | Calculator | `= 15 * 4` | Fast calculations (Enter to copy result) |
| `!` | Todo (Tasks) | `! Buy milk` | Task manager (Enter to save) |
| `@` | Web Search | `@ arch wiki` | Direct search in your default browser |
| `:` | Clipboard | `: (history list)` | Clipboard history (Text and Images) |
| `>` | Runner (Shell) | `> htop` | Execute shell commands |
| `/` | Files | `/Documents` | Search for files and directories |
| `.` | Symbols/Emoji | `. fire` | Search for emojis and unicode symbols (🔥) |
| `$` | Windows | `$ chrome` | Switch between open windows |
| `;` | Provider List | `;` | List all active providers |
| `%` | Bookmarks | `% google` | Search browser bookmarks |

## Clipboard Shortcuts (`:`)
- **Enter**: Copy and select item.
- **Ctrl + D**: Remove a specific item from history.
- **Ctrl + Shift + D**: Clear **entire** clipboard history.
- **Ctrl + I**: Toggle filters (Images Only / Text Only / Both).
- **Ctrl + P**: Pin item (prevents deletion during clear).
- **Ctrl + O**: Open item in text editor before copying.

## Technical Notes (Arch Linux)
- **Config Path:** `~/.config/walker/config.toml`
- **Backend:** `elephant` (Service daemon)
- **User Service:** `systemctl --user status elephant`
- **Installation:** Requires `elephant-bin` and specific provider packages (e.g., `elephant-calc-bin`, `elephant-clipboard-bin`) installed uniformly to avoid plugin version conflicts.
- **GNOME Compatibility:** Set `as_window = true` and `force_keyboard_focus = true` for optimal behavior on Mutter/Wayland.

---
**Related:** [[OS/Linux/Linux|Linux]], [[OS/Linux/Systemd|Systemd]]
