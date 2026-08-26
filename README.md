# Güven Deliktaş

RF and satellite communications engineering — link budgets, cascade power
analysis, and the tooling around them.

Most of what I build starts the same way: a calculation that lives in a
spreadsheet and a drawing that lives in someone's head, neither of which can be
checked. I like turning those into something with a test suite.

---

### 🛰 [satcom-link-budget](https://github.com/Guvendeliktas/satcom-link-budget) · MATLAB, Python

Ground-station link budget analysis with an automated Word report generator.
Slant range, FSPL, atmospheric and rain attenuation (ITU-R P.837/P.838/P.839),
system noise temperature, G/T, C/N₀, Eb/N₀ and margin — plus elevation sweeps,
LEO pass profiles and BER curves.

Verified against an independent reference calculation to **≤ 0.005 dB** across
69 numerical checks. Two deliberate deviations from the reference convention are
named, pinned by tests, and stated in every generated report.

### 📈 [rf-level-diagram](https://github.com/Guvendeliktas/rf-level-diagram) · Python, PySide6

Cascade power budget for SATCOM earth stations. The model is a **DAG, not a
flat chain** — polarisation, band splits, coupler monitor ports and A/B
redundancy are first-class.

To trust the engine I wrote a second, independent solver and compared them:
**13/13 nodes identical to the bit**, and `0.000e+00 dB` deviation across 300
randomised graph orderings. The noise chain reproduces a published antenna
datasheet's G/T of **37.1 dB/K** exactly. That verification round also caught a
real physics violation — a third cable on a two-output splitter was duplicating
power, so a chain fed 0 dBm produced +1.22 dBm. 1058 tests.

### 🔧 [rf-block-diagram](https://github.com/Guvendeliktas/rf-block-diagram) · Python, PySide6

Editor for RF block and cabling diagrams — component library, right-angle cable
routing, connectors drawn per **IEEE Std 315**, multi-page documents, and
title-blocked vector PDF from A4 to A0.

The layer that decides *what things look like* imports no Qt at all, which is
why 1011 tests run without a screen.

---

### How I work

- **No silent zeros.** A missing input produces "not computable", never a
  number. The absence of a result and a result of zero are different things.
- **Warn, don't refuse.** Tools should report problems, not block the engineer
  who understands their own system better than the tool does.
- **Verify against something outside the code.** A manufacturer datasheet, an
  independent solver, a second implementation — anything that doesn't share the
  original's assumptions.

### Stack

`Python` · `PySide6/Qt` · `MATLAB` · `SQLite` · `pytest` · `python-docx` ·
`NumPy` · RF/microwave systems · ITU-R propagation models

### Contact

<guvendeliktas@gmail.com>
