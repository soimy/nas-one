# nas-one

A from-scratch NAS chassis, modelled in FreeCAD.

## Layout

```
models/       FreeCAD documents
reference/    third-party ATX specifications + derived board data (see its README)
```

## Current state

`models/ATX-Base.FCStd` holds a single fully constrained sketch,
**`ATX_Board_Outline`**, used as the layout reference for the chassis:

- ATX board outline, **304.8 × 243.84 mm** (12" × 9.6"), origin at the bottom-left
  corner, rear edge along the top
- all **9 ATX mounting-hole centres** as plain sketch points (no holes modelled)
- all **7 PCIe expansion slots** marked with construction lines
- `FullyConstrained = True`, 26 geometries / 69 constraints / 24 dimensions

Board dimensions, the hole table and the PCIe slot table are documented in
[`reference/atx-board-data.md`](reference/atx-board-data.md) and mirrored as CSV.

## Toolchain

FreeCAD 1.1. No macros or external workbenches are required — the model is plain
sketch geometry.
