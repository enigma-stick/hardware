# Installing the SE051 library locally

The standalone SamacSys SE051 symbol and footprint are excluded from Git. Download them from the provider for local use. The included KiCad package stand-in remains available for rendering; the provider's part-specific STEP model is optional.

This excludes standalone library files only. KiCad also stores the placed SE051 symbol inside the schematic and the placed footprint inside the PCB. Those embedded copies are still present. These instructions do not establish permission to redistribute that data; permission or independent replacements are still needed to resolve that question.

## Download and copy

1. Visit [Component Search Engine](https://componentsearchengine.com/) and search for **SE051C2HQ1**, manufacturer **NXP**. Register/sign in if requested and review the applicable download terms.
2. Download the CAD model ZIP and extract it outside the repository. The original package used for this project identifies SamacSys and model version **1.1**, released **2022-07-01**. If the current download differs, compare its pins and pads with the design before updating any placed parts.
3. Copy the following files, creating the destination footprint directory if necessary. Paths in the right column are relative to the repository root.

| File in downloaded package | Local destination |
| --- | --- |
| `KiCad/SE051C2HQ1.kicad_sym` | `v1.1/libraries/SE051C2HQ1.kicad_sym` |
| `KiCad/QFN40P300X300X33-21N-D.kicad_mod` | `v1.1/libraries/Enigma_SE.pretty/QFN40P300X300X33-21N-D.kicad_mod` |

Do not copy the entire download into the repository. These destination paths are ignored by Git; existing local copies can be left in place.

## Register the libraries in KiCad 10

Open `v1.1/enigma-stick-v1.1.kicad_pro` through KiCad's project manager so the editors use the correct project.

In Schematic Editor, open **Preferences → Manage Symbol Libraries… → Project Specific Libraries**. The project already includes an entry named `SE051C2HQ1`; confirm it resolves to `${KIPRJMOD}/libraries/SE051C2HQ1.kicad_sym`. If missing, add the downloaded symbol library using that nickname and path.

In PCB Editor, open **Preferences → Manage Footprint Libraries… → Project Specific Libraries**. Add the `Enigma_SE.pretty` directory as a KiCad footprint library with nickname `Enigma_SE` and path `${KIPRJMOD}/libraries/Enigma_SE.pretty`, unless an equivalent entry already exists. The current project footprint table does not include this entry, so a fresh setup needs it.

The expected library identifiers are `SE051C2HQ1:SE051C2HQ1` for the symbol and `Enigma_SE:QFN40P300X300X33-21N-D` for the footprint. The placed component is **IC1**, with footprint pads **1–21**, including exposed pad **21**.

Registering the libraries does not require replacing the placed component. The board has project-specific artwork and a model association; inspect changes before using **Update Symbols from Library** or **Update Footprints from Library**, and rerun ERC/DRC after design changes.

See KiCad's [symbol library documentation](https://docs.kicad.org/10.0/en/eeschema/eeschema.html) and [footprint library documentation](https://docs.kicad.org/10.0/en/pcbnew/pcbnew.html) for library-table details.

## Optional part-specific 3D model

The original download includes `3D/SE051C2HQ1.stp`. For local visualization, copy it to the ignored path `v1.1/models/SE051C2HQ1.stp` and select it in IC1's footprint properties under **3D Models**. Verify orientation and seating against the board and package drawing; the existing stand-in's scale/offset should not be assumed to fit this different model. The supplied PCB continues to use the redistributable KiCad stand-in.
