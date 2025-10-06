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