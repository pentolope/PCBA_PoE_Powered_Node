# PCBA_PoE_Powered_Node — PoE-Powered Ethernet Sensor Node
## Design brief

Create a 100BASE-TX Ethernet sensor node powered only through IEEE 802.3af PoE. Include the PoE PD interface, isolated DC/DC conversion, Ethernet PHY/MCU, and connectors for several low-speed sensors on the isolated low-voltage side. Use an RJ45/magnetics arrangement appropriate to PoE. The board must respect isolation spacing around the DC/DC barrier and keep noisy flyback switching currents away from PHY analog circuitry.

## PoE powered-device interface

- Valid 802.3af detection signature at the PI; power accepted on Alternative A or B, either polarity.
- Operates across the standard's full PD input range (nominally 37–57 V) and survives maximum port voltage.
- Class signature matches the declared class; drawn power stays inside that class's limit in every state, not just on average.
- Maintain-power signature holds the port up in every firmware state; inrush and input capacitance stay inside the PD limits.

## Isolated conversion and rails

- No DC path, ground bond, shield or mounting hole connects PI-side return to secondary return.
- Secondary rails hold their tolerance across the PD input range and the step from all sensors idle to all active.
- Noise on the PHY analog rail stays inside the PHY's limit at its pins; a slow PSE ramp or brown-out ends in a clean reset.

## Isolation barrier

- No copper, plane, trace, via or fill crosses the barrier on any layer; only the transformer and the deliberate coupling parts do.
- Spacing and bridging parts meet at least the isolation 802.3 requires of a PD: 1500 V rms, 60 s, PI to other accessible conductors.
- Test points on PD input, converter output and each rail, and a marked probe reference each side of the barrier.

## Ethernet and sensor interfaces

- The RJ45/magnetics arrangement taps power from centre taps rated for the class's DC bias without saturating, and its shield scheme does not defeat the barrier.
- MDI pairs are 100 Ω differential, matched within pair, short between magnetics and jack, with cable-side terminations rated for PoE voltages.
- Sensor connectors sit wholly on the isolated side, number more than one, and each supplies a current-limited rail counted in the PD budget.

## Layout and noise separation

- Primary switching loop and secondary rectifier loop are each small and closed locally, and neither overlaps nor sits under the PHY analog section or the MDI.
- PHY analog supply, bias reference and reference clock sit away from the converter and its magnetics, with no switching node over or under them.
- Nothing routes under the flyback transformer or the magnetics, and the reference clock meets the ±0.01% baud tolerance 100BASE-X requires.

## Open choices

- MCU, PHY, and the interface between them.
- Whether PD front end, hot-swap switch and controller are one device or several, and the isolated feedback method.
- The class to declare, which follows from the measured worst-case budget.
- Integrated-magnetics jack or separate magnetics; rail count and voltages; sensor connector family and count.
