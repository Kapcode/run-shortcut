
# run-shortcut

A universal, cross-platform keyboard shortcut emulator for Linux. `run-shortcut` automatically detects whether you are running **X11** or **Wayland** and routes keystrokes through `xdotool` or `ydotool` accordingly.

Developed by [Kapcode](https://github.com/kapcode) for specialized macro solutions and system automation.

## 🚀 Features

- **Auto-Detection:** Automatically switches between `xdotool` (X11) and `ydotool` (Wayland).
- **Desktop Integration:** Native support for generating Pop!_OS/GNOME/Xfce `.desktop` app launchers.
- **Native Installation:** Includes a built-in installer to deploy itself to `/usr/local/bin`.
- **Strict Naming Enforcement:** Rejects execution if renamed or given a `.sh` extension, ensuring it is treated as a compiled system binary.
- **Modifier Support:** Handles complex combinations like `ctrl alt shift p` natively.
- **Human Simulation:** Includes fixed or randomized delays and dynamic "autowait" between keystrokes to mimic human typing.
- **Dependency Aware:** Performs intelligent version checks (via binary or `dpkg`) and provides compatibility warnings for older tool builds.

## 📦 Installation

The easiest way to use `run-shortcut` is to install it globally on your system. 

1. **Clone the repository:**
   ```bash
   git clone [https://github.com/kapcode/run-shortcut.git](https://github.com/kapcode/run-shortcut.git)
   cd run-shortcut



2. **Make it executable:**
```bash
chmod +x run-shortcut

```


3. **Install it globally:**
```bash
./run-shortcut --install

```


*(This copies the script to `/usr/local/bin/run-shortcut`. It will prompt for your `sudo` password if required.)*

### Uninstallation

To remove the tool from your system, simply run:

```bash
run-shortcut --uninstall

```

## 🖥️ Desktop Integration (App Launchers)

You can turn any macro into a clickable desktop application that appears in your system search bar (like the Pop!_OS Launcher).

### Create a Launcher

The `--make-launcher` command requires exactly **3 arguments**: `"Name"` `"-flags"` `"keys"`.
*(If you do not want to pass any flags, you must provide an empty string `""`).*

**Example with a delay (Recommended so the launcher loses focus before typing):**

```bash
run-shortcut --make-launcher "Paste" "-d 2000" "ctrl v"

```

**Example without flags:**

```bash
run-shortcut --make-launcher "Quick Refresh" "" "ctrl r"

```

### Manage Launchers

To see a list of all custom launchers created by this tool and their IDs:

```bash
run-shortcut --list-launchers

```

To delete a launcher from your system:

```bash
run-shortcut --remove-launcher paste

```

## 🛠 Usage (CLI)

The script takes a single string argument consisting of key names separated by spaces. Modifiers (e.g. `ctrl`, `alt`, `shift`) are held while the final key is pressed.

### Basic Shortcut

```bash
run-shortcut "ctrl o"

```

### With Delay (2 second wait before executing)

Useful if you need time to switch window focus before the macro fires:

```bash
run-shortcut -d 2000 "ctrl alt space"

```

### Human-like Randomized Typing

Add a random delay between 20ms and 100ms between every key event to simulate a human user:

```bash
run-shortcut -raw 20,100 "ctrl shift t"

```

### Focus Wait

Pause and wait for manual confirmation (pressing Enter in the terminal) before firing the keystrokes:

```bash
run-shortcut --focus-wait "super d"

```

### Debugging & Verbose Mode

If a shortcut isn't firing, use `-v` to see exactly which backend tool and keycodes are being used, as well as version detection:

```bash
run-shortcut -v "ctrl l"

```

## 🗺 Future Roadmap

* **Sequence Support (Multi-Step Macros):** Handle semicolon-separated strings (e.g., `"ctrl l; type 'https://kapcode.io'; enter"`).
* **Active Window Targeting:** Add `--window <name>` flag to focus specific windows before firing keys.
* **Virtual Input Device Management:** Logic to auto-start `ydotoold` if not running.
* **Environment Variable Overrides:** Support `RS_TOOL` overrides in `.bashrc`.
* **Standard Input (Pipe) Mode:** Allow reading keys from pipe (e.g., `echo "ctrl c" | run-shortcut -`).
* **Recording Module:** A `--record` flag to capture input and generate shortcut strings.
* **Profile Support:** Load complex macros from JSON/YAML files.

## ⚠️ Requirements

* **X11:** Requires `xdotool` (`sudo apt install xdotool`)
* **Wayland:** Requires `ydotool` and the `ydotoold` daemon running (`sudo apt install ydotool`)

## 📄 License

MIT

```

```
