# ⚡ run-shortcut

### Macro Engine & OSD for Kapcode Infrastructure

**Version: 1.9.1**

`run-shortcut` is a bash-based utility designed to handle keyboard and mouse automation across X11 and Wayland (Pop!_OS). It manages `xdotool` and `ydotool` backends automatically and provides a floating, balanced OSD for visual feedback.

---

## 📦 Dependencies

Ensure these system packages are present for full functionality.

### Core Execution

* **`xdotool`**: Backend for X11 environments.
* **`ydotool`**: Backend for Wayland environments (Mutter/GNOME).
* **`bash`**: The engine itself (v4.0+).

### HUD & Recording

* **`osd_cat` (xosd-bin)**: Provides the floating Cyan HUD.
* **`libinput-tools`**: Required for the `--record` hardware click capture.
* **`xrandr`**: Used to probe screen dimensions for Smart HUD placement.
* **`wlrctl`**: (Optional) Helper for absolute coordinate resolution on Wayland.

### Installation Command

```bash
sudo apt update && sudo apt install xdotool ydotool xosd-bin libinput-tools xrandr wlrctl

```

---

## ⚙️ Setup & Hardware Access

To install the binary globally and configure hardware permissions:

1. **Run the Installer:**
```bash
./run-shortcut --install

```


2. **Permissions & Reboot:** The installer adds your user to the `input` group and sets a `udev` rule for `/dev/uinput`. **A full reboot is required** for these hardware permissions to take effect.
3. **Daemon Check:** Wayland users require `ydotoold` to be running. The script attempts to start it automatically, but you can verify it manually:
```bash
pgrep -x ydotoold || ydotoold &

```



*Note: If you edit the script in your dev folder, run `./run-shortcut --reinstall` to sync changes to `/usr/local/bin`.*

---

## ⏺️ The Recorder

Instead of manual coordinate hunting, use the hardware recorder:

```bash
run-shortcut --osd --record

```

1. **Click your target** on the screen.
2. **Terminal Output:** The terminal will print the exact `run-shortcut` command.
3. **HUD Feedback:** The OSD will flash the captured `X, Y` coordinates in real-time.

---

## 🖱️ Usage Examples

### 1. Simple Key Combo

```bash
run-shortcut --osd "ctrl alt t"

```

### 2. Mouse Move + Click + Delay

```bash
run-shortcut --osd -m 1125 894 -c 1 -d 500 "Action Label"

```

### 3. Create a Dock Shortcut (Launcher)

```bash
run-shortcut --make-launcher "My Macro" "--osd -d 500" "alt o"

```

* **Launcher:** `~/.local/share/applications/rs-my-macro.desktop`
* **Wrapper:** `~/.local/bin/rs-wrap-my-macro`

---

## 📑 Command Reference

| Flag | Function |
| --- | --- |
| `--install` | Sets binary and `udev` rules. |
| `--reinstall` | Wipes and rebuilds from local source. |
| `--record` | Starts `libinput` click capture. |
| `--make-launcher` | Generates a .desktop file and shell wrapper. |
| `--remove-launcher` | Deletes a managed shortcut by ID. |
| `--osd` | Shows the floating cyan HUD (Bottom-Left). |
| `--color` | Overrides HUD color (e.g., `--color "green"`). |

---

## 🗺️ Roadmap

### Phase 1: Distribution

* **`.deb` Packaging:** Create a native Debian package to automate dependency checks and `udev` rule installation.
* **`install.sh` Wrapper:** A one-click installer for fresh workstations that handles user group assignments.
* **Systemd Integration:** Move `ydotoold` management into a user-level Systemd service for better reliability on Wayland.

### Phase 2: Advanced Macro Logic

* **Sequence Recorder:** Update `--record` to capture multiple clicks and export them as a single `.sh` macro.
* **Pixel-Search Triggers:** Integrate basic image-recognition to wait for specific UI elements before firing.
* **Interactive HUD:** Add "Dismiss" or "Cancel" functionality via OSD buttons.

### Phase 3: Kapcode Ecosystem

* **Android Bridge:** Use the **Kapcode Macro Controller** Android app to trigger PC macros over the local network.
* **Centralized Repo:** Move all custom macros into `/etc/kapcode/macros` for system-wide access.

---

**Kapcode Software Repository** | *2026*

---
