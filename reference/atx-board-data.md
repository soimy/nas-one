# ATX board data

Everything below is derived from the documents in this folder — see
[`README.md`](README.md) for sources.

## Coordinate frame

All values are millimetres unless marked `in`. The origin is the **bottom-left
corner of the board outline**, `+X` to the right, `+Y` up, matching the sketch
`models/ATX-Base.FCStd`.

Orientation follows **ATX Specification v2.2, Figure 2** (the plan view):

```
      +--------------------------------------------------+
      |  expansion-slot end  ──►  rear edge (REAR)  ──►  |  6.25" rear I/O shield
      |                                                  |  sits at the top-right
      |   ●  ●  ●                    ●                   |
      |                                                  |
      |   ●        ●                 ●                   |
      |                                                  |
      |   ●  ●  ●                    ●                   |
      +--------------------------------------------------+
     origin                                              x = 304.8
```

- **Top edge** = rear of the board (where the I/O shield and expansion brackets are)
- **Left edge** = the expansion-slot end (`x = 0`)
- **Right edge** = the I/O-shield end (`x = 304.8`)

## Board outline

| | mm | inch |
|---|---|---|
| Width (along the rear edge) | **304.8** | 12.000 |
| Depth | **243.84** | 9.600 |

Real ATX boards have roughly **R2** rounded corners (the bit-tech DXF uses
exactly `R2.000`); the sketch keeps a sharp rectangle because the corner radius is
not part of the ATX specification and a sharp rectangle is the safe envelope.

## Mounting holes — 9 required for ATX

From ATX v2.2 §3.2 / Figure 2. Verified against the bit-tech `ATX_Layout.dxf`
circle centres (exact match) and against the microATX layout: the 6 shared holes
line up only when the microATX board is shifted `+30.48 mm` along X, i.e. when the
two boards share the I/O end of the rear edge.

| Hole | ATX | microATX | X (mm) | Y (mm) | X (in) | Y (in) |
|:----:|:---:|:--------:|-------:|-------:|-------:|-------:|
| A | ✔ |   | 16.51 | 233.68 | 0.65 | 9.20 |
| C | ✔ | ✔ | 140.97 | 233.68 | 5.55 | 9.20 |
| F | ✔ | ✔ | 298.45 | 210.82 | 11.75 | 8.30 |
| G | ✔ |   | 16.51 | 78.74 | 0.65 | 3.10 |
| H | ✔ | ✔ | 140.97 | 78.74 | 5.55 | 3.10 |
| J | ✔ | ✔ | 298.45 | 78.74 | 11.75 | 3.10 |
| K | ✔ |   | 16.51 | 6.35 | 0.65 | 0.25 |
| L | ✔ | ✔ | 140.97 | 6.35 | 5.55 | 0.25 |
| M | ✔ | ✔ | 298.45 | 6.35 | 11.75 | 0.25 |
| B |   | ✔ | 95.25 | 233.68 | 3.75 | 9.20 |
| R |   | ✔ | 74.93 | 78.74 | 2.95 | 3.10 |
| S |   | ✔ | 95.25 | 78.74 | 3.75 | 3.10 |

Notes:

- Holes **A, G, K** are ATX-only (drawn as open circles in Figure 2); B, R, S are
  microATX-only. C, F, H, J, L, M are shared.
- The three holes on the bottom row (K, L, M, at `y = 6.35`) are the ones the
  specification calls out as *"mechanical support along the front edge of the full
  size ATX board"*.
- Hole **F** was promoted from optional to required in ATX 2.1.
- ATX v2.2 Figure 7 dimensionally confirms hole F as `.650` from the right edge
  and `.400` from the rear edge, and the third row as `6.500 [165.1]` from the
  rear edge.
- `x = 0.65 / 5.55 / 11.75 in` and `y = 0.40 / 6.50 / 9.35 in` from the rear edge.

## PCIe expansion slots — 7 slots

Slots run perpendicular to the rear edge, pitch **0.8 in = 20.32 mm** (ATX v2.2:
*"The slot spacing must remain constant"*, Figure 3 `.800 TYP BETWEEN CONNECTORS`).

| Slot | X (mm) | X (in) |
|:----:|-------:|-------:|
| 1 | 20.62 | 0.8119 |
| 2 | 40.94 | 1.6119 |
| 3 | 61.26 | 2.4119 |
| 4 | 81.58 | 3.2119 |
| 5 | 101.90 | 4.0119 |
| 6 | 122.22 | 4.8119 |
| 7 | 142.54 | 5.6119 |

Each slot spans **Y = 121.41 … 206.25 mm**, i.e. `1.480 … 4.820 in` measured from
the rear edge — an 84.84 mm long connector footprint, which matches the PCIe x16
connector contact length (≈85.6 mm) as well as the PCI connector body dimensioned
in ATX v2.2 Figure 3.

### How the X anchor was chosen

ATX v2.2 Figure 3 was converted to vector data and the PCI connector card-slot
centre-lines measured at **3.2119 / 4.0119 / 4.8119 in** and the AGP connector at
**5.6116 in** (from the board's left edge). Those four positions are exactly
`0.8119 + 0.8n`, so slots 4–7 reproduce the specification verbatim and slots 1–3
extend the same grid leftwards.

⚠️ **Absolute X carries roughly ±3 mm of uncertainty.** The figure's ISA connectors
sit on a different pin-1 datum (`0.25 + 0.8n`), and an independent drawing built
from the same specifications (bit-tech `ATX_Layout.dxf`) puts the connector bodies
at `18.53 + 20.32n` — about 2 mm left of the values above. The **pitch is exact**;
only the left/right shift of the whole group is soft. Edit `DistanceX = 20.62` on
the first slot line in the sketch to re-anchor, and the other six follow.

The frame is self-consistent with the I/O shield: the 6.25 in (158.75 mm) rear I/O
window occupies `x = 146.05 … 304.8`, and slot 7 at `x = 142.54` clears it.
