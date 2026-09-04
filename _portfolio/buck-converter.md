---
title: "DC-DC Buck Converter with PWM Voltage-Mode Control"
excerpt: "<b>180 nm CMOS &middot; 3.3 V &rarr; 1.8 V &middot; 1 MHz &middot; 86.2 % efficiency</b><br/>Every block designed from hand calculation: power stage, driver, active diode, error amplifier, Type-I compensator, RTCT oscillator and SR latch.<br/><img src='/images/portfolio/buck-converter/01-top-level-schematic.png' style='max-width:560px;width:100%;margin-top:0.75em' alt=''>"
collection: portfolio
sort_order: 6
header:
  teaser: portfolio/buck-converter/01-top-level-schematic.png
---

* **Context**: Power Management IC Design coursework (Prof. Wing Hung Ki), Fall 2024
* **Technology**: TSMC 180 nm CMOS (high-voltage models), ideal passive components
* **My role**: Sole author

## Specification and outcome

| Parameter | Target | Simulated |
|---|---|---|
| V<sub>g</sub> | 3.3 V | 3.3 V |
| V<sub>o</sub> | 1.8 V | 1.8 V |
| f<sub>s</sub> | 1 MHz | 1 MHz |
| I<sub>load</sub> (CCM) | 200 – 800 mA | 200 – 800 mA |
| Test I<sub>load</sub> in DCM | 100 mA | 100 mA |
| V<sub>o</sub> ripple in CCM | < 50 mV | **45.2 mV** |
| Efficiency | > 85 % | **86.21 %** |

| Additional measurement | Result |
|---|---|
| Line regulation | 0.165 % |
| Line transient overshoot / undershoot / settling | 0.784 V / 0.205 V / 170 µs |
| Load regulation | 0.0731 % |
| Load transient overshoot / undershoot / settling | 0.888 V / 0.193 V / 175 µs |

All specifications were met.

<figure>
  <img src="/images/portfolio/buck-converter/01-top-level-schematic.png" alt="Buck converter top-level schematic" loading="lazy">
  <figcaption>Complete buck converter with PWM voltage-mode control.</figcaption>
</figure>

## Power stage, from the ripple budget

Assuming CCM and steady state, D = M = V<sub>o</sub>/(V<sub>g</sub>η) = 0.625 and R<sub>L</sub> = 3.6 Ω
at 500 mA. Choosing a 400 mA inductor current ripple fixes

<p style="text-align:center"><em>L</em> = [(<em>V</em><sub>g</sub> &minus; <em>V</em><sub>o</sub>) / &Delta;<em>I</em><sub>L</sub>]&thinsp;<em>DT</em> = 2.34 &micro;H &rarr; <strong>2.35 &micro;H</strong></p>

and the 50 mV output ripple limit fixes

<p style="text-align:center"><em>C</em> &gt; &Delta;<em>I</em><sub>L</sub> / (8&thinsp;<em>f</em><sub>s</sub>&thinsp;&Delta;<em>V</em><sub>o</sub>) = 1 &micro;F &rarr; <strong>1.1 &micro;F</strong></p>

The power switch is a PMOS and the synchronous rectifier an NMOS active diode. Budgeting switch
resistance at 3 % of the load resistance gives R<sub>switch</sub> = 108 mΩ, which sets
(W/L)<sub>pmos</sub> = 150 m / 500 n and (W/L)<sub>nmos</sub> = 35 m / 600 n. Measured on the bench,
the PMOS came in at 93 mΩ and the NMOS at 96 mΩ against the 108 mΩ hand calculation.

<figure>
  <img src="/images/portfolio/buck-converter/02-power-switch-driver.png" alt="Power transistor driver schematic" loading="lazy">
  <figcaption>Four-stage tapered inverter chain driving the power transistor.</figcaption>
</figure>

<figure>
  <img src="/images/portfolio/buck-converter/09-driver-delay-sim.png" alt="Power transistor driver simulation" loading="lazy">
  <figcaption>Driver simulation with a 10 kΩ series source resistance: maximum propagation delay 1.15 ns.</figcaption>
</figure>

## Active diode

The NMOS synchronous rectifier is controlled by a comparator built from differential common-gate
amplifiers that compares the diode's anode and cathode, with two inverters as the output driver.

<figure>
  <img src="/images/portfolio/buck-converter/03-active-diode.png" alt="Active diode with control circuit" loading="lazy">
  <figcaption>Active diode and its comparator-based control circuit.</figcaption>
</figure>

<figure>
  <img src="/images/portfolio/buck-converter/10-active-diode-iv.png" alt="Active diode I-V characteristic" loading="lazy">
  <figcaption>I–V characteristic of the active diode, showing the expected behaviour with V<sub>on</sub> = 600 mV.</figcaption>
