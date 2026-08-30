# PoE-Powered Ethernet Sensor Node

A 100BASE-TX Ethernet sensor node powered only through IEEE 802.3af PoE, with an isolated DC/DC barrier and low-speed sensor connectors.

This repository holds the design problem for a **100BASE-TX Ethernet sensor node powered only through IEEE 802.3af PoE** — no other power input is named. The brief fixes the functional blocks (PoE PD interface, isolated DC/DC conversion, Ethernet PHY plus MCU, and connectors for several low-speed sensors on the isolated low-voltage side), requires an RJ45/magnetics arrangement appropriate to PoE, and imposes two placement-level constraints: respect isolation spacing around the DC/DC barrier, and keep noisy flyback switching currents away from PHY analog circuitry.

Everything else is design freedom. No part, vendor, package, converter controller, transformer, PHY, MCU, connector, sensor bus, rail voltage, power budget, isolation rating, board outline, or stackup is fixed by the brief; the metadata only says 4 layers is the *likely* count. The sensor quantity is stated as "several", not as a number. The design agent is expected to make and document those decisions here rather than treat any of them as pre-existing user requirements.

> **This board has not been designed.** There is no schematic, no layout and no
> part selection here — only the brief, a reading of the brief, and the
> scaffolding a design run needs. That is the intended state of this repository,
> not a gap in it.

## What the brief fixes, and what it leaves open

The brief pins down 13 requirements and deliberately leaves
18 decisions to whoever designs the board. The `Source` column says
which is which: `brief` is quoted from [BRIEF.md](BRIEF.md), `metadata` comes
from the benchmark catalogue, and `open` means the brief does not fix it.

| Aspect | Value | Source |
|---|---|---|
| Board function | 100BASE-TX Ethernet sensor node | brief |
| Power source | IEEE 802.3af PoE only — the brief names no other power input | brief |
| PoE PD interface | Required as a functional block; implementation unspecified | brief |
| Isolated DC/DC conversion | Required as a functional block; no controller, transformer, turns ratio or operating point is named | brief |
| Ethernet front end | Ethernet PHY plus MCU; no device, MAC interface or clocking named | brief |
| Connector / magnetics arrangement | RJ45 and magnetics, arrangement appropriate to PoE; integrated vs discrete not stated | brief |
| Sensor interfaces | Connectors for several low-speed sensors on the isolated low-voltage side; "several" is not a number and no bus is named | brief |
| Isolation spacing | Must be respected around the DC/DC barrier; no working voltage, creepage/clearance figure or safety standard is named | brief |
| Noise partitioning constraint | Flyback switching currents must be kept away from PHY analog circuitry — the brief's own wording is where "flyback" enters the design | brief |
| Likely layer count | 4 | metadata |
| Benchmark class | isolated-power-networking; difficulty 4/5; brief detail 3/5 | metadata |
| Primary stressors | PoE front end, isolation barrier, flyback transformer, Ethernet routing | metadata |
| Board outline, size and mounting | Not fixed by the brief — design agent's choice | open |
| Part selection (PD controller, transformer, PHY, MCU, connectors) and all rail voltages/currents | Not fixed by the brief — design agent's choice, to be decided and documented here | open |

The full split, with the verbatim brief text substantiating every fixed
requirement, is in [board/requirements.md](board/requirements.md) and
machine-readably in [board/requirements.json](board/requirements.json).

**Missing details are design freedom, not permission to fabricate unstated user
requirements.** A choice the brief left open is recorded as a decision, with its
reasoning — never promoted into a requirement.

## Benchmark position

| | |
|---|---|
| Benchmark id | 19 of 32 |
| Category | isolated-power-networking |
| Difficulty | 4 / 5 |
| Brief detail | 3 / 5 |
| Likely layer count | 4 |
| Primary stressors | PoE front end, isolation barrier, flyback transformer, Ethernet routing |

A difficulty-4, detail-3 board in the `isolated-power-networking` category: the brief states real architectural intent (PoE PD front end, an isolation barrier, flyback switching, Ethernet routing) but no numbers, so it tests whether an agent can derive a power budget, an isolation clearance target and a differential-pair stackup from cited standards and vendor data instead of asserting them. The four named stressors all converge on one floorplan problem — a PoE/flyback primary domain and a sensitive 100BASE-TX analog domain must coexist on the same board with a real barrier between them, and the brief states no outline, area or mechanical constraint at all, so the floorplan itself is the agent's to derive. It also tests restraint: the brief's silence on parts, rails, connectors, sensor count and outline is the main opportunity to fabricate requirements.

This repository is one of thirty-two. The suite, the protocol and the results
live in [PCBA_AutoDesignAndTest_Bench](https://github.com/pentolope/PCBA_AutoDesignAndTest_Bench).

## Repository layout

| Path | Contents |
|---|---|
| `BRIEF.md` | the supplied brief — authoritative, preserved byte for byte, never edited |
| `board/requirements.md` | what the brief fixes, what it leaves open, and where decisions get recorded |
| `board/requirements.json` | the same split, machine-readable, each fixed requirement bound to brief text |
| `board/manifest.template.json` | the toolkit's minimum manifest, pre-filled for this board |
| `board/toolchain.json` | where this board's build finds KiCad and the router |
| `benchmark/metadata.json` | the supplied catalogue entry — category, difficulty, detail, stressors |
| `docs/architecture.md` | the decisions this board must make, as questions, unanswered |
| `docs/sources.md` | the classes of evidence the design will have to cite |
| `docs/status.md` | what exists, what does not, and what is deliberately absent |
| `candidates/` | disposable search output, ignored by Git |
| `.claude/skills/` | the accountability-review skill [CLAUDE.md](CLAUDE.md) requires before a push |
| `tooling/PCBA_AutoDesignAndTest` | the shared verification/routing/release toolkit, as a pinned submodule |

## Getting the repository

The toolkit is a submodule and carries KiCad Routing Tools as a submodule of its
own, so clone recursively:

```bash
git clone --recursive https://github.com/pentolope/PCBA_PoE_Powered_Node.git
```

```bash
git submodule update --init --recursive
```

## Designing the board

Generic verification, routing and release logic is **not** written here. It is
consumed from `tooling/PCBA_AutoDesignAndTest`, which is board-agnostic by
construction and must stay that way; this repository owns the board and nothing
else. Start from
[the toolkit's onboarding guide](tooling/PCBA_AutoDesignAndTest/examples/onboarding.md),
and see [CLAUDE.md](CLAUDE.md) for the rules a design run works under.

```bash
python3 tooling/PCBA_AutoDesignAndTest/run.py preflight
```

## Brief integrity

`BRIEF.md` SHA-256 `5aaef1f5b82b3cc6e3575debcd27f63c86640ce9896bf7c6ec77589cd4469c4e`

Every quotation in `board/requirements.json` is bound to those exact bytes. If
the brief ever changes, the bindings are stale by construction — which is the
point of recording the digest.
