<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=gradient&customColorList=6,11,20&height=200&section=header&text=F1%20Race%20Replay&fontSize=75&fontColor=fff&animation=twinkling&fontAlignY=35&desc=Every%20Corner.%20Every%20Overtake.%20Relived.&descAlignY=60&descSize=20" width="100%"/>

<br/>

[![Python](https://img.shields.io/badge/Python-3.11%2B-E10600?style=for-the-badge&logo=python&logoColor=white&labelColor=0D0D0D)](https://python.org)
[![FastF1](https://img.shields.io/badge/FastF1-Telemetry-E10600?style=for-the-badge&logoColor=white&labelColor=0D0D0D)](https://github.com/theOehrly/Fast-F1)
[![Arcade](https://img.shields.io/badge/Arcade-Renderer-FF6B35?style=for-the-badge&logoColor=white&labelColor=0D0D0D)](https://api.arcade.academy)
[![License](https://img.shields.io/badge/License-MIT-E10600?style=for-the-badge&labelColor=0D0D0D)](LICENSE)

<br/>

<a href="https://github.com/isamkhan1809/f1-race-replay">
  <img src="https://readme-typing-svg.demolab.com?font=JetBrains+Mono&weight=700&size=22&pause=1000&color=E10600&center=true&vCenter=true&width=700&lines=Live+F1+Telemetry+%E2%80%94+Animated+in+Real+Time;Safety+Car+%7C+Leaderboard+%7C+Driver+Insights;Every+Race.+Every+Season.+On+Demand.;Powered+by+FastF1+%2B+Python+Arcade." alt="Typing SVG" />
</a>

</div>

---

<br/>

<div align="center">

```
  ╔══════════════════════════════════════════════════════════════╗
  ║                                                              ║
  ║   23 drivers. 60+ laps. Millions of GPS data points.         ║
  ║   Every corner, every overtake, every safety car.            ║
  ║                                                              ║
  ║           Now you can watch it all again.                    ║
  ║                                                              ║
  ╚══════════════════════════════════════════════════════════════╝
```

</div>

<br/>

## `>_ The Story`

> *Formula 1 generates more telemetry per race than almost any sport on earth — GPS position at 50Hz, tyre compounds, DRS activation, safety car deployment, sector times.*
>
> *FastF1 makes it accessible. This project makes it watchable.*
>
> *Select a year and a round. Watch every car race across the track in real time. Pause it. Rewind it. Check any driver's telemetry mid-race.*

<br/>

## `>_ What It Does`

<table>
<tr>
<td width="50%">

**Select a race:**
```
Year:  2025
Round: 12 (British Grand Prix)
Mode:  Race / Sprint / Qualifying
```

</td>
<td width="50%">

**Watch it live:**
```
🏎  VER  P1  — Medium   Lap 34/52
🏎  NOR  P2  — Hard     Lap 34/52
🟡  SC   DEPLOYING — Sector 2
🔴  PIA  OUT — Mechanical
```

</td>
</tr>
</table>

<br/>

## `>_ Architecture`

```
┌─────────────────────────────────────────────────────────────┐
│                    F1 RACE REPLAY ENGINE                    │
│                                                             │
│  ┌──────────────┐    ┌──────────────┐    ┌──────────────┐   │
│  │  GUI / CLI   │───▶│   FastF1     │───▶│  f1_data.py  │   │
│  │  Year/Round  │    │  Session     │    │  Frame Gen   │   │
│  │  Selector    │    │  Loader      │    │  SC Compute  │   │
│  └──────────────┘    └──────────────┘    └──────┬───────┘   │
│                                                 │           │
│                           ┌─────────────────────▼───────┐   │
│                           │     arcade_replay.py        │   │
│                           │     Track Renderer          │   │
│                           │     Driver Positions        │   │
│                           │     Leaderboard + HUD       │   │
│                           └─────────────────────┬───────┘   │
│                                                 │           │
│                           ┌─────────────────────▼───────┐   │
│                           │     Insights Menu           │   │
│                           │     Telemetry per Driver    │   │
│                           │     Speed · Gear · DRS      │   │
│                           └─────────────────────────────┘   │
└─────────────────────────────────────────────────────────────┘
```

<br/>

## `>_ Controls`

```
SPACE          → Pause / Resume
← / →          → Rewind / Fast Forward
↑ / ↓          → Speed up / Slow down
1 / 2 / 3 / 4  → Set speed (0.5× · 1× · 2× · 4×)
R              → Restart
D              → Toggle DRS zones
B              → Toggle progress bar
L              → Toggle driver name labels
Click          → Select driver (telemetry panel opens)
Shift+Click    → Multi-select
```

<br/>

## `>_ Get Running`

```bash
# Clone
git clone https://github.com/isamkhan1809/f1-race-replay.git
cd f1-race-replay

# Install
python -m venv venv && source venv/bin/activate
pip install -r requirements.txt

# Launch GUI menu
python main.py

# Or go straight to a race
python main.py --viewer --year 2025 --round 12
```

<br/>

## `>_ Run Modes`

```bash
python main.py                                               # GUI menu
python main.py --cli                                         # CLI menu
python main.py --viewer --year 2025 --round 12               # Race
python main.py --viewer --year 2025 --round 12 --sprint      # Sprint
python main.py --viewer --year 2025 --round 12 --qualifying  # Qualifying
python main.py --viewer --year 2025 --round 12 --no-hud      # Clean view
python main.py --viewer --year 2025 --round 12 --refresh-data # Force reload
```

<br/>

## `>_ Safety Car System`

The SC position is **simulated** from real F1 track status data (code `4`). No GPS exists for the actual safety car — it is computed ~500m ahead of the race leader.

```
SC Phases:
  deploying  →  animates from pit lane, pulsing amber glow
  on_track   →  leads field, steady amber, "SC" label
  returning  →  fades back to pit lane, "SC IN" label
```

<br/>

## `>_ Tech Stack`

<div align="center">

| Layer | Technology |
|---|---|
| **Data** | FastF1 (official F1 telemetry) |
| **Renderer** | Python Arcade |
| **Language** | Python 3.11+ |
| **Caching** | Local `.fastf1-cache/` + `computed_data/` |

</div>

<br/>

## `>_ Project Structure`

```
f1-race-replay/
├── main.py
├── src/
│   ├── f1_data.py           # Telemetry loading + SC position
│   ├── arcade_replay.py     # Renderer + UI
│   ├── interfaces/
│   │   ├── race_replay.py
│   │   └── qualifying.py
│   └── lib/
│       ├── tyres.py
│       └── time.py
├── computed_data/           # Auto-generated cache
└── .fastf1-cache/
```

<br/>

---

<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=gradient&customColorList=6,11,20&height=120&section=footer&animation=twinkling" width="100%"/>

<br/>

*Lights out. And away we go.*
*Real telemetry. Real races. Endlessly replayable.*

<br/>

⚠️ *No copyright infringement intended. F1 trademarks belong to their respective owners. All data from public APIs for educational use only.*

<br/>

[![GitHub](https://img.shields.io/badge/github-isamkhan1809-E10600?style=for-the-badge&logo=github&logoColor=white&labelColor=0D0D0D)](https://github.com/isamkhan1809)

</div>
