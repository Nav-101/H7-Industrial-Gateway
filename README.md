


![pcb](./5.png)

# PCB Design and Layout

The schematic design has now been translated into a complete **10-layer mixed-signal PCB layout** for the STM32H7 Industrial Gateway and Data Acquisition System.

The board integrates a high-performance STM32H743 microcontroller with external SDRAM and parallel NOR flash, USB High-Speed, Ethernet, CAN, RS-485, precision analogue acquisition, audio processing and a multi-rail power architecture.

Unlike a conventional microcontroller development board, this design required the simultaneous consideration of:

- High-density BGA escape routing
- High-speed parallel memory interfaces
- Controlled-impedance USB and Ethernet routing
- Power-distribution-network design
- Reference-plane and return-current continuity
- Mixed-signal partitioning
- Switching-regulator current-loop control
- Analogue noise reduction
- Thermal performance
- Manufacturing and assembly constraints
- Accessibility for programming, testing and board bring-up

![Completed STM32H7 Industrial Gateway PCB layout](assets/images/pcb-layout-complete.png)

*Completed 10-layer PCB layout showing the STM32H7 processor, external memories, communication interfaces, analogue acquisition circuitry and multi-rail power architecture.*

---

## Functional Placement and Board Partitioning

The PCB was divided into functional regions before detailed routing began. Components were positioned according to signal flow, interface timing, connector location, current paths and noise sensitivity rather than simply according to the available board space.

The STM32H7 BGA processor is located near the centre of the board. This provides relatively direct access to the external memory devices and the major communication and acquisition subsystems.

The principal functional regions are:

- **External SDRAM and NOR flash:** positioned close to the MCU to reduce FMC bus length, propagation delay, routing congestion and unnecessary layer transitions.
- **USB High-Speed subsystem:** located close to the USB-C connector to maintain a short USB differential path.
- **Ethernet subsystem:** arranged close to the Ethernet connector, with the PHY, magnetics and termination components forming a compact signal path.
- **Power-entry and regulation circuitry:** grouped near the DC and USB power inputs to contain high-current switching loops.
- **CAN and RS-485 interfaces:** positioned close to their field connectors to minimise the length of externally exposed internal traces.
- **Precision ADC and geophone front end:** located away from the external memory buses, high-frequency clocks and switching regulators.
- **Audio subsystem:** grouped around the audio codec and its associated analogue and digital connections.
- **Debug and user controls:** boot, reset, programming and status functions remain physically accessible.

This partitioning reduces routing complexity, shortens critical connections and helps prevent high-activity digital and switching circuits from coupling noise into sensitive analogue sections.

---

## 10-Layer Stackup

A **10-layer PCB construction** was selected to provide sufficient routing capacity for the fine-pitch BGA processor, parallel external-memory interfaces and multiple communication subsystems.

The stackup was developed to achieve the following objectives:

- Provide continuous ground-reference planes
- Maintain short high-frequency return-current paths
- Support controlled single-ended and differential impedance
- Provide sufficient internal routing capacity for the FMC memory buses
- Distribute multiple power rails with low resistance and inductance
- Separate sensitive analogue circuitry from high-activity digital routing
- Maintain a mechanically balanced and manufacturable construction

Critical signals are routed over uninterrupted reference planes. Where signals change layers, nearby ground-return vias are used where required to provide a corresponding transition path for the return current.

Trace geometry was selected using the PCB fabricator's proposed dielectric thicknesses, material properties and impedance capabilities. Critical trace widths and differential-pair dimensions were therefore derived from the actual PCB build-up rather than from generic trace-width rules.

---

## Power Architecture

The board contains several voltage domains required by the processor, external memories, communication PHYs, analogue circuitry and audio codec.

The power architecture includes:

- Protected external power entry
- USB-C and DC input options
- Switching voltage conversion
- Low-noise linear regulation
- Local subsystem filtering
- Power-status indication
- Bulk and local energy storage
- Protection against external transients

Regulator selection and rail allocation were based on expected current demand, efficiency, voltage tolerance, noise sensitivity and thermal performance.

Switching-regulator placement was driven by current-loop geometry. Input capacitors, switching components, inductors and output capacitors were positioned to minimise the high `di/dt` loops and contain the switch-node copper area.

---

## Power-Distribution Network and Decoupling

The power-distribution network was designed to provide more than the correct DC voltage. It must also maintain sufficiently low impedance during rapid changes in processor, memory and interface current.

