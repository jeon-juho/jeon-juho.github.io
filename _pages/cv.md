---
layout: archive
title: "CV"
permalink: /cv/
author_profile: true
redirect_from:
  - /resume
---

{% include base_path %}

[Download as PDF](/files/Juho_Jeon_CV.pdf)

Education
======
* **M.Phil. in Electronic and Computer Engineering**, HKUST, Sep 2024 – Dec 2026 (expected)
  * Advisor: Prof. Chik Patrick Yue
  * Teaching Assistant, ELEC3400 Integrated Circuit Designs and Systems (Prof. Howard Luong, Spring 2025)
  * Relevant coursework: Advanced Analog IC Analysis and Design; Power Management Integrated Circuit Design; RF Microsystems: Devices and Applications; Advanced AI Chip and System; High Frequency Circuit Design; Electronic Design Automation for VLSI Design
* **B.Eng. in Electronic Engineering**, minor in Information Technology, HKUST, Sep 2017 – Jun 2024
  * Second Class Honours, Division I
  * Academic leave: Sep 2019 – Aug 2021 (mandatory military service, Republic of Korea); Feb 2022 – Feb 2023 (full-time internship, Deloitte Advisory)
  * Relevant coursework: Analogue Integrated Circuits Design and Analysis; Integrated Circuits and Systems; CMOS VLSI Design; Integrated Power Electronics; Electronic Circuits; Signals and Systems; Signal Processing and Communications; Probability and Random Processes in Engineering; FPGA-based Design; Embedded Systems

Publications
======
* J. Jeon and C. P. Yue, "Digitally Reconfigurable Resolution Multi-Bit-per-Cycle SAR ADC: Design Trade-off Considerations," *IEEE Region 10 Conference (TENCON) 2026*, accepted.

Circuit design experience
======
* **28 nm CMOS Reconfigurable Multi-Resolution SAR ADC** — MPhil thesis, Sep 2024 – present
  * Advisor: Prof. Chik Patrick Yue \| post-layout simulation
  * Digitally reconfigurable SAR ADC supporting five resolution modes (5b–9b) via a 1-then-2-bit-per-cycle conversion scheme, with reconfigurability implemented entirely in digital logic — no switches added to the analog signal path.
  * 51.84 dB SNDR, 8.31 ENOB and 66.08 dB SFDR at 1.4 GS/s (0.9 V supply, 9b mode): a 23.8 fJ/conversion-step Walden FoM and 160 dB Schreier FoM, verified with post-layout extracted netlists for the DAC and comparator.
  * Enable-gated DAC switching architecture and mode-aware decoder allowing seamless mode transitions via a 4-bit control word with no analog reconfiguration.
  * Quantified the high-resolution-limited power trade-off (~9× FoM degradation from 9b to 5b mode) that arises from sharing a single DAC/comparator across all resolution modes.
  * Accepted for presentation at IEEE TENCON 2026. [Project page](/portfolio/reconfigurable-sar-adc/)

* **180 nm CMOS 10-bit SAR ADC** — final year thesis, Sep 2023 – May 2024
  * Advisor: Prof. Yihan Zhang \| schematic-level simulation, TSMC 180 nm \| First Runner-Up, ECE Best FYP Award
  * Designed and independently verified a 10-bit monotonic-switching SAR ADC (capacitive DAC, bootstrapped sampling switch, dynamic comparator, asynchronous SAR logic) in Cadence Virtuoso, reaching 9.09 ENOB and 1.92 mW at 2 MS/s. [Project page](/portfolio/sar-adc-10b-180nm/)

* **28 GHz Differential LNA**, Spring 2026 — RFIC Design coursework (Prof. Chik Patrick Yue), 22 nm TSMC CMOS
  * Differential cascode LNA with inductive source/gate degeneration: 17.4 dB gain, 1.74 dB NF, −14.1 dB S11 and 9.16 dBm IIP3 at 22.8 mW. [Project page](/portfolio/lna-28ghz/)

