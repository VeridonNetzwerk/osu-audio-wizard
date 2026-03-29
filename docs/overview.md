# Overview

osu! Audio Offset Wizard is a small browser tool to measure and calibrate input offset for rhythm games (for example osu!).

Purpose
- Help players determine the correct input offset for their setup.
- Provide a robust, repeatable measurement (median-based) and a clear, copyable result.

What this tool does (short)
- Schedules precise click sounds via the Web Audio API.
- Records user inputs (keyboard/mouse) and compares them to scheduled times.
- Filters out large outliers and applies robust statistics (median + MAD) to report a stable offset.

Files
- `index.html` — main app (scheduling, input handling, UI)
- `docs/` — this documentation
- `Verbesserungen.md` — improvement notes / spec
