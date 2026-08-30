# Requirements — PoE-Powered Ethernet Sensor Node

Two lists. The difference between them is the whole point of this file.

A **fixed requirement** is something [BRIEF.md](../BRIEF.md) asks for. Each one
below quotes the brief text that substantiates it; if a statement cannot be
quoted, it is not a requirement here. An **open decision** is a choice the brief
deliberately left to whoever designs this board.

> Missing details are design freedom, not permission to fabricate unstated user
> requirements.

Promoting a decision into a requirement is the failure this file exists to
prevent. Record a choice under the decision it answers, with the reasoning that
made it — never by adding it to the list above.

Bound to `BRIEF.md` SHA-256 `5aaef1f5b82b3cc6e3575debcd27f63c86640ce9896bf7c6ec77589cd4469c4e`.

## Fixed by the brief

### REQ-01 — The board is a 100BASE-TX Ethernet sensor node.

Brief text:

> Create a 100BASE-TX Ethernet sensor node powered only through IEEE 802.3af PoE.

### REQ-02 — The board is powered only through IEEE 802.3af PoE; the brief names no other power input.

Brief text:

> powered only through IEEE 802.3af PoE

### REQ-03 — The board includes a PoE PD interface.

Brief text:

> Include the PoE PD interface, isolated DC/DC conversion

### REQ-04 — The board includes isolated DC/DC conversion.

Brief text:

> isolated DC/DC conversion, Ethernet PHY/MCU, and connectors for several low-speed sensors

### REQ-05 — The board includes an Ethernet PHY and an MCU.

Brief text:

> Ethernet PHY/MCU, and connectors for several low-speed sensors on the isolated low-voltage side

### REQ-06 — The board provides connectors for several low-speed sensors.

Brief text:

> connectors for several low-speed sensors

### REQ-07 — Those sensor connectors are on the isolated low-voltage side of the barrier.

Brief text:

> several low-speed sensors on the isolated low-voltage side

### REQ-08 — The RJ45 and magnetics arrangement must be one appropriate to PoE.

Brief text:

> Use an RJ45/magnetics arrangement appropriate to PoE.

### REQ-09 — The layout must respect isolation spacing around the DC/DC barrier.

Brief text:

> The board must respect isolation spacing around the DC/DC barrier

### REQ-10 — The layout must keep noisy flyback switching currents away from the PHY analog circuitry.

Brief text:

> keep noisy flyback switching currents away from PHY analog circuitry

### REQ-11 — Where the brief is silent, the design agent must make and document reasonable engineering decisions rather than invent hidden user requirements.

Brief text:

> where the brief leaves choices open, make and document reasonable engineering decisions rather than inventing hidden user requirements.

### REQ-12 — Stated requirements in the brief are authoritative.

Brief text:

> Treat stated requirements as authoritative

### REQ-13 — This repository stays a consumer of the shared PCBA_AutoDesignAndTest toolkit; board-specific logic must not accumulate in the toolkit.

Brief text:

> The repository should remain a consumer of the shared `PCBA_AutoDesignAndTest` toolkit rather than accumulating board-specific logic in the toolkit.

## Open — the design agent decides

### OPEN-01 — PoE PD front-end implementation: how detection and classification signatures are formed, which 802.3af class is declared, whether an integrated PD controller or discrete arrangement is used, and how inrush and hot-swap are handled.

The brief requires a PoE PD interface and names IEEE 802.3af, but specifies no controller, no class, and no signature or inrush approach.

*Decision:* **not yet made.**

### OPEN-02 — Which PoE feed alternatives the node accepts — Alternative A, Alternative B, or both — and which pair-set polarities it accepts, and what circuitry at the input implements the behaviour chosen.

The brief names 802.3af but says nothing about which alternatives or polarities the node must accept.

*Decision:* **not yet made.**

### OPEN-03 — Isolated converter design: controller, transformer, turns ratio, switching frequency, peak-current and duty limits, snubber/clamp, and rectification scheme.

The brief requires isolated DC/DC conversion and refers to flyback switching currents, but fixes no device, no magnetics and no operating point.

*Decision:* **not yet made.**

### OPEN-04 — Secondary-side rail voltages, currents and total power budget, and the load tally that justifies them.

The brief states no rail voltage, no current, and no power figure anywhere; the available budget must be derived from the standard and the design's own loads.

*Decision:* **not yet made.**

### OPEN-05 — Feedback and regulation path across the barrier: optocoupler, primary-side regulation, auxiliary winding, or a digital isolator, plus any additional isolated signal crossings.

The brief says the DC/DC is isolated but is silent on how regulation information crosses the barrier.

*Decision:* **not yet made.**

### OPEN-06 — Where the isolation barrier is drawn on the board, and which side the PHY, the MCU and the magnetics sit on.

The brief places the sensors on the isolated low-voltage side but does not state the domain of the PHY/MCU or where the barrier cuts the floorplan.

*Decision:* **not yet made.**

### OPEN-07 — Isolation target: working voltage, the safety or insulation standard being met, and the resulting creepage and clearance distances, keepout width and any slot/cutout.

The brief requires that isolation spacing be respected but names no voltage, no standard and no dimension.

