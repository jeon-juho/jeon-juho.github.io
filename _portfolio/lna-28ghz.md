---
title: "28 GHz Differential Low-Noise Amplifier"
excerpt: "<b>22 nm CMOS &middot; 17.4 dB gain &middot; 1.74 dB NF &middot; 22.8 mW</b><br/>Differential cascode LNA with inductive source and gate degeneration, designed from device characterization through to noise, gain and power circles.<br/><img src='/images/portfolio/lna-28ghz/07-lna-schematic.png' style='max-width:560px;width:100%;margin-top:0.75em' alt=''>"
collection: portfolio
sort_order: 3
header:
  teaser: portfolio/lna-28ghz/07-lna-schematic.png
---

* **Context**: RFIC Design coursework (Prof. Chik Patrick Yue), Spring 2026
* **Technology**: 22 nm TSMC CMOS, 0.9 V supply
* **Topology**: Differential cascode with inductive source and gate degeneration
* **My role**: Sole author

## Device characterization first

Before any amplifier existed, the `nmos_rf_lvt_nw` device (W = 1 µm, L = 30 nm, 4 fingers) was
characterized so the design could start from measured, not assumed, parameters.

<figure>
  <img src="/images/portfolio/lna-28ghz/01-device-testbench.png" alt="RF device characterization testbench" loading="lazy">
  <figcaption>Testbench used to extract the RF characteristics of the device.</figcaption>
</figure>

<figure>
  <img src="/images/portfolio/lna-28ghz/02-device-equivalent-model.png" alt="Six-element equivalent circuit model" loading="lazy">
  <figcaption>Extracted six-element small-signal equivalent circuit model.</figcaption>
</figure>

<figure>
  <img src="/images/portfolio/lna-28ghz/03-nfmin.png" alt="Minimum noise figure versus frequency" loading="lazy">
  <figcaption>Minimum noise figure NF<sub>min</sub> in dB.</figcaption>
</figure>

<figure>
  <img src="/images/portfolio/lna-28ghz/04-h21-ft.png" alt="h21 magnitude giving the transit frequency" loading="lazy">
  <figcaption>|h<sub>21</sub>| versus frequency, giving f<sub>T</sub> = 197 GHz.</figcaption>
</figure>

<figure>
  <img src="/images/portfolio/lna-28ghz/05-gmax-fmax.png" alt="Maximum available power gain" loading="lazy">
  <figcaption>G<sub>max</sub>, the maximum power gain curve, giving f<sub>max</sub> = 202 GHz.</figcaption>
</figure>

## Sizing and bias

Sweeping f<sub>T</sub>, f<sub>max</sub> and NF against current density set the operating point:
**I<sub>den</sub> = 100 µA/µm** gives the minimum NF with acceptable f<sub>T</sub> and f<sub>max</sub>.
With a 15 mW budget on a 0.9 V supply the drain current ceiling is 16.67 mA; I<sub>D</sub> = 12 mA was
chosen for margin, setting the width to 120 µm (M = 30).

<figure>
  <img src="/images/portfolio/lna-28ghz/06-ft-fmax-nf-vs-iden.png" alt="fT, fmax and NF versus current density" loading="lazy">
  <figcaption>f<sub>T</sub>, f<sub>max</sub> and NF versus current density I<sub>den</sub> (µA/µm) — the plot the bias point was chosen from.</figcaption>
</figure>

At 28 GHz the chosen device gives C<sub>gs</sub> = 99.24 fF and g<sub>m</sub> = 109.56 mS. Matching
the real part of Z<sub>in</sub> to 50 Ω and resonating out the reactive part gives the degeneration
inductors directly:

<p style="text-align:center"><em>Z</em><sub>in</sub> = <em>g</em><sub>m</sub><em>L</em><sub>S</sub> / <em>C</em><sub>gs</sub> &nbsp;+&nbsp; <em>j</em>&thinsp;[&thinsp;&omega;(<em>L</em><sub>S</sub> + <em>L</em><sub>G</sub>) &minus; 1/(&omega;<em>C</em><sub>gs</sub>)&thinsp;]</p>

