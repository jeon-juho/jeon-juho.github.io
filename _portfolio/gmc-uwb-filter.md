---
title: "Continuous-Time Gm-C Channel-Selection Filter for UWB"
excerpt: "<b>90 nm CMOS &middot; 35 kHz &ndash; 259 MHz passband &middot; 5.16 dB gain</b><br/>Channel-selection filter taken from passive Chebyshev-I prototypes through ideal Gm cells and bandwidth-limited models to a transistor-level implementation.<br/><img src='/images/portfolio/gmc-uwb-filter/08-transistor-level-gmc-filter.png' style='max-width:560px;width:100%;margin-top:0.75em' alt=''>"
collection: portfolio
sort_order: 5
header:
  teaser: portfolio/gmc-uwb-filter/08-transistor-level-gmc-filter.png
---

* **Context**: Advanced Analog IC Design final project (Prof. Howard Luong), Fall 2024
* **Technology**: 90 nm TSMC CMOS
* **Team**: Three-person group project with M. J. Aslam and Y. C. Lau
* **My role**: Analysis of non-idealities in the filter (bandwidth-limited Gm cells and their optimization), the transistor-level implementation using the OTAs, and parameter tuning

## Approach

The filter is built in four deliberate stages, each one adding a layer of reality:

1. **Passive prototype** — a third-order Chebyshev-I low-pass cascaded with a first-order high-pass.
2. **Ideal Gm-C** — inductors and resistors replaced by ideal voltage-controlled current sources.
3. **Bandwidth-limited Gm-C** — each cell modelled as an ideal VCCS with parallel R<sub>out</sub> and
   C<sub>out</sub>, then re-optimized.
4. **Transistor level** — the [OTA from the midterm project](/portfolio/gain-boosted-ota/) dropped in
   as the actual gm cell.

Doing it in that order makes it possible to attribute every performance loss to a specific
non-ideality rather than to the design as a whole.

## Passive prototype and active transformation

Chebyshev-I was chosen because passband ripple is allowed. With f<sub>c</sub> = 255 MHz and
R<sub>S</sub>/R<sub>L</sub> = 0.1, the normalized prototype values scale to C<sub>f1</sub> = 4.686 pF,
L<sub>f2</sub> = 96.74 nH and C<sub>f3</sub> = 9.653 pF, with a 4.142 nF high-pass capacitor at
100 kHz. The passive filter loses 0.83 dB, so a single gain stage
(A<sub>v</sub> = G<sub>m1</sub>/G<sub>m2</sub> = 10 mS / 5 mS = 6.02 dB) is enough to reach the
passband gain target.

<figure>
  <img src="/images/portfolio/gmc-uwb-filter/01-passive-uwb-schematic.png" alt="Passive UWB filter schematic" loading="lazy">
  <figcaption>Passive UWB filter: third-order Chebyshev-I low-pass cascaded with a first-order high-pass.</figcaption>
</figure>

<figure>
  <img src="/images/portfolio/gmc-uwb-filter/02-ideal-gm-cell.png" alt="Ideal 10 mS gm cell" loading="lazy">
  <figcaption>Ideal gm cell (10 mS) used for the first active transformation.</figcaption>
</figure>

<figure>
  <img src="/images/portfolio/gmc-uwb-filter/03-active-gmc-testbench.png" alt="Active UWB Gm-C testbench" loading="lazy">
  <figcaption>Active UWB Gm-C testbench, with the floating inductor and source resistance converted into gm cells.</figcaption>
</figure>

<figure>
  <img src="/images/portfolio/gmc-uwb-filter/04-passive-response.png" alt="Passive filter frequency response" loading="lazy">
  <figcaption>Passive filter frequency response, annotated with every specification point: passband gain and ripple, both −3 dB corners, and lower-corner / adjacent / alternating channel attenuation.</figcaption>
</figure>

<figure>
  <img src="/images/portfolio/gmc-uwb-filter/05-ideal-gmc-response.png" alt="Ideal Gm-C filter frequency response" loading="lazy">
  <figcaption>Ideal Gm-C filter response — the gain stage lifts the passband from −0.83 dB to 5.19 dB with the shape preserved.</figcaption>
</figure>

## Where the non-idealities bite

Modelling each gm cell as a VCCS with g<sub>m</sub> = 5 mS, R<sub>out</sub> = 1 MΩ and
C<sub>out</sub> = 2 pF is enough to break the filter: the upper −3 dB corner collapses from 255 MHz to
**158.54 MHz**. Since there is only one inductor in the design, the parallel output capacitance
dominates it, and tuning the parallel capacitance recovers the corner to 262.26 MHz — at the cost of
pushing passband ripple to 2.92 dB.

