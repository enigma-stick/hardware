# Building the v1.1 prototype

Open the current [KiCad project](../v1.1/enigma-stick-v1.1.kicad_pro). Read the [review status](design-review.md) before ordering. Native sources are authoritative; regenerate exports after changes.

The standalone SE051 symbol and footprint are local downloads; follow the [library setup guide](se051-library-setup.md) to install them.

## Fabrication and assembly

The recorded design targets a two-layer, 34.4 × 20 mm FR-4 board, nominal 0.8 mm thick, with 1 oz outer copper, green mask and ENIG. All 27 installed components are on the front. The USB plug and antenna overhang the base PCB; leave space for both in tooling and any enclosure. ENIG is the recorded prototype finish, rather than a claim that every alternate finish has been evaluated.

The [JLCPCB BOM](../v1.1/manufacturing/JLCPCB-BOM.csv) lists 27 populated designators; bare test pads TP1/TP2 are excluded. Component availability, prices and assembly eligibility need checking with the supplier at order time.

Gerbers, drills and component placement files are generated release artifacts and are excluded from the source repository. Generate them from the current design in KiCad for a manufacturing release, and ensure the BOM and placement file cover the same installed parts. If the ESP32 module will be hand soldered, omit U3 from both files for that assembly variant.

Before accepting an order:

1. Confirm USB4155-03-C board-thickness tolerance and slot fit against its drawing and the board fabricator's actual finished thickness.
2. Obtain assembly-provider approval for this small board, panel/rails/tooling, and the USB/antenna overhangs. Do not assume omitting U3 qualifies for a cheaper service.
3. Review custom USB and SE051 lands, mask, paste and plated shell slots against manufacturer drawings in the Gerber/drill viewer.
4. Inspect every component in the provider's placement preview, particularly connector, module, secure element, IC orientation and LED polarity. CPL rotation has not been physically accepted.

For a manufacturing release, rerun ERC/DRC, inspect the exported layers and drills, and package the matching BOM and placement file with the fabrication outputs.

## Bring-up

Inspect assembly and check for shorts before powering. Verify VBUS and 3.3 V, regulator temperature and ripple under sustained firmware load. Program the separately developed firmware, then exercise USB enumeration/transfers, SE051 communication, BOOT and CHIP_EN reset. Test RF operation with the intended enclosure and antenna clearance.

SW1 is BOOT; SW2 resets CHIP_EN. SW3 is the internal factory-reset input: GPIO4 → normally open switch → GND. Enable the MCU's internal pull-up; pressed reads zero. Firmware must implement debounce and the factory-reset action. The PCB switch is intended to be inaccessible from outside an enclosure. TP1/TP2 provide UART TX/RX debug access.

USB signal integrity, thermal behavior and RF performance require physical validation. No firmware, enclosure or provisioning credentials are supplied in this repository.
