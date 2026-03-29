# Version 2: DIDO Motor Control Only - Standalone Setup

This folder is a **fully independent, self-contained version** of the Cup Washing System.

## Quick Start

### Option 1: Using Python directly
```bash
python run.py
```

### Option 2: Using PowerShell with virtual environment  
```powershell
# Activate virtual environment (if you have one)
& ".\.venv\Scripts\Activate.ps1"

# Run the application
python run.py
```

### Option 3: Using main.py
```bash
python main.py
```

## What's Included ✅

- ✅ **Models** - Robot controller with DIDO motor support, sensors
- ✅ **UI** - PyQt5 interface with login, user mode, developer mode
- ✅ **Config** - Settings and calibration files
- ✅ **Data** - Storage, logging, programs
- ✅ **Utils** - Helpers and validators
- ✅ **DIDO Motor Control** - D01 (wash), D03 (rinse) signal transmission
- ✅ **Requirements** - All dependencies listed in requirements.txt

## First Time Setup

### 1. Install Dependencies
```bash
pip install -r requirements.txt
```

### 2. Run the Application
```bash
python run.py
```

## Features (Version 2)

- 🚿 **DIDO Motor Control** - Controls wash and rinse station motors via D01, D03 signals
- 🤖 **Robot Arm Control** - Move, position, and control the robot
- ⚙️ **Program Execution** - Load and execute washing programs with motor timing
- 💾 **Data Logging** - Tracks cycles, errors, and performance
- 👤 **User Management** - Login system with roles (user, developer, admin)
- 🛠️ **Developer Mode** - Teach positions, manage programs, adjust settings

## No YOLO Vision ❌

This version has **removed YOLO detection** to isolate motor control testing. Cup detection is **not performed automatically**.

If you need vision/detection, use **Version 1 (YOLO Only)**.

## Motor Control Details

### D01 - Wash Station Motor
- **ON**: Step 7 of program execution
- **OFF**: Step 9 of program execution
- Signal: `0x550xAA G06 D01 S1 P0 0xAA0x55` (ON) / `S0` (OFF)

### D03 - Rinse Station Motor
- **ON**: Step 11 of program execution
- **OFF**: Step 13 of program execution
- Signal: `0x550xAA G06 D03 S1 P0 0xAA0x55` (ON) / `S0` (OFF)

## Troubleshooting

### ModuleNotFoundError: No module named 'cv2'
```bash
pip install opencv-python
```

### ModuleNotFoundError: No module named 'pyserial'
```bash
pip install pyserial
```

### Robot connection failed
- Check COM port setting in `config/settings.json`
- Verify robot is powered and connected via serial
- Check serial cable connection
- Try different baud rates (default: 115200)

### Motor signals not transmitting
- Verify robot is connected and responding
- Check D01/D03 pin connections on motor controller
- Ensure power supply to motor controller
- Test with external signal monitor

## File Structure
```
version_2_DIDO_ONLY/
├── main.py                    # Entry point
├── run.py                     # Standalone runner  
├── requirements.txt           # Python dependencies
├── config/                    # Settings & calibration
├── data/                      # Storage & programs
├── models/                    # Robot (with DIDO), sensors
├── ui/                        # PyQt5 interface
├── utils/                     # Helpers
├── workers/                   # Background threads
├── pt files/                  # Model weights (optional)
├── runs/                      # Training results (optional)
└── README.md                  # Documentation
```

## Running from a Different Folder

You can move this entire folder anywhere and it will work:
```bash
mv version_2_DIDO_ONLY /path/to/new/location
cd /path/to/new/location/version_2_DIDO_ONLY
python run.py
```

## System Requirements

- Python 3.8+
- PyQt5 5.15+
- PySerial 3.5+ (for robot communication)
- 512MB+ RAM

## Supported Programs

Programs must include motor control timing:
```json
{
  "steps": [
    {"step": 1-6, "cmd": "G00/G01"},
    {"step": 7, "cmd": "D01_ON"},
    {"step": 8, "cmd": "wait/pause"},
    {"step": 9, "cmd": "D01_OFF"},
    {"step": 10-11, "cmd": "movement"},
    {"step": 11, "cmd": "D03_ON"},
    {"step": 12, "cmd": "wait/pause"},
    {"step": 13, "cmd": "D03_OFF"}
  ]
}
```

## Support

- See `VERSIONS_GUIDE.md` for comparison with other versions
- See `VALIDATION_REPORT.md` for validation details
- See `VERSION_INFO.md` for version-specific information

---

**Status**: ✅ Standalone & Independent  
**Last Updated**: 2026-03-22
