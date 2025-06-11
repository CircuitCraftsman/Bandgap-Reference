# Bandgap-Reference
Open-Source Bandgap Reference Circuit

# Contents
- [Introduction](#Introduction)
  - [Used Tools](#Used-Tools)
- [Theory](#Theory)
  - [Specifications](#Specifications)
- [Schematic](#Schematic)
- [Pre-Layout Simulations](#Pre-Layout-Simulations)
- [Layout](#Layout)
- [Post-Layout Simulations](#Post-Layout-Simulations)
- [Future Work](#Future-Work)
- [References](#References)

# Introduction
This is an open-source voltage-mode bandgap reference circuit, designed using the Skywater 130 process design kit (PDK). 

## Used Tools

- Xschem

![Xschem](https://github.com/CircuitCraftsman/Bandgap-Reference/blob/main/Images/Xschem.png)

   - Xschem is a schematic capture program that allows the creation of a hierarchical representation of circuits using a top-down approach. By focusing on interfaces, hierarchy, and instance properties, a complex system can be described in terms of simpler building blocks. A VHDL, Verilog, or Spice netlist can be generated from the drawn schematic, allowing the simulation of the circuit. The key feature of the program is its drawing engine, written in C and using the Xlib drawing primitives; this gives very good speed performance, even in huge circuits. The user interface is built with the Tcl-Tk toolkit; TCL is the extension language.

- Ngspice

    - Ngspice is an open-source mixed-level/mixed-signal electronic circuit simulator. It is a successor of the latest stable release of Berkeley SPICE, version 3f.5, which was released in 1993. A small group of maintainers and the user community contribute to the ngspice project by providing new features, enhancements, and bug fixes.

- Magic VLSI

    - Magic is a venerable VLSI layout tool, written in the 1980s at Berkeley by John Ousterhout, now famous primarily for writing the scripting interpreter language Tcl. Due in part to its liberal Berkeley open-source license, magic has remained popular with universities and small companies. The open-source license has allowed VLSI engineers with a bent toward programming to implement clever ideas and help magic stay abreast of fabrication technology. However, it is the well-thought-out core algorithms that lend magic the greatest part of its popularity. Magic is widely cited as being the easiest tool to use for circuit layout, even for people who ultimately rely on commercial tools for their product design flow.

- SkyWater 130

    - SKY130 is a mature 180 nm- 130 nm hybrid technology developed by Cypress Semiconductor that has been used for many production parts. SKY130 is now available as a foundry technology through SkyWater Technology Foundry. The technology is the 8th generation SONOS technology node (130nm).



# References
