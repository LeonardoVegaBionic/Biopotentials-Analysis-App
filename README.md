# Biopotential Analysis Suite

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

An open-source, modular desktop application for processing, visualising and
analysing biomedical signals. The suite is built around a plugin-style
architecture, so new processing modules can be added without touching the
existing ones. The current release ships with a full cardiorespiratory
coordination pipeline; additional modules for other biopotentials are under
development.

The project is aimed at researchers, students and educators who need a
reproducible and extensible environment for biomedical signal analysis, with
no dependency on commercial software.

---

## Table of contents

- [Current modules](#current-modules)
- [Planned modules](#planned-modules)
- [Installation](#installation)
- [Quick start](#quick-start)
- [Input data](#input-data)
- [Output files](#output-files)
- [Citation](#citation)
- [License](#license)
- [Contact](#contact)

---

## Current modules

### Signal filtering

Load a signal in `.txt`, `.csv` or `.mat` format, select a channel, and apply
low-pass, high-pass, band-pass or band-stop filters. Four filter designs are
available (Butterworth, Chebyshev, Elliptic, Bessel), with adjustable order
and cut-off frequencies. The original and filtered signals are shown side by
side, and the result can be exported to CSV. A batch mode applies the same
filter to many files at once.

### Cardiorespiratory coordination (CRC)

A complete pipeline for studying the temporal relationship between cardiac and
respiratory rhythms:

- ECG conditioning and R-peak detection with a custom Pan-Tompkins
  implementation.
- ECG-derived respiration (EDR) reconstruction from beat-to-beat signed QRS
  area, with adaptive outlier suppression and linear interpolation onto the
  ECG time grid.
- Six respiratory landmark definitions: MAX, MIN, RS, FS, RMI and FMI.
- Time-based coordigram with Gaussian kernel smoothing.
- Recurrence-point coordination percentage at two tolerances (ε = 0.11 s and
  0.21 s).
- Automatic EDR quality assessment combining deterministic rules, a Random
  Forest classifier and an Isolation Forest outlier detector, with a colour
  code (green / yellow / red) indicating the reliability of each recording.
- Batch processing with per-recording HTML reports and a summary CSV.

### EDR (standalone)

Reconstructs the EDR from an ECG recording without requiring a respiratory
reference. Useful for building EDR-only pipelines or for testing the
reconstruction on new data. Runs in single-file or batch mode, with the same
quality assessment used by the CRC module.

### FFT extraction

Computes the power spectral density of any channel using Welch's method, marks
the dominant peak, and reports its frequency and power. Runs on any signal
loaded through the standard interface.

### Signal viewer

Loads a recording and displays all channels as stacked, time-linked subplots.
Channels can be selected or deselected individually, a time window can be
applied, and per-channel statistics (mean, standard deviation, minimum,
maximum, number of finite samples) are shown in a table. The visible range and
the statistics table can be exported to CSV.

---

## Planned modules

The architecture is designed so that new biopotentials can be integrated as
additional modules. The following are under consideration or in early
development:

- **EEG processing**: band decomposition, spectral analysis and event-related
  potentials.
- **EMG processing**: onset detection, envelope extraction and fatigue
  indices.
- **Additional cardiac metrics**: heart rate variability, QT interval analysis
  and beat-to-beat morphology.
- **Time-frequency analysis**: wavelet and Hilbert transforms for
  non-stationary signals.
- **Real-time acquisition**: streaming from microcontrollers and low-cost
  acquisition boards over serial or Bluetooth.

Each module is independent, so adding one does not affect the others. The menu
in the main window is designed to grow as modules are added.

---

## Installation

### Option 1 — Standalone executable (no Python required)

Download the latest executable from the
[Releases](../../releases) page, unzip it, and double-click
`Biopotentials Analysis App.exe`. No installation, no dependencies, no
internet connection required.

**Minimum requirements:**

- Windows 10 or later (64-bit)
- 4 GB RAM (8 GB recommended for batch processing)
- 2 GB free disk space
- 1280 × 800 display
- Microsoft Visual C++ Redistributable 2015–2022 (usually already installed)
