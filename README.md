# NMR Console — Section A

**Project 3** for *Basic Skills for Experimentalists* (TIGP 2026) — Tee Ren Qian.

The class built one instrument together: a small NMR console on an ESP32-S3. A 2 mT field, a
bottle of water, a pulse at 89 kHz, and the free induction decay that comes back turned into a
spectrum on a phone. This repository presents **Section A — the analog section**: the board work
(3a), the housing (3b), the firmware driver and the phone panel.

**Project site:** https://renqian03.github.io/nmr-console-section-a/

## What is in this repository

This is the *presentation* of the work. The KiCad files themselves live in the class repository,
in my section's folder — this is where the renders, photos, measurements and write-up go.

| Path | What |
|---|---|
| `index.html` | the project website (GitHub Pages serves it from the repository root) |
| `images/` | renders, screenshots and photos |

## Section A — the analog group

Thirteen nets on the front panel, from link header J1 out to the SMA field and the TX coil
terminal:

`AI1`–`AI8` · `AO1` `AO2` · `AUX` · `RX` · `TX`

The front panel is one board routed by four students, divided **by nets rather than by area** —
every panel net runs from a link header at an edge to a connector in the middle, so a geometric
cut would leave half a trace on every boundary.

### The design number

The class coil is 400 turns of AWG26 on a 4 × 10 cm former: L = 2.53 mH, R_DC = 6.7 Ω. Resonated
at 89.4 kHz with 1.25 nF and loaded to Q = 10, it presents **14.2 kΩ** — and that, not the 6.7 Ω
of the wire, is the source impedance the amplifier sees.

| | OPA1656 | OPA1612 |
|---|---|---|
| voltage noise | 2.9 nV/√Hz | **1.1 nV/√Hz** |
| current noise | 6 fA/√Hz | 1.7 pA/√Hz |
| i_n × 14.2 kΩ | 0.09 nV/√Hz | **24.2 nV/√Hz** |
| penalty over the tank's own 15.3 nV/√Hz | **0.15 dB** | 5.4 dB |

The part with less than half the voltage noise is 5.3 dB worse on this tank. The crossover
impedance `e_n / i_n` says why: 483 kΩ for the OPA1656, 647 Ω for the OPA1612, with the tank at
14.2 kΩ sitting below one and above the other.

*"Low noise" is a property of the source impedance, not of the amplifier.*

## Links

- Class board repository: https://github.com/TIGP-Experimental-Methods/class-board-2026
- Class project wall: https://tigp-experimental-methods.github.io/showcase-2026/
- Project 1 — Unfair Golf: https://renqian03.github.io/unfair-golf/
- Project 2 — Glowmeter: https://renqian03.github.io/glowmeter/

## To do

- [ ] Route the 13 nets; DRC clean; 3D render into `images/zone-3d.png`
- [ ] Pull request against the class repository, with the render in the description
- [ ] Write the two section answers into the site in my own words
- [ ] Housing (Project 3b) — renders, CAD export, photos
- [ ] Firmware driver and phone panel; the measured noise floor in LSB rms
- [ ] Card on the class project wall (`project: "3"`)
