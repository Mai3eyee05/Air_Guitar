# 🎸 Air Guitar

An Arduino-based **gesture-controlled musical instrument** that uses an IMU to detect the orientation of a handheld controller and maps its movement along the **X–Y plane to eight different musical chords**.

## Overview

The Air Guitar project explores how motion sensing can be used as an alternative musical interface.

An **MPU6050 IMU** is used to measure the orientation and motion of the controller. The Arduino reads the sensor data and communicates it to a computer over serial communication. A Python program processes the received data, identifies the controller's position within the defined **X–Y regions**, and generates the corresponding chord in real time.

The final implementation divides the X–Y plane into **8 regions**, with each region corresponding to a different chord.

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
                │ Controller  │
                └──────┬──────┘
                       │
                  Serial Data
                       │
                       ↓
                ┌─────────────┐
                │    Python   │
                │ Gesture &   │
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
| Arduino          | Reads the IMU and sends sensor data        |
| MPU6050          | Measures acceleration and angular velocity |
| HW-290           | Hardware interface used in the setup       |
| HW-104 Amplifier | Amplifies the audio output                 |
| Speaker          | Produces the final sound                   |

## Software

* **Arduino / C++** — IMU interfacing and serial communication
* **Python** — gesture processing and audio generation
* **sounddevice** — real-time audio output
* **PySerial** — communication between Arduino and Python

## How It Works

### 1. Motion Sensing

The MPU6050 measures:

* Acceleration along the **X, Y and Z axes**
* Angular velocity about the **X, Y and Z axes**

The sensor communicates with the Arduino using the **I²C protocol**.

### 2. Orientation Detection

The Arduino reads the IMU measurements and sends the relevant sensor values to the computer through the serial interface.

The motion data is used to determine the controller's orientation in the **X–Y plane**.

### 3. X–Y Chord Mapping

The controller's X–Y orientation is divided into **8 regions**.

Each region corresponds to a different musical chord:

```text
                 Y
                 ↑
          ┌──────┬──────┐
          │      │      │
          │      │      │
      ────┼──────┼──────┼────→ X
          │      │      │
          │      │      │
          └──────┴──────┘

             8 chord regions
```

The detected region determines which chord is played.

This allows the user to control the chord progression simply by changing the orientation of the controller.

### 4. Audio Generation

The Python program receives the sensor/control data from the Arduino through the serial port.

Based on the detected X–Y region, the program selects the corresponding chord and generates the audio using `sounddevice`.

The audio is then sent to the output hardware.

## Chord Mapping

The final implementation uses **8 different chords**, mapped to different regions of the X–Y plane.

| Region   | Chord   |
| -------- | ------- |
| Region 1 | Chord 1 |
| Region 2 | Chord 2 |
| Region 3 | Chord 3 |
| Region 4 | Chord 4 |
| Region 5 | Chord 5 |
| Region 6 | Chord 6 |
| Region 7 | Chord 7 |
| Region 8 | Chord 8 |

> The exact chord mapping can be found in the Python implementation.

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
├── media/
│   ├── setup.jpg
│   └── demo.mp4
│
└── README.md
```

## Setup

### Arduino

1. Connect the MPU6050 to the Arduino using I²C.
2. Upload the Arduino sketch from the `Arduino/` directory.
3. Connect the Arduino to the computer through USB.
4. Identify the serial port assigned to the Arduino.

### Python

Install the required packages:

```bash
pip install pyserial sounddevice
```

Update the serial port in the Python script if required:

```python
PORT = "COM6"
```

Run the program:

```bash
python air_guitar.py
```

Move the controller through the defined X–Y regions to switch between the eight chords.

## Key Concepts

This project involved:

* **IMU-based motion sensing**
* **Accelerometer and gyroscope data**
* **I²C communication**
* **Arduino-based embedded systems**
* **Serial communication**
* **X–Y gesture/region mapping**
* **Python hardware interfacing**
* **Real-time audio generation**

## Future Improvements

Possible extensions include:

* Adding more chords and notes
* Detecting **strumming gestures** separately from chord selection
* Implementing sensor fusion for more robust orientation estimation
* Adding different instrument sounds
* Improving gesture classification and reducing accidental chord changes
* Making the system completely standalone without requiring a computer

## Author

**Maitreyee Gedam**
Engineering Physics, IIT Bombay