<figure>
  <img src="/images/portfolio/gmc-uwb-filter/06-bandwidth-limited-gm-cell.png" alt="Bandwidth-limited gm cell model" loading="lazy">
  <figcaption>Bandwidth-limited gm cell: ideal VCCS with parallel output resistance and capacitance.</figcaption>
</figure>

<figure>
  <img src="/images/portfolio/gmc-uwb-filter/07-optimized-gmc-filter.png" alt="Optimized Gm-C filter with bandwidth limitation" loading="lazy">
  <figcaption>Gm-C filter after re-optimizing the passive values around the bandwidth-limited cells.</figcaption>
</figure>

<figure>
  <img src="/images/portfolio/gmc-uwb-filter/09-bw-limited-response.png" alt="Bandwidth-limited filter response" loading="lazy">
  <figcaption>Response with bandwidth-limited gm cells simply substituted in — note the upper corner at 158.54 MHz.</figcaption>
</figure>

<figure>
  <img src="/images/portfolio/gmc-uwb-filter/10-optimized-bw-limited-response.png" alt="Optimized bandwidth-limited filter response" loading="lazy">
  <figcaption>Response after optimization: the upper corner is back in specification at 262.26 MHz.</figcaption>
</figure>

## Transistor level

The midterm OTA needed one modification to serve here: it is fully differential, while the filter
needs differential input and single-ended output. A 1 MΩ resistor across the differential output
delivers the single-ended current. The input transistor lengths were also shortened to reduce the
cell's parallel capacitance, trading away some OTA gain to buy filter bandwidth.

<figure>
  <img src="/images/portfolio/gmc-uwb-filter/12-ota-gm-cell.png" alt="OTA reused as the transistor-level gm cell" loading="lazy">
  <figcaption>The OTA from the midterm project, adapted into the transistor-level gm cell.</figcaption>
</figure>

<figure>
  <img src="/images/portfolio/gmc-uwb-filter/08-transistor-level-gmc-filter.png" alt="Transistor-level Gm-C filter" loading="lazy">
  <figcaption>Transistor-level Gm-C filter with every ideal cell replaced by the real OTA.</figcaption>
</figure>

<figure>
  <img src="/images/portfolio/gmc-uwb-filter/11-transistor-level-response.png" alt="Transistor-level filter frequency response" loading="lazy">
  <figcaption>Transistor-level filter response. Higher nonlinearity moved the ripple outside the passband, which is what degrades the adjacent and alternating channel attenuation.</figcaption>
</figure>

## Results across all four stages

| Parameter | Specification | Passive | Ideal Gm | BW-limited Gm | Optimized BW-limited | Transistor level | Met |
|---|---|---|---|---|---|---|---|
| Passband gain | 0 – 10 dB | −0.83 | 5.19 | 5.45 | 5.16 | **5.16 dB** | ✓ |
| Passband ripple | ≤ 1 dB | 0.11 | 0.115 | 0.49 | 2.92 | **0** | ✓ |
| Lower −3 dB f<sub>lo</sub> | 5 kHz – 2 MHz | 35.13 | 35.13 | 37.54 | 34.96 | **35.26 kHz** | ✓ |
| Upper −3 dB f<sub>up</sub> | 253 – 264 MHz | 254.79 | 254.76 | 158.54 | 262.26 | **258.82 MHz** | ✓ |
| Lower corner atten. | > 15 dBc @ dc | 30.87 | 30.87 | 31.15 | 30.86 | **30.94 dBc** | ✓ |
| Adjacent channel atten. | > 12 dBc @ 500 MHz | 20.94 | 20.94 | 42.53 | 26.84 | **13.46 dBc** | ✓ |
| Alternating channel atten. | > 30 dBc @ 792 MHz | 33.46 | 33.46 | 58.40 | 44.02 | **19.40 dBc** | ✗ |

## What went wrong, and what it taught

**The first attempt used a fourth-order Chebyshev low-pass** and every specification collapsed in a
way optimization could not fix — two series inductors meant two more gm cells, and their
non-idealities compounded. Rebuilding the prototype at a lower order was the fix.

**The alternating channel attenuation was never met** — 19.40 dBc against a 30 dBc target. Tuning
passive values stops helping at a certain point: the stopband simply is not steep enough beyond the
upper cutoff because the gm cell's output capacitance is higher than the design assumed. The real
fix is a gm cell with higher unity-gain bandwidth at the same input g<sub>m</sub>, which is a
redesign of the amplifier rather than of the filter. Recognising *which* block a specification
failure belongs to was the most transferable lesson from this project.
