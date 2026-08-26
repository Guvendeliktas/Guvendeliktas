# Güven Deliktaş

**Electronics engineer working where deep learning meets wireless communications.**

I came into this from the RF side — spectrum analysers, IQ captures, link
budgets — and kept running into the same wall: the interesting problems in
wireless are the ones where the signal is messy and the model has to figure it
out anyway. So I spend my time on both halves. SDR and modulation on one side,
neural networks on the other, and the plumbing that makes them meet.

The other thing I keep doing: turning calculations that live in spreadsheets and
drawings that live in someone's head into tools with a test suite. Three of them
are below.

---

## What I've worked on

###  Automatic modulation classification from real over-the-air signals

My senior project, and the piece of work I'm most attached to. A full **TX–RX
pipeline built with SDR and LabVIEW**: transmit, capture, and label real
over-the-air IQ data across **24 modulation schemes** (ASK, PSK, FSK, QAM and
OFDM subchannels), then train a **dual-stream ResNet** on it — **~94 %
classification accuracy**.

The part that mattered was the dataset. Synthetic IQ is easy and teaches a model
the wrong thing; collecting real captures meant the impairments were real too.

> 🏆 **Third Place — Senior Design Project Competition**, 34th IEEE Signal
> Processing and Communications Applications Conference (**SIU 2026**)
>
> 📄 G. Deliktaş, E. Arslan, H. Polat, L. Özkan and S. B. Edibali,
> [**"A Deep Learning Approach for SDR-Based Automatic Modulation Classification"**](https://ieeexplore.ieee.org/document/11636794),
> in Proc. IEEE 34th SIU, 2026.
> [![IEEE Xplore](https://img.shields.io/badge/IEEE%20Xplore-Read%20the%20paper-00629B?logo=ieee&logoColor=white)](https://ieeexplore.ieee.org/document/11636794)

### 📡 RF and SATCOM engineering tools

Built during an RF test and field engineering internship, then cleaned up and
published here. Field work — link budget validation, spectrum analyser
measurements, characterising signal patterns — kept feeding back into what the
tools needed to do.

| | |
|---|---|
| [**satcom-link-budget**](https://github.com/Guvendeliktas/satcom-link-budget) | Link budget analysis for LEO and GEO ground stations, with an automated Word report generator. ITU-R propagation models, elevation sweeps, BER curves. Verified to **≤ 0.005 dB** across 69 numerical checks. `MATLAB` `Python` |
| [**rf-level-diagram**](https://github.com/Guvendeliktas/rf-level-diagram) | Cascade power budget as a **DAG, not a flat chain**. Validated against an independently written second solver — 13/13 nodes identical to the bit — and against a manufacturer datasheet's G/T. Caught a real physics violation in existing diagrams. **1058 tests.** `Python` `PySide6` |
| [**rf-block-diagram**](https://github.com/Guvendeliktas/rf-block-diagram) | Editor for RF block and cabling diagrams; connectors drawn per IEEE Std 315, title-blocked vector PDF from A4 to A0. The layer deciding *what things look like* imports no Qt, so **1011 tests** run without a screen. `Python` `PySide6` |

---


## Background

**B.Sc. Electronics Engineering** — Gebze Technical University, 2022–2026
*Graduated with Honour Degree*

**Erasmus+** — Politechnika Poznańska, Poland (Computing and Telecommunications)
Machine learning, NLP and digital signal processing coursework.

Also: industrial internships in data transmission pipelines and
communication-device integration, and in PLC/automation basics — the
unglamorous end of "getting equipment to talk to each other", which turns out to
be most of engineering.

## Tools

- **ML / Data** — PyTorch · NumPy · Pandas · scikit-learn · CNN & ResNet architectures · dataset creation and labelling
- **RF / Comms** — SDR & USRP · digital modulation (ASK/PSK/FSK/QAM/OFDM) · IQ acquisition and preprocessing · ITU-R P.618/P.676 · LEO & GEO link budgets
- **Test & instrumentation** — spectrum analyser · signal generator · LabVIEW · TX–RX test setup
- **Languages & tooling** — Python · MATLAB/Simulink · C · Git · LTspice

## Get in touch

📧 <guvendeliktas@gmail.com> · 💼 [linkedin.com/in/guven-deliktas](https://www.linkedin.com/in/guven-deliktas) · 📄 [IEEE Xplore](https://ieeexplore.ieee.org/document/11636794)

Open to roles in RF systems, wireless communications and applied machine
learning — and always happy to talk about any of the above.
