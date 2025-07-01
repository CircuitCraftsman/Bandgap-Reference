# Bandgap-Reference
Open-Source Self-Biased Current-Mode Bandgap Reference Circuit

# Contents
- [Introduction](#Introduction)
  - [Used Tools](#Used-Tools)
- [Theory](#Theory)
  - [Specifications](#Specifications)
- [Schematic](#Schematic)
- [Pre-Layout Simulations](#Pre-Layout-Simulations)
- [Layout](#Layout)
  - [Design of subcells](#Design-of-subcells)
- [Post-Layout Simulations](#Post-Layout-Simulations)
- [Future Work](#Future-Work)
- [References](#References)

# Introduction
This is an open-source, self-biased current-mode bandgap reference circuit, designed using the Skywater 130 process design kit (PDK). The bandgap reference provides a stable and temperature-independent reference voltage, which is essential for analog and mixed-signal integrated circuits. The design focuses on achieving low power consumption and good accuracy over a wide temperature range. This implementation serves as a fundamental building block for various analog systems such as ADCs, DACs, and sensor interfaces.

![Circuit Diagram](https://github.com/TechBlueprint-V/Bandgap-Reference/blob/main/Images/Bandgap%20Schematic.png?raw=true)
## Used Tools

- Xschem

![Xschem](https://github.com/CircuitCraftsman/Bandgap-Reference/blob/main/Images/Xschem.png)

Xschem is a schematic capture program that allows the creation of a hierarchical representation of circuits using a top-down approach. By focusing on interfaces, hierarchy, and instance properties, a complex system can be described in terms of simpler building blocks. A VHDL, Verilog, or Spice netlist can be generated from the drawn schematic, allowing the simulation of the circuit. The key feature of the program is its drawing engine, written in C and utilizing the Xlib drawing primitives, which provides very good speed performance, even in large circuits. The user interface is built with the Tcl-Tk toolkit; TCL is the extension language.



- Ngspice

![Ngspice](https://github.com/CircuitCraftsman/Bandgap-Reference/blob/main/Images/Ngspice_logo.jpg)

Ngspice is an open-source mixed-level/mixed-signal electronic circuit simulator. It is a successor of the latest stable release of Berkeley SPICE, version 3f.5, which was released in 1993. A small group of maintainers and the user community contribute to the ngspice project by providing new features, enhancements, and bug fixes.



- Magic VLSI

![Magic](https://github.com/CircuitCraftsman/Bandgap-Reference/blob/main/Images/Magic.png)

Magic is a venerable VLSI layout tool, written in the 1980s at Berkeley by John Ousterhout, now famous primarily for writing the scripting interpreter language Tcl. Due largely in part to its liberal Berkeley open-source license, magic has remained popular with universities and small companies. The open-source license has enabled VLSI engineers with a programming background to implement innovative ideas and help maintain the pace of fabrication technology. However, it is the well-thought-out core algorithms that lend magic the greatest part of its popularity. Magic is widely cited as being the easiest tool to use for circuit layout, even for people who ultimately rely on commercial tools for their product design flow.



- SkyWater 130

![Skywater 130](https://github.com/CircuitCraftsman/Bandgap-Reference/blob/main/Images/Skywater%20130.png)

SKY130 is a mature 180nm- 130nm hybrid technology developed by Cypress Semiconductor that has been used for many production parts. SKY130 is now available as a foundry technology through SkyWater Technology Foundry. The technology is the 8th generation SONOS technology node (130nm).


- Inkscape

![Inkscape](https://github.com/CircuitCraftsman/Bandgap-Reference/blob/main/Images/Inkscape.webp)

Inkscape is a vector graphics editor. It is used for both artistic and technical illustrations, such as cartoons, clip art, logos, typography, diagrams, and flowcharts. It uses vector graphics to allow for sharp printouts and renderings at unlimited resolution and is not bound to a fixed number of pixels like raster graphics. It is free and open-source software released under a GNU General Public License (GPL) 2.0 or later.

# Theory

A **Bandgap Reference (BGR)** circuit is an essential analog building block used to generate a stable and temperature-independent reference voltage. It typically produces an output voltage around **1.2 V**, which is close to the bandgap voltage of silicon at 0 K. This voltage remains relatively constant over a wide temperature range and supply voltage variations, making it critical in precision analog, mixed-signal, and digital systems.

The operation of a BGR circuit relies on the combination of two types of temperature-dependent voltages:

- **CTAT (Complementary-To-Absolute-Temperature)**: A voltage that decreases with increasing temperature, typically the base-emitter voltage (V<sub>BE</sub>) of a bipolar transistor.
  
  <p align="center">
  <img src="https://github.com/TechBlueprint-V/Bandgap-Reference/blob/main/Images/CTAT%20curve.jpg" alt="CTAT curve" width="500"/>
</p>
  
- **PTAT (Proportional-To-Absolute-Temperature)**: A voltage that increases with temperature, derived from the difference between two V<sub>BE</sub> voltages with different current densities.

<p align="center">
  <img src="https://github.com/TechBlueprint-V/Bandgap-Reference/blob/main/Images/PTAT%20curve.jpg" alt="PTAT curve" width="500"/>
</p>

By summing a CTAT and a scaled PTAT component, the temperature coefficients can be cancelled, resulting in a temperature-independent reference.

<p align="center">
  <img src="https://github.com/CircuitCraftsman/Bandgap-Reference/blob/main/Images/Bandgap%20Diagram.png" alt="Bandgap Diagram" width="500"/>
</p>

### Types of bandgap references available in literature:
- Voltage-Mode Bandgap Reference  
- Current-Mode Bandgap Reference  
- Sub-Bandgap Reference  
- CMOS-Only Bandgap Reference  
- Curvature-Corrected Bandgap Reference  
- Dynamic Bandgap Reference  
- Low Power Bandgap Reference  
- High-Precision Bandgap Reference

### Applications

Bandgap references are widely used in:

- Analog-to-Digital Converters (ADCs)
- Digital-to-Analog Converters (DACs)
- Voltage regulators (LDOs, SMPS)
- Clock circuits and PLLs
- Sensor interface circuits

### Advantages

- Low temperature coefficient
- Process and supply variation tolerance
- Fully CMOS-compatible implementations are possible

### Disadvantages

- Limited accuracy without trimming or calibration
- Power consumption in precision designs
- Susceptible to mismatch and layout parasitics

Bandgap reference circuits are fundamental in modern integrated circuits where stable voltage references are critical for proper operation across varying environmental and operational conditions.

### Specifications

| Parameter             | Value               |
|-----------------------|---------------------|
| Supply Voltage        | 1.8 V               |
| Temperature Range     | -40°C to 125°C      |
| Power Consumption     | < 60 µW             |
| Off Current           | < 2 µA              |
| Start-up Time         | < 2 µs              |
| Tempco for V<sub>ref</sub> | < 50 ppm           |

# Schematic
**Testbench circuit**

![Bandgap Testbench](https://github.com/TechBlueprint-V/Bandgap-Reference/blob/main/Images/Bandgap_tb.png)


**Bandgap Circuit**

![Bandgap Reference](https://github.com/TechBlueprint-V/Bandgap-Reference/blob/main/Images/Bandgap%20Reference.png)

- To get a 1:8 emitter area ratio, I placed 8 pnp BJTs in parallel. It is also useful for matching in the layout.

# Pre-Layout Simulations

V<sub>ref</sub>

![Vref](https://github.com/TechBlueprint-V/Bandgap-Reference/blob/main/Images/Vref.png)

- Temperature sweep from -50°C to +150°C.

**PTAT**

![PTAT](https://github.com/TechBlueprint-V/Bandgap-Reference/blob/main/Images/PTAT.jpg)

**CTAT**

![CTAT](https://github.com/TechBlueprint-V/Bandgap-Reference/blob/main/Images/CTAT.jpg)

**PTAT+CTAT**

![PTAT+CTAT](https://github.com/TechBlueprint-V/Bandgap-Reference/blob/main/Images/CTAT%2BPTAT.jpg)

# Layout

## Design of subcells

**NFET pair M2 and M3 having W=5um L=1um**

![NFET_M2 M3](https://github.com/TechBlueprint-V/Bandgap-Reference/blob/main/Images/NFET_M2%20M3.png)

**Starter NFETs M6 and M7 having W=1um L=7um**

![NFET](https://github.com/TechBlueprint-V/Bandgap-Reference/blob/main/Images/NFET.png)

**PFET pair M1 and M4 and M5 having W=5um L=2um**

![NFET](https://github.com/TechBlueprint-V/Bandgap-Reference/blob/main/Images/PFET.png)

**Starter PFETs having W=5um L=1um**

![Starter_PFET](https://github.com/TechBlueprint-V/Bandgap-Reference/blob/main/Images/Starter_PFET.png)

**5K resistor W=0.35um L=4.255um**

![Res_5k](https://github.com/TechBlueprint-V/Bandgap-Reference/blob/main/Images/Res_5k.png)

**33K resistor network W=0.35um L=11um**

![Res_network](https://github.com/TechBlueprint-V/Bandgap-Reference/blob/main/Images/Res%20network.png)

**PNP BJTs area of 0.68x0.68**

![PNP BJTs](https://github.com/TechBlueprint-V/Bandgap-Reference/blob/main/Images/BJT.png)

**PNP BJT array consisting of 8 BJTs**

![BJT array](https://github.com/TechBlueprint-V/Bandgap-Reference/blob/main/Images/BJT_array.png)

**Full layout**

![Layout](https://github.com/TechBlueprint-V/Bandgap-Reference/blob/main/Images/Layout.png)

# Future Work

- Develop a fully matched, compact, and guard-ring protected layout to minimize mismatch and substrate noise effects.

- Perform Monte Carlo simulations and corner analysis to evaluate the robustness of the bandgap reference against process, voltage, and temperature (PVT) variations.

- Explore advanced curvature compensation techniques to improve reference voltage stability over a wider temperature range.

- Investigate modifications to reduce quiescent current, enabling ultra-low power operation for battery-powered applications.

- Conduct post-layout simulations including parasitic capacitances and resistances to validate performance under realistic conditions.

- Fabricate the design in a silicon process (e.g., SkyWater 130nm) and perform on-chip measurements to verify simulation results.

- Integrate the bandgap reference with Analog-to-Digital Converters (ADC) and System-on-Chip (SoC) platforms to test system-level performance.

# References

1. A. S. Sedra and K. C. Smith, *Microelectronic Circuits*, 7th Edition, Oxford University Press, 2014.    
2. B. Razavi, *Design of Analog CMOS Integrated Circuits*, McGraw-Hill, 2001.  
3. Tümdevre Tasarım ve Eğitim Laboratuvarı (TÜTEL) - https://www.youtube.com/watch?v=rkp89Vu2I20&list=PL99hEJZD7EMjbRal9I6Ee27xq0lvl9abq  
4. https://www.youtube.com/watch?v=p5buXBxCbq8&t=501s&pp=ygUQc3RlZmFuIHNjaGlwcGVycw%3D%3D  
5. SkyWater Technology Foundry, "SkyWater 130nm PDK Documentation," [https://skywater-pdk.readthedocs.io](https://skywater-pdk.readthedocs.io)  
6. https://github.com/silicon-vlsi/BGR_DESIGN_SKY130nm.git
7. https://www.youtube.com/watch?v=bYbkz8FXnsQ&t=1885s&pp=ygUQc3RlZmFuIHNjaGlwcGVycw%3D%3D
8. https://www.youtube.com/watch?v=XvBpqKwzrFY&t=5190s


