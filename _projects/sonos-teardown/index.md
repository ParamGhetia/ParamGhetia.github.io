---
layout: post
title: Portable MP3 Player
description: I designed the full system schematic for a portable MP3 player using an ESP32-WROOM, building the entire system from scratch. This included selecting and connecting components like the VS1053 decoder, TP4056 battery charger, MP1584 buck converter, and an OLED display. I integrated multiple input methods including a rotary encoder, joystick, and tactile switches, and accounted for power regulation, USB-C charging with CC logic, and ESD protection. The design also features an SD card module for storage. All connections, passive components, and protection circuitry were planned out and finalized in a complete schematic using KiCad.
skills: 
  - Schematic Design
  - KiCad

main-image: /3269-04.jpg
---

---
# Schematic
{% include image-gallery.html images="mpschematic.webp" height="400" %}

# Design Highlights

## Safe and Stable Power Regulation 
- A buck converter (MP1584) is used to step down the variable battery voltage (3.0 – 4.2 V) to a clean and regulated 3.3 V supply. This protects sensitive components and ensures reliable operation. Input and output capacitors are placed around the converter to minimize voltage ripple and protect against transient spikes.

## ESD Protection for SD Card and Data Lines
- Electrostatic discharge protection diodes are placed on high-speed I/O lines, particularly around the SPI-connected SD card reader. These protect the ESP32 and other digital components from voltage spikes and accidental static discharges during card insertion or handling.

## Audio Output with Stereo Mixing
- The headphone jack is connected to the VS1053 audio decoder’s stereo output, with left and right channels combined for compatibility with standard 3.5mm headphones (like Apple wired earbuds). This simplifies audio output while retaining clarity and stereo balance.

## Digital Signal Processing on the VS1053 Decoder
- The VS1053 module handles MP3 decoding on-board, converting compressed audio into analog signals. It performs digital-to-analog conversion (DAC) internally and supports features like equalization and soft volume control, offloading this processing from the ESP32.

## Robust Capacitor Network for Noise Suppression
- Decoupling capacitors are placed near all major ICs to ensure local voltage stability and to reduce power line noise. Electrolytic and ceramic capacitors work together to smooth both low and high-frequency disturbances, improving system reliability.

## Modular, Breadboard-Friendly Architecture
- The schematic was designed to be easily tested on a breadboard, with clear separation of subsystems like power, audio, display, and input. All modules were chosen in breadboard-compatible formats before being prepared for PCB layout, ensuring easier debugging and iteration.

## User Interface with Multi-Modal Controls
- Inputs include a rotary encoder, joystick, and several tactile switches. These allow intuitive navigation of playback controls and menus on the OLED display. Button layout and orientation were planned with ergonomic use in mind, including ideas for bumper-style triggers in a future enclosure.

# Specifications
## Microcontroller
- ESP32-WROOM Module – Dual-core Wi-Fi + Bluetooth SoC with GPIO, SPI, I²C

## Audio System
- VS1053B MP3 Audio Decoder – Supports MP3, WAV, OGG playback; SPI interface
  
## Power Management
- TP4056 Li-ion Charger Module (with USB-C input)
- Charging from USB-C VBUS (5 V)
- Integrated charge status LEDs (CHRG/STDBY)
- CE and TEMP pins configured for always-on charging
- MP1584 Buck Converter
- Input: 3.0–4.2 V (from battery)
- Output: 3.3 V regulated for ESP32 and peripherals
- 3.7 V Li-ion Battery
- TP4056 BAT pin
  
## Storage
- MicroSD Card Reader Module (ADA254)
  
## Display
- 1.5-inch Waveshare RGB OLED (128×128)
  
## User Input
- Rotary Encoder Module (SW MEC 5E) – For menu navigation and selection
- 2× 90° Tactile Switches – Side buttons for extra controls
- DS Joystick Module (KY-023) – Analog directional input
  
## Misc.
- ESD7104 ESD Protection Diode Array
- Various Resistors
- Various Capacitors

# Initial Design Requirements
The following requirements were established at the start of the project to guide the schematic and system design for a fully functional, portable MP3 player:

## Core Functionality
1. Must use the ESP32-WROOM microcontroller for audio control, UI handling, and storage access.
2. Must decode and play standard MP3 (and optionally WAV/OGG) audio files using a dedicated decoder.
3. Must provide audio output via a 3.5 mm headphone jack.

## Storage
1. Must store audio files on a microSD card using the SPI interface.
2. The SD module must be directly accessible by the ESP32.

## Power
1. Must be battery-powered via a rechargeable 3.7 V Li-ion cell.
2. Must support USB-C charging using a charger module.
3. Must provide stable, regulated power to ESP32 and peripherals using a buck converter.
4. Must implement basic USB-C compliance using a 5.1 kΩ pull-down resistor on CC pin.
5. Must include some kind of capacitor filtering and basic ESD protection.

## Display & UI
1. Must include a color OLED display for UI and song display.
2. Must provide intuitive physical control inputs:
3. Rotary encoder for navigation
4. Joystick for menu control
5. Ideally, multiple tactile buttons for playback control and power

## Connectors
1. Must include a JST connector for safe battery connection.
2. Must have USB-C power input and headphone output.

## Protection & Stability
1. Must include ESD protection on USB and sensitive IO lines.
2. Must use decoupling capacitors near key ICs and power rails.
3. Must ensure clean power delivery and minimal noise for audio playback.

## Form Factor
1. Should be compact and modular enough to support:
   - Custom PCB layout
   - 3D-printed enclosure design
   - Should expose debug or programming headers (optional but preferred)

# Next Steps
## Finalize PCB Design
1. Convert the complete schematic into a PCB layout.
2. Properly route high-speed and power traces (e.g., between ESP32, VS1053, SD module, and MP1584).
3. Double-check pin alignment, footprint sizes, and clearance.
4. Add silkscreen labels, test points, and mounting holes.
## Order the PCB
1. Export Gerber files from your PCB design tool.
2. Use JLCPCB (or another fab service) to order the boards.
## Assemble and Test
1. Solder through-hole components and connectors.
2. Power the board via USB-C and test charging functionality.
3. Check 3.3 V regulation, audio playback, display output, and user input response.
4. Debug and revise if necessary.
## Design 3D Enclosure
1. Use Fusion 360, FreeCAD, or SolidWorks to design a custom enclosure.
2. Account for component height, button access, headphone jack, charging port, and airflow.
3. Export to STL and 3D print for fit testing.
##Finalize & Iterate
1. Make any needed adjustments to the PCB or case design.
2. Optimize for comfort, usability, and durability.
3. If successful, build a second revision with improvements.


