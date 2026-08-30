# Architecture — PoE-Powered Ethernet Sensor Node

**A worksheet, not a design.** Every line below is a question this board has to
answer, and none of them is answered here. Nothing in this file is a
recommendation, and the order of the sections carries no preference.

The questions were derived from [the brief](../BRIEF.md) and from what this
board is meant to stress in the benchmark:

- PoE front end
- isolation barrier
- flyback transformer
- Ethernet routing

Those are the places where a wrong answer shows up in copper.

Answer them in this file as the design is made, each answer carrying the
evidence that supports it, and record the corresponding choice against its
`OPEN-nn` entry in [board/requirements.md](../board/requirements.md). An answer
without evidence is a guess wearing a document's clothes — and this benchmark is
allowed to refuse an unsupported claim rather than invent one.

## PoE PD front end (IEEE 802.3af)

- Which 802.3af class does this node declare, and what load tally justifies that class rather than a lower or higher one?
- How is the detection signature presented, and how is the classification signature formed and removed?
- Which feed alternatives (A, B, or both) and which pair-set polarities does the input accept, and what implements that?
- What limits inrush at PD power-up, and what is the hot-swap element's worst-case dissipation during that event?
- What is the assumed PI voltage range at the node's input, and does every downstream block still operate at the bottom of it?
- Which parts of the front end sit in the non-isolated domain, and where does that domain end?

## Isolation barrier definition

- What working voltage is the barrier rated for, and which insulation standard or clause is the design meeting?
- What creepage and clearance numbers follow from that rating, and from which cited table?
- Is the barrier implemented as a keepout band, a routed slot, or both, and how wide?
- Which components straddle the barrier (transformer, feedback device, Y-capacitor), and does each one's own datasheet isolation rating meet or exceed the board target?
- Does any copper, silkscreen, via, test point or mounting hardware violate the barrier on any layer?
- How is the barrier checked mechanically — is there a rule or a DRC constraint that will catch a later violation?

## Isolated DC/DC converter

- What secondary rails, at what voltage and current, does the rest of the board actually need, and how was that budget built?
- What converter topology is chosen, and how does it relate to the flyback switching currents the brief's noise constraint names?
- What controller, transformer, turns ratio and switching frequency are chosen, and what evidence supports the transformer's power handling and isolation rating?
- How does regulation information cross the barrier, and what is the stability story for that loop?
- Where does the primary switching-node loop (switch, sense, clamp/snubber, input capacitance) run, what is its enclosed area, and what target was set for it?
- What clamps the leakage-inductance spike, and what does that cost in dissipation?
- Does the converter start and stay in regulation across the full assumed input range and the worst-case load step?

## Ethernet magnetics, RJ45 and the PoE power tap

- Integrated magjack or discrete magnetics plus a separate RJ45 — what drives that choice for this board?
- Do the chosen magnetics expose usable centre taps, and are those taps rated for the PD current this node draws?
- How is the PoE power tapped from the pairs, and what path does that current take on the board?
- What termination and common-mode network sits on the cable side, and how is the connector shield treated?
- What isolation voltage do the magnetics themselves provide between cable side and PHY side, and does that satisfy the cable-facing requirement independently of the DC/DC barrier?

## Ethernet PHY, MAC and MCU

- Which MAC interface connects PHY and MCU, and does the MCU integrate the MAC or is a separate controller needed?
- What is the PHY reference-clock source, and what accuracy does 100BASE-TX demand of it?
- How are PHY straps, management interface, reset and power sequencing handled without conflicting with normal I/O use?
- What does the MCU need in terms of memory, peripherals and pin count to serve both Ethernet and the sensor interfaces?
- How is the node provisioned — MAC address, firmware load, first bring-up — and what hardware access does that require?

## 100BASE-TX signal integrity and routing

- What differential impedance target applies to the MDI pairs, and what stackup geometry achieves it on this board?
- What length do the PHY-to-magnetics and magnetics-to-RJ45 runs come out at, and what makes those lengths defensible?
- What reference plane sits under the MDI pairs along their whole length, and are there any plane splits or barrier gaps crossed?
- How are the pairs matched intra-pair, and what spacing separates them from each other and from anything else?
- Is any part of the MDI path routed near the converter switching node, the transformer, or their return currents?
- What is the keepout policy under and around the magnetics?

## Sensor interfaces on the isolated low-voltage side

- How many sensor connectors are provided, and what makes that number the right reading of "several"?
- What bus or signal type do the low-speed sensors use, and is it uniform across connectors?
- What connector type and pinout is used, and is the pinout keyed or otherwise protected against reversed insertion?
- Is power supplied to the sensors, at what rail and with what per-connector current limit or protection?
- How long are the sensor cables assumed to be, and does the interface choice survive that length?
- What protects these connectors from ESD and miswiring, given they leave the board?

## Grounding, return paths and noise partitioning

- What ground domains exist (PoE/primary, isolated secondary, chassis/shield), and where is each one's boundary drawn?
- Is anything intentionally coupled across the barrier — a Y-capacitor, a resistor — and what is the justification and rating?
- Where does the converter primary return current physically flow, and does any part of that loop share copper or a plane region with PHY analog circuitry?
- Where does the PD current returning from the magnetics centre taps flow, and does it pass under the PHY?
- How is the PHY's analog supply and its termination reference decoupled and referenced?
- What separates the switching-node copper from anything sensitive — distance, a plane, a guard, or a layer?

## Stackup, floorplan and mechanical

- What is the actual layer count and stackup, and do the isolation barrier and the MDI impedance target both survive it?
- How is the board divided into PoE/primary, converter, PHY/Ethernet and sensor regions, and does that division put the barrier in one clean line?
- Where do the RJ45 and the sensor connectors sit relative to the board edge and to each other?
- What board outline, dimensions and mounting provisions are chosen, and what enclosure or keepout assumption drives them?
- Does the fabricator support the minimum trace/space, slot width and controlled-impedance stackup this design needs at this layer count?

## Protection, EMC and thermal

- What ESD and surge levels are targeted on the cable-facing side, and what implements that without loading the MDI pairs?
- What filtering or common-mode suppression is applied to the PoE input and the converter, and against what emissions target?
- Which components dissipate the most power, at worst case, and what copper area or airflow removes that heat?
- What is the assumed ambient, and does every part stay inside its rating there?
- Does the switching frequency or its harmonics land anywhere that matters for this node's own analog circuitry?

## Bring-up, test and manufacturability

- How is the board powered and debugged during bring-up, given the brief powers it only through PoE?
- What test points exist, and how are the isolated and non-isolated sides probed without bridging the barrier?
- What is the production test sequence — PD negotiation, rail check, link-up, sensor enumeration — and what fixture does it need?
- Is there link/status indication, and on which side of the barrier does it live?
- What DFM constraints (component spacing near the barrier, connector retention, panelization) does the assembly process impose?

## Answers still owed

All of them. See [status.md](status.md).
