# Güven Deliktaş

**Electronics engineer working across RF systems and machine learning.**

Two sides of the same problem, mostly. RF system engineering — link budgets,
cascade analysis, spectrum measurements, SATCOM ground stations — and deep
learning applied to signals captured from real hardware rather than simulated.

I also keep turning calculations that live in a spreadsheet, and drawings that
live in one engineer's head, into tools with a test suite. Three of those are
below.

---

## Automatic modulation classification, over the air

Senior project. An SDR pipeline — USRP-2901, LabVIEW, PyTorch — that classifies
**24 modulation types** (ASK, PSK, FSK, QAM and OFDM) from **real over-the-air
I/Q**, in real time.

The classifier is hierarchical rather than flat: single-carrier vs multi-carrier
first, then the modulation within each branch. Both stages use a dual-stream
1D-ResNet reading time (I/Q) and frequency (FFT) together.

> 🏆 **Third Place** — Undergraduate Project Competition, **SIU 2026**
> (34th IEEE Signal Processing and Communications Applications Conference)
>
> 📄 G. Deliktaş, E. Arslan, H. Polat, L. Özkan, S. Büyükçorak,
> [*"A Deep Learning Approach for SDR-Based Automatic Modulation Classification"*](https://ieeexplore.ieee.org/document/11636794),
> in Proc. IEEE 34th SIU, 2026.
> [![IEEE Xplore](https://img.shields.io/badge/IEEE%20Xplore-Read%20the%20paper-00629B?logo=ieee&logoColor=white)](https://ieeexplore.ieee.org/document/11636794)

**The paper covers where the project started** — an earlier 12-class stage,
before QAM, OFDM and the hierarchy. The final 24-class system that won the award
isn't published as a repo: it's a team project and the dataset was collected on
lab hardware, so it isn't mine alone to put online.

If you want the rest of it — the architecture, the results, why the OFDM branch
was the hard part — [email me](mailto:guvendeliktas@gmail.com).

*Team project with Evren Arslan and Halenur Polat, advised by
Dr. Saliha Büyükçorak Edibali.*

---

## RF & SATCOM engineering tools

Built during an RF test and field engineering internship, then cleaned up and
published here.

| | |
|---|---|
| [**satcom-link-budget**](https://github.com/Guvendeliktas/satcom-link-budget) | LEO/GEO ground-station link budgets with an automated Word report generator. ITU-R propagation models, elevation sweeps, BER curves. Verified to **≤ 0.005 dB** across 69 numerical checks. `MATLAB` `Python` |
| [**rf-level-diagram**](https://github.com/Guvendeliktas/rf-level-diagram) | Cascade power budget as a **DAG, not a flat chain**. Validated against a second solver written independently — 13/13 nodes identical to the bit — and against a manufacturer datasheet's G/T. **1058 tests.** `Python` `PySide6` |
| [**rf-block-diagram**](https://github.com/Guvendeliktas/rf-block-diagram) | Editor for RF block and cabling diagrams. Connectors drawn per IEEE Std 315, title-blocked vector PDF from A4 to A0. The layer that decides how things look imports no Qt, so **1011 tests** run without a screen. `Python` `PySide6` |

---

## Background

**B.Sc. Electronics Engineering** — Gebze Technical University, 2022–2026
*Graduated with Honour Degree*

**Erasmus+** — Politechnika Poznańska, Poland — Computing and Telecommunications
Machine learning, NLP and digital signal processing coursework.

Two industrial internships before that: data transmission pipelines and
communication-device integration, and PLC/automation basics.

## Tools

- **ML / Data** — PyTorch · NumPy · Pandas · scikit-learn · CNN & ResNet architectures · dataset creation and labelling
- **RF / Comms** — SDR & USRP · digital modulation (ASK/PSK/FSK/QAM/OFDM) · I/Q acquisition and preprocessing · ITU-R P.618/P.676 · LEO & GEO link budgets
- **Test & instrumentation** — spectrum analyser · signal generator · LabVIEW · TX–RX test setup
- **Languages & tooling** — Python · MATLAB/Simulink · C · Git · LTspice

## Get in touch

📧 <guvendeliktas@gmail.com> · 💼 [linkedin.com/in/guven-deliktas](https://www.linkedin.com/in/guven-deliktas) · 📄 [IEEE Xplore](https://ieeexplore.ieee.org/document/11636794)
