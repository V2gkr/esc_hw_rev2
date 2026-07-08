# ESC HW Rev2 - E-Bike BLDC Motor Driver

Rev2 hardware for an electronic speed controller (ESC) for an e-bike. Designed in KiCad.

## Key Specifications

| Parameter | Value |
|---|---|
| Nominal battery voltage | 36 V |
| Nominal motor power | 250 W |
| MCU | STM32G431CBT6 |
| Gate driver | DRV8320S |
| Phase current sensing |  low-side shunts |
| Rotor position feedback | Hall sensors |
| Interfaces | CAN FD, UART |
| Indication | LEDs (Green / Red) |
| Control | Reset button |

## Board Architecture

The project is split into several KiCad hierarchical schematic sheets:

- **MCU.kicad_sch** - STM32G431CBT6 support circuitry: power supply, crystals, debug interface, reset button, LEDs.
- **Power.kicad_sch** - 36 V input power stage, protection, DC/DC converters for logic and gate driver supply.
- **Inverter.kicad_sch** - three-phase power inverter stage based on DRV8320S and power MOSFETs.
- **Measurements.kicad_sch** - phase current sensing circuitry (3 low-side shunts) and Hall sensor interfaces.
- **CAN.kicad_sch** - CAN FD transceiver and supporting circuitry.
- **BLDC_Test.kicad_sch / BLDC_Test.kicad_pcb / BLDC_Test.kicad_pro** - top-level schematic and PCB layout tying all sheets above together.

## Key Subsystems

### Power Stage
Three-phase MOSFET inverter driven by the **DRV8320S** gate driver (built-in protection: overtemperature, overcurrent, gate drive undervoltage, etc.).

### Current and Rotor Position Sensing
- 3 low-side shunts - phase current measurement for FOC/trapezoidal commutation and overcurrent protection.
- Hall sensors - rotor position detection for low-speed commutation and start-up under load.

### Communication Interfaces
- **CAN FD** - primary control/telemetry channel (e.g. integration with a BMS or a central e-bike controller).
- **UART** - debugging, logging, alternative control/flashing channel.

### Indication and Control
- Green / Red LEDs - status indication (ready, fault, CAN activity, etc. â€” defined by firmware).
- Reset button - hardware MCU reset.

## Project Status

Hardware only (rev2). Firmware is maintained in a separate repository (see [`esc_fw_rev2`](https://github.com/V2gkr/esc_fw_rev2/tree/main)).

## TODO
- [ ] Export schematics to PDF for quick viewing without KiCad
- [ ] Bill of Materials (BOM)
- [ ] Board photos/renders
- [ ] Datasheet links for key components (DRV8320S, STM32G431CBT6)

## Tools
Designed in **KiCad**.