which yields **L<sub>S</sub> = 45.29 pH** and **L<sub>G</sub> = 280.3 pH**, with
L<sub>d</sub> = 32.31 pH resonating the 1 pF load.

<figure>
  <img src="/images/portfolio/lna-28ghz/07-lna-schematic.png" alt="Differential LNA schematic" loading="lazy">
  <figcaption>Schematic of the 28 GHz differential cascode LNA.</figcaption>
</figure>

<figure>
  <img src="/images/portfolio/lna-28ghz/08-testbench.png" alt="Differential LNA testbench" loading="lazy">
  <figcaption>Testbench for the differential LNA.</figcaption>
</figure>

## Performance

<figure>
  <img src="/images/portfolio/lna-28ghz/09-s11-rin-nf.png" alt="S11, input resistance and noise figure" loading="lazy">
  <figcaption>S11, R<sub>in</sub> and NF. At 28 GHz, S11 = −14.05 dB and NF = 1.74 dB.</figcaption>
</figure>

<figure>
  <img src="/images/portfolio/lna-28ghz/10-voltage-gain.png" alt="LNA voltage gain versus frequency" loading="lazy">
  <figcaption>Voltage gain: 17.44 dB at 28 GHz.</figcaption>
</figure>

<figure>
  <img src="/images/portfolio/lna-28ghz/11-p1db.png" alt="1 dB compression point" loading="lazy">
  <figcaption>Input-referred 1 dB compression point: −8.84 dBm.</figcaption>
</figure>

<figure>
  <img src="/images/portfolio/lna-28ghz/12-iip3.png" alt="Third-order input intercept point" loading="lazy">
  <figcaption>IIP3: 9.16 dBm.</figcaption>
</figure>

<figure>
  <img src="/images/portfolio/lna-28ghz/13-stability-kf-delta.png" alt="Stability factors Kf and Delta versus frequency" loading="lazy">
  <figcaption>Δ &lt; 1 and K<sub>f</sub> &gt; 1 across 10–60 GHz — the LNA is unconditionally stable over the band.</figcaption>
</figure>

| Requirement | Target | Simulated |
|---|---|---|
| Input matching \|S11\| | < −12 dB | **−14.06 dB** |
| Center frequency f<sub>0</sub> | 28 GHz | 28 GHz |
| Voltage gain | > 12 dB @ f<sub>0</sub> | **17.44 dB** |
| Power consumption | < 30 mW | **22.78 mW** |
| Noise figure | < 5 dB | **1.74 dB** |
| IIP3 | > −15 dBm | **9.16 dBm** |

## Constant-parameter circles

The noise, available-gain and power-gain circles say something the summary table does not: **the
input impedance cannot be chosen for one figure of merit at a time.**

<figure>
  <img src="/images/portfolio/lna-28ghz/14-noise-circles.png" alt="Constant noise figure circles" loading="lazy">
  <figcaption>Constant-noise-figure circles. The smallest circle is the lowest achievable NF (2 dB).</figcaption>
</figure>

<figure>
  <img src="/images/portfolio/lna-28ghz/15-available-gain-circles.png" alt="Constant available gain circles" loading="lazy">
  <figcaption>Constant available-gain circles; the smallest circle corresponds to the highest gain (12 dB).</figcaption>
</figure>

<figure>
  <img src="/images/portfolio/lna-28ghz/16-power-gain-circles.png" alt="Constant power gain circles" loading="lazy">
  <figcaption>Constant power-gain circles. Higher power-gain circles converge toward the inductive region, so an inductive input impedance is essential for power gain.</figcaption>
</figure>

Read together, the circles show that low NF and high gain only coincide where the noise and gain
circles intersect, and that neither is reachable without an inductive/capacitive component in the
input impedance. Adding the power-gain circles narrows the usable region further — low NF, high
voltage gain and high power gain live at the intersection of all three, which is what makes the
degeneration inductor values the critical design decision rather than an afterthought.