The PDN implementation includes:

- Dedicated power and ground planes
- Local high-frequency decoupling at device supply pins
- Bulk capacitance at regulators and major loads
- Short capacitor-to-pin current paths
- Closely positioned power and ground vias
- Bottom-side decoupling around the BGA processor
- Multiple vias for higher-current layer transitions
- Filtered supplies for sensitive analogue and physical-layer circuitry
- Reduced neck-downs and current bottlenecks in power copper

Power and ground via placement was considered together with capacitor placement so that the complete transient-current loop remained short and low inductance.

---

## STM32H7 BGA Escape Strategy

The STM32H743 is implemented in a fine-pitch BGA package. Its inner balls cannot be routed directly on the component layer, requiring a structured escape strategy.

The BGA implementation uses:

- Short breakout traces
- Controlled neck-down within dense fanout regions
- Signal vias allocated according to destination and routing direction
- Direct access from power and ground balls to internal planes
- Local decoupling beneath and around the package
- Routing-layer allocation based on interface groups
- Nearby ground vias for signals transitioning between reference layers

Power and ground connections were prioritised during the fanout process so that signal escape did not compromise the processor's transient-current paths.

The fanout was also planned around the direction of the major interfaces, including the external memory buses, USB ULPI, Ethernet RMII, audio, ADC and industrial communication interfaces.

---

## External SDRAM Interface

External SDRAM is connected to the STM32 Flexible Memory Controller and provides additional high-speed volatile memory.

The interface includes:

- A 16-bit data bus
- Address signals
- Bank-address signals
- SDRAM clock
- Clock-enable signal
- Chip-select signal
- Row-address strobe
- Column-address strobe
- Write-enable signal
- Byte-mask signals

The SDRAM was positioned close to the processor to reduce bus length and routing congestion.

The routing strategy considered:

- Clock-to-command timing
- Clock-to-data timing
- Signal-group skew
- Maximum route length
- Series damping resistance
- Via-count control
- Layer assignment
- Stub avoidance
- Continuous reference-plane support

Signals were grouped according to their electrical and timing functions rather than applying one arbitrary length-matching requirement to every net.

---

## Parallel NOR Flash Interface

The parallel NOR flash is also connected through the STM32 FMC and provides non-volatile memory with direct memory-mapped access.

The interface includes:

- Address bus
- Data bus
- Chip-enable control
- Output-enable control
- Write-enable control
- Reset
- Ready or wait-state signalling
- Byte-lane control

The NOR flash was positioned close to the MCU, with address, data and control signals routed as organised groups.

Series damping resistors were included where required to reduce ringing and improve signal settling. Resistor placement was selected according to signal direction and driver location rather than being placed arbitrarily along the route.

---

## USB High-Speed and ULPI

USB High-Speed operation is provided through an external ULPI PHY.

The STM32H7 contains the USB controller, while the external PHY performs the electrical signalling required at the USB connector.

The ULPI interface includes:

- Eight-bit bidirectional data bus
- ULPI clock
- Direction signal
- Next-data signal
- Stop signal
- PHY reset
- PHY control and status communication

Series damping resistors are used where required between the MCU and PHY to reduce edge-related ringing and overshoot.

The USB D+ and D− signals were routed as a controlled-impedance differential pair. The PCB implementation considered:

- Short distance between the PHY and USB-C connector
- Controlled USB differential impedance
- Closely matched positive and negative trace lengths
- Consistent pair spacing
- Minimal via usage
- Continuous ground reference
- Symmetrical connector breakout
- ESD protection positioned close to the connector
- Short VBUS-sensing and protection paths
- USB-C configuration-channel connections

The USB PHY crystal, decoupling and supply-filtering components were placed close to the relevant PHY pins.

---

## Ethernet and RMII

The Ethernet subsystem connects the STM32 Ethernet MAC to an external 10/100 Ethernet PHY through RMII.

The RMII interface includes:

- Transmit data
- Receive data
- Transmit enable
- Carrier-sense and data-valid signalling
- Management data interface
- Management clock
- 50 MHz reference clock
- Reset and configuration straps

The PHY is positioned close to the Ethernet magnetics and connector. The magnetics-to-connector path was kept short, while the Ethernet MDI signals were routed as controlled-impedance differential pairs.

Particular attention was given to:

