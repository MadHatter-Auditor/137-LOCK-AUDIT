# Intelligent Cooling System Optimization with 137-LOCK Formulas

This project provides an **intelligent cooling system** for computers and other hardware. It uses mathematical formulas based on **137-LOCK principles** to monitor system temperatures and dynamically adjust fan speeds, ensuring efficient cooling while preventing overheating and maximizing hardware performance.

## Table of Contents

1. [Project Overview](#project-overview)
2. [Features](#features)
3. [How It Works](#how-it-works)
4. [Installation & Setup](#installation-setup)
5. [Usage](#usage)
6. [Future Improvements](#future-improvements)
7. [License](#license)

## Project Overview

This intelligent cooling system dynamically adjusts the cooling behavior of computers and hardware systems based on temperature readings. The system uses **thermodynamic formulas** and **feedback loops** from the 137-LOCK project to control fan speeds, ensuring that the system stays cool without excessive energy use.

The cooling system can be easily adapted for various hardware configurations, and it's designed to be **modular** for future extensions and improvements.

## Features

- **Real-time temperature monitoring**: Continuously measures the CPU/GPU temperatures.
- **Dynamic fan speed control**: Adjusts fan speed based on the system's temperature.
- **Expandable architecture**: Easily adaptable for future improvements (e.g., machine learning, multiple fans, integration with other software).
- **Energy-efficient**: Helps prevent unnecessary energy consumption by dynamically adjusting cooling.

## How It Works

1. **Temperature Measurement**: The system continuously measures the temperature of CPU/GPU using system sensors.
2. **Fan Speed Control**: When the temperature exceeds a threshold, the system increases the fan speed. If the temperature falls below the safe limit, the system reduces fan speed.
3. **Feedback Loop**: The system adjusts fan speeds dynamically, constantly monitoring the temperature and making real-time adjustments.

### Key Formula:
To determine fan speed based on temperature:


fan_speed = (T_i - T_env) * constant_factor


Where:
- **T_i** is the current temperature of the hardware.
- **T_env** is the environmental or reference temperature.
- **constant_factor** is an adjustable factor to set the responsiveness of fan speed.

## Installation & Setup

### Prerequisites

Before starting, ensure you have the following installed:
- **Python 3.x** (Download from [python.org](https://www.python.org/))
- **psutil** library (used for retrieving system temperature data)

### Install Dependencies:
To install the required Python dependencies, run the following command:

```bash
pip install psutil
Clone the Repository:

Next, clone the repository to your local machine:

git clone https://github.com/your-username/your-repo-name.git
cd your-repo-name

This will download the project files to your system.

Usage

Once everything is set up, you can start the cooling system by running the script:

python cooling_system.py

This script will automatically monitor the CPU/GPU temperature and adjust the fan speed accordingly.

Example Output:
CPU Temperature: 75°C -> Increase fan speed to 90%
GPU Temperature: 80°C -> Increase fan speed to 95%
Future Improvements
Self-Learning Algorithms: Implement machine learning to adapt the cooling strategy based on usage patterns, optimizing fan speed and cooling strategies over time.
Multiple Fan Control: For larger systems, support individual fan control for better cooling efficiency.
Integration with Cooling Software: Integrate with tools like MSI Afterburner or SpeedFan to control more advanced cooling mechanisms.
License

This project is licensed under the MIT License - see the LICENSE
 file for details.
