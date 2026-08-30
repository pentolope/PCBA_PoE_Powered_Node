# Benchmark entry — board 19 of 32

[metadata.json](metadata.json) is the supplied catalogue entry for this board,
preserved byte for byte from the seed pack. It is the same record that appears
in `boards_index.json` in
[PCBA_AutoDesignAndTest_Bench](https://github.com/pentolope/PCBA_AutoDesignAndTest_Bench), and the two must agree.

| | |
|---|---|
| Repository | `PCBA_PoE_Powered_Node` |
| Board id | `poe_powered_node` |
| Category | isolated-power-networking |
| Difficulty | 4 / 5 |
| Brief detail | 3 / 5 |
| Likely layer count | 4 |
| Primary stressors | PoE front end, isolation barrier, flyback transformer, Ethernet routing |

`difficulty` is how hard the board is. `detail` is how much of it the brief
states — and a low `detail` is not a low bar. A detail-1 brief leaves the
architecture open on purpose, and an agent that fills the silence with invented
user requirements has failed the board more thoroughly than one that designs it
badly.

A difficulty-4, detail-3 board in the `isolated-power-networking` category: the brief states real architectural intent (PoE PD front end, an isolation barrier, flyback switching, Ethernet routing) but no numbers, so it tests whether an agent can derive a power budget, an isolation clearance target and a differential-pair stackup from cited standards and vendor data instead of asserting them. The four named stressors all converge on one floorplan problem — a PoE/flyback primary domain and a sensitive 100BASE-TX analog domain must coexist on the same board with a real barrier between them, and the brief states no outline, area or mechanical constraint at all, so the floorplan itself is the agent's to derive. It also tests restraint: the brief's silence on parts, rails, connectors, sensor count and outline is the main opportunity to fabricate requirements.

## What goes here

Compact results only: metrics, verdicts, and the commit each was measured at.
The evidence for a result is the artefact the toolkit recomputes, not a summary
of it.

Routing search output, candidate pools, build trees and field-solver dumps do
**not** go here. They are ignored by [.gitignore](../.gitignore) and are
regenerated from what is committed. Thirty-two repositories share one benchmark
clone; weight here is paid thirty-two times.

## Protocol

The attempt protocol is defined once, in the umbrella repository, so that
thirty-two boards cannot drift into thirty-two protocols. See
[PCBA_AutoDesignAndTest_Bench/BENCHMARK.md](https://github.com/pentolope/PCBA_AutoDesignAndTest_Bench/blob/main/BENCHMARK.md).