- RMII reference-clock routing
- PHY strap and reset states
- Reference-resistor placement
- MDI differential-pair symmetry
- Differential-pair spacing
- Termination placement
- Magnetics and connector proximity
- Shield and chassis-current paths
- Separation from switching-power circuitry

---

## CAN Interface

The CAN interface provides robust differential communication with external industrial and automotive equipment.

The subsystem includes:

- MCU CAN controller connection
- CAN transceiver
- Transceiver enable or standby control
- Bus termination
- External connector
- Transient protection
- Ground-reference connection

The CAN transceiver, termination and protection components are positioned close to the external connector.

This arrangement minimises the length of unprotected internal traces and provides a direct path for transient currents before they can enter the main PCB area.

---

## RS-485 Interface

The RS-485 subsystem provides differential serial communication for industrial multidrop networks.

The design includes:

- RS-485 transceiver
- Driver-enable control
- Receiver-enable control
- Bus termination
- Failsafe biasing
- External connector
- Transient protection
- Ground-reference connection

The transceiver and protection components are positioned near the connector to minimise internal exposure to cable-induced disturbances.

The routing and schematic design account for:

- Differential signalling
- Half-duplex control
- Bus termination
- Default receiver state
- Multidrop topology
- Ground-potential differences
- External transient exposure

---

## Precision Analogue Acquisition

The board includes a precision sigma-delta ADC and an analogue front end intended for low-level sensor and geophone measurements.

The analogue section was placed in a quieter region of the board, separated from:

- External memory buses
- High-frequency clocks
- USB and Ethernet digital activity
- Switching-regulator nodes
- High-current power paths

The analogue signal chain includes:

- Bipolar sensor-signal handling
- Mid-supply bias generation
- AC coupling
- High-pass filtering
- Low-pass filtering
- Op-amp buffering
- ADC input-drive control
- Reference-voltage decoupling
- Protection at external analogue connectors

Sensitive and high-impedance nodes were kept short. Filter and bias components were positioned close to the corresponding amplifier and ADC pins.

The analogue and digital circuitry use a deliberate grounding strategy based on continuous return paths rather than arbitrary splits in the ground plane.

---

## Audio Subsystem

The audio subsystem is based around an external audio codec connected to the STM32 SAI/I²S peripheral.

The subsystem includes:

- Digital audio data
- Bit clock
- Frame or left-right clock
- Master clock where required
- I²C control
- Analogue audio inputs
- Analogue audio outputs
- Supply filtering
- Local decoupling
- Coupling and filtering components

Analogue audio components were grouped close to the codec, while digital clocks and data signals were routed with controlled return paths.

The codec and analogue signal paths were separated from the external memory buses and switching-power circuitry to reduce noise coupling.

---

## Clocking, Reset, Boot and Programming

The board includes accessible hardware for startup control, programming and debugging.

This includes:

- MCU reset control
- Boot-mode selection
- SWD programming and debugging
- Status indicators
- Main clock sources
- Peripheral PHY clock sources
- Reset control for external devices
- Accessible debug and test connections

Crystal components were placed close to their corresponding devices, with short oscillator traces and minimal loop area.

Clock signals were treated as high-speed signals regardless of their nominal frequency because their electrical behaviour is determined primarily by edge rise time.

---

## Constraint-Driven Routing

Routing was performed using interface-specific rules rather than applying one generic trace width and clearance across the complete board.

Separate design-rule classes were established for:

- USB differential signals
- Ethernet differential signals
- SDRAM clock, data, address and control groups
- NOR flash address, data and control groups
- High-frequency clocks
- Analogue inputs and references
- Power rails with different current requirements
- BGA breakout regions
- CAN and RS-485 differential signals
- Low-speed control and status signals

Constraints included:

- Trace width
- Clearance
- Via size
- Differential-pair geometry
- Controlled impedance
- Maximum route length
- Matched-length groups
- Allowable skew
- Layer allocation
- Reference-plane requirements

Layer transitions were minimised on critical signals. Where a transition was unavoidable, the corresponding return-current path was also considered.

---

## Reference Planes and Return Paths

The routing strategy was developed around the principle that every signal forms a current loop.

At high frequencies, signal return current follows the path of lowest impedance, normally directly beneath the trace on the nearest reference plane.

The PCB therefore avoids routing critical signals across:

- Ground-plane splits
- Plane voids
- Large antipads
- Unreferenced layer regions
- Discontinuous copper areas

Ground stitching vias are used where required to connect reference planes and support return-current transitions.

