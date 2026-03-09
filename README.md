# ⚡ Kapcode run-shortcut

**The Universal Linux Macro Engine**

`run-shortcut` is a high-performance wrapper for `xdotool` and `ydotool`. It automatically detects your display server (X11 vs. Wayland), manages hardware daemons, handles complex hardware permissions, and provides real-time On-Screen Display (OSD) feedback.

## 🚀 Features

* **Auto-Switching Display Logic**: Seamlessly switches between `xdotool` (X11) and `ydotool` (Wayland).
* **Integrated OSD**: Uses `xosd-bin` to provide a non-focus-stealing visual cue during macro execution.
* **Auto-Daemon Management**: Automatically checks for and starts `ydotoold` if it's missing.
* **One-Command Permissions**: Configures `uinput` udev rules and user groups during installation.
* **GUI Launcher Generator**: Create `.desktop` files for your dock that inherit your full environment and log errors to `/tmp`.

---

## 🛠 Installation

### 1. Dependencies

```bash
# For Wayland support
sudo apt install ydotool

# For OSD visual cues
sudo apt install xosd-bin

```

### 2. Global Setup

Run the install flag from your project directory. This copies the binary to `/usr/local/bin` and configures hardware permissions.

```bash
./run-shortcut --install

```

> [!IMPORTANT]
> A reboot is required after the first installation to apply the new `uinput` hardware rules and group memberships.

---

## ⌨️ CLI Usage

| Flag | Description |
| --- | --- |
| `--osd` | Show the red "⚡ MACRO" overlay on the bottom right. |
| `-d <ms>` | Initial delay. Crucial for letting GUI menus close before typing. |
| `-m <X> <Y>` | Move the mouse to absolute coordinates. |
| `-c <1|2|3>` | Click mouse button (1=Left, 2=Middle, 3=Right). |
| `-aw <ms>` | Autowait: Pause between specific key/mouse events. |
| `-v` | Verbose mode: Debug environment and socket info. |

**Example Command:**

```bash
run-shortcut --osd -d 1000 -m 500 500 -c 1 "ctrl alt t"

```

---

## 🖥 Launcher Management (Dock Macros)

Create a persistent shortcut that appears in your Pop!_OS launcher or dock. These launchers use an intelligent wrapper to bridge environment variables between the GUI and the terminal.

### Create:

```bash
run-shortcut --make-launcher "Speak Text" "--osd -d 2000" "alt o"

```

### List & Remove:

```bash
run-shortcut --list-launchers
run-shortcut --remove-launcher "speak-text"

```

---

## 📂 Infrastructure Layout

* **Binary**: `/usr/local/bin/run-shortcut`
* **Wrappers**: `~/.local/bin/rs-wrap-*` (Handles environment bridging)
* **Launchers**: `~/.local/share/applications/rs-*.desktop`
* **Logs**: `/tmp/rs-*.log` (Check these if a dock icon fails)

---

## 🗺 Future Roadmap
* [ ] **Testing in X11**: need to test in X11, the tool used is differnt in Wayland and X11.
* [ ] **Recording Mode**: Add `--record` to capture live mouse coordinates and clicks.
* [ ] **Sequence Support**: Handle semicolon-separated commands in one string.
* [ ] **Window Targeting**: Force focus on specific app titles before firing.
* [ ] **Native OSD**: A Go/Python-based overlay for pure Wayland environments.

---
