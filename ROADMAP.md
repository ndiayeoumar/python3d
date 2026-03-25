# 🗺️ Python 3D Modelling — Learning Roadmap

> **Approach:** Project-based. Every phase ends with something printed or rendered.
> **Pace:** 3–5 hours/week → ~6 months total.
> **Stack:** Trimesh · CadQuery · Blender/bpy · Open3D

---

## Repo Structure

```
python-3d-journey/
├── ROADMAP.md
├── README.md                  # Learning log — update weekly
├── environment/
│   ├── requirements.txt
│   └── setup.md
├── assets/                    # STLs, renders, photos of prints
├── 1_trimesh/
│   ├── 01_mesh_basics.py
│   ├── 02_operations.py
│   └── projects/
│       └── name_tag/
├── 2_cadquery/
│   ├── 01_workplanes.py
│   ├── 02_boolean_ops.py
│   └── projects/
│       └── tool_holder/
├── 3_blender/
│   ├── 01_bpy_basics.py
│   ├── 02_bmesh.py
│   └── projects/
│       └── generative_vase/
├── 4_open3d/
│   ├── 01_point_clouds.py
│   ├── 02_reconstruction.py
│   └── projects/
│       └── terrain_tile/
└── 5_capstone/
    └── projects/
        └── TBD/
```

---

## Environment Setup

```bash
# Create dedicated conda environment
conda create -n python3d python=3.11
conda activate python3d

# phase 1 & 4 dependencies
pip install trimesh numpy open3d scipy

# Phase 2
pip install cadquery

# Phase 3 — Blender ships its own Python interpreter
# Install this for IDE autocompletion only
pip install fake-bpy-module

# Optional but useful
pip install matplotlib jupyter
```

---

## Phase 1 — Mesh Foundations
**Tool:** Trimesh + NumPy
**Duration:** ~6 weeks (weeks 1–6)
**Status:** 🔲 Not started

### What you'll learn
- The mesh data structure: vertices `(N,3)`, faces `(M,3)`, normals
- Loading and inspecting STL/OBJ files
- Basic operations: translate, rotate, scale, section, merge
- Watertightness, volume, center of mass
- Boolean operations (union, difference, intersection)
- Exporting print-ready STL files

### Key concepts
| Concept | Analogy |
|---|---|
| Vertex | A tuple `(x, y, z)` — a point in space |
| Face | An index triplet `(i, j, k)` — three vertices forming a triangle |
| Mesh | A NumPy array collection — just data |
| Normal | A unit vector perpendicular to a face — used for lighting & orientation |
| Watertight | A closed, manifold mesh — required for 3D printing |

### Weekly breakdown
| Week | Topic | Script |
|---|---|---|
| 1 | Load STL, inspect vertices/faces, visualize | `01_mesh_basics.py` |
| 2 | Transforms: translate, rotate, scale | `02_operations.py` |
| 3 | Boolean ops: union, difference | `03_booleans.py` |
| 4 | Watertightness, repair, volume | `04_analysis.py` |
| 5–6 | Anchor project | `projects/name_tag/` |

### 🖨️ Anchor Project: Parametric Name Tag
Write a script that generates a flat rectangular tag with raised text,
fully parameterized (width, height, thickness, text size). Export to STL and print.

```python
# Signature of the script to build
def generate_name_tag(
    name: str,
    width: float = 60.0,
    height: float = 25.0,
    thickness: float = 3.0,
    text_height: float = 1.5,
) -> trimesh.Trimesh:
    ...
```

**Definition of done:**
- [ ] Script runs with no manual intervention
- [ ] STL is watertight (`mesh.is_watertight == True`)
- [ ] Printed successfully on Ender-3 V3 SE
- [ ] Photo added to `assets/`

---

## Phase 2 — Parametric CAD
**Tool:** CadQuery
**Duration:** ~6 weeks (weeks 7–12)
**Status:** 🔲 Not started

