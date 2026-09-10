# Portable Battery-Powered Cocktail Machine

<p align="center">
  <img src="images/hero.png" width="460" alt="Portable cocktail machine prototype">
</p>

A portable battery-powered cocktail-mixing prototype integrating power electronics, pump-driven fluid handling, embedded control, a rotary/LCD user interface, and a multi-part FDM-printed mechanical enclosure.

The project focused on packaging electrical, mechanical, and fluid-handling subsystems into a compact physical prototype, progressing from system architecture and subsystem testing through CAD design, assembly, and system integration.

**Project period:** Fall 2025  
**Institution:** Brown University  
**Course:** ENGN 1650 Undergraduate Capstone  
**Team:** 4-person team — 3 graduate students and 1 undergraduate student

---

## Project Goal

The project explored how a portable cocktail-mixing device could combine fluid handling, embedded electronics, battery power, and a user interface within a compact physical product.

The prototype incorporated:

- a battery-powered pump for fluid movement;
- an STM32-based embedded control system;
- LCD and rotary-control interfaces;
- USB-C power input and Li-ion battery charging;
- separate power rails for logic electronics and the pump;
- a removable liquid container;
- a custom multi-part enclosure designed for FDM fabrication.

The goal was to move beyond a conceptual product model and develop a physically integrated prototype in which the electrical, mechanical, and fluid-handling subsystems could be assembled and tested together.

---

## Highlights

- **1S Li-ion battery-powered architecture**
- USB-C 5 V power input and battery charging
- Dedicated regulated logic power
- **12 V boost rail** for pump operation
- MAX17048 battery monitoring
- STM32L412C8T6-based control architecture
- LCD + rotary encoder / button interface
- MOSFET-based pump control
- Full Fusion 360 mechanical assembly
- Custom FDM-printable threaded container interface
- Dedicated PCB, pump, and LCD mounting features
- Detailed mechanical part and assembly drawings
- Bench pump testing and complete physical prototype assembly

---

## My Contributions

My primary work focused on **power electronics, mechanical design, prototype integration, and team coordination**.

- Led the four-person team through design reviews, subsystem development, and prototype integration.
- Co-developed the overall system schematic, with primary ownership of the power-management section.
- Designed the 1S Li-ion power architecture, including USB-C input, battery charging, regulated logic power, 12 V pump power conversion, and battery monitoring.
- Independently designed the complete mechanical enclosure and assembly in Fusion 360.
- Developed custom FDM-printable threaded interfaces and mechanical clearances for the removable container.
- Designed dedicated mounting structures for the PCB, pump, LCD, and enclosure components.
- Produced detailed mechanical part and assembly drawings.
- Coordinated electrical, firmware, and mechanical integration toward the completed physical prototype.
- Supported subsystem testing and final prototype assembly.

### Team Collaboration

The project was developed collaboratively across electrical, firmware, and mechanical work.

Within the shared system design, I owned the power-management section of the schematic and independently developed the mechanical enclosure and assembly. I also led system-level integration and team coordination.

The MCU/control schematic and most of the embedded firmware were primarily developed by other team members. They are included in this repository only where useful for documenting the architecture and integration of the complete system.

---

## System Architecture

The prototype combines two main electrical power domains with embedded control and a fluid-handling path.

```text
                 USB-C 5 V
                     │
                     ▼
              Battery Charging
                     │
                 1S Li-ion
                     │
            ┌────────┴────────┐
            │                 │
            ▼                 ▼
       Logic Supply       12 V Boost
            │                 │
            ▼                 ▼
     STM32 + Display         Pump
            │                 │
     Encoder / Button         │
            │                 ▼
            └──── Control ──► Fluid Path
                              │
                              ▼
                     Removable Container
```

Battery state is monitored electrically and communicated to the control system, while the higher-voltage pump rail is generated separately from the logic supply.

This architecture allows the low-voltage embedded electronics and the pump subsystem to operate from the same portable single-cell battery source.

---

## Electrical Design

### Power Management

<p align="center">
  <img src="electrical/power-schematic.png" width="900" alt="Cocktail machine power-management schematic">
