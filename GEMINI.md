# GEMINI Context: PES Board Project

This project, **PES Board**, is an embedded systems development environment for the Nucleo-F446RE microcontroller, complemented by a custom "PES Board" shield designed at ZHAW. It is primarily used for robotics and control workshops.

## Project Overview

- **Hardware Stack:** ST Nucleo-F446RE (STM32F446RE) + PES Board Shield.
- **Framework:** [Arm Mbed OS 6](https://os.mbed.com/mbed-os/).
- **Primary Language:** C++ (Embedded).
- **Main Peripherals:** DC Motors (3), Servos (4), Encoders (3), 9-axis IMU, SD Card, Ultrasonic/IR sensors.
- **Architecture:** Periodic task execution within a main loop, supported by a rich set of peripheral drivers in the `lib/` directory.

## Directory Structure

- `src/main.cpp`: Entry point. Often uses a periodic timer loop (typically 20ms/50Hz).
- `lib/`: Custom drivers for sensors and actuators (e.g., `DCMotor`, `IMU`, `EncoderCounter`).
- `include/`: Header files. `PESBoardPinMap.h` is critical as it maps PES Board peripherals to Nucleo pins.
- `docs/`: Extensive documentation, tutorials, and workshop instructions in Markdown.
- `docs/solutions/`: Reference implementations for various workshops and tasks.
- `platformio.ini`: Configuration for building with PlatformIO.
- `mbed_app.json`: Configuration for Mbed OS (baud rate, stack size, components).

## Building and Running

### PlatformIO (Recommended for CLI)
- **Build:** `pio run`
- **Upload:** `pio run --target upload`
- **Monitor:** `pio device monitor -b 115200`

### Mbed Studio
- **Build:** Use the **Hammer** icon.
- **Flash:** Use the **Play** icon.

### Manual Flashing
1. Build the project to generate a `.bin` file (usually in `BUILD/NUCLEO_F446RE/ARMC6/`).
2. Drag and drop the `.bin` file onto the Nucleo drive (e.g., `NODE_F446RE`) that appears when connected via USB.

## Development Conventions

### Code Structure
- **Periodic Loop:** `main()` typically initializes objects and then enters a `while(true)` loop that uses a `Timer` and `thread_sleep_for` to maintain a constant execution frequency.
- **User Interaction:** The blue **USER BUTTON** (mapped to `BUTTON1` or `PC_13`) is frequently used to toggle a `do_execute_main_task` flag.
- **Serial Output:** `printf` is configured to use the ST-Link serial port at **115200 baud**.

### Hardware Safety
- **Power:** Turn the PES Board **OFF** before changing hardware connections.
- **Batteries:** Always have battery packs connected when using the charger; the charger is NOT a power supply.
- **Pin Mapping:** Always include `PESBoardPinMap.h` and use the defined constants (e.g., `PB_PWM_M1`, `PB_A0`) instead of raw pin names to ensure compatibility across board versions.

### Style Guide
- Markdown links in `docs/` should have all words capitalized (e.g., `[Course Setup]`).
- Source files are bold-italic (e.g., ***main.cpp***).
- Pins and buttons are bold (e.g., **PB_9**, **USER BUTTON**).
- Functions and variables use backticks (e.g., ``main()``, ``enable_motors``).

## Key Files for Reference
- `include/PESBoardPinMap.h`: Hardware pin definitions.
- `src/main.cpp`: Template/current implementation.
- `platformio.ini`: Build configuration.
- `docs/markdown/tips.md`: General development and programming advice.
- `docs/markdown/course_setup.md`: Environment setup details.
