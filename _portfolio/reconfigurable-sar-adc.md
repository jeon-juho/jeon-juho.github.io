---
title: "Digitally Reconfigurable 5b–9b Multi-Bit-per-Cycle SAR ADC"
excerpt: "<b>28 nm CMOS &middot; 1.4 GS/s &middot; 8.31 ENOB &middot; 23.8 fJ/conv.-step</b><br/>MPhil thesis. Five resolution modes (5b&ndash;9b) selected purely in digital logic, with no switches added to the analog signal path. Accepted at IEEE TENCON 2026.<br/><img src='/images/portfolio/reconfigurable-sar-adc/01-architecture-timing.png' style='max-width:560px;width:100%;margin-top:0.75em' alt=''>"
collection: portfolio
sort_order: 1
header:
  teaser: portfolio/reconfigurable-sar-adc/01-architecture-timing.png
---

* **Context**: MPhil thesis, HKUST — advisor Prof. Chik Patrick Yue
* **Technology**: 28 nm CMOS, 0.9 V supply
* **Verification**: Post-layout extracted netlists for the capacitive DAC and comparator; schematic level for SAR logic, sampling switch and clock network
* **Outcome**: Accepted for presentation at [IEEE TENCON 2026](/publication/2026-tencon-reconfigurable-sar-adc)
* **My role**: Sole designer — architecture, circuit design, layout of the DAC and comparator, simulation and analysis

## The problem

Wireline receivers have to serve many coexisting standards, and providers commonly ship a separate
SerDes IP block per standard. A single ADC that can trade bandwidth, resolution and power on demand
would collapse that portfolio into one block.

Prior resolution-reconfigurable SAR ADCs switch resolution by **disconnecting MSB capacitors in the
DAC**. The on-resistance of those switches degrades settling accuracy, which confines the technique
to relatively slow, high-precision converters in older nodes. For gigahertz-rate wireline work in an
advanced node, something else is needed.

**This design makes resolution a purely digital decision.** The capacitive DAC array is never
structurally altered and no switch is inserted into the signal path, so the GS/s-class speed of the
underlying 1-then-2b/cycle converter survives in every mode.

## Architecture

The ADC is 2× time-interleaved. Each channel holds four 7-bit capacitive DACs (DAC1P/1N/2P/2N) and
three comparators, with one shared SAR control logic block generating the digital output word.
Resolution is selected by a 4-bit mode word: in 9b mode a conversion runs SAM-1b-2b-2b-2b-2b, and
lower modes suppress LSB-group decisions — 5b mode compresses to SAM-1b-2b-2b. Changing modes
touches nothing analog.

<figure>
  <img src="/images/portfolio/reconfigurable-sar-adc/01-architecture-timing.png" alt="Proposed architecture and per-mode timing diagrams" loading="lazy">
  <figcaption>Proposed architecture of the resolution-reconfigurable 1-then-2b/cycle SAR ADC (a) and the timing diagram for each of the five resolution modes (b).</figcaption>
</figure>

## What makes it reconfigurable

Reconfigurability comes from augmenting the standard DAC switching logic with an **enable (EN)**
signal. Of the seven switching-logic blocks, three keep conventional operation and four are gated by
an EN encoder that decodes the 4-bit mode word and asserts enables only for the active bit range. In
9b mode B8–B0 are all live; in 5b mode B4 becomes the LSB and the lower four blocks are disabled.
The scheme adds no load to the capacitive DAC during operation.

The **register mux (RMUX) with enable** resets at each sampling event, gated by the enable signal,
and holds its output high or low based on the comparator decision at that cycle — so unused LSB
outputs are suppressed cleanly instead of propagating indeterminate values. The output-path decoder
remaps the thermometer-to-binary conversion and bit ordering per mode, keeping MSB and LSB positions
aligned in the output word.

<figure>
  <img src="/images/portfolio/reconfigurable-sar-adc/02-dac-switching-rmux.png" alt="Enable-gated DAC switching architecture and register mux with enable" loading="lazy">
  <figcaption>Proposed DAC switching architecture with the EN encoder (a), and the register mux (RMUX) with enable (b).</figcaption>
</figure>

## Capacitive DAC

The unit capacitance C<sub>U</sub> = 0.5 fF is set by the kT/C noise floor of the *highest*
resolution mode. Because one array is shared by every mode, that choice creates a deliberate excess
capacitance at low resolution — the central trade-off this work sets out to quantify. The figure
below builds the argument with binary-weighted demonstration arrays before showing the non-binary
7-bit structure actually used, realised with 0.5 fF fringe capacitors for their matching and charge
density.

