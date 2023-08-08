# Anomaly detection in time series by data denoising
This project aims to apply various denoising techniques to identify anomalies in
various forms of time series, e.g. in vibrations, medical or radio signals.

## Status
The current work is summarised here:

- **qiskit_qae/ts_qiskit_qae_v1_0**: TS QAE based on binary encoding of TS windows developed and tested, results are not promising.

## Files
This repository consists of the following groups of notebooks:

- **dataset**: samples of data used by the notebooks
- **classic_pytorch**: classically computed solutions with PyTorch
- **classic_tensorflow**: classically computed solutions with Tensorflow
- **qiskit_qae**: quantum autoencoders with Qiskit
- **pennylane_qae**: quantuym autoencoders with PennyLane
- **runs**: experimental runs with important results
- **tutorials**: tutorials and demos from external sources
- **legacy**: prgrams no longer needed or used

## Software installation
To get installation details of Python, Anaconda / Miniconda, Pytorch, Tensorflow, Qiskit and PennyLane 
please refer to their respective web sites.
