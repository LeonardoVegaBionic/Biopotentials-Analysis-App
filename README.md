# Biopotential Analysis Suite

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
- [Citation](#citation)
- [License](#license)
- [Contact](#contact)

---

## Current modules

### Signal filtering

Load a signal in `.txt`, `.csv` or `.mat` format, select a channel, and apply
low-pass, high-pass or band-pass Butterworth filters. The original and filtered
signals are displayed side by side, and the result can be exported to CSV.

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
  Forest classifier and an Isolation Forest outlier detector.
- Batch processing with per-recording HTML reports and a summary CSV.

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

### Requirements

- Python 3.10 or higher
- Operating system: Windows, Linux or macOS

## Quick start

    1. Launch the application with python (biopotentials analysis.py).
    2. The main window shows a lateral menu with the available modules. Modules that are not yet implemented appear greyed out.
    3. Select a module to open its workspace. Each module has its own controls,plots and export options.
    4. For the CRC module:
        - Load the signals files (.txt, .csv, .mat).
        - Choose an output folder to save the results.
        - Choose the ECG and respiration channels.
        - Set the sampling rate and the analysis duration.
        - Set the number of cycles for coordigram and the source of this (respiration, edr or both).
        - Choose if you want to calculate EDR and if respiration is available.
        - Click Process to run the pipeline.
        - Switch to the Coordigram tab to see the results for all six landmark definitions.
    5. For the Filters module:
        - Load the bipotential signal.
        - Choose the channel of biopotential.
        - Set the sampling rate.
        - Choose the filter type and set the frequencies to work.
        - Click Process to run the pipeline.
    6. For the FFT Extraction Module:
        - Load the bipotential signal.
        - Choose the channel of biopotential.
        - Set the sampling rate.
        - Click Process to run the pipeline.

## Input data

    The suite accepts signals in three formats:

    1. .txt and .csv: one column per channel, one row per sample. The delimiter is detected automatically.
    2. .mat: MATLAB files with one or more numeric arrays of equal length.

    Channels are selected from a drop-down menu after the file is loaded. The same loading interface is shared by all modules, so new modules inherit the same format support.

## License
This project is distributed under the MIT License. See the LICENSE file for
details.

## Contact
For questions, bug reports or feature requests, please open an issue on the GitHub repository or contact:

Leonardo Ivan Vega Reyes - lvegar1700@alumno.ipn.mx

Jose Javier Reyes Lagos - javier.reyes@cinvestav.mx