</p>

The power-management schematic was my primary electrical design contribution.

The design includes:

| Function | Implementation |
| --- | --- |
| External input | USB-C 5 V |
| Battery | 1S Li-ion, 500 mAh |
| Battery charging | MCP73831 |
| Logic power conversion | TPS63031 buck-boost |
| Pump supply | TPS61040 boost converter |
| Pump rail | 12 V |
| Battery monitoring | MAX17048 |

The power architecture separates the low-voltage logic domain from the pump supply while allowing both to operate from the same single-cell battery.

The charging section accepts 5 V through USB-C and charges the 1S Li-ion battery. The battery rail then feeds the logic-power and pump-power conversion stages.

---

### Control Electronics

<p align="center">
  <img src="electrical/control-schematic.png" width="900" alt="Cocktail machine MCU and control schematic">
</p>

The control side of the system includes:

- `STM32L412C8T6`
- external flash memory
- LCD interface
- rotary encoder / user-button interface
- ST-Link / SWD programming connection
- I2C connection to the battery-monitoring circuit
- pump MOSFET control

This schematic is shown to provide context for the complete electrical architecture and its interaction with the power-management section.

The MCU/control circuitry and most embedded firmware were primarily developed by other team members as part of the shared system design.

---

### PCB Layout — Work in Progress

<p align="center">
  <img src="electrical/pcb-layout-wip.png" width="900" alt="Work-in-progress PCB layout for cocktail machine">
</p>

A custom PCB implementation was started during the project, including board-shape development, component placement, and partial routing.

The layout was **not completed or fabricated**, and no custom-board bring-up or validation is claimed.

It is included here as design-process documentation rather than as a finished PCB implementation.

---

## Mechanical Design

The mechanical system was designed in Fusion 360 as a multi-part assembly intended for FDM prototyping.

<p align="center">
  <img src="images/cad-overview.png" width="520" alt="Fusion 360 CAD overview of portable cocktail machine">
</p>

The enclosure had to package several different subsystems within a compact cylindrical product:

```text
Top Interface
├── LCD
├── Rotary Control
└── Top Enclosure

Main Body
├── PCB
├── Battery
├── Pump
├── Wiring
└── Fluid Connections

Lower Interface
└── Removable Liquid Container
```

Mechanical design therefore focused not only on external appearance, but also on internal component placement, mounting, assembly access, and printable interfaces.

---

### Assembly Design

<p align="center">
  <img src="mechanical/assembly-exploded.png" width="760" alt="Exploded assembly drawing of cocktail machine">
</p>

The exploded assembly drawing documents the relationship between the enclosure, internal supports, fluid-handling components, electronics, and removable container.

[View full exploded assembly drawing (PDF)](mechanical/assembly-exploded.pdf)

A second drawing documents the completed assembly and overall component relationship:

[View assembly overview (PDF)](mechanical/assembly-overview.pdf)

---

### Removable Container & Printable Thread

<p align="center">
  <img src="images/modular-container.png" width="520" alt="Cocktail machine with removable threaded container">
</p>

The lower container was designed as a removable module using a custom FDM-printable threaded connection.

The mechanical drawing specifies:

| Parameter | Design value |
| --- | ---: |
| Container diameter | 70 mm |
| Container height | 140 mm |
| Nominal capacity | 540 mL |
| Thread pitch | 3.0 mm |
| Thread depth | 1.2 mm |
| Effective thread length | 10 mm |
| Radial clearance | 0.3 mm |

The clearance and relatively coarse thread geometry were selected to make the connection practical to prototype using FDM printing rather than relying on fine production-machined thread geometry.

<p align="center">
  <img src="mechanical/container-thread.png" width="760" alt="Container and custom thread engineering drawing">
</p>

[View full container and thread drawing (PDF)](mechanical/container-thread.pdf)

---

### Enclosure & Component Mounting

The main enclosure was divided into multiple printable parts so that internal components could be installed and accessed during prototype assembly.

<p align="center">
  <img src="images/prototype-side.png" width="440" alt="Side view of portable cocktail machine prototype">