### What you'll learn
- Workplanes and coordinate systems
- Sketches: lines, arcs, constraints
- 3D operations: extrude, pocket, revolve, loft
- Boolean ops at a higher abstraction level
- Fillets, chamfers, shells
- Exporting to STEP and STL

### Key concepts
| Concept | Analogy |
|---|---|
| Workplane | A 2D coordinate system — like a canvas placed in 3D space |
| Sketch | A 2D shape on a workplane — like an SVG path |
| Extrude | Push a sketch into 3D — like inflating a flat shape |
| Pocket | Cut a sketch into a solid — the inverse of extrude |
| Fillet | Round an edge — purely geometric smoothing |

### Weekly breakdown
| Week | Topic | Script |
|---|---|---|
| 7 | Workplanes, boxes, cylinders | `01_workplanes.py` |
| 8 | Sketches, extrude, pocket | `02_sketches.py` |
| 9 | Boolean ops, assemblies | `03_boolean_ops.py` |
| 10 | Fillets, chamfers, shells | `04_finishing.py` |
| 11–12 | Anchor project | `projects/tool_holder/` |

### 🖨️ Anchor Project: Printer Tool Holder
Parametric wall-mounted holder for Ender-3 tools (spatula, nozzle wrench, PTFE cutter).
Fully configurable via a dict of tool diameters. Print and mount it.

```python
# Signature of the script to build
def generate_tool_holder(
    tools: list[dict],   # [{"name": "spatula", "diameter": 8.0}, ...]
    wall_thickness: float = 3.0,
    base_width: float = 80.0,
    mounting_hole_diameter: float = 4.0,
) -> cq.Assembly:
    ...
```

**Definition of done:**
- [ ] Script accepts arbitrary tool list
- [ ] STEP and STL exported
- [ ] Printed and physically mounted near printer
- [ ] Photo added to `assets/`

---

## Phase 3 — Generative & Artistic
**Tool:** Blender + bpy
**Duration:** ~6 weeks (weeks 13–18)
**Status:** 🔲 Not started

### What you'll learn
- Blender's Python scripting workspace and console
- Creating meshes from scratch with `bmesh`
- Procedural modifiers via code (subdivision, boolean, array, displace)
- Parametric geometry: math-driven curves and surfaces
- Basic rendering automation via Python

### Key concepts
| Concept | Analogy |
|---|---|
| `bpy.ops` | High-level Blender actions — like clicking the GUI |
| `bmesh` | Low-level mesh editing — like direct DOM manipulation |
| Modifier | A non-destructive transformation stack — like CSS filters |
| Driver | A value linked to a formula or variable — like a spreadsheet cell |
| Scene | A container for objects, lights, camera — like a DOM tree |

### Weekly breakdown
| Week | Topic | Script |
|---|---|---|
| 13 | Blender Python console, create basic objects | `01_bpy_basics.py` |
| 14 | bmesh: build mesh from scratch | `02_bmesh.py` |
| 15 | Modifiers as code | `03_modifiers.py` |
| 16 | Math-driven surfaces (sine, noise, spirals) | `04_math_surfaces.py` |
| 17–18 | Anchor project | `projects/generative_vase/` |

### 🖨️ Anchor Project: Generative Vase
A Blender Python script that generates a vase whose profile is defined
by a mathematical function. Randomizable with a seed. Rendered and printed.

```python
# Signature of the script to build
def generate_vase(
    profile_fn,          # callable: height -> radius
    height: float = 120.0,
    segments: int = 64,
    seed: int = 42,
) -> None:              # adds object directly to Blender scene
    ...
```

**Definition of done:**
- [ ] Script produces different vases from different seeds
- [ ] Render saved to `assets/`
- [ ] Vase is watertight and printed
- [ ] Photo added to `assets/`

---

## Phase 4 — Data-Driven Meshes
**Tool:** Open3D + Trimesh + NumPy
**Duration:** ~6 weeks (weeks 19–24)
**Status:** 🔲 Not started

