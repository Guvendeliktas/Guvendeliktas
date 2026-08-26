# Güven Deliktaş

**Electronics engineer. RF systems on one side, deep learning on the other, and a
lot of time spent in the gap between them.**

I like the problems where the signal is genuinely messy — real hardware, real
channel, carrier frequency offset, I/Q imbalance, all of it — and something still
has to make a decision about it. That covers both halves of what I do: RF system
engineering (link budgets, cascade analysis, spectrum measurements, SATCOM ground
stations) and the neural networks I point at the resulting mess.

The other recurring theme: I keep finding calculations that live in a spreadsheet
nobody trusts, and drawings that live in one engineer's head. I turn those into
tools with a test suite. Three of them are further down.

---

##  Automatic modulation classification, over the air

My senior project. A complete SDR pipeline — generate, transmit, receive,
classify — built on **USRP-2901 + LabVIEW + PyTorch**, classifying **24
modulation types** from **real over-the-air I/Q**, in real time.

No simulated datasets. That was the whole point: simulated I/Q is clean and
teaches a model the wrong lesson. Real captures come with CFO, phase noise, I/Q
imbalance and amplifier nonlinearity included, free of charge, whether you wanted
them or not.

**The design decision I'd defend in any interview:** a single flat 24-class model
struggles, and it's not the model's fault. Sum enough OFDM subcarriers and the
time-domain signal goes approximately Gaussian — which makes OFDM *trivial* to
tell apart from single-carrier, and simultaneously makes OFDM sub-types very hard
to tell apart from *each other*. One classifier, two contradictory jobs.

So it's split into a **three-stage hierarchy**:

| Stage | Job | Input | Accuracy |
|---|---|---|---|
| **1** | single-carrier vs multi-carrier | FFT | **96.59 %** |
| **2A** | OFDM sub-type — 8 classes | I/Q + FFT + HOS | **83.97 %** |
| **2B** | single-carrier — 16 classes | I/Q + FFT | **93.98 %** |
| | **end-to-end, 24 classes** | | **81.82 %** |
| | end-to-end, 22 classes *(see below)* | | **90.90 %** |

Each stage trains independently, so when something goes wrong you can see *where*
— and confidence composes down the chain as `P(stage 1) × P(stage 2)`.

**Why 22 classes and not 24:** 4-QAM and 4-PSK have physically identical
constellations. Not a bug, not a training problem — the same points in the same
places. The model was being asked to distinguish two things that are the same
thing, and it dutifully collapsed to 20.2 % on OFDM-4QAM. Remove the pair and
OFDM-PSK goes 64.6 % → 83.9 %, OFDM-QAM 61.0 % → 83.4 %. Sometimes the honest
answer is that the label set is wrong.

**Model:** dual-stream 1D-ResNet — one branch on raw I/Q (time: amplitude and
phase), one on the normalised FFT magnitude (frequency: spectral signature),
concatenated into the classifier head. The OFDM branch gets a third input,
**higher-order statistics** (a cumulant fingerprint that goes to zero in Gaussian
noise — exactly the thing that makes OFDM sub-types hard).

The two streams pull their weight in different places: FSK separates cleanly in
the FFT branch because the frequency deviations are right there; ASK/PSK/QAM
separate in the I/Q branch. Neither alone is enough.

**Some numbers I like:** ≈1.35 M segments of 1024 samples across 7 SNR levels
(−10 … +20 dB), with 50-sample gaps between neighbouring segments so no block
leaks from train into test. Real-time inference runs USRP → LabVIEW → TCP →
Python at ~100–150 ms per segment, using **literally the same preprocessing code**
as training, because the fastest way to get a great validation score and a useless
system is to let those two drift apart. At ≥ +5 dB SNR it sits around 99.6 %. It
beats the classic single-stage VT-CNN2 baseline (79.94 %) by roughly 11 points.
Trained on a single GTX 1650 in about 14–16 hours, which I mention mostly to say
you don't need a cluster.

