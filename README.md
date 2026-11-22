# CUBESAT-TELEMETRY-SIMULATOR-USING-ARDUINO-UNO
Arduino-only CubeSat telemetry simulator. A satellite Arduino reads an LM35 temperature sensor and sends checksummed packets to a ground-station Arduino, which verifies them and shows live temperature, packet count and errors on a 16x2 LCD. Includes signal-loss alert. No Python or LoRa needed.

A low-cost simulation of a CubeSat telemetry downlink built with two Arduino boards. The "satellite" Arduino measures temperature with an LM35 sensor and transmits it as a checksummed data packet every second. The "ground station" Arduino receives the packet, verifies its integrity, and displays the live telemetry on a 16x2 LCD.

The project demonstrates the core ideas of satellite telemetry: onboard sensing, packet formatting, data transmission, error detection, and ground-station monitoring. It uses no Python and no radio module; a wired serial link stands in for the radio link.

## Features
- Real-time temperature sensing with the LM35 (0.1 °C resolution)
- Custom telemetry packet: `$CUBESAT,<seq>,<temp_x10>*<checksum>`
- XOR checksum for detecting corrupted packets
- Packet sequence numbers and error counter
- Live LCD display of temperature, packet number and error count
- "Signal lost" alert when no valid packet arrives for 3 seconds
- Serial Monitor output for debugging on both boards

## Hardware
- 2 x Arduino Uno/Nano
- LM35 temperature sensor
- 16x2 LCD (HD44780, no I2C)
- 10k potentiometer, 220 ohm resistor, breadboard, jumper wires

## How It Works
1. The satellite Arduino reads the LM35 on A0, averages 10 samples, and converts the result to degrees Celsius.
2. It builds a packet with a sequence number, temperature and XOR checksum, and sends it over SoftwareSerial at 9600 baud.
3. The ground station Arduino reads the packet, recomputes the checksum, and rejects it if it doesn't match.
4. Valid data is shown on the LCD and printed to the Serial Monitor.

## Future Work
Additional sensors (light, battery voltage), LCD pages, buzzer alarm, mission elapsed time, and SD card logging.