### What you'll learn
- Point clouds: generating, loading, visualizing, sampling
- Surface reconstruction: Poisson, Ball Pivoting
- Marching cubes: scalar field → mesh
- Mesh smoothing, simplification, repair
- Real scientific data formats (PDB, NIfTI, GeoTIFF)

### Key concepts
| Concept | Analogy |
|---|---|
| Point cloud | A set of raw `(x,y,z)` points — no connectivity, like raw reads in bioinformatics |
| Reconstruction | Inferring surface from points — like assembly from reads |
| Marching cubes | Iso-surface extraction from a voxel grid — like contour lines on a map, in 3D |
| SDF | Signed Distance Field — a function f(x,y,z) = distance to surface |
| Voxel grid | A 3D array of values — like a 3D numpy array |

### Weekly breakdown
| Week | Topic | Script |
|---|---|---|
| 19 | Point cloud basics, visualization | `01_point_clouds.py` |
| 20 | Surface reconstruction from points | `02_reconstruction.py` |
| 21 | Marching cubes, scalar fields | `03_marching_cubes.py` |
| 22 | Real data: GeoTIFF elevation | `04_geodata.py` |
| 23–24 | Anchor project | `projects/terrain_tile/` |

### 🖨️ Anchor Project: 3D Terrain Tile
Download real SRTM elevation data, convert to mesh via marching cubes,
scale and frame it, export to STL and print a physical terrain tile.

```python
# Signature of the script to build
def generate_terrain(
    lat: float, lon: float,          # center coordinates
    size_km: float = 10.0,           # area to capture
    vertical_exaggeration: float = 2.0,
    base_thickness: float = 3.0,
) -> trimesh.Trimesh:
    ...
```

**Definition of done:**
- [ ] Script takes lat/lon and produces STL automatically
- [ ] Terrain is recognizable and geographically accurate
- [ ] Printed with visible topographic detail
- [ ] Photo added to `assets/`

---

## Phase 5 — Capstone
**Tool:** All of the above
**Duration:** Open-ended (weeks 25+)
**Status:** 🔲 Not started

### Goal
Build something non-trivial that combines at least two phases.
Chosen at the end of Phase 4 based on interests at that point.

### Candidate projects
| Project | Tools | Description |
|---|---|---|
| Protein mesh converter | Trimesh + Open3D | PDB → printable 3D mesh |
| Procedural city generator | CadQuery + Trimesh | Parametric printable architectural blocks |
| Parametric watch stand | CadQuery | Config-driven, adapts to any watch |
| Bioinformatics sculpture | Open3D + Blender | Genomic dataset → 3D art object |

---

## Progress Tracker

| Phase | Start | End | Anchor Project | Printed |
|---|---|---|---|---|
| 1 — Trimesh | — | — | Name Tag | 🔲 |
| 2 — CadQuery | — | — | Tool Holder | 🔲 |
| 3 — Blender/bpy | — | — | Generative Vase | 🔲 |
| 4 — Open3D | — | — | Terrain Tile | 🔲 |
| 5 — Capstone | — | — | TBD | 🔲 |

---

## Resources

### Trimesh
- Docs: https://trimesh.org
- GitHub: https://github.com/mikedh/trimesh

### CadQuery
- Docs: https://cadquery.readthedocs.io
- Primer: https://cadquery.readthedocs.io/en/latest/primer.html

### Blender / bpy
- API Docs: https://docs.blender.org/api/current/
- Scripting intro: https://docs.blender.org/manual/en/latest/editors/text_editor.html

### Open3D
- Docs: http://www.open3d.org/docs/release/
- Tutorials: http://www.open3d.org/docs/release/tutorial/

### General
- Thingiverse (STL models): https://www.thingiverse.com
- Printables (STL models): https://www.printables.com
- SRTM elevation data: https://earthexplorer.usgs.gov
- Protein structures (PDB): https://www.rcsb.org
