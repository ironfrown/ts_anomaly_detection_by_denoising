# Anomaly detection in time series by data denoising
This project aims to apply various denoising techniques to identify anomalies in
various forms of time series, e.g. in vibrations, medical or radio signals.

## Status
**Current version: V3.06**
- Several tests conducted on the full-QAE to determine its performance in response to the size of additional DoF qubits / rotation and entangling block repetions / latent vs. trash space.
- Full tests to support the paper for ICCS'2024,

**The current work is summarised here:**

- **TS QAE binary encoding**: Completed / QAE based on binary encoding of TS windows, abandoned.
- **TS QAE unary encoding**: Completed / QAE based on unary encoding of TS windows, abandoned.
- **TS QAE angle encoding**: Completed / QAE based on angle encoding of TS windows, adopted.
- **ICCS'2024 paper**: Completed / Tests to support ICCS'2024 paper on TS denoising.

## Files
This repository consists of the following groups of notebooks:

- *classic_pytorch*: classically computed solutions with PyTorch 
- *classic_tensorflow*: classically computed solutions with Tensorflow
- *dataset*: samples of data used by the notebooks
- **images**: images used in the notebooks 
- *legacy*: programs kept for archival use only
- **qiskit_qae**: quantum autoencoders with Qiskit
  - *beer_qiskit_v5*: results for ICCS'2024 Qiskit final runs V3.06 (can change, archive in *tests*)
  - *beer_torch*: results for ICCS'2024 PyTorch final runs V3.04 (can change, archive in *tests*)
  - *tests*: important tests, e.g. ICCS'2024 initial and final submission + utilities V3.06
  - *vault*: QAE versions for critical design decisions
- *pennylane_qae*: quantum autoencoders with PennyLane
- *play_ground*: small tests of various features
- *runs*: experimental runs with important results
- *tutorials*: tutorials and demos from external sources
- **utils**: various utilities to support TS manipulation

Folders in *italic* not synchronised, for development use only.

## Software installation
To get installation details of Python, Anaconda / Miniconda, Pytorch, Tensorflow, Qiskit and PennyLane 
please refer to their respective web sites.

## Running qiskit_qae
- Perform the following tasks:
  - Create a folder for your logs, which will store pre-processed data, trained models, their parameters, analyses and plots
  - Ensure all notebooks refer to the log (LOG_NAME), named data (DATA_NAME), project/modeling case (CASE_NAME) and figures path (FIGURES_PATH)
  - Other notebooks will require paths to models and their parameters (TRAIN_PATH and PARAMS_PATH), analysis info and scores (ANALYSIS_PATH and PARAMS_PATH)
  - Each notebook will load the previously processed data/models/parameters/results as appropriate
  - Each notebook will need to configure some of their(requires references to individual files from logs) parameters
- Execute the following notebooks, ensuring all suitable variables refer to the logs/data/case, and their parameters are configured:
  - Notebook **ts_qae_vx_xx_data.ipynb**: creates a database (requires loading a data set and configuring its parameters)
    - Data sets are stored with various transformations applied, e.g. orginal data for training and validation, data with noise and differencing, plus data encoded for quantum circuit encoding
    - Data set configuration includes: data set name (name), number of samples (n), window size (w), window step (ws), level of noise applied (z), the number of noisy series replications (zr)
    - Other parameters are fixed or can be derived from data stored, e.g. training/validation split, horizon (1), scale (1), panning (0), major and minor version of the system that generated data
    - Data configuration will be stored in a file identifying the data set name and its parameters, e.g. \$DATA_PATH/beer_n160_w8_ws4_z0.03_zr1_info.json
    - For convenience, the last stored data set is also saved in: \$DATA_PATH/info.json
  - Notebook **ts_qae_vx_xx_training.ipynb**: trains a QAE models and saves the model parameters (requires configuring training parameters)
    - The notebook requires to load a data set to be used for model training and validation, this is done by loading the specific data set configuration, and based on this information the relevant data files
    - The basic information about the model trained in this notebook is stored in the folder \$TRAIN_PATH, i.e.  a history of the model training cost, its cost-optimised parameters for the model initialisation, and the model hyper-parameters
    - A complete set of the model parameters is saved in the \$PARAMS_PATH folder
    - Each model is defined by its case name (e.g. "beer_xdf_2"), data set in use (n, w, ws, z and zr), as well as the ansatz repeatitions (reps), circuit additioina width (aw), size of latent space (lat), and the type of entanglement use (e.g. "sca")
    - Other coinfiguration parameters include: the number of core circuit qubits (same as the widow length, however note that additional qubits may be addded), the number of trash qubits (always equal to the number of core qubits minus the size of latent space), interval between data shuffles during training, interval between cost and parameter logging, cost function type, the number of training epochs, number of shots for circuit execution, the random seed applied in training, the major and minor version of the software that created the model
    - Some information about model training has not beed saved in the configuration, e.g. the type of ansatz used to build the circuit, or the type of the quantum execution environment (QPU, GLU or CPU) - these details are at the moment hard-coded in software
    - Model configuration is stored in a a training folder, e.g. \$TRAIN_PATH/beer_n160_w8_ws4_z0.03_zr1_reps2_aw3_sca_lat7_info.json'
  - Notebook **ts_qae_vx_xx_analysis.ipynb**: analyses a trained QAE models and saves the results (requires configuring data reduction parameters and the selection of window set for analysis)
    - The notebook requires to load a data set to be used for model training and validation, this is done by loading the specific data set configuration, and based on this information the relevant data files
    - The notebook also needs to load the configuration of a specific model training, based on this information, also load the history of costs and parameters saved at each training cycle
    - The notebook goals are to downsize the cost history to a more manageable size (say from 2000 data points to 50), calculate and save performance scores (such as R2, RMSE, MAE and MAPE) at the selected training intervals, find the best training and validation scores for the entire cycle of model evolution, identify the optimum training and validation parameters, produce charts for the model performance indicators
    - Other notebooks goals are to calculate the performance score on a smaller set of training and validation windows, reintegrate all windowed (and overlapping) series into cohesive time series (for the original, noisy and QAE reconstructed time series)
  - Notebook **ts_qae_vx_xx_plots.ipynb**: plots data, trainig and analysis results (requires provision of references to individual files from logs)
    - The notebook requires to load a data set to be used for model training and validation, this is done by loading the specific data set configuration, and based on this information the relevant data files
    - The notebook also needs to load the configuration of a specific model training, based on this information, also load the history of costs and parameters saved at each training cycle
    - The main goals of this notebook are to visualise results of the model execution and analysis, some of those visualisations have previously appeared in other notebooks