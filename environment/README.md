# Reference environment

The frozen experiment archives record the following Kaggle runtime for the source/internal experiments:

- Python 3.12.13
- PyTorch 2.10.0+cu128
- torchvision 0.25.0+cu128
- NumPy 2.0.2
- pandas 2.3.3
- scikit-learn 1.6.1
- NVIDIA Tesla T4

The notebooks also use Matplotlib, Pillow, and tqdm. Their exact versions were not recorded in the compact environment audit, so they are intentionally left unpinned in `requirements.txt`.

CUDA-enabled PyTorch installation can be platform-specific; use the appropriate PyTorch wheel/index for your system.