This approach reduces loop area, signal distortion, crosstalk and electromagnetic emissions.

---

## Mixed-Signal Partitioning

The board contains high-speed digital, switching-power and low-level analogue circuitry on the same PCB.

Noise control was therefore based on:

- Functional placement
- Current-path containment
- Reference-plane continuity
- Separation of noisy and sensitive traces
- Short analogue signal paths
- Controlled clock routing
- Local filtering and decoupling
- Careful connector placement
- Avoidance of unnecessary ground-plane splits

The objective was not to create isolated schematic blocks that ignore return-current behaviour, but to control where noise is generated and how it can couple into adjacent circuitry.

---

## Design for Test and Bring-Up

The board includes accessible controls and test provisions to support systematic initial power-up and subsystem verification.

These include:

- SWD programming and debugging access
- Reset and boot controls
- Power and status indicators
- Accessible communication connectors
- Power-rail measurement points
- External access to industrial interfaces
- Analogue input and output access
- Series-link and isolation components where appropriate

Bring-up will proceed in stages:

1. Visual and assembly inspection
2. Resistance-to-ground checks
3. Current-limited initial power-up
4. Power-rail verification
5. Reset and clock verification
6. SWD connection and MCU identification
7. Minimal firmware execution
8. SDRAM testing
9. NOR flash testing
10. USB PHY and enumeration testing
11. Ethernet PHY and link testing
12. CAN and RS-485 testing
13. ADC calibration and analogue testing
14. Audio-interface testing

This staged approach reduces the risk of enabling several unverified subsystems simultaneously and makes fault isolation more systematic.

---

## Design Verification and Manufacturing Readiness

The physical layout is complete, but formal checking and manufacturing-release activities remain necessary before fabrication.

The final verification process includes:

- Schematic and PCB consistency review
- ERC and DRC resolution
- Critical symbol and pin-number verification
- Footprint and package verification
- Power-plane inspection
- Return-path inspection
- Controlled-impedance confirmation with the fabricator
- Memory length and skew review
- Differential-pair inspection
- Copper-pour and thermal-relief review
- Gerber and drill-file inspection
- BOM verification
- Placement-file verification
- Assembly-documentation review
- Independent design review

The layout should therefore be considered **physically complete but still undergoing final design verification prior to manufacturing release**.

---

## Project Outcome

Completion of the PCB layout represents the transition from system and circuit design to a manufacturable hardware platform.

The board brings together:

- High-performance embedded processing
- External high-speed memory
- USB High-Speed communication
- 10/100 Ethernet
- CAN and RS-485 industrial interfaces
- Precision analogue acquisition
- Audio processing
- Multi-rail power conversion
- High-density multilayer PCB implementation

The project has provided practical experience in schematic architecture, component selection, power-distribution design, controlled impedance, signal integrity, mixed-signal layout, BGA fanout, external-memory routing and design-for-manufacture.

The next project stage is fabrication, assembly and structured board bring-up. Test results, design corrections, oscilloscope measurements and subsystem-validation results will be documented as the hardware is commissioned.
The layout is being organised into functional zones: power entry and regulation, high-speed digital memory/interface routing, industrial communications, Ethernet/USB connectivity, and low-noise analog/audio acquisition. The next focus is controlled routing of the FMC SDRAM/NOR memory bus, USB/Ethernet signal paths, PDN refinement, decoupling placement, and maintaining clean separation between noisy digital domains and precision analog circuitry.



## Project Objective
A high-performance, 10-layer embedded system designed for industrial edge computing, 
high-speed data logging, and audio-frequency signal processing. This project 
demonstrates expertise in high-speed digital design (SDRAM/QSPI), complex 
communications (Ethernet/CAN/RS485), and precision mixed-signal integration.
![frontpg](./frontpg.png)
## Key Technical Features
*   **Core:** STM32H7 (ARM Cortex-M7) running at 400MHz+.
*   **Memory Architecture:** 
    *   External SDRAM via 32-bit FMC interface for high-speed buffering.
    *   QSPI NOR Flash for robust firmware storage and assets.
*   **Connectivity:** 
    *   Industrial Comms: Isolated CAN and RS485 (TIA/EIA-485) for field-bus reliability.
    *   Networking: 10/100 Ethernet (RMII interface) for IoT gateway functionality.
    *   USB: USB-C OTG for high-speed configuration and data offloading.
