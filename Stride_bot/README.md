
# Ayush Quadruped PyBullet Simulation

This project simulates a quadruped robot in PyBullet using:
- Inverse kinematics (`src/IK_solver.py`)
- Body/leg kinematics model (`src/kinematic_model.py`)
- Gait generation (`src/gaitPlanner.py`)
- Runtime sliders and camera controls (`src/pybullet_debugger.py`)

## Requirements

- Python 3.8+ (3.10+ recommended)
- `pip`
- Windows/Linux/macOS

## 1) Setup

From inside the `Stride_bot` folder:

```bash
python -m venv .venv
```

Activate environment:

Windows (PowerShell):
```powershell
.venv\Scripts\Activate.ps1
```

Linux/macOS:
```bash
source .venv/bin/activate
```

Install dependencies:

```bash
pip install numpy pybullet
```

## 2) Prepare Mesh Assets

`ayushbot.urdf` uses mesh paths like:
`package://STL_simulation/base_link.stl`

So you must extract `STL_simulation.zip` in this project root so this folder exists:

```text
Stride_bot/STL_simulation/
```

## 3) Run

Run from the `Stride_bot` directory:

```bash
python bot_walk.py
```

If everything is correct, PyBullet GUI opens and the robot appears on a plane.

## Runtime Controls

### GUI sliders
- `x, y, z`: body translation offset
- `roll, pitch, yaw`: body orientation
- `L`: linear step magnitude
- `Lrot`: rotational component
- `angleWalk`: walk direction angle (degrees)
- `stepPeriod`: gait period (seconds)
- `step_dur_asym`: duty-cycle asymmetry control
- `TROT` / `BOUND`: gait mode selector

### Keyboard camera controls
- `H` / `F`: yaw +
- `T` / `G`: pitch +
- `Z` / `X`: zoom in/out
- `Esc`: disconnect simulation

## Project Structure

```text
Stride_bot/
├─ bot_walk.py
├─ ayushbot.urdf
├─ STL_simulation.zip
└─ src/
   ├─ IK_solver.py
   ├─ geometrics.py
   ├─ kinematic_model.py
   ├─ gaitPlanner.py
   └─ pybullet_debugger.py
```

## Troubleshooting

1. `No module named pybullet`
- Run: `pip install pybullet`

2. URDF mesh not found (`STL_simulation/...`)
- Extract `STL_simulation.zip` so `Stride_bot/STL_simulation` exists.

3. Nothing moves
- Increase `L` slider, set `stepPeriod` around `0.5-1.5`, and keep either `TROT=1` or `BOUND=1`.

4. Import error for debug module
- This repo now uses: `from src.pybullet_debugger import pybulletDebug`

