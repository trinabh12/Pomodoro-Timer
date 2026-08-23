# Pomodoro Timer

A small Tkinter desktop app implementing the Pomodoro Technique — 25-minute work sessions broken up with short and long breaks, tracked with checkmarks.

## About

The app cycles through work and break periods automatically:

- **Work session** — 25 minutes, timer shown in green.
- **Short break** — 5 minutes, after each work session (shown in pink).
- **Long break** — 20 minutes, after every 4th work session (shown in red).

Each completed work session adds a ✔ checkmark below the timer, so you can see how many "pomodoros" you've finished in a row.

## Repository contents

| File | Description |
|---|---|
| `main.py` | The app: timer logic, session cycling, and Tkinter UI. |
| `tomato.png` | Tomato image displayed behind the countdown, loaded relative to the script. |
| `.gitattributes` | Git line-ending/attributes configuration. |

## Getting started

### Prerequisites

- Python 3
- Tkinter (ships with most standard Python installs; on Linux you may need to install it separately, e.g. `sudo apt install python3-tk`)

No external packages are required beyond the standard library.

### Usage

Run the script from the project root, so it can find `tomato.png`:

```bash
git clone https://github.com/trinabh12/Pomodoro-Timer.git
cd Pomodoro-Timer
python main.py
```

A window titled "Pomodoro" will open.

- Click **Start** to begin (or resume) the countdown.
- Click **Reset** to stop the timer and clear the checkmarks.

## How it works

- A `reps` counter increments each time `start_timer()` runs, and its value (odd/even, and divisibility by 8) determines whether the next session is work, a short break, or a long break.
- `countdown()` recursively schedules itself every second via `window.after(1000, ...)`, updating the on-canvas timer text (`MM:SS`) until it reaches zero, then kicks off the next session automatically.
- After every completed work session, a ✔ is appended to the `check_marks` label.

## Notes

- This is a GUI app and needs a display; it won't run headless (e.g. plain SSH or CI) without a virtual display like Xvfb.
- The timer durations (`WORK_MIN`, `SHORT_BREAK_MIN`, `LONG_BREAK_MIN`) are constants at the top of `main.py` if you want to customize the session lengths.