*   **Analog & Audio Subsystems:**
    *   **Codec:** TLV320AIC3104 (24-bit Stereo) for voice-band processing and I/O.
    *   **Precision ADC:** ADS1220 (24-bit Delta-Sigma) for high-accuracy sensor data acquisition.
*   **PCB Topology:** 8-layer stackup optimized for Signal Integrity (SI), 
    Power Integrity (PI), and EMI/EMC compliance in harsh environments.


## ⚡ Power Distribution Network (PDN) & Protection
The power subsystem is designed to provide stable, low-noise rails while ensuring hardware longevity through multi-stage industrial protection. 

### 1. Input Protection and Source Management
The board features a dual-input architecture supporting both a DC Jack (unregulated) and USB-C (VBUS).
* **Primary Protection:** The DC input includes a surface-mount fuse (**F1**) and a transient voltage suppressor (**D5**) to protect against overcurrent and high-voltage spikes.
* **Power Multiplexing (TPS2113A):** A dedicated power mux (**U2**) manages the transition between the DC input and USB power. It prevents back-feeding and ensures a seamless 5V supply to the downstream regulators.
![Power Front-End](./powerfront.png)

### 2. Multi-Stage Voltage Regulation
The design utilizes a hierarchical approach to down-conversion to optimize efficiency and noise performance:
* **Intermediate Rail (AP63205):** A synchronous buck converter (**U1**) steps down the primary DC input to a stable $5\text{V}$ rail.
* **Digital System Rails (TLV62569):** Two high-frequency synchronous buck converters (**U5**, **U6**) generate the $3.3\text{V}$ I/O rail and the $1.2\text{V}$ STM32 core rail. These are sized to handle high-frequency switching loads from the FMC bus and the Cortex-M7 core.
* **Precision Analog Rail (LP5907):** To ensure the integrity of the 24-bit ADC and Audio Codec, an **LP5907** ultra-low-noise LDO (**U8**) is used to derive a dedicated ($3.3\text{V}$) analog supply 3.3V_ANA.

### 3. Signal Integrity and ESD Protection
* **USB-C Interface:** The USB data lines ($D+/D-$) and Configuration Channel ($CC$) lines are protected by **TPD2EUSB30** ESD suppressor arrays (**D3**, **D4**). 
* **Common Mode Filtering:** A common-mode choke (**L2**) is implemented on the USB differential pair to mitigate EMI.
* **Noise Isolation:** A ferrite bead (**L5**) and dedicated decoupling network isolate the analog power domain from high-frequency digital switching noise.

## 🧠 External Memory Architecture (SDRAM & Parallel NOR Flash)

The system utilizes a high-performance memory subsystem consisting of both volatile and non-volatile memory. To optimize pin count, both devices are integrated onto a shared 16-bit parallel bus via the STM32H7 Flexible Memory Controller (FMC).

### Component Summary
| Memory Type | Part Number | Capacity | Interface |
| :--- | :--- | :--- | :--- |
| **SDRAM** | AS4C4M16SA | 64 MB | 16-bit Synchronous (120MHz) |
| **NOR Flash** | S29GL128S | 16 MB | 16-bit Asynchronous (Page Mode) |

### 1. High-Speed SDRAM Workspace
The SDRAM serves as the primary volatile workspace for the 480MHz Cortex-M7 core, providing the necessary bandwidth for large data buffers and real-time processing.
* **Clock Management:** The interface is driven by a 120MHz SDCLK. A 22 Ohm series termination resistor is placed at the source to prevent signal reflections and overshoot.
* **16-bit Data Path:** Configured to balance high-speed throughput with PCB routing density.
* **Bank Management:** All 4 internal banks are utilized, with the FMC managing the row/column addressing logic.
![Memory](./memory.png)

### 2. Non-Volatile Parallel NOR Flash
The S29GL128S provides high-reliability storage for firmware and critical system data, supporting Execute-in-Place (XiP) functionality.
* **Page Mode Optimization:** Configured to use 8-word page access. While the initial random access time is 100ns, subsequent burst reads from the same page are reduced to 25ns.
* **Hardware Handshaking:** The RY/BY# (Ready/Busy) output is connected to the FMC_NWAIT pin with a 4.7k Ohm pull-up resistor. This allows the hardware to automatically stall the processor during Flash programming or erase operations if the bus is accessed.
* **Write Protection:** The WP# pin is tied to the 3.3V IO rail to ensure the memory is always available for updates, with software-level protection providing the secondary security layer.

