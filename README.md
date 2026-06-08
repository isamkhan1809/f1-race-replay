<div align="center">

```
███████╗ ██╗    ██████╗  █████╗  ██████╗███████╗    ██████╗ ███████╗██████╗ ██╗      █████╗ ██╗   ██╗
██╔════╝███║    ██╔══██╗██╔══██╗██╔════╝██╔════╝    ██╔══██╗██╔════╝██╔══██╗██║     ██╔══██╗╚██╗ ██╔╝
█████╗  ╚██║    ██████╔╝███████║██║     █████╗      ██████╔╝█████╗  ██████╔╝██║     ███████║ ╚████╔╝
██╔══╝   ██║    ██╔══██╗██╔══██║██║     ██╔══╝      ██╔══██╗██╔══╝  ██╔═══╝ ██║     ██╔══██║  ╚██╔╝
██║      ██║    ██║  ██║██║  ██║╚██████╗███████╗    ██║  ██║███████╗██║     ███████╗██║  ██║   ██║
╚═╝      ╚═╝    ╚═╝  ╚═╝╚═╝  ╚═╝ ╚═════╝╚══════╝   ╚═╝  ╚═╝╚══════╝╚═╝     ╚══════╝╚═╝  ╚═╝   ╚═╝
```

### *Every Corner. Every Overtake. Relived.*

[![Python](https://img.shields.io/badge/Python-3.11%2B-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://python.org)
[![FastF1](https://img.shields.io/badge/FastF1-Data-E10600?style=for-the-badge)](https://github.com/theOehrly/Fast-F1)
[![Arcade](https://img.shields.io/badge/Arcade-Engine-FF6B35?style=for-the-badge)](https://api.arcade.academy)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow?style=for-the-badge)](LICENSE)

---

> **A Python application that downloads live F1 telemetry, animates every car on track, and lets you replay entire race weekends — with Safety Car, live leaderboard, and driver insights.**

</div>

---

## ◈ Watch the Race Unfold

```
┌──────────────────────────────────────────────────────────────────┐
│                    F1 RACE REPLAY ENGINE                         │
│                                                                  │
│   FastF1 API ──→ Telemetry Fetch ──→ Frame Computation           │
│                        │                    │                    │
│                   GPS positions         Safety Car               │
│                   Tyre compounds        simulation               │
│                   Lap times             ↓                        │
│                        └──────────→ Arcade Renderer              │
│                                         │                        │
│                               ┌─────────────────┐               │
│                               │  LIVE DASHBOARD │               │
│                               │  ─────────────  │               │
│                               │  Track Map      │               │
│                               │  Leaderboard    │               │
│                               │  Tyre Compounds │               │
│                               │  Telemetry HUD  │               │
│                               │  Safety Car     │               │
│                               └─────────────────┘               │
└──────────────────────────────────────────────────────────────────┘
```

---

## ◈ Features

| Feature | Description |
|---|---|
| **Race Replay** | Real-time animated driver positions on rendered track |
| **Safety Car** | Animated SC deploy/return with pulsing glow effect |
| **Live Leaderboard** | Driver positions + tyre compounds, updated every frame |
| **Telemetry Insights** | Speed, gear, DRS, lap time per selected driver |
| **Qualifying Mode** | Lap-by-lap qualifying session replay |
| **Sprint Support** | Sprint race and Sprint Qualifying sessions |
| **Interactive Controls** | Pause, rewind, fast-forward, variable playback speed |
| **Insights Menu** | Floating pit-wall panel launched automatically |
| **Checkpointing** | Computed telemetry cached — instant re-runs |
| **GUI + CLI Menu** | Pick year/round from a graphical or terminal menu |

---

## ◈ Controls

```
SPACE          → Pause / Resume
← / →          → Rewind / Fast Forward
↑ / ↓          → Increase / Decrease playback speed
1 / 2 / 3 / 4  → Set speed directly (0.5× · 1× · 2× · 4×)
R              → Restart replay
D              → Toggle DRS zones
B              → Toggle progress bar
L              → Toggle driver names on track
Click          → Select driver for telemetry
Shift + Click  → Multi-select drivers
```

---

## ◈ Quick Start

```bash
# 1. Clone
git clone https://github.com/isamkhan1809/f1-race-replay.git
cd f1-race-replay

# 2. Virtual environment
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate

# 3. Install dependencies
pip install -r requirements.txt

# 4. Launch GUI menu
python main.py

# 5. Or go directly to a race
python main.py --viewer --year 2025 --round 12
```

---

## ◈ All Run Modes

```bash
# GUI menu (default)
python main.py

# CLI menu
python main.py --cli

# Direct race
python main.py --viewer --year 2025 --round 12

# No HUD
python main.py --viewer --year 2025 --round 12 --no-hud

# Sprint race
python main.py --viewer --year 2025 --round 12 --sprint

# Qualifying
python main.py --viewer --year 2025 --round 12 --qualifying

# Force refresh cached data
python main.py --viewer --year 2025 --round 12 --refresh-data
```

---

## ◈ Safety Car System

The Safety Car is **simulated** from real F1 track status data (`session.track_status`, code `4`). Since the F1 API provides no GPS for the actual SC, its position is computed ~500m ahead of the race leader.

| Phase | Visual |
|---|---|
| `deploying` | Animates from pit lane onto track, pulsing amber glow, "SC DEPLOYING" label |
| `on_track` | Leads field, steady amber glow, "SC" label |
| `returning` | Fades back to pit lane, "SC IN" label |

---

## ◈ Building Custom Telemetry Windows

```python
from src.gui.pit_wall_window import PitWallWindow

class MyInsightWindow(PitWallWindow):
    def setup_ui(self):
        # Build your custom UI
        pass

    def on_telemetry_data(self, data):
        # Receive live telemetry every frame
        pass
```

See [docs/PitWallWindow.md](./docs/PitWallWindow.md) for the full guide.

---

## ◈ Project Structure

```
f1-race-replay/
├── main.py                      ← Entry point
├── src/
│   ├── f1_data.py               ← Telemetry + SC position computation
│   ├── arcade_replay.py         ← Renderer + UI logic
│   ├── ui_components.py         ← Buttons, leaderboard
│   ├── interfaces/
│   │   ├── race_replay.py       ← Race interface + SC rendering
│   │   └── qualifying.py        ← Qualifying interface
│   └── lib/
│       ├── tyres.py             ← Tyre type definitions
│       └── time.py              ← Time formatting
├── resources/                   ← Preview images
├── computed_data/               ← Auto-generated telemetry cache
└── .fastf1-cache/               ← FastF1 data cache
```

---

## ◈ Requirements

```
Python 3.11+
fastf1 · arcade · numpy
```

---

## ◈ Disclaimer

No copyright infringement intended. Formula 1 and related trademarks are the property of their respective owners. All data is from publicly available APIs for educational and non-commercial purposes only.

---

<div align="center">

**Lights out. And away we go.**

*MIT License*

</div>
