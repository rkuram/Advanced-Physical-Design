# Advanced-Physical-Design-Using-OpenLANE-Sky130
This project was done as a part of Advanced Physical Design using OpenLANE/Sky130 workshop.


## Description
This repository is a summary of the 5-day workshop of Advances Physical Design using OpenLANE flow and Google-Skywater130 open surce PDKs. This workshop helped me gain hands-on experience of tools that are used in physical design flow using open source EDA tools on Google-skywater130nm technology open source PDK.


## Contents
- Introsuction to OpenLANE

- Day1: SoC Design and familiarity to open source EDA tools

- Day 2: Chip floorplan and Introduction to Library cells

- Day 3: Design and Characterization of cells using Magic Layout tool and ngSpice

- Day 4: Timing Analysis using OpenSTA, Clock Tree Synthesis and Signal Integrity

- Day 5: Routing and SPEF Extraction


## Introduction to OpenLANE
OpenLANE is an automated RTL to GDSII flow based on several components including OpenROAD, Yosys, Magic, Netgen, Fault, OpenPhysSyn, SPEF-Extractor and custom methodology scripts for design exploration and optimization. The amin goal of OpenLANE is to produce clean (no LVS, DRC and timing violation) GDSII with no human intervention. OpenLANE is tuned for Skywater 130nm open PDK and be containerized to harden macros and chips.

OpenLane has two modes of operations:
- **Autonomous Mode:** Push button flow
- **Interactive:** Run commands and steps and look at results while executing


## Day 1: SoC Design and familiarity to open source EDA tools
DAy 1 started with brif introduction of conccepts like Board design vs Chip design, QFN-48 packages, components of chips (core, die, pads) and also difference between Foundary IPs and Macros. We also looked at fundamentals of RISC-V ISA and how the ISA flow helps in communicating applications( high-level programs) with hardware (GDSII).

(*insert picture of ISA flow*)

There are there components required for open-sorce implementatiom Digital ASIC Design:
- **RTL IP:** open source platforms like github.com, librecores.org, opencores.org
- **EDA tools:** Qflow, OpenROAD, OpenLANE
- **PDK data:** Google and Skywater130 open PDK

### Simplified RTL to GDSII flow:
- **Synthesis:** Converts RTL to a circuit out of components form the standard cell library .In standard cell library, each cell has difeerent views/ models like Electrical, HDL, SPICE, Layout (detailed and abstract), delay 
- **Floor planning:**  
  - *Chip floor planning:* partitioning the chip die between different system buildings blocks and placing the I/O pads
  - *Macro Floor planning:* Macro dimensions, pin locations, rows and routing definitions
- **Power planning:** The power network is constructed by connecting to all components to vertical and horizontal metal srips reducing IR drop.
- **Placement:** For macros, place the gate level netlist cells in the rows and placed closed to each other to ensure low resistance and successful routing.
  - *Global:* optimal positions for all cells, such positions are not legal and may overlap
  - *Detailed:* the positions from global are minially altered to be near.
- **Clock Tree synthesis:** To deliver the clock to all sequrential circuits (e.g., FF) with minimum skew. It is designed in a good shape in usually a tree (H, X).
-	**Routing:** to implement the nets that connects the cell together, uses available metal layers provided by pdks. Skywateer pdk defines six routing layers ( 1-titanimum interconnect layers and 5-aluminium interconnect layers). Router use routing grids which are huge, dived and conquer approach.
  - *Global routing:*  generates routing guides.
  - *Detailed routing:* uses the routing guides to implement the actual wiring.
-	**Layout:** 
  - Phyisal Verifiaction:
    - DRC
    - LVS
  -	Timing Verifaction
    -	STA

![OpenLANE Flow](https://github.com/efabless/openlane/blob/master/doc/openlane.flow.1.png)

Concepts like Design exploration (exploring design picking out the best configuyration to clean layout), Synthesis exploration (to pick the best strategy) and fixing antenna rule violations using Antenna diodes are explained.

### LAB:
- Running OpenLANE
Commands to run OpenLANE:
```
@ openlane_working_dir\openlane_FLOW directory
./flow.tcl -interactive
% package require openlane 0.9
% prep -design picorv32a
```    
- Calculating FF ratio
Commands to run synthesis in openLane.
```
% run_synthesis
``` 


## Day 2: Chip floorplan and Introduction to Library cells