### 3. Bus Multiplexing and Pin Sharing
A key challenge of the design is the physical sharing of the address and data bus between two different memory technologies.
* **Address Mapping:** The FMC_A14/BA0 and FMC_A15/BA1 pins are multiplexed. The hardware ensures that when SDRAM is active (SDNE0 Low), the Bank Address logic takes precedence; when Flash is active (NE1 Low), the standard Address logic is applied.
* **Bus Contention Prevention:** Chip Select (CS) signals are strictly independent. The SDRAM remains in a High-Impedance (High-Z) state while the Flash is being accessed, and vice-versa.
* **Synchronized Reset:** The Flash RESET# pin is connected to the global system NRST, ensuring the memory controller and the storage device are synchronized during power-up or watchdog reset events.

### 4. Schematic-Level Signal Integrity Measures
While the physical routing is reserved for the next phase, the schematic includes critical foundational elements to ensure high-speed stability:

## 🌐 Industrial Ethernet Interface (10/100 Mbps)

The communication subsystem features a high-reliability 10/100 Mbps Ethernet interface using the **Microchip LAN8720AI** Industrial Temperature PHY. This stage is critical for edge-gateway connectivity and real-time data streaming.

### Interface & Synchronization
* **RMII Architecture:** The system utilizes the Reduced Media Independent Interface (RMII) to minimize pin count while maintaining a 100 Mbps data rate. 
* **Synchronous Clocking:** A dedicated **50MHz Active Oscillator** provides a unified reference clock to both the LAN8720AI and the STM32H7 RMII_REF_CLK input. This hardware-level synchronization eliminates the jitter common in MCU-generated clocks (MCO), ensuring stable link performance in high-EMI environments.

### Power Domain Isolation & Signal Integrity
To protect the precision of the 24-bit ADC, the Ethernet power domain is strictly isolated:
* **Isolated Rails:** The PHY analog supply (VDDA) and the RJ45 magnetics center taps are derived from the main 3.3V digital rail through a high-impedance **Ferrite Bead**. This prevents high-frequency switching noise from the transceivers from coupling into the sensitive analog acquisition rails.
* **Magnetic Integration:** The design utilizes an **RJ45 MagJack (HR911105A)** with integrated 1:1 isolation transformers. This provides 1500Vrms isolation and integrated common-mode filtering.
* **Termination:** 49.9 Ohm (1%) precision resistors are utilized for differential pair impedance matching, placed in close proximity to the PHY pins.
![ETHERNET](./ETHERNETT.png)
### Protection & Robustness
* **ESD Suppression:** The differential TX/RX pairs are protected by a low-capacitance ESD array, ensuring the high-speed signal integrity is not compromised while providing protection against cable-discharge events (CDE).
* **Common Mode Filtering:** A discrete common-mode choke is placed on the differential lines to suppress radiated emissions, aiding in future EMC compliance testing.

### Bootstrap Configuration
The PHY is hardware-configured at power-up via strapping resistors:
* **nINTSEL:** Configured for **REF_CLK In** mode to accept the 50MHz external oscillator.
* **REGOFF:** Internal 1.2V regulator enabled, simplifying the power tree and reducing external component requirements.
* **PHYAD:** Hardware-set to Address 0 for deterministic software initialization via the MDIO/MDC management interface.

* ## 🚌 Industrial Communication Zone (CAN-FD & RS-485)

The gateway features a dual-protocol industrial bus zone designed for long-distance reliability and automotive-grade communication. Both interfaces include multi-stage ESD protection and configurable bus termination.

### 1. CAN-FD (Flexible Data-Rate)
The CAN interface is powered by the **TCAN1051V** transceiver, supporting data rates up to 5 Mbps.
* **Level Shifting:** The "V" variant is utilized to bridge the 3.3V STM32H7 FDCAN logic with the 5V CAN bus standard.
* **Industrial Protection:** A dedicated **PESD2CAN** TVS diode array is placed at the DB9 connector to clamp high-voltage transients.
* **Configurable Termination:** A $120\Omega$ termination resistor is included via a physical jumper (**JP2**), allowing the board to act as either a node or a bus terminator.
* **Standardization:** The DB9 connector follows the **CiA 303-1** industry-standard pinout (Pin 2: CAN-L, Pin 7: CAN-H).