<figure>
  <img src="/images/portfolio/reconfigurable-sar-adc/03-dac-array-comparison.png" alt="Comparison of dedicated and reconfigurable capacitive DAC arrays" loading="lazy">
  <figcaption>Capacitive DAC arrays: (a) dedicated 3b DAC, (b) dedicated 7b DAC, (c) reconfigurable DAC in 3b mode with the lower four capacitors grounded, (d) reconfigurable DAC in 7b mode, and (e) the actual non-binary DAC structure of the proposed design.</figcaption>
</figure>

## Comparator

The comparator is a preamplifier followed by a strong-arm latch. The preamplifier lets the latch
transistors be sized smaller without exposing the capacitive DAC nodes directly to latch kickback —
important because DAC1N sees kickback from two comparators within a single conversion cycle. The
constraint is tightest in 9b mode, where 0.5 LSB is about 0.9 mV on a 0.9 V supply. Standalone at
1 GS/s in 9b mode the comparator burns 21.9 µW, roughly 74 % of it in the preamplifier.

<figure>
  <img src="/images/portfolio/reconfigurable-sar-adc/04-comparator-kickback.png" alt="Comparator schematic with preamplifier and latch" loading="lazy">
  <figcaption>Proposed comparator (preamplifier + strong-arm latch) and the kickback noise paths into the capacitive DAC nodes.</figcaption>
</figure>

<figure>
  <img src="/images/portfolio/reconfigurable-sar-adc/05-layout-dac-comparator.png" alt="Layout of the capacitive DAC and comparator" loading="lazy">
  <figcaption>Layout view of the capacitive DAC (a) and the comparator (b). These blocks were simulated from post-layout extracted netlists including parasitic R and C.</figcaption>
</figure>

## Results

<figure>
  <img src="/images/portfolio/reconfigurable-sar-adc/06-fft-all-modes.png" alt="FFT spectra across all five resolution modes" loading="lazy">
  <figcaption>Simulated Nyquist-rate FFT spectra across all five resolution modes. The noise floor drops progressively from 5b to 9b, and harmonic spurs become more distinct as the linearity requirement of the high-resolution-optimized DAC and comparator tightens.</figcaption>
</figure>

| Mode | Speed | Power | SNDR | ENOB | SFDR | FoM<sub>W</sub> | FoM<sub>S</sub> |
|---|---|---|---|---|---|---|---|
| 5b | 2.2 GS/s | 11.12 mW | 29.34 dB | 4.58 b | 39.27 dB | 211 fJ/c.-s. | 139 dB |
| 6b | 1.6 GS/s | 9.33 mW | 32.87 dB | 5.17 b | 44.78 dB | 162 fJ/c.-s. | 142 dB |
| 7b | 1.6 GS/s | 9.74 mW | 39.03 dB | 6.19 b | 53.25 dB | 83.4 fJ/c.-s. | 148 dB |
| 8b | 1.4 GS/s | 9.38 mW | 40.76 dB | 6.48 b | 55.70 dB | 75.1 fJ/c.-s. | 149 dB |
| **9b** | **1.4 GS/s** | **10.41 mW** | **51.84 dB** | **8.31 b** | **66.08 dB** | **23.8 fJ/c.-s.** | **160 dB** |

In 9b mode the design has the best Walden FoM among the compared prior art operating above
0.5 GS/s per channel, at a Schreier FoM competitive with the state of the art for multi-bit-per-cycle
SAR ADCs.

## The trade-off, quantified

FoM<sub>W</sub> degrades monotonically as resolution drops — roughly **9× from 9b to 5b**. Rather
than hide that, the paper isolates the two dominant mechanisms:

1. **DAC sizing.** Total capacitance is fixed by the 9b noise target, so low-resolution modes pay
   about 16× excess switching energy.
2. **Comparator design.** The preamplifier exists to meet the 9b kickback requirement and must stay
   on in every mode, becoming fixed overhead where it would otherwise be unnecessary.

These are the inherent cost of sharing hardware across a wide resolution range without analog
reconfiguration — the quantitative counterpart to the "no switches in the signal path" benefit.

<figure>
  <img src="/images/portfolio/reconfigurable-sar-adc/07-fom-vs-prior-art.png" alt="Walden and Schreier figure of merit across resolution modes against prior art" loading="lazy">
  <figcaption>Walden FoM<sub>W</sub> and Schreier FoM<sub>S</sub> across resolution modes, plotted against selected prior art from the ISSCC/VLSI ADC survey.</figcaption>
</figure>

## Known limits and next steps

Foreground offset calibration is applied per channel via a shift-register-controlled R2R DAC; **gain
mismatch and timing skew are not calibrated**, and their quantitative impact on SNDR is not
characterized in this simulation-based work. The 0.5 fF fringe capacitor mismatch figure is taken
from a 90 nm characterization; a dedicated Monte Carlo analysis in 28 nm remains future work.