* **Gain-Boosted Folded-Cascode Fully-Differential OTA**, Fall 2024 — Advanced Analog IC Design coursework (Prof. Howard Luong), 90 nm TSMC CMOS
  * Gain-boosted folded-cascode OTA with resistive CMFB: 81.6 dB gain, 604 MHz UGF, 61.5° phase margin, 103 dB CMRR and −66 dB THD at 1.93 mW (±1 V supply). [Project page](/portfolio/gain-boosted-ota/)

* **Continuous-Time Gm-C Channel-Selection Filter for UWB**, Fall 2024 — Advanced Analog IC Design coursework (Prof. Howard Luong), 90 nm TSMC CMOS
  * Gm-C UWB bandpass filter (35 kHz – 259 MHz) taken from passive Chebyshev-I prototypes through to transistor-level implementation, meeting passband gain/ripple, corner-frequency and adjacent-channel specs. [Project page](/portfolio/gmc-uwb-filter/)

* **DC-DC Buck Converter with PWM Voltage-Mode Control**, Fall 2024 — Power Management IC Design coursework (Prof. Wing Hung Ki), 180 nm TSMC CMOS
  * 3.3 V-to-1.8 V, 1 MHz synchronous buck converter: 86.2 % peak efficiency and 45.2 mV ripple across a 200–800 mA CCM load. [Project page](/portfolio/buck-converter/)

Work experience
======
* **Deloitte Advisory**, Hong Kong — Cyber Security Intern, Feb 2022 – Feb 2023
  * Built and deployed identity and access management (IAM) workflows and a demonstration web application (Okta, Salesforce, Hong Kong iAMSmart) for client engagements.
* **Gense Technologies**, Hong Kong — Electronic Engineer Intern, Dec 2021 – Jan 2022
  * Verified and validated a portable medical imaging device through testbench characterization and clinical trial, confirming compliance with design specifications.
  * Proposed an alternative constant-current-source design to meet a lower load-regulation requirement.
* **Republic of Korea Army** — Sergeant, Wireline Communication Squad Leader, Sep 2019 – Apr 2021
  * Led a wireline communication squad, directing installation and maintenance operations.
  * Installed, maintained and secured military communication systems including wireline and optical wireline transceivers, satellite communication systems, wireless transceivers, alarm systems and surveillance cameras.

Leadership
======
* **Deputy Teaching Assistant Coordinator**, ECE Dept., HKUST, Sep 2025 – Jul 2026
  * Planned and organized departmental programs and events for graduate teaching assistants; provided peer mentoring.
  * Hosted the monthly ECE Future Leaders PG Seminar Series, a platform for graduate students to broaden knowledge within and beyond their fields.
  * Guided postgraduate program outreach activities.
  * Provided teaching materials for teaching assistants: Prevention and Guidelines for Plagiarism in Class.
* **ECE Student Ambassador**, ECE Dept., HKUST, Sep 2023 – Jun 2024
  * Advised junior students on academic and non-academic matters; supported departmental outreach activities.
  * Hosted and managed department-level gathering activities.

Honors and awards
======
* **First Runner-Up — ECE Best Final Year Project/Thesis Award**, ECE Dept., HKUST, Jun 2024
* **Dean's List**, ECE Dept., HKUST, Spring 2023
* **Top 5 Innovative Solution — Sustainability Smart Campus Competition**, HKUST, Nov 2021

Skills
======
* **Circuit design**: analog/mixed-signal CMOS IC design, SAR ADCs and data converters, mm-wave RF circuits (LNA), power management ICs, PCB design, FPGA, RTL-to-GDSII flow, digital circuit design
* **Tools**: Cadence Virtuoso, Spectre, ADE, Synopsys, HSPICE, Altium Designer, Advanced Design System (ADS), Ansys HFSS, Xilinx Vivado
* **Programming**: MATLAB, Python, Verilog, Verilog-A
* **Languages**: Korean (native), English (professional), Mandarin Chinese (intermediate)
