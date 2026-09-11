# reference — ATX board reference material

Third-party documents and derived data used to model the ATX motherboard in
`../models/`. Nothing in here is our own work; see **Sources & licensing** below.

## Layout

```
reference/
├── atx/
│   ├── ATX_Specification_v2.2.pdf          Intel ATX spec — board size + mounting holes
│   └── microATX_Specification_v1.2.pdf     Intel microATX spec — hole sub-set cross-check
├── motherboard-layouts/
│   ├── ATX_Layout.dxf / .pdf               bit-tech layout pack (2D, millimetres)
│   ├── mATX_Layout.dxf / .pdf
│   └── Mini-ITX_Layout.dxf / .pdf
├── atx-board-data.md                       derived dimensions + how they were verified
├── atx-mounting-holes.csv                  machine-readable hole centres
└── pcie-slots.csv                          machine-readable PCIe slot centrelines
```

## Sources & licensing

| File | Origin | Notes |
|---|---|---|
| `atx/ATX_Specification_v2.2.pdf` | Intel, via the Internet Archive capture of `formfactors.org/developer/specs/atx2_2.pdf` (capture `20040205033536`) | Intel's own licence text inside the document grants the right to reproduce the specification for any purpose **provided the "Important Information and Disclaimers" section (paragraphs 1–4) is reproduced in whole** — it is, on PDF pages 2–3. |
| `atx/microATX_Specification_v1.2.pdf` | Intel, via the Internet Archive capture of `formfactors.org/developer/specs/matxspe1.2.pdf` (capture `20040221041404`) | Same Intel licence terms. |
| `motherboard-layouts/*` | [bit-tech.net — "How to Make a Motherboard Tray from Scratch"](https://bit-tech.net/guides/modding/case-mod/how-to-make-a-motherboard-tray-from-scratch/1/), July 2018 | Freely downloadable companion files (`MotherboardLayoutFiles.zip`). No explicit licence is stated by the author; treat as **reference-only, do not redistribute commercially**. The Fusion 360 `.f3d` source was dropped to keep the repo small — only the DXF/PDF exports are kept. |

`formfactors.org` no longer resolves; both Intel documents were retrieved from the
Wayback Machine. Every coordinate in `atx-board-data.md` was re-derived from these
files and cross-checked between them, not copied from a secondary summary.

## Re-downloading

```sh
mkdir -p reference/atx reference/motherboard-layouts

curl -L -o reference/atx/ATX_Specification_v2.2.pdf \
  "https://web.archive.org/web/20040205033536id_/http://www.formfactors.org/developer/specs/atx2_2.pdf"

curl -L -o reference/atx/microATX_Specification_v1.2.pdf \
  "https://web.archive.org/web/20040221041404id_/http://www.formfactors.org/developer/specs/matxspe1.2.pdf"

curl -L -o /tmp/layouts.zip \
  "http://bit-tech.net/media/file/2018/7/MotherboardLayoutFiles.zip"
unzip -j /tmp/layouts.zip '*/DXF/*' '*/PDF/*' -d reference/motherboard-layouts/
```