### 2. RS-485 (Differential Serial)
For long-distance serial communication (up to 1.2km), a half-duplex **3.3V RS-485 Transceiver (SP3485/MAX3485)** is implemented.
* **Fail-Safe Biasing:** To prevent "ghost" data during bus idle states, external $10\text{k}\Omega$ pull-up/pull-down resistors are placed on the A and B lines. This ensures a defined logic state even when no drivers are active.
* **Directional Control:** A single GPIO pin manages the combined **RE/DE** (Receive/Driver Enable) lines, allowing the STM32H7 to switch seamlessly between transmit and receive modes.
* **Asymmetrical ESD Protection:** Utilizes an **SM712** TVS diode specifically designed for RS-485, accommodating the unique -7V to +12V common-mode voltage range of the protocol.
* **Impedance Matching:** Includes a $22\Omega$ series termination resistor at the MCU UART TX pin to minimize signal reflections.

![RS](./RS.png)

### 🧪 Validation & Testing Strategy (PLANNED)
* **CAN-FD:** Verified using a PC-based CAN analyzer (e.g., PCAN-USB) to monitor frame integrity at 5 Mbps.
* **RS-485:** Tested via a USB-to-RS485 bridge using the **Modbus RTU** protocol to simulate industrial sensor data acquisition.
* **Series Termination:** Included 22 Ohm resistors on high-speed lines (like SDCLK) to manage impedance and dampen potential reflections at the source.
* **Decoupling Strategy:** Implemented a comprehensive decoupling matrix for the BGA footprints, utilizing a mix of 100nF and 1uF ceramic capacitors to provide local charge reservoirs for every power pin.
* **Pin Mapping Logic:** Carefully mapped the multiplexed FMC pins (A14/BA0 and A15/BA1) to ensure the STM32H7 can correctly address both the 4-bank SDRAM and the linear Page-Mode Flash without electrical conflicts.
* **Hardware Handshaking:** Integrated the RY/BY# to NWAIT hardware link with a dedicated pull-up resistor to prevent bus-stall issues during Flash erase/write cycles.

* ## Audio Subsystem (TLV320AIC3104)

### Overview
This module integrates a 24-bit Low-Power Stereo Audio Codec to provide high-quality 
audio-frequency I/O for voice-over-IP (VoIP) or acoustic monitoring.

![codec](./codec.png)
### Design Implementation
*   **Digital Interface:** Connected via STM32H7 Serial Audio Interface (SAI) 
    using DMA for zero-CPU-load audio streaming. Control handled via I2C.
*   **Input Stage:** 
    *   Mono Microphone input via 3.5mm TRS jack.
    *   Implemented using a **Pseudo-Differential** configuration (MIC1LP/MIC1LM) 
        to maximize common-mode noise rejection on the 8-layer board.
    *   AC-coupled via 100nF C0G capacitors for DC offset removal.
*   **Output Stage:**
    *   Stereo Headphone output via 3.5mm TRS jack.
    *   **AC-Coupled Strategy:** Utilizes 47µF high-quality tantalum capacitors to 
        block DC bias (VCM), ensuring compatibility with all standard 32Ω headphones 
        and protecting the load from power-on transients.
    *   Return path grounded to a dedicated Analog Ground (AGND) plane to minimize 
        digital return current interference.
*   **Diagnostic Features:** 
    *   Parallel 2.54mm headers included for direct probe access to Line-Out 
        (LEFT_LOP/M) and Speaker paths, facilitating bench-top testing and 
        external amplification expansion.
### **Precision Data Acquisition Subsystem (ADS1220)**

#### **Overview**
This module is a high-resolution, 24-bit sensing interface designed to capture low-frequency seismic signals from geophones and industrial sensors. By combining the **ADS1220** Delta-Sigma ADC with a custom-engineered **Analog Front End (AFE)**, the system achieves professional-grade signal integrity on an 8-layer industrial board.

![ADC](./ADC_I.png)
#### **Key Design Implementations**

*   **Precision Voltage Reference:** 
    *   Utilizes the **REF5025AIDR** ultra-low-noise 2.5V reference (U20) to ensure absolute measurement accuracy.
    *   Includes high-frequency decoupling ($1\mu F$ and $100nF$) to stabilize the reference input during high-speed sampling cycles.