</p>

The enclosure incorporates dedicated geometry for:

- PCB positioning;
- pump support;
- LCD mounting;
- rotary-control access;
- fluid connections;
- screw-based assembly;
- removable-container attachment.

Detailed drawings are available for the primary enclosure components:

- [Main body shell drawing (PDF)](mechanical/main-body-shell.pdf)
- [Top shell and knob drawing (PDF)](mechanical/top-shell-knob.pdf)

---

## User Interface Integration

<p align="center">
  <img src="images/control-interface.png" width="440" alt="Cocktail machine LCD and rotary control interface">
</p>

The upper enclosure integrates the display and rotary control into the physical product form.

The mechanical CAD had to account for component positioning, external access, fastening, and clearances while preserving the overall enclosure geometry.

The user interface was therefore treated as an electromechanical integration problem rather than as an isolated cosmetic feature.

---

## Prototype & Testing

The project progressed through subsystem testing before full mechanical integration.

### Pump Subsystem Test

[▶ Watch pump subsystem test](demo/pump-test.mov)

The pump and liquid-transfer path were tested separately before integration into the final enclosure.

This provided an early functional check of the fluid-handling subsystem independent of the complete mechanical assembly.

### Assembly Demonstration

[▶ Watch prototype assembly demonstration](demo/assembly-demo.mp4)

The assembly demonstration shows the physical integration of the enclosure components and internal hardware into the completed prototype.

The final physical build brought together:

- the FDM-printed enclosure;
- removable container;
- pump and fluid path;
- embedded electronics;
- battery system;
- display and user control;
- mechanical mounting hardware.

---

## Engineering Limitations & Lessons

### 1. Custom PCB Was Not Completed

The project progressed from schematic design into PCB placement and partial routing, but the custom PCB was not completed or fabricated.

As a result, this repository does not claim custom-board bring-up, assembly, or electrical validation.

A future revision could complete the layout, perform DRC review, fabricate the board, and validate the power and control sections independently before full-system integration.

### 2. FDM-Printed Interfaces Require Manufacturing-Aware Geometry

Features such as the removable-container thread cannot simply reproduce fine machined-thread geometry.

The prototype used a relatively coarse **3 mm thread pitch** and **0.3 mm radial clearance** to create a more printable and assembleable interface.

This reinforced the importance of designing mechanical features around the manufacturing process rather than only around ideal CAD geometry.

### 3. Packaging Drives Cross-Domain Tradeoffs

The enclosure had to accommodate the PCB, pump, battery, display, wiring, fluid connections, fasteners, and removable container within a compact form.

Changes to one subsystem therefore affected the others.

This made mechanical packaging and subsystem coordination central parts of the engineering process rather than tasks performed only after the electrical design was complete.

### 4. Prototype Validation Scope

The preserved project evidence includes schematic development, pump subsystem testing, mechanical drawings, assembly, and a completed physical prototype.

It does not represent a production-qualified product or a completed reliability-validation program.

The project is presented here as an integrated engineering prototype and system-development case study.

---

## Repository Scope

This repository is intended as an **engineering portfolio and technical case study**, not as a complete open-source hardware or software release.

Included materials:

- prototype photographs;
- selected electrical schematics;
- work-in-progress PCB layout documentation;
- mechanical CAD overview;
- mechanical engineering drawings in PNG and PDF format;
- subsystem and assembly demonstration videos.

The following materials are intentionally not published:

- the complete Altium project;
- complete Fusion 360 / CAD source files;
- manufacturing files for the unfinished PCB;
- teammate-developed firmware source;
- complete course-development archives;
- third-party libraries and reference files.

The published material is intended to demonstrate the project's power-electronics design, mechanical development, system integration, prototyping, and engineering documentation.

---

## Acknowledgments

This project was developed at **Brown University** as part of the **ENGN 1650 Undergraduate Capstone**.

The four-person team consisted of **three graduate students and one undergraduate student**.

I am grateful to my teammates for their contributions to the MCU/control electronics, embedded firmware, and other parts of the integrated prototype.