> 🏆 **Third Place — Undergraduate Project Competition, SIU 2026**
> (34th IEEE Signal Processing and Communications Applications Conference)
> — awarded to the full 24-class hierarchical system described above.
>
> 📄 **A portion of this work** was accepted as a SIU 2026 paper, covering the
> earlier 12-class stage (ASK/PSK/FSK only, before QAM, OFDM and the hierarchy):
> G. Deliktaş, E. Arslan, H. Polat, L. Özkan, S. Büyükçorak,
> [*"A Deep Learning Approach for SDR-Based Automatic Modulation Classification"*](https://ieeexplore.ieee.org/document/11636794),
> in Proc. IEEE 34th SIU, 2026.
>
> [![IEEE Xplore](https://img.shields.io/badge/IEEE%20Xplore-Read%20the%20paper-00629B?logo=ieee&logoColor=white)](https://ieeexplore.ieee.org/document/11636794)
>
> Team project with Evren Arslan and Halenur Polat, advised by
> Dr. Saliha Büyükçorak Edibali.

**The code for this one isn't on GitHub** — it's a team project and the dataset
was collected on lab hardware, so it isn't mine alone to publish. If you want to
dig into it, [email me](mailto:guvendeliktas@gmail.com): I'm glad to walk through
the architecture, the training setup, the confusion matrices, or why the OFDM
branch was the hard part.

---

## 📡 RF & SATCOM engineering tools

Built during an RF test and field engineering internship, then cleaned up and
published. The field work fed the tools directly: it's hard to stay relaxed about
a link budget you can't check after you've spent a week checking one with a
spectrum analyser.

| | |
|---|---|
| [**satcom-link-budget**](https://github.com/Guvendeliktas/satcom-link-budget) | LEO/GEO ground-station link budgets with an automated Word report generator. ITU-R propagation models, elevation sweeps, BER curves. Verified to **≤ 0.005 dB** across 69 numerical checks. `MATLAB` `Python` |
| [**rf-level-diagram**](https://github.com/Guvendeliktas/rf-level-diagram) | Cascade power budget as a **DAG, not a flat chain**. I wrote a second solver from scratch just to disagree with the first one — it didn't: 13/13 nodes identical to the bit. It also caught existing diagrams quietly creating energy. **1058 tests.** `Python` `PySide6` |
| [**rf-block-diagram**](https://github.com/Guvendeliktas/rf-block-diagram) | Editor for RF block and cabling diagrams. Connectors drawn per IEEE Std 315, title-blocked vector PDF from A4 to A0. The layer that decides what things *look* like imports no Qt at all, so **1011 tests** run without a screen. `Python` `PySide6` |

---

## Background

**B.Sc. Electronics Engineering** — Gebze Technical University, 2022–2026
*Graduated with Honour Degree*

**Erasmus+** — Politechnika Poznańska, Poland — Computing and Telecommunications
Machine learning, NLP and DSP coursework, and a semester of discovering how many
ways there are to explain the same equation.

Also two industrial internships: data transmission pipelines and
communication-device integration, and PLC/automation basics. The unglamorous
business of getting equipment to talk to each other, which turns out to be most
of engineering.

## Tools

- **ML / Data** — PyTorch · NumPy · Pandas · scikit-learn · CNN & ResNet architectures · dataset creation and labelling
- **RF / Comms** — SDR & USRP · digital modulation (ASK/PSK/FSK/QAM/OFDM) · I/Q acquisition and preprocessing · ITU-R P.618/P.676 · LEO & GEO link budgets
- **Test & instrumentation** — spectrum analyser · signal generator · LabVIEW · TX–RX test setup
- **Languages & tooling** — Python · MATLAB/Simulink · C · Git · LTspice

## Get in touch

📧 <guvendeliktas@gmail.com> · 💼 [linkedin.com/in/guven-deliktas](https://www.linkedin.com/in/guven-deliktas) · 📄 [IEEE Xplore](https://ieeexplore.ieee.org/document/11636794)

Always happy to talk about RF, modulation, or why your link budget disagrees with
your spectrum analyser. The modulation classification work isn't published as a
repo, but the paper is linked above and my inbox is open for the rest of it.
