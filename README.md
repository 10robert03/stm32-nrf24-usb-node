# STM32-nRF24 Wireless USB Node

A compact 2-layer PCB featuring an **STM32C011** microcontroller and an **nRF24L01+** 2.4GHz wireless transceiver. This project was designed to bridge the gap between custom wireless sensor networks and USB-enabled host systems.

**⚠️ Project Status:** This project is currently in the **Hardware Prototype** stage. The PCB layout is complete, but the board has not yet been fully assembled or laboratory tested. Use with caution for production environments.

## Technical Highlights
- **Microcontroller:** STM32C011 (Arm Cortex-M0+), chosen for its efficiency and compact form factor.
- **Wireless Interface:** nRF24L01+ module connector, providing low-power 2.4GHz communication via SPI.
- **USB-UART Bridge:** Integrated **MCP2200** for seamless serial debugging and data acquisition.
- **Power Management:** Supports wide input voltage (5V - 36V) via **TSR 0.5-2433** DC/DC buck regulator.
  - Reverse polarity protection via Schottky diode.
  - Decoupled USB-C port (Data only) to prevent VBUS conflicts with host devices.

## Engineering Lessons & Design Choices

During the development of this board, several critical hardware engineering principles were implemented to ensure stability and signal integrity:

### 1. High-Frequency Signal Integrity
* **Series Termination:** Integrated series resistors on high-speed lines to dampen ringing and control rise/fall times. This minimizes electromagnetic interference (EMI) and prevents signal reflections.
* **Impedance Control:** Careful routing of USB D+/D- differential pairs to maintain signal quality for the MCP2200 bridge.

### 2. Clock & Timing Precision
* **Independent Oscillators:** Implemented separate external crystals for the STM32 (8 MHz) and MCP2200 (12 MHz). 
* **Parasitic Optimization:** Load capacitors were placed in immediate proximity to the crystals to minimize parasitic inductance and ensure a stable startup of the oscillation.

### 3. Power Integrity & Noise Suppression
* **Decoupling Strategy:** Strategic placement of ceramic decoupling capacitors (100nF) directly at the VCC pins of each IC to provide local energy storage and filter high-frequency switching noise.
* **RF-Sensitive Filtering:** Added LC-filtering stages at the output of the switching regulator to provide a "clean" 3.3V rail for the nRF24L01+, which is highly sensitive to power supply ripple.

### 4. Advanced PCB Layout Techniques
* **Tight Component Placement:** Mastered the challenge of placing high-pin-count components (USB-C, STM32, MCP2200) in a very confined space while maintaining minimum clearance for the Ground Plane (GND).
* **Thermal Management:** Solid Ground Fill on the bottom layer acts as a heat sink and provides a low-impedance return path for all signals.

##  Project Structure
- `/Screenshots`: High-resolution renders, schematic snips, and hardware photos.
- `stm32c_nrf.kicad_pcb`: The 2-layer board layout.
- `stm32c_nrf.kicad_sch`: The full electrical schematic.