</figure>

## Error amplifier and Type-I compensation

A two-stage op-amp provides the loop gain, designed for maximum unity-gain frequency subject to
60 dB of low-frequency gain, with equal 0.2 V overdrive across the devices and R<sub>Z</sub> = 1/g<sub>m5</sub>
cancelling the right-half-plane zero.

<figure>
  <img src="/images/portfolio/buck-converter/04-error-amplifier.png" alt="Error amplifier schematic" loading="lazy">
  <figcaption>Two-stage error amplifier.</figcaption>
</figure>

<figure>
  <img src="/images/portfolio/buck-converter/12-error-amp-bode.png" alt="Error amplifier Bode plot" loading="lazy">
  <figcaption>Error amplifier Bode plot: 62.06 dB low-frequency gain, 12.75 kHz UGF, 89.7° phase margin.</figcaption>
</figure>

The compensator is Type-I. Requiring the loop gain to be below 0 dB at the power stage's second pole
(s = j·621970) gives C<sub>1</sub>R<sub>1</sub> > 8.876 µ, so C<sub>1</sub> > 12.68 nF; 15 nF was used
for margin.

<figure>
  <img src="/images/portfolio/buck-converter/05-type-i-compensator.png" alt="Type I compensator" loading="lazy">
  <figcaption>Type-I compensator built around the error amplifier.</figcaption>
</figure>

## Clocking: RTCT oscillator, PWM comparator, SR latch

The RTCT oscillator generates the ramp and the synchronous pulse at a fixed 1 MHz, from
f<sub>s</sub> = k/(C<sub>T</sub>R<sub>T</sub>) with k = 12, R<sub>T</sub> = 110 kΩ and
C<sub>T</sub> = 90 pF. It splits into a reference current generator, a ramp generator, and a
hysteretic comparator with SR latch.

<figure>
  <img src="/images/portfolio/buck-converter/06-rtct-oscillator.png" alt="RTCT oscillator schematic" loading="lazy">
  <figcaption>RTCT oscillator generating the ramp and clock signals.</figcaption>
</figure>

<figure>
  <img src="/images/portfolio/buck-converter/11-oscillator-transient.png" alt="RTCT oscillator transient response" loading="lazy">
  <figcaption>Oscillator transient: two synchronous 1 MHz signals, with the ramp swinging from 150.3 mV to 1.327 V.</figcaption>
</figure>

<figure>
  <img src="/images/portfolio/buck-converter/07-pwm-comparator.png" alt="PWM comparator schematic" loading="lazy">
  <figcaption>PWM comparator — a two-stage op-amp without compensation, since no pole-zero cancellation is needed here.</figcaption>
</figure>

<figure>
  <img src="/images/portfolio/buck-converter/08-sr-latch.png" alt="NOR gate SR latch schematic" loading="lazy">
  <figcaption>NOR-gate SR latch combining the comparator output and the oscillator clock. Only QB is needed, since it drives the PMOS power transistor.</figcaption>
</figure>

## Converter behaviour

<figure>
  <img src="/images/portfolio/buck-converter/13-ccm-steady-state.png" alt="CCM steady-state operation at 500 mA" loading="lazy">
  <figcaption>CCM steady state at I<sub>load</sub> = 500 mA: V<sub>o</sub> = 1.80 V, ripple 45.2 mV, ΔI<sub>L</sub> = 396 mA, duty cycle 0.624 at 1 MHz — closely matching the hand calculation.</figcaption>
</figure>

<figure>
  <img src="/images/portfolio/buck-converter/14-dcm-operation.png" alt="DCM operation at 100 mA" loading="lazy">
  <figcaption>DCM at I<sub>load</sub> = 100 mA. The active diode blocks reverse inductor current; the small residual ripple in the inductor current comes from the diode's V<sub>on</sub>. Voltage-mode control moves the duty cycle from 0.624 to 0.422 to hold V<sub>o</sub> at 1.8 V.</figcaption>
</figure>

<figure>
  <img src="/images/portfolio/buck-converter/15-line-transient.png" alt="Line transient response" loading="lazy">
  <figcaption>Line transient response for a 3.0 V → 3.6 V input step.</figcaption>
</figure>

<figure>
  <img src="/images/portfolio/buck-converter/16-load-transient.png" alt="Load transient response" loading="lazy">
  <figcaption>Load transient response for an 800 mA → 200 mA load step.</figcaption>
</figure>

## Scope and next steps

The bandgap reference was replaced with ideal sources for V<sub>BG</sub>, V<sub>H</sub> and
V<sub>L</sub>, and the passives are ideal. The clear next steps are a soft-start circuit, a Type-II
compensator for faster transient response, a supply-independent current source, and post-layout
simulation.
