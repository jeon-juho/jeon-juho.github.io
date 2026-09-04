---
title: "Digitally Reconfigurable Resolution Multi-Bit-per-Cycle SAR ADC: Design Trade-off Considerations"
collection: publications
category: conferences
permalink: /publication/2026-tencon-reconfigurable-sar-adc
excerpt: 'A 28 nm CMOS SAR ADC whose resolution is reconfigurable from 5 to 9 bits entirely through digital logic, with no switches added to the analog signal path — 8.31 ENOB at 1.4 GS/s and 23.8 fJ/conversion-step in 9b mode.'
date: 2026-10-01
venue: 'IEEE Region 10 Conference (TENCON)'
citation: 'J. Jeon and C. P. Yue, &quot;Digitally Reconfigurable Resolution Multi-Bit-per-Cycle SAR ADC: Design Trade-off Considerations,&quot; <i>IEEE Region 10 Conference (TENCON) 2026</i>, accepted.'
---

**Juho Jeon** and **Chik Patrick Yue**, Department of Electronic and Computer Engineering, HKUST.

## Abstract

This paper presents a 28 nm CMOS resolution-reconfigurable successive approximation register
(SAR) analog-to-digital converter (ADC) supporting five resolution modes from 5 bits to 9 bits.
Resolution reconfigurability is achieved entirely through digital logic control, without
disconnecting any capacitors in the digital-to-analog converter (DAC), preserving high-speed
capability. Building on the 1-then-2b/cycle conversion scheme, the proposed design chooses the
number of bits converted per cycle depending on the resolution mode. A reconfigurable SAR logic
with enable-gated DAC switching logic and a mode-aware decoder enables seamless switching between
resolution modes by toggling a 4-bit mode control word. The design operates with a 0.9 V supply
and is verified through partially post-layout (cell-based) simulation, with the DAC and comparator
blocks confirmed using post-layout extracted netlists. In 9-bit mode, the ADC achieves a
signal-to-noise-and-distortion ratio (SNDR) of 51.84 dB at Nyquist, with an effective number of
bits (ENOB) of 8.31 bits, a Walden figure of merit of 23.8 fJ/conversion-step, and a Schreier
figure of merit of 160 dB, at a total sampling rate of 1.4 GS/s.

*Index terms* — SAR ADC, reconfigurable resolution, 1-then-2b/cycle SAR ADC, multi-bit-per-cycle
SAR ADC.

## Contributions

* A digitally reconfigurable resolution scheme for 1-then-2b/cycle SAR ADCs that introduces no
  analog switching elements, preserving GS/s-class operation across all modes.
* An enable-gated DAC switching logic and mode-aware decoder that supports five resolution modes
  via a 4-bit control word, with mode switching taking effect from the immediately subsequent
  conversion cycle.
* A quantitative analysis of the high-resolution-limited trade-offs in power efficiency across
  resolution modes, with explicit identification of the dominant loss mechanisms.

The design, the figures and a fuller walkthrough of the results are on the
[project page](/portfolio/reconfigurable-sar-adc/).
