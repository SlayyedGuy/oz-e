# OZ Hardware Module

## About

The OZ Hardware Module complements the OZ Shell Script by providing fan speed control capabilities based on real-time
temperature readings. This module enables you to efficiently manage temperatures and fan speeds for optimal system performance and reliability.

To build and upload OZ, you will use one of these tools:

- Arduino IDE
- VSCode with PlatformIO

OZ is optimized to build with the PlatformIO IDE extension for Visual Studio Code. You can also build OZ using the Arduino IDE.

### Supported Boards

The following boards are currently supported by OZ:

- Arduino Uno
- Arduino Nano
- Arduino Mega
- ESP32
- ESP8266
- ...

## Quick Start using PlatformIO

1. Clone the OZ repository to your local machine.
2. Using [VSCode](https://code.visualstudio.com/download) and [PlatformIO](https://platformio.org/install/ide?install=vscode) import `platformio.ini` project file.
3. Open PlatformIO.
4. Choose your board in project configuration under "Generic Options" Default is set to `wemos_d1_mini32`.
5. Edit the `config.h` file to configure OZ firmware. Adjust fan ports, initial fan speed, minimum fan speed, and temperature sensor settings as needed.
6. Connect the OZ Hardware Module (Arduino/ESP) to your computer via USB.
7. Ensure that the necessary Arduino serial drivers (FTDI, cp210x..) are installed, if required by your operating system.
8. Click PlatformIO: upload arrow or click `Project Tasks/General/Upload` button in the side platformIO menu.
9. Run [OZ.sh](https://github.com/IxiAngel/OZ/blob/main/src/linux/OZ.sh) after reading the OZ Shell Script [Readme](https://github.com/IxiAngel/OZ/blob/main/src/linux/README.md).

If you prefer to build and upload OZ using [Arduino IDE](https://www.arduino.cc/en/software):

1. Clone the OZ repository to your local machine.
2. Navigate to the `arduino/OZ` directory.
3. Open the `OZ.ino` file with Arduino Studio.
4. Edit the `config.h` file to configure OZ firmware. Adjust fan ports, initial fan speed, minimum fan speed, and temperature sensor settings as needed.
5. Add OneWire and DallasTemperature libraries.
6. Select the correct board and port.
7. Press `Verify/Compile` or `Upload` to the board.
8. Connect the OZ Hardware Module (Arduino/ESP) to your computer via USB.
9. Run [OZ.sh](https://github.com/IxiAngel/OZ/blob/main/src/linux/OZ.sh) after reading the OZ Shell Script [Readme](https://github.com/IxiAngel/OZ/blob/main/src/linux/README.md).

## Protocol and Interface

The OZ Hardware Module communicates with the system using a serial interface. It accepts commands in a specific format to adjust
fan speeds based on temperature readings received from the system.

### Command Format

```
{command,parameter1,parameter2,...}
```

### Commands

- `{0,fanIndex,fanSpeed}`: Sets speed of a single fan by fan index.
- `{1,fanBits=fanSpeed,...}`: Sets speed of multiple fans by fan bit index.
- `{2}`: Returns temperature from the temperature sensor.
- `{setConfig,optionName,value}`: Sets configuration option (tempSensorPin, tempSensorMaxTemp, tempSensorMaxTempFanSpeed, minFanSpeed).
- `{reset}`: Resets the fan controller.

Example:

```
{1,3=75}
```

This command sets the fan speed of the fans associated with the bit pattern `3` (first two fans) to 75%.

## Different Hardware Examples

OZ Hardware Module can be adapted to various hardware configurations and interfaces. Here are some examples:
![](/Schematics/OZ_Circuit_Schematic.png)

### Example 1: Arduino-based Module

- **Hardware**: Arduino Uno
- **Interface**: USB Serial
- **Components**: PWM-compatible fans, temperature probe (optional)
- **Configuration**: Upload the provided firmware to the Arduino Uno board.
- **Usage**: Connect fans and temperature probe to the Arduino, and control fan speeds using the serial interface. See [Schematic](OZ_Circuit_Schematic.png).

### Example 2: ESP32 HAT

- **Hardware**: ESP32/ESP-01
- **Interface**: USB Serial
- **Components**: PWM-compatible fans, temperature probe (optional)
- **Configuration**: Upload the provided firmware to the ESP board.
- **Usage**: Connect fans and temperature probe to the ESP, and control fan speeds using the serial interface.

### Example 3: OZ PCB HAT

- **Hardware**: Custom PCB with hat for Arduino/ESP
- **Interface**: USB Serial
- **Components**: PWM-compatible fans, temperature probe (optional)
- **Configuration**: Download and manufacture the PCB via JLC-PCB or similar, program the microcontroller.
- **Usage**: Connect fans, power, and temperature probe to the custom PCB HAT with Arduino or ESP32.


## Safety Considerations

**!!! WARNING: You are using this software at your own risk. Improperly configured or wired fan controller modules can damage your
hardware. Setting fan speeds too low can lead to overheating, which can also cause damage to your hardware. !!!**

To ensure safe operation:

- Ensure that the fan controller module is correctly connected and configured to avoid damaging hardware due to inadequate cooling.
- Use CAUTION when defining fan speed curves and temperature thresholds to prevent overheating and oscillations.
- Follow the safety principles or there will be problems!

## Contributions

Contributions to OZ are welcome!
Whether you're a seasoned developer or a newcomer, we appreciate all contributions that help improve OZ for the community.

## Support

For any questions, issues, or feedback, please open an issue on GitHub.

---
Copyright (c) 2024 ARSARK Developers
