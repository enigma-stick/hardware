# Rendering models — 2026-10-27

Both models are attached to the placed footprints in enigma-stick-v1.1.kicad_pcb. Close and reopen KiCad's3D viewer to refresh an already-open view.

## USB-C J1

Uses the existing unmodified supplier CAD file `../libraries/USB4155-03-C_REVA.step` (its original license/provenance header is retained). The model is referenced via `${KIPRJMOD}` for portability. OpenCascade inspection established its native axes and mounting-face coordinates before alignment.

Placed model transform: rotation X=-90°, offset(0,-14.05,0.15)mm, scale1. The rear mounting tabs map to board X102.3/Y106.425 and113.825, coincident with the two shell slots. The solder-tail lower plane is seated at the board top. The matching model association was also saved in the project-local USB footprint library through Konnect.

This is a visualization/alignment update; connector thickness/fit and manufacturing acceptance still require the checks in the [build notes](../../docs/build.md).

## SE051 IC1

`SE051C2-visual-standin.step` is a verbatim copy of KiCad's installed `Package_DFN_QFN.3dshapes/UQFN-20-1EP_3x3mm_P0.4mm_EP1.85x1.85mm.step`. Its original copyright/license header is retained. This is an approximate visual stand-in, not an official NXP SE051 solid model.

The donor model measures3×3×0.52mm. In the board model association, X/Y scale remain1 and Z scale is0.32/0.52=0.6153846153846154, matching NXP's nominal3×3×0.32mm seated envelope. It has20 perimeter terminals and a pin-one dot. Lead and exposed-pad detail are illustrative; it is not an enclosure-clearance or footprint-validation authority. [NXP SOT1969-1 drawing](https://www.nxp.com/docs/en/package-information/SOT1969-1.pdf).

The placed IC1 model association is saved in the PCB. The old project-library IC1 footprint uses legacy `(module ...)` syntax, so Konnect refuses library-model editing for that file; its original library association was preserved. If that library footprint is refreshed/replaced later, retain or reapply the placed-model selection above.

## Outputs and verification

- `../reports/enigma-stick-v1.1-3d.png`:2400×1400 perspective render with shadows.
- KiCad10.0.7 native raytracer generated the images; no synthesized imagery or raster retouching.
- Live pad dictionaries for J1 and IC1 exactly match their pre-change readbacks. The complete324-segment live trace inventory also matches exactly.
- No electrical or placement changes were requested or made. Fabrication exports were not regenerated for this visualization update.
