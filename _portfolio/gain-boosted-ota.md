---
title: "Gain-Boosted Folded-Cascode Fully-Differential OTA"
excerpt: "<b>90 nm CMOS &middot; 81.6 dB gain &middot; 604 MHz UGF &middot; 1.93 mW</b><br/>Folded-cascode OTA with gain-boosting auxiliary amplifiers and resistive CMFB, sized from a hand-calculated current budget and iterated to spec.<br/><img src='/images/portfolio/gain-boosted-ota/01-main-amplifier.png' width='1231' height='618' style='max-width:560px;width:100%;margin-top:0.75em' alt=''>"
collection: portfolio
sort_order: 4
header:
  teaser: portfolio/gain-boosted-ota/01-main-amplifier.png
---

* **Context**: Advanced Analog IC Design coursework (Prof. Howard Luong), Fall 2024
* **Technology**: 90 nm TSMC CMOS, ±1 V supply
* **Team**: Three-person group project with M. J. Aslam and Y. C. Lau
* **My role**: Design parameter calculation, testbench construction and simulation verification of the schematics

## Specification and outcome

| Parameter | Specification | Hand calculation | Simulation |
|---|---|---|---|
| Power consumption | ≤ 2.0 mW | 1.92 mW | **1.933 mW** |
| Low-frequency gain A<sub>o</sub> | ≥ 80 dB | 80 dB | **81.59 dB** |
| Unity gain frequency f<sub>o</sub> | ≥ 600 MHz | 764 MHz | **604.33 MHz** |
| Slew rate | ≥ 20 V/µs | 80 V/µs | **51 V/µs** |
| Phase margin | ≥ 60° | 60° | **61.49°** |
| CMRR | ≥ 80 dB | 89.54 dB | **103 dB** |
| PSRR (dc) | ≥ 80 dB | — | 27.05 dB |
| DC output | 0 V ± 50 mV | 0 V | **−1.54 mV** |
| Differential output swing | ≥ ±1.2 V | ±1.6 V | **±1.58 V** |
| THD (v<sub>id</sub> = 75 % FS) | ≤ −40 dB | — | **−66 dB** |
| Input offset voltage | ≤ 50 mV | 5.2 mV | **−1.43 mV** |
| Equivalent input noise (1 MHz BW) | ≤ 1 mV<sub>rms</sub> | 5.99 µV<sub>rms</sub> | **6.20 µV<sub>rms</sub>** |

Every specification is met except PSRR, which is discussed below.

## Topology and why

A **folded cascode** main amplifier balances gain against bandwidth while still allowing a large
output swing: PMOS cascode transistors raise output impedance for gain, and NMOS devices in the
signal path keep the swing wide. **Gain-boosting auxiliary amplifiers** (single-stage differential)
add roughly 25 dB on top of the main amplifier's 55 dB without meaningful extra power. Common-mode
feedback is resistor-based with a single-stage amplifier acting as the comparator, which keeps the
CMFB loop simple and cheap.

<figure>
  <img src="/images/portfolio/gain-boosted-ota/01-main-amplifier.png" width="1231" height="618" alt="Main folded-cascode amplifier schematic" loading="lazy">
  <figcaption>Main amplifier: NMOS input differential pair with PMOS tail current source, folded into a cascode output stage.</figcaption>
</figure>

<figure>
  <img src="/images/portfolio/gain-boosted-ota/02-aux-amp-and-cmfb.png" width="1231" height="671" alt="Auxiliary gain-boosting amplifier and CMFB circuit" loading="lazy">
  <figcaption>Gain-boosting auxiliary amplifiers and the resistive common-mode feedback circuit.</figcaption>
</figure>

## Sizing from a current budget

Transistor sizing came from the overdrive-voltage method, W/L = 2I<sub>D</sub>/(µC<sub>ox</sub>V<sub>OD</sub><sup>2</sup>),
driven by three hard constraints:

* **Transconductance.** UGF = g<sub>m</sub>/(2πC<sub>L</sub>) with the specified load sets
  g<sub>m</sub> ≥ 3.77 mS; it was overdesigned to 4.8 mS to absorb the non-dominant pole.
* **Power.** A 2 mW ceiling on a ±1 V supply is a 1000 µA budget, split as 660 µA for the main
  amplifier, 120 µA per p-type auxiliary amplifier, less for the n-type (electron mobility), and the
  same again for CMFB — 1920 µW total.
* **Output swing.** ±1.2 V differential caps the total overdrive of the four stacked cascode devices
  at roughly 400 mV, which 90 nm can supply comfortably.

## Simulation results

<figure>
  <img src="/images/portfolio/gain-boosted-ota/03-open-loop-gain-and-cmrr.png" width="1231" height="295" alt="Open-loop gain and phase, and CMRR" loading="lazy">
  <figcaption>(a) Low-frequency gain, UGF and phase margin — 81.59 dB, 604.33 MHz, 61.49°. (b) Common-mode rejection ratio.</figcaption>
</figure>

<figure>
  <img src="/images/portfolio/gain-boosted-ota/04-psrr-and-input-noise.png" width="1231" height="397" alt="PSRR and equivalent input noise" loading="lazy">
  <figcaption>(c) Power supply rejection ratio. (d) Equivalent input noise, integrating to 6.20 µV<sub>rms</sub> over 1 MHz.</figcaption>
</figure>

<figure>
  <img src="/images/portfolio/gain-boosted-ota/05-thd-fft.png" width="1231" height="208" alt="THD from FFT of transient simulation" loading="lazy">
  <figcaption>FFT of the transient simulation at v<sub>id</sub> = 75 % V<sub>FS</sub>, giving THD = −66.18 dB.</figcaption>
</figure>

## Why the process node changed mid-project

The design started in 180 nm and could not simultaneously satisfy PSRR, phase margin, THD and UGF.
Two things forced the move to 90 nm:

* **Output swing.** In 180 nm the workable overdrive voltage sits around 150–200 mV, which leaves no
  room to hit both the swing target and everything else. In 90 nm, 50–150 mV is usable, and the lower
  threshold voltage also made it easier to keep the auxiliary amplifier transistors in saturation
  under the given bias conditions.
* **Unity-gain frequency.** Longer channels and higher parasitic capacitance in 180 nm cap
  f<sub>T</sub>, and with it the UGF.

The switch also brought its own difficulty: on a ±1 V supply the channel-length modulation parameter
varies strongly with bias, and different models (hvt, lvt) apply depending on each transistor's
V<sub>DS</sub>. Reaching the operating points assumed in hand calculation took several iterations.

## Honest limitation

**PSRR came in at 27 dB against an 80 dB specification** and was never resolved. Every other
specification was met after the node change, which points at either the measurement procedure or the
simple bias circuit as the cause — a more advanced bias circuit would likely improve it. It is the
one part of the project I would want to redo properly.

This OTA was later reused as the transistor-level gm cell in the
[UWB channel-selection filter](/portfolio/gmc-uwb-filter/).
