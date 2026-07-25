# H7 Industrial Gateway & Data Acquisition System





<section id="pcb-design" class="project-section">

    <div class="section-header">
        <h2>PCB Design and Layout</h2>
        <p>
            The schematic has now been translated into a complete 
            <strong>10-layer mixed-signal PCB design</strong> for the STM32H7 Industrial Gateway.
        </p>
    </div>

    <figure class="project-figure">
        <img
            src="assets/images/pcb-layout-complete.png"
            alt="Completed 10-layer PCB layout of the STM32H7 Industrial Gateway"
            class="project-image"
        >
        <figcaption>
            Completed PCB layout showing the central STM32H7 processor, external memories,
            communication interfaces, analogue acquisition circuitry and multi-rail power system.
        </figcaption>
    </figure>

    <h3>Design Overview</h3>

    <p>
        The completed board integrates a high-performance STM32H743 microcontroller with
        external SDRAM and parallel NOR flash, USB High-Speed, Ethernet, CAN, RS-485,
        precision analogue acquisition, audio processing and a multi-rail power architecture.
    </p>

    <p>
        The PCB was developed as a practical study of advanced hardware design rather than
        as a conventional microcontroller development board. Its implementation required
        simultaneous consideration of:
    </p>

    <ul>
        <li>High-density BGA escape routing</li>
        <li>High-speed parallel memory interfaces</li>
        <li>Controlled-impedance USB and Ethernet signals</li>
        <li>Power-distribution-network design</li>
        <li>Reference-plane and return-current continuity</li>
        <li>Mixed-signal partitioning</li>
        <li>Switching-regulator current-loop control</li>
        <li>Analogue noise reduction</li>
        <li>Thermal performance</li>
        <li>Manufacturing and assembly constraints</li>
        <li>Accessibility for test, programming and board bring-up</li>
    </ul>

    <h3>Functional Placement and Board Partitioning</h3>

    <p>
        The board was divided into functional regions before detailed routing began.
        Components were positioned according to signal flow, interface timing, power-current
        paths, connector location and noise sensitivity rather than simply according to
        available board space.
    </p>

    <p>
        The STM32H7 BGA is located near the centre of the PCB. This provides relatively direct
        access to the external memory devices and the major communication and acquisition
        subsystems.
    </p>

    <ul>
        <li>
            <strong>SDRAM and NOR flash:</strong>
            positioned close to the MCU to reduce FMC bus length, propagation delay,
            routing congestion and unnecessary layer transitions.
        </li>

        <li>
            <strong>USB High-Speed subsystem:</strong>
            positioned close to the USB-C connector to maintain a short USB differential path.
        </li>

        <li>
            <strong>Ethernet subsystem:</strong>
            arranged close to the RJ45 connector, with the PHY, magnetics and termination
            components forming a compact signal path.
        </li>

        <li>
            <strong>Power-entry and regulation circuitry:</strong>
            grouped near the DC and USB power inputs to contain high-current switching loops.
        </li>

        <li>
            <strong>CAN and RS-485 interfaces:</strong>
            placed near their field connectors to minimise unprotected internal routing.
        </li>

        <li>
            <strong>Precision ADC and geophone front end:</strong>
            located away from the external memory buses, high-speed clocks and switching
            regulators.
        </li>

        <li>
            <strong>Audio subsystem:</strong>
            grouped around the codec and its associated analogue and digital connections.
        </li>

        <li>
            <strong>Debug and user controls:</strong>
            boot, reset, status indication and programming access remain physically accessible.
        </li>
    </ul>

    <h3>10-Layer Stackup</h3>

    <p>
        A 10-layer construction was selected to provide sufficient routing capacity for the
        BGA processor and parallel memory interfaces while preserving continuous reference
        planes for high-speed signals.
    </p>

    <p>
        The stackup was developed around the following objectives:
    </p>

    <ul>
        <li>Provide dedicated ground-reference planes</li>
        <li>Maintain short return-current paths</li>
        <li>Support controlled single-ended and differential impedance</li>
        <li>Provide internal routing capacity for the FMC memory interfaces</li>
        <li>Distribute multiple power rails with low resistance and inductance</li>
        <li>Separate sensitive analogue circuitry from high-activity digital routing</li>
        <li>Maintain a mechanically balanced and manufacturable construction</li>
    </ul>

    <p>
        Trace geometry was selected using the fabricator's dielectric thicknesses,
        material properties and impedance capability. Critical trace widths were therefore
        derived from the actual PCB build-up rather than selected using generic rules.
    </p>

    <h3>Power Architecture and PDN</h3>

    <p>
        The board contains several voltage domains required by the processor, memory,
        communication PHYs, analogue circuitry and audio codec. The power architecture
        includes protected power entry, switching conversion, low-noise regulation and
        local filtering.
    </p>

    <p>
        Switching-regulator placement was driven by current-loop geometry. Input capacitors,
        switching components, inductors and output capacitors were positioned to minimise
        the high <em>di/dt</em> loops and to contain the switch-node copper area.
    </p>

    <p>
        The power-distribution network uses:
    </p>

    <ul>
        <li>Dedicated power and ground planes</li>
        <li>Local high-frequency decoupling at device supply pins</li>
        <li>Bulk capacitance at regulators and major loads</li>
        <li>Short capacitor-to-pin connections</li>
        <li>Closely spaced power and ground vias</li>
        <li>Bottom-side decoupling around the BGA region</li>
        <li>Filtered supplies for sensitive analogue and physical-layer circuitry</li>
        <li>Multiple vias where higher current must pass between layers</li>
    </ul>

    <p>
        The objective is not only to provide the correct DC rail voltage, but also to
        maintain a sufficiently low supply impedance during rapid changes in processor,
        memory and interface current.
    </p>

    <h3>STM32H7 BGA Escape</h3>

    <p>
        The STM32H743 is implemented in a fine-pitch BGA package. Its inner balls cannot be
        routed directly on the component layer, so a structured escape strategy was required.
    </p>

    <p>
        The BGA implementation uses:
    </p>

    <ul>
        <li>Short breakout traces</li>
        <li>Controlled neck-down within the dense fanout region</li>
        <li>Signal vias allocated according to destination and routing direction</li>
        <li>Direct access from power and ground balls to internal planes</li>
        <li>Local decoupling beneath and around the package</li>
        <li>Routing-layer allocation based on interface groups</li>
        <li>Nearby ground vias to support return-current transitions</li>
    </ul>

    <p>
        Power and ground connections were prioritised during fanout so that signal escape
        did not compromise the processor's transient-current paths.
    </p>

    <h3>External SDRAM and NOR Flash</h3>

    <p>
        The board uses the STM32 Flexible Memory Controller to interface with external
        SDRAM and parallel NOR flash. These buses contain address, data, command, clock
        and control signals with different timing relationships.
    </p>

    <p>
        Their implementation required consideration of:
    </p>

    <ul>
        <li>The 16-bit data bus</li>
        <li>Address and bank-address signals</li>
        <li>SDRAM clock and clock-enable signals</li>
        <li>Row, column and write command signals</li>
        <li>Byte-mask signals</li>
        <li>NOR read, write, chip-select and wait-state control</li>
        <li>Series damping resistors</li>
        <li>Maximum route length and allowable skew</li>
        <li>Layer assignment and via-count control</li>
        <li>Continuous reference planes beneath the bus</li>
    </ul>

    <p>
        The memory signals were divided into timing-related groups rather than applying one
        arbitrary length-matching rule to every signal. Clock, data, address and control
        nets were constrained according to their electrical role and the timing requirements
        of the connected devices.
    </p>

    <h3>USB High-Speed and ULPI</h3>

    <p>
        USB High-Speed operation is provided through an external ULPI PHY. The STM32H7
        contains the USB controller, while the external PHY performs the high-speed physical
        signalling required at the USB connector.
    </p>

    <p>
        The ULPI interface includes an 8-bit bidirectional data bus together with clock,
        direction, next and stop control signals. Series damping resistors are used where
        required to reduce edge-related ringing between the MCU and PHY.
    </p>

    <p>
        The USB D+ and D− traces were treated as a controlled-impedance differential pair.
        Routing considerations included:
    </p>

    <ul>
        <li>Short distance between the PHY and USB-C connector</li>
        <li>Controlled differential impedance</li>
        <li>Closely matched positive and negative trace lengths</li>
        <li>Consistent pair spacing</li>
        <li>Minimal via usage</li>
        <li>Continuous ground reference</li>
        <li>Symmetrical connector breakout</li>
        <li>ESD protection positioned close to the connector</li>
        <li>Short VBUS-sensing and protection paths</li>
    </ul>

    <h3>Ethernet and RMII</h3>

    <p>
        The Ethernet subsystem connects the STM32 MAC to an external 10/100 Ethernet PHY
        through RMII. The interface includes transmit, receive, management and 50 MHz
        reference-clock signals.
    </p>

    <p>
        The PHY is positioned close to the Ethernet magnetics and RJ45 connector. The
        magnetics-to-connector path is kept short, and the Ethernet MDI traces are routed
        as controlled-impedance differential pairs.
    </p>

    <p>
        Particular attention was given to:
    </p>

    <ul>
        <li>RMII clock routing</li>
        <li>PHY strap and reset states</li>
        <li>Reference-resistor placement</li>
        <li>MDI differential-pair symmetry</li>
        <li>Termination placement</li>
        <li>Magnetics and RJ45 proximity</li>
        <li>Shield and chassis-current paths</li>
        <li>Separation from switching-power circuitry</li>
    </ul>

    <h3>Precision Analogue Acquisition</h3>

    <p>
        The board includes a precision sigma-delta ADC and an analogue front end intended
        for low-level sensor and geophone measurements.
    </p>

    <p>
        The analogue circuitry was placed in a quieter region of the board and separated
        from the FMC memory buses, switching regulators and high-frequency clocks.
        Sensitive nodes were kept short, and filtering components were positioned close
        to the relevant amplifier and ADC pins.
    </p>

    <p>
        The analogue implementation includes:
    </p>

    <ul>
        <li>Bipolar sensor-signal handling</li>
        <li>Mid-supply bias generation</li>
        <li>AC coupling</li>
        <li>High-pass and low-pass filtering</li>
        <li>Op-amp buffering</li>
        <li>ADC input-current and source-impedance control</li>
        <li>Reference-voltage decoupling</li>
        <li>Protection at external analogue connectors</li>
        <li>Controlled analogue return paths</li>
    </ul>

    <p>
        The analogue and digital sections share a deliberate grounding strategy based on
        continuous return paths rather than arbitrary splits in the ground plane.
    </p>

    <h3>CAN and RS-485 Interfaces</h3>

    <p>
        CAN and RS-485 provide robust communication with external industrial equipment.
        The transceivers, termination components and protection devices are located close
        to their respective connectors.
    </p>

    <p>
        This arrangement keeps externally exposed traces short and places transient
        protection before signals enter the internal board area.
    </p>

    <p>
        The physical-layer design considers:
    </p>

    <ul>
        <li>Differential routing</li>
        <li>Bus termination</li>
        <li>Failsafe states</li>
        <li>Transceiver enable and standby control</li>
        <li>Connector grounding</li>
        <li>TVS protection</li>
        <li>Common-mode interference</li>
        <li>Field-wiring and multidrop-bus behaviour</li>
    </ul>

    <h3>Audio Subsystem</h3>

    <p>
        The audio codec combines analogue input and output circuitry with digital audio
        communication through the STM32 SAI/I²S peripheral.
    </p>

    <p>
        Analogue audio components are grouped close to the codec, while digital clock and
        data signals are routed with controlled return paths. Codec supply filtering and
        local decoupling reduce coupling from the processor, memory and switching converters.
    </p>

    <h3>Constraint-Driven Routing</h3>

    <p>
        Routing was performed using interface-specific constraints rather than a single
        generic trace rule.
    </p>

    <p>
        Separate design-rule classes were defined for:
    </p>

    <ul>
        <li>USB differential signals</li>
        <li>Ethernet differential signals</li>
        <li>Memory clocks, data, address and control groups</li>
        <li>High-frequency clock signals</li>
        <li>Analogue inputs and references</li>
        <li>Power rails with different current requirements</li>
        <li>BGA breakout regions</li>
        <li>Low-speed control and status signals</li>
    </ul>

    <p>
        Layer changes were minimised on critical signals. Where a reference-plane transition
        was unavoidable, nearby ground-return vias were used to preserve the high-frequency
        current path.
    </p>

    <h3>Design for Test and Bring-Up</h3>

    <p>
        The board includes accessible controls and test provisions to support initial
        power-up and systematic subsystem verification.
    </p>

    <ul>
        <li>SWD programming and debugging access</li>
        <li>Reset and boot controls</li>
        <li>Power and status indicators</li>
        <li>Accessible communication connectors</li>
        <li>Power-rail measurement points</li>
        <li>Subsystem isolation and series-link components</li>
        <li>External access to industrial and analogue interfaces</li>
    </ul>

    <p>
        Bring-up will proceed in stages, beginning with resistance checks and current-limited
        power-up, followed by rail, reset, clock and programming verification. External
        memories and communication interfaces will then be enabled and tested individually.
    </p>

    <h3>Design Verification and Manufacturing Readiness</h3>

    <p>
        Although the physical layout is complete, release for fabrication requires a formal
        verification process. This includes:
    </p>

    <ul>
        <li>Final schematic and PCB consistency review</li>
        <li>ERC and DRC resolution</li>
        <li>Critical footprint and pin-number verification</li>
        <li>Power-plane and return-path inspection</li>
        <li>Controlled-impedance confirmation with the fabricator</li>
        <li>Memory length and skew review</li>
        <li>Differential-pair inspection</li>
        <li>Gerber and drill-file inspection</li>
        <li>BOM and placement-file reconciliation</li>
        <li>Assembly and manufacturing documentation review</li>
    </ul>

    <h3>Project Outcome</h3>

    <p>
        Completion of the PCB layout represents the transition from circuit design to a
        manufacturable hardware platform. The board brings together power electronics,
        high-speed digital design, precision analogue acquisition, industrial communications
        and dense multilayer PCB implementation within a single system.
    </p>

    <p>
        The next project stage is fabrication, assembly and structured board bring-up.
        Results from power testing, memory validation, USB and Ethernet operation,
        communication-interface testing and analogue measurements will be documented as
        the hardware is commissioned.
    </p>

</section>
![pcb](./5.png)
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
