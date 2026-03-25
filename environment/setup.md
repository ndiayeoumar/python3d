# Environment Setup

## Prerequisites

- [Miniconda](https://docs.conda.io/en/latest/miniconda.html) or [Anaconda](https://www.anaconda.com/download)
- Python 3.11 (managed by conda)
- macOS / Linux / Windows (WSL2 recommended on Windows)

---

## 1. Create and activate the conda environment

```bash
conda create -n python3d python=3.11
conda activate python3d
```

---

## 2. Install Phase 1 & 4 dependencies

```bash
pip install -r environment/requirements.txt
```

This installs:
| Package | Purpose |
|---|---|
| `trimesh` | Mesh loading, inspection, transforms, booleans, STL export |
| `numpy` | The numerical backbone — meshes are just arrays |
| `open3d` | Point clouds, surface reconstruction (Phase 4) |
| `scipy` | Scientific utilities — spatial, interpolation, signal |
| `matplotlib` | 2D plotting, useful for inspecting cross-sections |
| `pyglet` | Trimesh viewer backend on macOS |

---

## 3. Phase 2 — CadQuery (install when you reach it)

CadQuery depends on OpenCASCADE (OCCT), which is best installed via conda-forge:

```bash
conda install -c conda-forge cadquery
```

Or via pip (slower, may require build tools):

```bash
pip install cadquery
```

---

## 4. Phase 3 — Blender / bpy

Blender ships its **own** Python interpreter and does not use your conda env.
Scripts are run from inside Blender's scripting workspace.

For IDE autocompletion only (no Blender needed):

```bash
pip install fake-bpy-module
```

To run headless renders from the terminal:

```bash
blender --background --python your_script.py
```

Download Blender: https://www.blender.org/download/

---

## 5. Verify the setup

Run this quick sanity check:

```bash
python - <<'EOF'
import trimesh, numpy, open3d, scipy, matplotlib
box = trimesh.creation.box()
print("trimesh OK —", len(box.vertices), "vertices")
print("numpy OK —", numpy.__version__)
print("open3d OK —", open3d.__version__)
print("scipy OK —", scipy.__version__)
print("matplotlib OK —", matplotlib.__version__)
EOF
```

Expected output (versions may vary):

```
trimesh OK — 8 vertices
numpy OK — 1.x.x
open3d OK — 0.x.x
scipy OK — 1.x.x
matplotlib OK — 3.x.x
```

---

## 6. VS Code integration (optional but recommended)

1. Install the [Python extension](https://marketplace.visualstudio.com/items?itemName=ms-python.python)
2. Select interpreter: `Cmd+Shift+P` → "Python: Select Interpreter" → choose `python3d`
3. Install [Pylance](https://marketplace.visualstudio.com/items?itemName=ms-python.vscode-pylance) for type hints and autocompletion

---

## Updating this file

Add a note here whenever you install a new package or change the environment,
so the setup remains reproducible.

| Date | Change |
|---|---|
| 2026-03-25 | Initial setup — Phase 1 deps installed |