*Decision:* **not yet made.**

### OPEN-08 — Magnetics arrangement: integrated magjack versus discrete magnetics with a separate RJ45, and how PoE power is tapped (centre-tap access, current rating, termination network).

The brief only requires an arrangement "appropriate to PoE" and names no part or configuration.

*Decision:* **not yet made.**

### OPEN-09 — Ethernet PHY selection, the MAC interface (and whether the MAC lives in the MCU or a separate device), reference-clock source and strapping/management interface.

The brief names "Ethernet PHY/MCU" as a block with no device, interface or clocking specified.

*Decision:* **not yet made.**

### OPEN-10 — MCU selection: architecture, memory, package, peripheral set and how it is provisioned (MAC address, firmware, bootloader).

The brief names an MCU only as a block, with no family, vendor or capability stated.

*Decision:* **not yet made.**

### OPEN-11 — Sensor interface definition: how many connectors "several" means, connector type and pinout, the bus or signal type used, and whether sensor power is provided.

The brief gives a vague quantity and calls the sensors "low-speed" without naming a protocol, connector or count.

*Decision:* **not yet made.**

### OPEN-12 — Stackup and impedance: layer assignment, dielectric and copper thicknesses, reference planes, and the trace geometry that hits the 100BASE-TX differential target, plus whether controlled impedance is ordered.

Metadata gives 4 as a likely layer count only; the brief states no stackup, no dielectric and no impedance number.

*Decision:* **not yet made.**

### OPEN-13 — Grounding strategy: primary/secondary/chassis ground definitions, any Y-capacitor or stitching across the barrier, and how the shield and RJ45 termination network connect.

The brief is silent on grounding beyond requiring isolation spacing and noise separation.

*Decision:* **not yet made.**

### OPEN-14 — Transient protection strategy on the RJ45, the PoE input and the sensor connectors, and any surge or ESD level targeted.

The brief does not mention protection, ESD or surge at all; the exposure is inherent to a cable-connected PoE node, so the level and approach are the design's to set.

*Decision:* **not yet made.**

### OPEN-15 — Thermal design: dissipation budget and copper/airflow strategy for the PD hot-swap element, the converter switch and the magnetics, and the ambient assumed.

The brief states no ambient, enclosure, power dissipation or thermal requirement.

*Decision:* **not yet made.**

### OPEN-16 — EMC approach: common-mode chokes, filtering, switching-node containment and any conducted/radiated emissions target.

The brief flags flyback noise as a placement concern but sets no emissions target or filtering requirement.

*Decision:* **not yet made.**

### OPEN-17 — Board outline, dimensions, connector edge placement, mounting holes and any enclosure or panelization assumption.

The brief states no mechanical constraint of any kind.

*Decision:* **not yet made.**

### OPEN-18 — Test and bring-up provisions: debug/programming access, test points, link/status indication, and how the isolated side is exercised safely in production test.

The brief specifies no test, debug or indicator requirement.

*Decision:* **not yet made.**

## Where a decision gets recorded

1. Set `chosen` and `rationale` on the matching entry in
   [requirements.json](requirements.json). **That file is the authoritative
   record**, and the only one the benchmark's scripts read: a decision written
   only in prose is invisible to `board_status.py` and to any result that
   counts how many decisions an attempt actually made.
2. Answer it under its `OPEN-nn` heading here as well, with the reasoning and
   the evidence that made the choice. This file is the readable copy; where the
   two disagree, the JSON is what happened.
3. Cite the datasheet or standard in [docs/sources.md](../docs/sources.md).

A choice recorded this way stays visibly a choice. That is what lets a later
reader tell this board's engineering apart from its brief.

## Where this board is most likely to be faked

Places where a design run would be tempted to assert something it cannot
substantiate:

- Isolation distances asserted as a number with no cited working voltage, pollution degree or standard clause. The brief demands respected spacing and supplies no figure — inventing "8 mm" is exactly the failure mode this board is built to catch.
- PoE power budget fabricated. The brief names 802.3af but no class, no rails and no load; a design that states an available wattage without deriving it from the standard and its own load tally is asserting a requirement the user never gave.
- Secondary rail voltages invented. Nothing in the brief states a rail; any 3.3 V / 5 V assumption is a design decision that must be recorded as such, not presented as given.
- "Kept away from PHY analog circuitry" claimed as satisfied without showing the primary switching loop, the return-current path, or the actual separation achieved. Distance on a placement drawing is not the same as a return path that does not share copper with the PHY.
- Differential impedance quoted without a stackup. The 100BASE-TX target means nothing until layer thicknesses, dielectric and trace geometry are chosen and the fabricator confirms it.
- The magnetics choice glossed over. PoE power extraction depends on centre taps that exist and are current-rated; a magjack picked for footprint convenience may not support the PD path at all.
- Four layers treated as a fixed given rather than metadata's "likely" count, then never re-checked against the isolation slot, the barrier keepout and the impedance target competing for the same stackup.
- "Several" sensors quietly converted into a specific number, connector and bus without flagging that the brief left all three open; likewise a board outline or size assumed, when the brief states no mechanical constraint at all.
