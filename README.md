# BOSCH — BEA CAN Communication & Diagnostics

An embedded systems practice project using the **STM32F405RGT6**, **CAN/UART** communication, and a **Python/Tkinter** diagnostic tool.

## Project Structure

| Path | Description |
| --- | --- |
| `03_BEA_BasicConfiguredSourceCode/` | STM32 firmware, STM32CubeIDE configuration, HAL/CMSIS drivers, and linker scripts. |
| `01_Diagnostic/BEA2026_Diag_Checker/` | Desktop application for sending and receiving serial data and running diagnostic services. |
| `01_Diagnostic/` | Diagnostic practice documentation and the system topology diagram. |
| `02_Communication/` | CAN communication practice documentation. |
| `BEA_pratical_tool_Installation_guide.docx` | Tool installation guide. |
| `BEA_CAN2CAN_DEMO_TEN1HC_HUST.hex` | Prebuilt HEX firmware included in the original project materials. |

## Features Implemented in the Source Code

- CAN1/CAN2 communication and UART data processing.
- CAN data validation using counters and checksums.
- Diagnostic services: `0x22` (Read Data By Identifier), `0x27` (Security Access), and `0x2E` (Write Data By Identifier).
- Temperature readings, CAN ID readings, and CAN ID change requests.
- A Python interface with COM port and baud rate selection, String/Hex data modes, and TX/RX logging.

This overview is based on the source code. Actual operation must be verified with the appropriate board and CAN/serial hardware.

## Running the Diagnostic Tool on Windows

Requirements: **Python 3.12** with Tcl/Tk support and the driver for your USB-to-serial device.

Open PowerShell in the project root directory:

```powershell
cd 01_Diagnostic/BEA2026_Diag_Checker
py -3.12 -m venv .venv
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
.\.venv\Scripts\python.exe BEA_DiagChecker.py
```

Connect the device and select the correct COM port and baud rate. The firmware currently configures UART at **115200 baud, 8N1**. See the [diagnostic tool README](01_Diagnostic/BEA2026_Diag_Checker/README.md) for more details; absolute drive paths in that document are examples from the original development environment.

### Running the Python Tests

From `01_Diagnostic/BEA2026_Diag_Checker/`:

```powershell
.\.venv\Scripts\python.exe -m pip install pytest
.\.venv\Scripts\python.exe -m pytest
```

The existing tests use simulated serial connections and do not require a physical board.

## Opening and Building the Firmware

1. Install STM32CubeIDE and the required tools/drivers according to the included documentation.
2. Import the existing project from `03_BEA_BasicConfiguredSourceCode/`.
3. Check the **STM32F405RGT6** target, build configuration, and hardware connections.
4. Build the project, then flash the firmware using a tool compatible with the board.

The `.ioc` file is preserved from the original project. Compare its configuration with the current source code before regenerating code. The included HEX file has not been verified as a build of the current source version.

## Files and Licensing

- `.gitignore` excludes build output, Python environments, caches, logs, and temporary Office files.
- Documentation, HEX firmware, and STM32CubeIDE configuration files are retained.
- Existing STMicroelectronics/Arm copyright notices and licenses in `Drivers/` are preserved. This repository does not add a license covering all of its contents.
