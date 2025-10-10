# Marlin 2.1.2.5 Configuration for Tevo Tarantula

This repository contains a customized `Configuration.h` and `Configuration_adv.h` for Marlin 2.1.2.5, tailored for a Tevo Tarantula 3D printer.

## Hardware Specifications

These configuration files are set up for a Tevo Tarantula with the following key components:

*   **Motherboard:** MKS Gen L
*   **Display:** RepRapDiscount Smart Controller (2004 LCD)
*   **Stepper Drivers:** A4988
*   **Extruder:** Stock Tevo Tarantula Extruder
*   **Bed:** Standard Bed (200x200mm) with PID heating enabled

## Key Features Enabled

*   Mesh Bed Leveling (Manual)
*   Linear Advance (K=0)
*   Babystepping
*   Power Loss Recovery
*   Classic Jerk
*   EEPROM Storage

## How to Use

1.  Download a fresh copy of the [Marlin 2.1.2.5 firmware](https://github.com/MarlinFirmware/Marlin/releases/tag/2.1.2.5).
2.  Replace the default `Configuration.h` and `Configuration_adv.h` files in the `Marlin/` subdirectory with the files from this repository.
3.  Compile and upload the firmware using PlatformIO in Visual Studio Code.

---

*These configuration files are provided as-is. Always review the settings before flashing the firmware to your printer, especially if your hardware differs from the specifications listed above.*

## PID Tuning Explanation

### Why you should perform a PID tune

PID (Proportional, Integral, Derivative) tuning is a calibration procedure that helps your 3D printer maintain a stable and consistent target temperature. Without it, you can experience temperature fluctuations that negatively affect print quality, such as inconsistent extrusion, blobs, or stringing.

Here's why it's important:

*   **Optimal temperature control:** A well-tuned PID algorithm allows the firmware to make precise, real-time adjustments to the heater's power output. This eliminates the large temperature swings of a simpler "bang-bang" heating method, where the heater is just turned on or off.
*   **Improved print quality:** Stable temperatures lead to more consistent filament melting and extrusion. This helps ensure better layer adhesion and higher overall print quality by preventing defects caused by thermal variations.
*   **Adapting to hardware changes:** You should always perform a PID tune when you install a new hotend, heater cartridge, thermistor, or part cooling fan. New components change the thermal properties of your setup, so new PID values are needed to maintain proper temperature control.
*   **Mitigating external factors:** By tuning the PID with the part cooling fan on, the calibration accounts for the fan's cooling effect on the hotend. This results in more stable temperatures during actual printing.

### Commented G-code for PID tuning

This sequence of G-code commands is designed to perform a PID autotune on the extruder (E0) at a printing temperature of 210°C.

```gcode
; Start of PID tuning sequence
G28 ; Home the printer to a safe, known starting position.
G1 X50 Y50 F3000 ; Move the extruder to a position away from the center of the bed to avoid potential heat damage.
M106 S255 ; Turn the part cooling fan on to 100% to simulate real printing conditions and get a more accurate tune.
M303 E0 S210 C8 ; Begin the PID autotune. E0 specifies the extruder, S210 sets the target temperature, and C8 sets 8 calibration cycles.
; The printer will cycle heating and cooling, then display the optimal P, I, and D values in the terminal.
; End of auto-tuning process.
M301 P<Kp_value> I<Ki_value> D<Kd_value> ; Replace with your calculated P, I, and D values and send the command.
M500 ; Save the newly tuned PID settings to the printer's EEPROM so they are not lost.
M107 ; Turn off the part cooling fan.
```