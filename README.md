# Anomaly detection in time series by data denoising
This project aims to apply various denoising techniques to identify anomalies in
various forms of time series, e.g. in vibrations, medical or radio signals.

## Status
**Current version: V3.06**
- Several tests conducted on the full-QAE to determine its performance in response to the size of additional DoF qubits / rotation and entangling block repetions / latent vs. trash space.
- Full tests to support the paper for ICCS'2024,

**The current work is summarised here:**

- **qiskit_qae/ts_qae_qiskit_binary_...**: TS QAE based on binary encoding of TS windows developed and tested, abandoned.
- **qiskit_qae/ts_qae_qiskit_unary_...**: TS QAE based on unary encoding of TS windows developed and tested, abandoned.
- **qiskit_qae/ts_qae_qiskit_angles_...**: TS QAE based on angle encoding of TS windows developed and tested, results are promising.

## Files
This repository consists of the following groups of notebooks:

- **classic_pytorch**: classically computed solutions with PyTorch
- **classic_tensorflow**: classically computed solutions with Tensorflow
- **dataset**: samples of data used by the notebooks
- **images**: images used in the notebooks 
- **legacy**: programs kept for archival use only
- **qiskit_qae**: quantum autoencoders with Qiskit
  - *beer_qiskit_v5*: results for ICCS'2024 Qiskit final runs V3.06 (can change, archive in *tests*)
  - *beer_torch*: results for ICCS'2024 PyTorch final runs V3.04 (can change, archive in *tests*)
  - *tests*: important tests, e.g. ICCS'2024 initial and final submission + utilities V3.06
  - *vault*: QAE versions for critical design decisions
- **pennylane_qae**: quantuym autoencoders with PennyLane
- **play_ground**: small tests of various features
- **runs**: experimental runs with important results
- **tutorials**: tutorials and demos from external sources

## Software installation
To get installation details of Python, Anaconda / Miniconda, Pytorch, Tensorflow, Qiskit and PennyLane 
please refer to their respective web sites.

## Running qiskit_qae
- Perform the following tasks:
  - Create a folder for your logs, which will store pre-processed data, trained models, their parameters, analyses and plots
  - Ensure all notebooks refer to the log (LOG_NAME), named data (DATA_NAME) and modeling case (CASE_NAME)
  - Each notebook will load the previously processed data/models/parameters/results as appropriate
  - Each notebook will need to configure some of their(requires references to individual files from logs) parameters
- Execute the following notebooks, ensuring all suitable variables refer to the logs/data/case, and their parameters are configured:
  - Notebook **ts_qae_vx_xx_data.ipynb**: creates a database (requires loading a data set and configuring its parameters)
  - Notebook **ts_qae_vx_xx_training.ipynb**: trains a QAE models and saves model parameters (requires configuring training parameters)
  - Notebook **ts_qae_vx_xx_analysis.ipynb**: analyses a trained QAE models and saves the results (requires configuring data reduction parameters and the selection of window set for analysis)
  - Notebook **ts_qae_vx_xx_plots.ipynb**: plots data, trainig and analysis results (requires provision of references to individual files from logs)
