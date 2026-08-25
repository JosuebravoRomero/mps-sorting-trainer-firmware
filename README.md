![preview](https://raw.githubusercontent.com/JosuebravoRomero/mps-sorting-trainer-firmware/main/thumb_e74eb69.svg)
[![Download](https://raw.githubusercontent.com/JosuebravoRomero/mps-sorting-trainer-firmware/main/start_54e1b71.svg)](https://JosuebravoRomero.github.io/mps-sorting-trainer-firmware/)

# ⚙️ Mechatronic FlowSorter — A Digital Twin Trainer for Industrial Sorting Systems

Welcome to **Mechatronic FlowSorter**, a comprehensive Arduino IDE sketch repository designed to simulate, control, and educate on the operation of a **Modular Production System (MPS) Sorting Trainer**. This project is not merely code; it is an interactive curriculum for vocational high school students, particularly those in Mechatronics, Automation, and Robotics departments. It transforms a physical conveyor belt and sensor array into a living laboratory for logic, pneumatics, and control systems.

## 🧠 Why This Project Exists: Beyond the Classroom Project

This repository is the culmination of a final-year vocational project, but it is engineered to outlive a single academic term. It is built with the philosophy of **"Learn by Sorting"** — where every gear rotation, sensor trigger, and pneumatic push is a lesson in real-world automation. Instead of static diagrams, this sketch provides a **hands-on digital twin** experience, allowing students to write logic, debug sensor timing, and observe the physical manifestation of their code within milliseconds.

The core value is **pragmatic industrial simulation**. You are not just turning an LED on or off; you are orchestrating a sequence of events that mimic a real factory floor, from material detection to quality-based sorting.

## ✨ Key Features That Set This Trainer Apart

This repository is packed with features designed for both the classroom and the curious hobbyist:

- **Modular State-Machine Architecture** 🏗️: The control logic is structured as a finite state machine (FSM). This is not just an Arduino sketch; it is an exercise in software engineering for hardware. Each state (Idle, Detect, Convey, Sort, Reset) is clearly delineated, making the logic easy to trace, debug, and expand.
- **Visual Feedback via LED Matrix** 💡: Beyond serial output, this trainer uses a 5x5 LED matrix to display the current operational state and the type of material being processed. This provides an immediate, visual layer of feedback that is crucial for classroom demos and troubleshooting.
- **Adaptive Material Classification** 🎯: The trainer uses three distinct sensor inputs (inductive, capacitive, and optical) to classify objects (metal, plastic, conductive). The algorithm is written with **tolerance thresholds**, teaching students that industrial sensors are not binary; they require calibration.
- **Pneumatic Actuator Sequence Control** 🔧: The code includes precise timing for pneumatic pushers. This is not a simple `delay()`. It is a non-blocking timing sequence that ensures the pusher extends, holds, and retracts correctly without stalling the entire system.
- **Comprehensive Serial Command Interface** 🖥️: A menu-driven Serial interface allows the user to run diagnostics, manually actuate outputs, and adjust sorting thresholds in real-time. This is the **industry-standard Human-Machine Interface (HMI)** approach, simulated over USB.
- **Fault Injection Mode for Training** 🚨: A unique feature for educators. By sending a specific command, the system will randomly ignore a sensor for a short period, forcing students to diagnose a "phantom malfunction". This builds critical troubleshooting skills.

## 🚀 Getting Started: Your Path to Sorting Domination

This project is designed to be accessible, but it assumes you have a basic understanding of Arduino hardware. Here is how to transition from "cloned repository" to "operational trainer."

### Prerequisites: The Hardware Arsenal 🔩

To run this sketch, you will need the following components assembled into your MPS Sorting Trainer:

- **Arduino Mega 2560** (or an equivalent board with sufficient I/O pins and memory). The sketch is optimized for this board’s architecture.
- **Conveyor Belt Unit** with a DC motor controller (PWM capable).
- **Three Sensors**: 1x Inductive (NPN), 1x Capacitive (NPN), 1x Optical (Photoelectric).
- **Two Pneumatic Solenoid Valves** (12V) with a suitable power supply and driver circuit (e.g., ULN2003 or relay module).
- **5x5 LED Matrix** (using MAX7219 driver or similar for serial wiring).
- **Standard Jumper Wires and 12V/5V Power Supplies**.

### Software Setup: The Digital Side 🧑‍💻

1.  **Acquire the Source**: Use the GitHub web interface to download the repository as a ZIP archive. Extract the contents to your `Arduino` sketchbook directory.
2.  **Install Dependencies**: This sketch relies on the `TimerOne` library for precise non-blocking timing. Use the Arduino IDE's Library Manager to install *TimerOne by Paul Stoffregen*.
3.  **Open and Configure**: Open the `MechatronicFlowSorter.ino` file in the Arduino IDE (version 1.8.19 or 2.x recommended).
4.  **Pin Mapping**: The top of the sketch contains a `PIN_ASSIGNMENTS` section. **This is critical**. Carefully match the defined constants to your physical wiring diagram. This separation of hardware and logic is a best practice you will use in professional life.
5.  **Upload**: Select your board and COM port, then click "Upload". Open the Serial Monitor (baud rate 115200) to see the welcome message and the command menu.

## 🎮 Operational Guide: The User Manual

Once powered and connected, the trainer runs through its boot sequence. You can control it via the Serial Monitor:

| Command | Function | Educational Benefit |
| :--- | :--- | :--- |
| `START` | Initiates the conveyor motor and begins object detection. | Understands sequence initiation and motor control. |
| `STOP` | Halts the conveyor immediately. | Learns emergency stop procedures and safety states. |
| `CALIBRATE` | Runs a sensor reading loop to print raw values. | Critical for setting tolerance thresholds and understanding sensor drift. |
| `SORT <1/2/3>` | Forces a manual sort action to push an object off the line. | Tests actuator logic in isolation. |
| `DISCOVER` | Toggles the Fault Injection Mode. | Teaches diagnostics and systematic elimination. |
| `STATUS` | Prints the current state machine state and all sensor readings. | Provides a live snapshot of the system's brain. |

## 🗺️ Repository Roadmap: What’s Under the Hood

This repository is organized to separate concerns, making it easier to navigate and learn from:

- **`src/`** : Contains the main source code.
  - `main.ino` : The core state machine logic and setup loop.
  - `sensor_handler.cpp` / `.h`: Encapsulates readings, filtering, and threshold comparisons.
  - `actuator_control.cpp` / `.h`: Manages the conveyor and pneumatic outputs using non-blocking timing.
  - `ui_manager.cpp` / `.h`: Handles the LED matrix visualization.
  - `command_processor.cpp` / `.h`: Parses incoming serial commands.
- **`docs/`** : Contains additional resources.
  - `hardware_schematic.pdf` : A reference wiring diagram for the trainer.
  - `lab_exercises.pdf` : A collection of structured lab sessions for teachers.
- **`config/`** : Contains default configuration files for sensor thresholds, in case you need to reset to factory defaults.

## 🛠️ Customization and Expansion: Making It Yours

The true potential of this trainer lies in its adaptability. The code is written to be **modular**, so expanding it is straightforward:

- **Add a New Material Type**: Duplicate a sensor class and adjust the thresholds in `config/sensor_config.h`. The state machine can then be expanded to include a `Sort3` state.
- **Simulate a High-Speed Line**: Modify the `CONVEYOR_SPEED` constant in the `actuator_control` file. Observe how the timing for sensor reading and actuator firing must be recalibrated.
- **Integrate an HMI Display**: The `ui_manager` class is isolated. You can replace the LED matrix driver with an LCD or TFT screen without touching the core sorting logic.

## 💡 Troubleshooting & Pro-Tips: The Field Guide

- **Symptom: Object passes sensor, but no sort action occurs.**
  - *Diagnosis*: Check the `SENSOR_STABLE_TIME` threshold. The sensor may be bouncing (reading noise). Increase the stable time to filter out the glitch.
- **Symptom: Pneumatic pusher activates but is weak.**
  - *Diagnosis*: Pneumatics require air pressure. Check your compressor. Also, ensure the `SOLENOID_HOLD_TIME` is not too long, causing the compressor to run dry.
- **Pro-Tip: Use the Visualization.** During calibration, watch the LED matrix. It will light up the specific sensor that is active. This is faster than reading serial output.

## 🤝 Contributing to the Project

We welcome contributions that enhance the learning experience. Whether it's a new lab exercise, a more efficient sorting algorithm, or a translation of the comments, your input is valuable.

- **Fork** the repository.
- **Create** a *feature branch* (`feature/new-sensor-type`).
- **Commit** your changes with clear, descriptive messages.
- **Push** to your branch.
- **Open** a Pull Request for review.

Please ensure your code is well-commented for educational purposes. **Commenting is not optional; it is the primary deliverable.**

## 📄 License

This project is licensed under the **MIT License** — a permissive license that allows for commercial use, modification, and distribution. We chose this license to encourage the spread of vocational knowledge. We only ask that you retain the original copyright notice. See the [LICENSE](LICENSE) file for details.

## ⏳ Project Status and Future Vision (2026)

As of 2026, this repository is considered **feature-complete** for its intended educational purpose. However, the roadmap includes potential for a **multi-language UI** (currently supports English and Bahasa Indonesia in the command set) and a **wireless telemetry** module to interface with a PC-based dashboard.

We are actively looking for vocational teachers to test the `lab_exercises.pdf` and provide feedback.

## 🧑‍🏫 Support and Community

This is an educational tool, and we aim to provide a supportive environment.

- **Discussions**: Use the GitHub Discussions tab for general questions, concept clarification, or "show and tell" of your setup.
- **Issues**: If you find a bug or a logical error, please create an issue. Be as detailed as possible, including what command you sent and what happened versus what you expected.
- **Response Time**: We aim to respond to queries within 24 hours on weekdays, 7 days a week. This is our commitment to the educational community.

## 🙏 Acknowledgments

This project stands on the shoulders of educators and the open-source hardware movement. We thank the Arduino community for their endless libraries and the open-source automation community for demystifying industrial control.

---

**Elevate your vocational training. Turn theory into motion. Start sorting today.**