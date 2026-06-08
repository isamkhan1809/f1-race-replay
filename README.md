<div align="center">

```
███████╗ ██╗    ██████╗  █████╗  ██████╗███████╗    ██████╗ ███████╗██████╗ ██╗      █████╗ ██╗   ██╗
██╔════╝███║    ██╔══██╗██╔══██╗██╔════╝██╔════╝    ██╔══██╗██╔════╝██╔══██╗██║     ██╔══██╗╚██╗ ██╔╝
█████╗  ╚██║    ██████╔╝███████║██║     █████╗      ██████╔╝█████╗  ██████╔╝██║     ███████║ ╚████╔╝
██╔══╝   ██║    ██╔══██╗██╔══██║██║     ██╔══╝      ██╔══██╗██╔══╝  ██╔═══╝ ██║     ██╔══██║  ╚██╔╝
██║      ██║    ██║  ██║██║  ██║╚██████╗███████╗    ██║  ██║███████╗██║     ███████╗██║  ██║   ██║
╚═╝      ╚═╝    ╚═╝  ╚═╝╚═╝  ╚═╝ ╚═════╝╚══════╝   ╚═╝  ╚═╝╚══════╝╚═╝     ╚══════╝╚═╝  ╚═╝   ╚═╝
```

<img src="https://readme-typing-svg.demolab.com?font=Fira+Code&weight=600&size=20&pause=1000&color=E10600&center=true&vCenter=true&width=700&lines=Every+Corner.+Every+Overtake.+Relived.+%F0%9F%8F%8E%EF%B8%8F;Live+F1+Telemetry+%E2%80%94+Animated+in+Real+Time;Safety+Car+%7C+Leaderboard+%7C+Driver+Insights;Powered+by+FastF1+%26+Python+Arcade" alt="Typing SVG" />

<img src="https://media.giphy.com/media/kGnvCfL0PZ54WOKo3p/giphy.gif" width="360" />

[![Python](https://img.shields.io/badge/Python-3.11%2B-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://python.org)
[![FastF1](https://img.shields.io/badge/FastF1-Data-E10600?style=for-the-badge)](https://github.com/theOehrly/Fast-F1)
[![Arcade](https://img.shields.io/badge/Arcade-Engine-FF6B35?style=for-the-badge)](https://api.arcade.academy)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow?style=for-the-badge)](LICENSE)

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
python main.py                                          # GUI menu
python main.py --cli                                    # CLI menu
python main.py --viewer --year 2025 --round 12          # Direct race
python main.py --viewer --year 2025 --round 12 --sprint # Sprint
python main.py --viewer --year 2025 --round 12 --qualifying  # Qualifying
python main.py --viewer --year 2025 --round 12 --no-hud      # No HUD
python main.py --viewer --year 2025 --round 12 --refresh-data # Force refresh
```

---

## ◈ Safety Car System

The Safety Car is **simulated** from real F1 track status data (code `4`). Position is computed ~500m ahead of the race leader.

| Phase | Visual |
|---|---|
| `deploying` | Animates from pit lane, pulsing amber glow, "SC DEPLOYING" label |
| `on_track` | Leads field, steady amber glow, "SC" label |
| `returning` | Fades to pit lane, "SC IN" label |

---

## ◈ Project Structure

```
f1-race-replay/
├── main.py                      ← Entry point
├── src/
│   ├── f1_data.py               ← Telemetry + SC position
│   ├── arcade_replay.py         ← Renderer + UI
│   ├── interfaces/
│   │   ├── race_replay.py
│   │   └── qualifying.py
│   └── lib/
│       ├── tyres.py
│       └── time.py
├── resources/
├── computed_data/
└── .fastf1-cache/
```

---

## ◈ Disclaimer

No copyright infringement intended. Formula 1 and related trademarks are property of their respective owners. All data is from publicly available APIs for educational and non-commercial purposes only.

---

<div align="center">

**Lights out. And away we go.**

*MIT License*

<br/>

F1 fan, Python developer, or into motorsport data visualisation?<br/>
Let's connect — built by <a href="https://github.com/isamkhan1809">Isam Khan</a> &nbsp;|&nbsp;
<a href="https://linkedin.com/in/isam-khan-3a1260292"><img src="https://img.shields.io/badge/-LinkedIn-0A66C2?style=flat-square&logo=linkedin&logoColor=white&labelColor=000000"/></a>
<a href="https://isamkhan.com"><img src="https://img.shields.io/badge/-isamkhan.com-00D9FF?style=flat-square&logo=googlechrome&logoColor=white&labelColor=000000"/></a>

</div>
