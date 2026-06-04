# Installing i3 Window Manager on Ubuntu

**i3** is a lightweight, tiling window manager that's highly configurable and popular among developers. Here's a complete step-by-step guide to install and set it up on Ubuntu.

## Installation Steps

### 1. Update Your System
Open a terminal and run:
```
sudo apt update
sudo apt upgrade
```

### 2. Install i3
Install the i3 window manager package:
```
sudo apt install i3
```

This installs the core i3 window manager. You may also want to install additional components:
```
sudo apt install i3-wm i3status i3lock suckless-tools
```

Here's what each package does:
- **i3-wm**: The core window manager
- **i3status**: A lightweight status bar for i3
- **i3lock**: A simple screen locker
- **suckless-tools**: Includes dmenu, a fast application launcher

### 3. Install a Display Manager (if needed)
If you don't have a login screen, install one:
```
sudo apt install lightdm lightdm-gtk-greeter
```

### 4. Select i3 at Login
Log out of your current session. At the login screen, look for a session selector (usually a menu or button). Select **i3** from the available window managers and log in.

Alternatively, if you're using a terminal-based login, you can edit `~/.xinitrc`:
```
echo "exec i3" >> ~/.xinitrc
```

Then start X with:
```
startx
```

### 5. Complete Initial Setup
When you first log into i3, you'll be prompted to generate a configuration file. Choose **Yes** when asked, and select your preferred modifier key (typically the **Super/Windows key** or **Alt**).

This creates `~/.config/i3/config` with sensible defaults.

---

## Essential i3 Keybindings to Know

| Keybinding | Action |
|---|---|
| **Mod + Return** | Open a terminal |
| **Mod + d** | Open dmenu (application launcher) |
| **Mod + [1-9]** | Switch to workspace 1-9 |
| **Mod + Shift + [1-9]** | Move window to workspace 1-9 |
| **Mod + Arrow Keys** | Navigate between windows |
| **Mod + v** | Split window vertically |
| **Mod + h** | Split window horizontally |
| **Mod + f** | Toggle fullscreen |
| **Mod + Shift + q** | Close window |
| **Mod + Shift + e** | Exit i3 |

(Replace **Mod** with your chosen modifier key, usually Super/Windows key)

---

## Post-Installation Configuration

### Install a Terminal Emulator
i3 uses whatever terminal is configured in its config file. Install a good one:
```
sudo apt install alacritty
```

Or use the default:
```
sudo apt install xterm
```

### Edit Your i3 Config
Open the configuration file:
```
nano ~/.config/i3/config
```

Common customizations:
- Change the terminal emulator: Find the line `bindsym $mod+Return exec i3-sensible-terminal` and replace with your preferred terminal
- Adjust colors, gaps, and fonts
- Add custom keybindings

### Install Additional Tools
Consider installing these complementary tools:
```
sudo apt install feh nitrogen polybar rofi
```

- **feh/nitrogen**: Wallpaper setters
- **polybar**: Advanced status bar (alternative to i3status)
- **rofi**: Advanced application launcher (alternative to dmenu)

---

## Troubleshooting

**Blank screen after login?** Press **Mod + Return** to open a terminal, then troubleshoot from there.

**i3 not appearing in login menu?** Make sure `lightdm` is installed and set as your display manager:
```
sudo dpkg-reconfigure lightdm
```

**Config not loading?** Check for syntax errors:
```
i3 -C
```

---

That's it! You now have a functional i3 setup. From here, you can customize the configuration file to match your workflow. i3's real power comes from its keyboard-driven workflow and extensive customization options.