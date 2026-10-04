# ☕ Insomnia

> Keep your Linux computer awake, without forgetting about it.

Tools like Caffeine hide in the system tray, where it's easy to forget they're
running. Insomnia takes the opposite approach.

## Features

- Blocks system suspend, and optionally screen blanking
- Optional time limit (30 min to 8 hours, or indefinitely)
- Status and remaining time shown in the taskbar title
- Colored window: bright when active, muted when inactive
- Single instance: launching it again brings the window to the front
- Locks are always released, even if the app crashes or gets killed

## Requirements

Python 3 with PyGObject and GTK 3, and systemd. These are installed by default on Linux Mint (tested on Cinnamon).

## Installation

```bash
mkdir -p ~/.local/bin ~/.local/share/applications
cp insomnia ~/.local/bin/ && chmod +x ~/.local/bin/insomnia
cp insomnia.desktop ~/.local/share/applications/
```

Insomnia then shows up in the application menu under Accessories. It blocks sleep as soon as it starts.

## How it works

Two mechanisms are used together:

- `Gtk.Application.inhibit()`, which goes through the session manager and is honored by the screensaver and the desktop power manager
- a `systemd-inhibit` lock, honored by logind

The logind lock is tied to the app's PID, so it can never outlive the app. You can check active locks with `systemd-inhibit --list`.

Closing the laptop lid still suspends the computer.

## Customization

Window colors are set by the `COLOR_*` constants at the top of the `insomnia` script.

## License

Do whatever the hell you want with it.