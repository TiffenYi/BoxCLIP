# BoxCLIP

Vision-language joint learning for  box-supervised change detection in remote sensing

## 1. Environment Setup

<h3>Supported Platforms</h3>

- Linux / macOS
- Python ≥ 3.6 (Tested on Python 3.8)
- PyTorch ≥ 1.7 (Tested on PyTorch 1.9.0)
- CUDA ≥ 9.2 (Tested on CUDA 11.1)
- GCC ≥ 5.0

### Installation Guide

This project is developed based on [BoxInstSeg](https://github.com/LiWentomng/BoxInstSeg). Follow the steps below to set up the environment:

#### Step 1: Create Conda Environment

```bash
conda create -n BoxCLIP python=3.8 -y
conda activate BoxCLIP
```

#### Step 2: Install PyTorch, torchvision and torchaudio

Refer to the [official installation guide](https://pytorch.org/get-started/previous-versions/). For CUDA 11.1:

```bash
pip install torch==1.9.0+cu111 torchvision==0.10.0+cu111 torchaudio==0.9.0 -f https://download.pytorch.org/whl/torch_stable.html
```

#### Step 3: Install MMCV via OpenMIM

```bash
pip install -U openmim
mim install mmcv-full==1.5.0
```

#### Step 4: Clone the Repository

```bash
git clone https://github.com/TiffenYi/BoxCLIP
cd BoxCLIP
```

#### Step 5: Install Dependencies

```bash
bash setup.sh
```

------

## 2. Dataset Structure

The dataset should follow the structure below:

```
dataset/
├── annotations/       # Box-level COCO-style .json annotations
├── train/
│   ├── A/             # First temporal image
│   ├── B/             # Second temporal image
│   └── label/         # Pixel-wise labels (optional, for comparison)
├── test/
│   ├── A/             
│   ├── B/           
│   └── label/  
└── val/
    ├── A/
    ├── B/
    └── label/
```

> `annotations/` contains COCO-style `.json` files used for training with box-level supervision.
>  `label/` folders contain optional pixel-level labels for evaluation or comparison.

------

## 3. Usage

### 3.1 Training

To train the model using a specified config file:

```bash
python tools/train.py path/to/config.py
```

### 3.2 Evaluation and Visualization

To run inference using a trained model and save the prediction visualizations:

```bash
python result.py path/to/config.py path/to/model.pth --show-dir path/to/output_images/
```

To evaluate a trained model and compute metrics such as **Precision**, **Recall**, **F1-score**, and **IoU**:

```bash
python find_best_model.py path/to/config.py path/to/work_dir/ --show-dir path/to/output_results/
```

**Arguments:**

- `path/to/config.py`: the config file used for training
- `path/to/work_dir/`: the directory where training checkpoints are saved
- `--show-dir`: the folder to save evaluation results and visualizations

## 4. Acknowledgements

This work is based on [BoxInstSeg](https://github.com/LiWentomng/BoxInstSeg). We thank the authors for their open-source contribution.



