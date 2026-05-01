# EMG4HerGO – Partial Code Release
﻿
This repository contains a partial implementation of **EMG4HErgo**, a modified EMG-to-pose estimation framework. The core improvements focus on **feature extraction** and **decoding modules**, while the training data and basic environment/configuration are inherited from the public **[emg2pose](https://github.com/facebookresearch/emg2pose)** dataset and codebase.
﻿
> **Note**: This is a **pre‑publication partial release**. After the paper is accepted, we will publish the fully cleaned and documented code. The current version is intended to allow reviewers/early adopters to verify the core methodological changes.
﻿
## Quick Setup
﻿
Since the environment, data loader, and training pipeline follow emg2pose, the easiest way to run EMG4HerGO is:
﻿
1. **Set up emg2pose** following its official instructions (including dependencies, `environment.yml`, and data preparation).
2. **Replace** the feature extractor and decoder modules with the ones provided in this repository:
- `networks.py` – contains the **TCN (Temporal Convolutional Network)** implementation for feature extraction.
- `lightning.py` – includes the updated Lightning module with the new decoder.
- Configuration for the TCN is located under `config/network/`. To switch feature extractors, modify the corresponding YAML file under `config/experiment/` (e.g., set the network type to `tcn`).
3. Config files are under `config/` (e.g., `base.yaml`, `experiment/`, `network/`, `optimizer/`, `pose_module/`).
﻿
## Code Structure (Partial)

emg4hergo/
├── config/                       # Configuration files
│   ├── experiment/               # Switch feature extractor here
│   ├── network/                  # TCN and other network configs
│   ├── optimizer/
│   ├── pose_module/
│   └── base.yaml
├── emg4hergo_main/               # Core package (feature extractor, decoder)
│   ├── plots_Patch/              # Plotting utilities (legacy folder)
│   ├── plots4paper/              # Paper‑ready plotting scripts
│   ├── tests/                    # Unit tests
│   ├── training_results/         # Logs and checkpoints (empty in release)
│   ├── UmeTrack/                 # Auxiliary tracking module
│   ├── lightning.py              # PyTorch Lightning model
│   ├── networks.py               # TCN implementation (feature extractor)
│   ├── SelfData2visualData_converter.py  # Data conversion for visualization
│   ├── train_spyder_run.py       # Training script
│   ├── visualization.py          # Qualitative visualization only
│   ├── visualization_3DHandEMGJoints_exporter.py
│   ├── visualization_3Dplot.py
│   ├── visualization_Side2Side.py
│   └── visualization_Video.py
├── environment.yml               # (Optional – mostly same as emg2pose)
├── hand_joint_prediction.png     # Example hand joint prediction visualization
└── ergo/                         # Ergonomic scoring results (vision‑only)
    ├── validation_results/       # Scoring outputs on validation set
    └── handpose_model.pth        # Pretrained hand pose recognition network


##  Notes
﻿
- **Data**: All training uses the **emg2pose public dataset**. We do not redistribute the data.
- **Feature extractor switching**: The TCN configuration is stored in `config/network/`. To change the feature extractor, edit the appropriate YAML file under `config/experiment/` (e.g., set `network: tcn`). The TCN code is provided in `networks.py`.
- **Decoder**: The decoder implementation will be **gradually updated** in future commits. The current release focuses on the feature extraction improvements.
- **Visualization scripts** (e.g., `visualization.py`, `visualization_3D*.py`, `visualization_Video.py`) are **only for qualitative visualization**. They do **not** participate in model training or quantitative analysis.
- **Dependencies**: See `environment.yml`. It is nearly identical to emg2pose’s; only minor additions may exist.
- **Reproducibility**: Running `train_spyder_run.py` with the provided configs and a working emg2pose environment should reproduce the results reported in our paper (once the full code is released).
- **Ergonomic scoring (`ergo/` folder)**: This folder contains partial results of automatic ergonomic scoring for hand postures predicted from EMG. The scoring is **purely vision‑based** (operates directly on the predicted 3D hand joints) and does **not** use EMG signal features. The underlying implementation code is **not released** in this partial distribution. The `validation_results/` subfolder shows example outputs on the validation set.


 
## Citation & Full Release
﻿
If you use this code, please cite our work (to be added after publication). The complete, polished code will be made available at **(https://github.com/chenyin7255-eng/emg4hergo.git)** upon paper acceptance.
﻿
For questions, contact the authors.

**本项目不可用于商业行为** (This project is not permitted for commercial use.)
