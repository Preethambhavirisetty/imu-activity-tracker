# 🧭 Smart IMU Orientation & Activity Tracker

![Python](https://img.shields.io/badge/Python-3.10+-3776AB?logo=python&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-013243?logo=numpy&logoColor=white)
![Matplotlib](https://img.shields.io/badge/Matplotlib-11557c)
![Ruff](https://img.shields.io/badge/lint-ruff-D7FF64)
![mypy](https://img.shields.io/badge/types-mypy_strict-2A6DB2)

Turns raw accelerometer and gyroscope data into real-time orientation and activity labels. Works with a simulated stream or a microcontroller (MPU6050 / LSM6DSOX) over serial.

## Features
- Raw accel/gyro ingestion from a simulated source or a serial CSV stream
- Low-pass and high-pass filtering
- Madgwick sensor fusion for orientation
- Activity detection: idle, walking, running, falling, gestures
- Live 3D orientation view with Matplotlib
- `imu-tracker` CLI; pytest tests; ruff + strict mypy config

## Screenshot
<!-- Add a GIF of the 3D visualization: docs/demo.gif -->
![Demo](docs/demo.gif)

## Tech stack
Python 3.10+ · NumPy · Matplotlib · pyserial · pytest · ruff · mypy

## Project structure
```
.
├── src/imu_tracker/
│   ├── cli.py, __main__.py   # imu-tracker CLI
│   ├── sources.py            # simulated + serial sources
│   ├── filters.py            # low/high-pass filters
│   ├── fusion.py             # Madgwick filter
│   ├── activity.py           # activity detection
│   ├── pipeline.py, models.py, config.py
│   └── visualization.py      # 3D orientation plot
├── examples/sample_serial_format.csv
├── tests/                    # test_activity, test_filters, test_fusion
└── pyproject.toml
```

## Getting started
```bash
git clone https://github.com/Preethambhavirisetty/imu-activity-tracker.git
cd imu-activity-tracker
python3 -m venv .venv && source .venv/bin/activate
pip install -e ".[dev]"

imu-tracker simulate --duration 20 --visualize   # simulated, with 3D view
imu-tracker simulate --duration 10               # print-only
imu-tracker serial --port /dev/tty.usbmodem1101 --baud 115200 --visualize
```
Serial format: `timestamp,accel_x,accel_y,accel_z,gyro_x,gyro_y,gyro_z` (accel in g, gyro in deg/s).

### Dev
```bash
pytest
ruff check src tests
mypy src
```

## Environment variables
None.

## Contributing
1. Fork the repo and create a branch: `git checkout -b feature/your-change`
2. Commit using [Conventional Commits](https://www.conventionalcommits.org/) (`feat: …`, `fix: …`)
3. Push and open a pull request against `main`

## License
No license file yet. Add one (MIT is a common choice) via **Add file → Create new file → `LICENSE` → Choose a license template**, then update this section.

> Tip: set `authors` in `pyproject.toml` to your name (it currently says "IMU Tracker").
