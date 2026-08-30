# PCBA_PoE_Powered_Node — PoE-Powered Ethernet Sensor Node

**Benchmark ID:** 19  
**Difficulty:** 4/5  
**Brief detail:** 3/5  
**Category:** isolated-power-networking  
**Likely layer count:** 4  
**Primary stressors:** PoE front end, isolation barrier, flyback transformer, Ethernet routing

## Design brief

Create a 100BASE-TX Ethernet sensor node powered only through IEEE 802.3af PoE. Include the PoE PD interface, isolated DC/DC conversion, Ethernet PHY/MCU, and connectors for several low-speed sensors on the isolated low-voltage side. Use an RJ45/magnetics arrangement appropriate to PoE. The board must respect isolation spacing around the DC/DC barrier and keep noisy flyback switching currents away from PHY analog circuitry.

## Benchmark intent

This brief is intentionally one member of a heterogeneous PCBA-autodesign benchmark. Treat stated requirements as authoritative; where the brief leaves choices open, make and document reasonable engineering decisions rather than inventing hidden user requirements. The repository should remain a consumer of the shared `PCBA_AutoDesignAndTest` toolkit rather than accumulating board-specific logic in the toolkit.
