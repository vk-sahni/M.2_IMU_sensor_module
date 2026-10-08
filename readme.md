# M.2 RP2350 IMU Sensor Module

A KiCad hardware design for a compact M.2 Key A sensor module built around the Raspberry Pi RP2350B. The board combines an MPU-9250 motion sensor and a BME280 environmental sensor, with UAV and ArduPilot integration as the intended use case.

> **Project status:** Work in progress. The repository contains KiCad design files only; it does not include firmware or establish plug-and-play ArduPilot compatibility. The current design has outstanding KiCad ERC/DRC violations and is not ready for fabrication or flight use.

## Design overview

- **MCU:** RP2350B
- **IMU:** MPU-9250 (accelerometer, gyroscope, and magnetometer)
- **Environmental sensor:** BME280 (pressure, temperature, and humidity)
- **Memory:** W25Q128JVSIQ QSPI flash and APS6404L PSRAM
- **Removable storage:** MicroSD card socket
- **Host connection:** M.2 Key A edge connector
- **Other interfaces:** USB Type-C, SWD test points, and status LEDs
- **Power:** On-board XC6220 3.3 V regulators

The M.2 connector schematic maps 5 V power and sensor I2C signals, including separate `SDA`/`SCL` and `MPU_SDA`/`MPU_SCL` nets. Check the full schematic and target host pinout before connecting the module; M.2 is a connector format, not a guarantee of electrical or firmware compatibility.

## ArduPilot integration

This is a hardware design intended for UAV sensor and ArduPilot integration experiments. ArduPilot supports sensor communications over protocols such as I2C, SPI, UART, and CAN, but a sensor board still needs a compatible driver/backend, wiring, and configuration. This repository does not contain that firmware integration or demonstrate that an ArduPilot flight controller can detect these sensors through this M.2 connection.

Before attempting integration, verify the M.2 host pinout and voltage levels, determine which controller owns each bus, and confirm that the target ArduPilot firmware supports the required sensors and connection arrangement. See the official [ArduPilot sensor-driver documentation](https://ardupilot.org/dev/docs/code-overview-sensor-drivers.html).

## Repository contents

- `PCIe_Pie.kicad_pro` — KiCad project settings
- `PCIe_Pie.kicad_sch` and the other `*.kicad_sch` files — top-level and hierarchical schematics
- `PCIe_Pie.kicad_pcb` — PCB layout
- `CM4IO.pretty/` — project footprint library
- `CM4IO.3dshapes/` — 3D models used by footprints
- `sym-lib-table`, `fp-lib-table` — KiCad library table configuration

## Open the design

1. Install KiCad.
2. Open `PCIe_Pie.kicad_pro`.
3. Review the complete schematic hierarchy and PCB, including the project-local footprint and 3D model libraries.

## Validation status

KiCad command-line ERC and DRC checks run against the current design reported outstanding violations, including unconnected items. Review and resolve these in KiCad before generating manufacturing files. No fabrication outputs, assembled-board test results, sensor calibration results, or flight-test results are included in this repository.

## Safety

Treat the design as experimental. Verify the schematic, PCB rules, power rails, connector orientation, and signal levels before powering hardware. Bench-test and validate the complete sensor/firmware path before any UAV flight; do not rely on this module as a flight-critical sensor without appropriate testing and failsafes.

## References

- [ArduPilot sensor drivers and supported communication protocols](https://ardupilot.org/dev/docs/code-overview-sensor-drivers.html)
- [MPU-9250 datasheet](https://invensense.tdk.com/wp-content/uploads/2015/02/PS-MPU-9250A-01-v1.1.pdf)

