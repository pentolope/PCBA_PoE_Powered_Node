# Sources — PoE-Powered Ethernet Sensor Node

The evidence this board's design will have to cite. **Classes of document, not
documents:** the specific parts are not chosen yet, so naming a datasheet here
would be choosing one.

A number that reaches the board carries its provenance: source, document id or
URL, retrieval date, units, and the condition it applies under. A number without
that is not evidence, and no live network lookup may change a validation or
release result.

| Kind of source | What the design needs from it |
|---|---|
| IEEE 802.3 PoE clauses (the brief names IEEE 802.3af): PD detection and classification signatures, PI voltage range, power limits, Alternative A/B pair usage | The brief pins the power source to 802.3af, so the power budget, class behaviour and input voltage range must be quoted from the standard rather than assumed. |
| IEEE 802.3 100BASE-TX / PMD clauses: MDI signalling, return loss and termination expectations | The brief fixes 100BASE-TX; the routing and termination requirements derive from the standard, not from designer preference. |
| PD controller / hot-swap device datasheet: signature behaviour, class programming, inrush limiting, SOA and thermal data | The PoE front end's compliance and its worst-case dissipation are device-specific and must be cited from the chosen part. |
| Controller and power-switch datasheets for the converter topology chosen: operating range, current limit, switching frequency, package thermal resistance | The converter operating point and dissipation claims need device data behind them, whatever topology the design settles on. |
| Isolation transformer datasheet: power rating, turns ratio, leakage inductance, isolation voltage and pin-to-pin creepage | The barrier rating is only as good as the transformer's own rating, and the leakage spike drives the clamp design. |
| Ethernet magnetics / magjack datasheet: turns ratio, centre-tap DC current rating, common-mode rejection, hipot isolation voltage | The brief requires an arrangement appropriate to PoE, which turns on whether the magnetics can carry PD current on their centre taps. |
| Ethernet PHY datasheet and layout application note: MDI termination, reference-clock accuracy, MAC interface timing, strapping and power sequencing | PHY analog behaviour and its layout keepouts are the thing the flyback noise constraint is protecting. |
| MCU datasheet: peripheral and pin capability, MAC availability, package and thermal data, supply requirements | The brief names an MCU as a block; every capability claim about it must come from its own datasheet. |
| Insulation coordination clearance/creepage tables from a recognised safety standard, at the chosen working voltage and pollution degree | The brief requires isolation spacing but names no number; the distance must be derived from a cited table, not chosen. |
| Datasheet for whatever device carries feedback or signalling across the barrier (optocoupler, digital isolator, auxiliary winding): working voltage, transient immunity, transfer characteristic, package creepage | Whatever crosses the barrier must itself be rated for the barrier, and the crossing method is the design's to choose. |
| Fabricator capability and stackup documentation: minimum trace/space, slot and cutout width, available 4-layer stackups, controlled-impedance tolerances | The impedance target, the isolation slot and the routing density all have to be inside what the chosen fabricator will build. |
| Assembly and DFM capability data: component-to-component spacing, connector retention, courtyard and panelization rules, test-access requirements | A board mixing an RJ45, a wound transformer and fine-pitch digital parts has assembly constraints that must be checked, not assumed. |

## Recording a source, once one is chosen

Replace the class with the actual document — manufacturer, part number, revision
and date — and state the fact taken from it, in the units the document uses.
Keep the class row: it says why the document was needed.

JLCPCB-wide process limits are **not** recorded here. They live in the toolkit's
`profiles/jlcpcb/`, with their own provenance; this board records only its own
tighter targets and its own selected options. A limit copied into two places is
a rival threshold, and the toolkit has a gate that says so.
