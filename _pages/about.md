---
permalink: /
title: "Juho Jeon"
excerpt: "Analog and mixed-signal IC designer working on high-speed data converters."
author_profile: true
redirect_from:
  - /about/
  - /about.html
---

I am an MPhil candidate in Electronic and Computer Engineering at **HKUST**, advised by
**Prof. Chik Patrick Yue**. I design **analog and mixed-signal integrated circuits**, with a
focus on **high-speed SAR ADCs for ADC-DSP-based wireline receivers**.

My thesis work is a 28 nm CMOS SAR ADC whose resolution is reconfigurable from 5 bits to 9 bits
purely in the digital domain — no switches are inserted into the analog signal path — so a single
converter can trade bandwidth, resolution and power across communication standards without giving
up GS/s-class speed. That work has been accepted for presentation at **IEEE TENCON 2026**.

Across my MPhil and undergraduate work I have taken designs from hand calculation through
transistor-level simulation to post-layout extraction in **28 nm, 22 nm, 90 nm and 180 nm CMOS**,
covering data converters, mm-wave RF front-ends, operational amplifiers, continuous-time filters
and switching power converters.

Research interests
------
* **Data converters** — SAR and multi-bit-per-cycle ADCs, reconfigurable and time-interleaved architectures
* **Wireline communication circuits** — ADC-DSP-based receivers, SerDes front-ends
* **Analog / mixed-signal design** — comparators, capacitive DACs, low-noise amplification, calibration

Selected projects
------

| Project | Technology | Headline result |
|---|---|---|
| [Reconfigurable 5b–9b multi-bit-per-cycle SAR ADC](/portfolio/reconfigurable-sar-adc/) | 28 nm CMOS | 8.31 ENOB, 1.4 GS/s, 23.8 fJ/conv.-step |
| [10-bit monotonic-switching SAR ADC](/portfolio/sar-adc-10b-180nm/) | 180 nm CMOS | 9.09 ENOB at 2 MS/s, 1.92 mW |
| [28 GHz differential LNA](/portfolio/lna-28ghz/) | 22 nm CMOS | 17.4 dB gain, 1.74 dB NF, 22.8 mW |
| [Gain-boosted folded-cascode OTA](/portfolio/gain-boosted-ota/) | 90 nm CMOS | 81.6 dB gain, 604 MHz UGF, 1.93 mW |
| [Gm-C channel-selection filter for UWB](/portfolio/gmc-uwb-filter/) | 90 nm CMOS | 35 kHz – 259 MHz passband |
| [PWM voltage-mode buck converter](/portfolio/buck-converter/) | 180 nm CMOS | 86.2 % peak efficiency, 45.2 mV ripple |

Every project page carries the schematics, layouts and simulation results behind these numbers —
see the [Projects](/portfolio/) page.

Contact
------
The fastest way to reach me is by email: <jjeonaa@connect.ust.hk>. I am also on
[LinkedIn](https://www.linkedin.com/in/juho-jeon/).
My [CV](/cv/) is available here and as a [PDF](/files/Juho_Jeon_CV.pdf).
