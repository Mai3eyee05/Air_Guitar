# Air_Guitar
# 🎸 Air Guitar

An Arduino-based **gesture-controlled musical instrument** that uses an IMU to detect hand movements and orientation, translating them into musical chords and audio output in real time.

## Overview

The Air Guitar project turns physical hand movements into musical input without requiring a physical guitar.

An **MPU6050 IMU** mounted on the controller captures motion and orientation data. The Arduino processes the sensor readings and communicates the detected gesture/state to a computer over serial communication. A Python program then maps the input to musical chords and generates the corresponding audio.

The system supports four chords:

**C · G · Am · F**

## System Architecture

```text
        Hand Movement
              ↓
        ┌─────────────┐
        │   MPU6050   │
        │     IMU     │
        └──────┬──────┘
               │ I²C
               ↓
        ┌─────────────┐
        │   Arduino   │
        │  Controller │
        └──────┬──────┘
               │ Serial
               ↓
        ┌─────────────┐
        │    Python   │
        │ Audio Logic │
        └──────┬──────┘
               │
               ↓
        ┌─────────────┐
        │    Audio    │
        │   Output    │
        └─────────────┘
```

## Hardware

| Component        | Purpose                                    |
| ---------------- | ------------------------------------------ |
| Arduino          | Reads the IMU and sends motion data        |
| MPU6050          | Measures acceleration and angular velocity |
| HW-290           | Used as part of the hardware interface     |
| HW-104 Amplifier | Amplifies the audio signal                 |
| Speaker          | Produces the final audio output            |

## Software

* **Arduino / C++** — sensor interfacing and serial communication
* **Python** — gesture processing and audio generation
* **sounddevice** — real-time audio output
* **Serial communication** — transfers sensor/control data from Arduino to Python

## How It Works

### 1. Motion Sensing

The MPU6050 measures:

* Linear acceleration along the X, Y and Z axes
* Angular velocity about the X, Y and Z axes

The sensor communicates with the Arduino using the **I²C protocol**.

### 2. Motion Data Processing

The Arduino reads the IMU measurements and sends the relevant values through the serial interface.

These measurements are used to determine the current orientation/movement of the controller.

### 3. Chord Mapping

The detected state is mapped to one of four predefined chords:

| Input Region / Gesture | Chord |
| ---------------------- | ----- |
| Region 1               | C     |
| Region 2               | G     |
| Region 3               | Am    |
| Region 4               | F     |

This allows the user to change chords by moving the controller through different regions.

### 4. Audio Generation

The Python program receives the control data from the Arduino through the serial port and generates the corresponding audio using `sounddevice`.

The audio is then sent to the output hardware.

## Repository Structure

```text
Air-Guitar/
│
├── Arduino/
│   └── air_guitar.ino
│
├── Python/
│   └── air_guitar.py
│
├── README.md
│
└── media/
    └── ...
```

## Setup

### Arduino

1. Connect the MPU6050 to the Arduino using I²C.
2. Upload the Arduino sketch from the `Arduino/` directory.
3. Connect the Arduino to the computer through USB.
4. Note the serial port assigned to the Arduino.

### Python

Install the required Python packages:

```bash
pip install pyserial sounddevice
```

Update the serial port in the Python script if necessary:

```python
PORT = "COM6"
```

Then run:

```bash
python air_guitar.py
```

Move the controller to change between the four chord regions and generate the corresponding audio.

## Key Concepts

This project involved working with:

* **IMU-based motion sensing**
* **Accelerometers and gyroscopes**
* **I²C communication**
* **Arduino-based embedded systems**
* **Serial communication**
* **Python hardware interfacing**
* **Real-time audio generation**
* **Gesture-based control**

## Future Improvements

Some possible extensions include:

* Adding more chords and notes
* Implementing strumming detection using acceleration/gyroscope data
* Using sensor fusion for more accurate orientation estimation
* Adding different instrument sounds
* Improving gesture recognition and reducing accidental chord changes
* Making the system completely standalone without requiring a computer

## Author

**Maitreyee Gedam**
Engineering Physics, IIT Bombay
