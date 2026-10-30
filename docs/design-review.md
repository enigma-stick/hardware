# v1.1 design review status

This summarizes the recorded 2026-10-14 electrical/layout review, followed by a 2026-10-27 visualization update. It is historical evidence rather than a fresh check of future edits.

| Check | Recorded result |
| --- | --- |
| Schematic ERC | 0 errors, 0 warnings |
| PCB DRC | 0 errors, 0 unconnected items, 57 warnings |
| Assembly population | 27 installed parts; 26 for hand-solder-U3 variant |
| Manufacturing acceptance | Incomplete; supplier placement/fit/tooling checks remain |

Of the 57 DRC warnings, 29 are library-copy differences associated with intentional artwork/reference changes, 27 concern custom assembly metadata carried in the schematic, and one is a connected, tented UART RX via stub. TP2 is the exposed RX test pad. These warnings were documented rather than suppressed. The schematic-derived BOM carries assembly metadata.

The electrical review compared all 162 pad/drill/net dictionaries with the placement inventory. The later 3D update compared the USB/SE051 pad dictionaries and the full 324-segment trace inventory with pre-update readbacks; those matched. Raw diagnostics and check exports are excluded from the source repository; rerun checks against the current design before manufacturing.

The coarse automated preflight's READY result covered outline/routing/configured minimum constraints only. It did not establish connector fit, supplier acceptance, physical CPL orientation, or land-pattern correctness against drawings. Those open checks are listed in [build instructions](build.md).

USB routes have asymmetric layer changes and about 3.9 mm summed length difference. Differential impedance and USB eye quality have not been verified. Regulator thermal capacity and antenna behavior in an enclosure also need bench tests. The SE051 3D model is illustrative, not an official NXP clearance model.