*   **Active Virtual Ground (1.65V Bias):** 
    *   An **OPA320AIDBVR** (U21) buffers a $10k\Omega$ precision divider (R101, R102) to generate a "stiff" $1.65V$ mid-rail reference.
    *   This "lifts" bipolar geophone signals into the positive common-mode range of the ADC, allowing full-wave capture on a single $3.3V$ supply.
*   **Industrial Front-End Protection:** 
    *   **SMAJ12CA TVS Diode (D6):** Provides a differential clamp at the input connector (P3) to protect against ESD and cable surges.
    *   **Current Limiting:** $100\Omega$ series resistors (R107, R108) safeguard the AFE components from over-voltage transients.
*   **Signal Conditioning & Filtering:**
    *   **AC Coupling:** $10\mu F$ capacitors (C123, C124) block DC offsets while maintaining a flat frequency response for seismic vibrations.
    *   **DC Biasing:** $220k\Omega$ resistors (R103, R104) prevent the inputs from floating and establish a stable $1.65V$ operating point.
    *   **Passive Anti-Aliasing:** A balanced RC filter ($1k\Omega$ / $470nF$) provides a low-pass cutoff at $\approx 338Hz$. This suppresses digital switching noise from the **STM32H7** and **SDRAM** planes.
*   **Digital Integration:**
    *   Communicates with the MCU via high-speed SPI (SPI2) with hardware synchronization via the **DRDY** (Data Ready) pin.
    *   The $100\Omega$ series resistor (R96) on the CS line prevents ringing on the chip-select signal during high-speed bus transactions.

#### **Technical Specifications**
*   **Resolution:** 24-bit Delta-Sigma.
*   **Reference Voltage:** 2.5V (External REF5025).
*   **Filter Cutoff ($f_c$):** $\approx 338Hz$.
*   **Input Topology:** Fully Differential with Pseudo-Differential DC Bias.

*   # High-Speed USB 2.0 (480 Mbps) ULPI PHY Integration
![usb](./usb_hs.png)
## Project Overview
Integrated a dedicated **High-Speed USB 2.0** physical layer into a multi-layer industrial gateway design. By utilizing the **Microchip USB3320** standalone PHY, the system achieves a reliable **480 Mbps** data rate, essential for high-bandwidth seismic data offloading and real-time telemetry.

## Hardware Architecture & Design Details

### 1. ULPI (UTMI+ Low Pin Interface)
* **Digital Highway**: Connected the STM32H7 to the USB3320 via a **12-pin bidirectional ULPI bus**.
* **Signal Damping**: Implemented **22Ω series termination resistors** on all high-speed digital lines (DATA[0:7], DIR, NXT, STP, and CLKOUT) to mitigate signal reflections and ringing on the 8-layer PCB.
* **Timing Control**: Utilized the **60 MHz CLKOUT** generated by the PHY to synchronize the ULPI data bus, ensuring stable data latching between the Link and PHY layers.

### 2. High-Precision Clocking
* **Quartz Selection**: Integrated a **YSX321SL 24 MHz Crystal**. 
* **Stability**: Selected a part with **±10 ppm frequency tolerance** to meet the strict bit-rate accuracy requirements of the USB 2.0 specification.
* **Oscillator Design**: The crystal was selected to match the USB3320's requirements for parallel resonant mode and fundamental vibration.

### 3. Power and Analog Signal Integrity
* **Analog Biasing**: Used a precision **8.06 kΩ (1%) resistor** on the `RBIAS` pin to calibrate the internal transceiver's analog drivers.
* **LDO Stability**: Tied **VBAT** and **VDD33** together and supported them with a **2.2 μF low-ESR ceramic capacitor** (C131) to stabilize the internal 1.8V LDO.
* **Noise Isolation**: Employed **Ferrite Beads (L8, L9)** on the 3.3V and 1.8V rails to isolate the high-speed digital switching noise of the PHY from sensitive analog sensor circuitry.
* **OVP and Sensing**: Integrated a **10 kΩ series resistor** (R109) on the VBUS line to protect the PHY's internal sensing logic against over-voltage conditions.

## Key Senior Design Considerations
* **Pin Mapping Strategy**: Successfully resolved critical pin conflicts between the ULPI data bus and Ethernet RMII signals on Port B of the STM32H7 by remapping Ethernet TX signals to Port G.
* **8-Layer Routing**: Managed the layout of the 480 MHz differential pair (D+/D-) with **90Ω differential impedance** and carefully matched the trace lengths of the 60 MHz ULPI bus to maintain strict timing margins.
