# [CVPR 2026 Oral] :ocean: SEATrack: Simple, Efficient, and Adaptive Multimodal Tracker 
Official implementation of [**SEATrack: Simple, Efficient, and Adaptive Multimodal Tracker**]().

[Models & Raw Results](https://drive.google.com/drive/folders/1dDKtK11pX8rmP1pYvgpdLndNjX2hqjYQ?usp=sharing)
(Google Driver)
[Models & Raw Results](https://pan.baidu.com/s/1QNFkLc0AXvQ8l7LkUYYcCg?pwd=r4s7)
(Baidu Driver)

## News
**[Apr 13, 2026]**
- We release codes, models, and raw results.

## Introduction
- :ocean: A simple unified visual multimodal tracking framework for RGB-T, RGB-D, and RGB-E tracking.

- SEATrack achieves strong performance on multiple multimodal tracking benchmarks.

- SEATrack is highly training-friendly, with only **0.6M** trainable parameters and **63.5 FPS** inference speed.

- We expect SEATrack to inspire more attention to cross-modal alignment for future multimodal tracking research.

<div align="center">
  <img width="70%" src="assets/Framework.png"/>
</div>

## Results
### Overall Performance
<div align="center">
  <img width="70%" src="assets/Results.png"/>
</div>

### Visualization
<div align="center">
  <img width="70%" src="assets/Vis.png"/>
  <img width="40%" src="assets/Frame_Loss.png"/>
</div>

## Usage
### Installation
Create and activate a conda environment with required packages:
```
conda env create -f environment.yaml
conda activate seatrack
```

### Data Preparation
- [LasHeR](https://github.com/BUGPLEASEOUT/LasHeR)
- [RGBT234](https://pan.baidu.com/share/init?surl=weaiBh0_yH2BQni5eTxHgg)(qvsq)
- [DepthTrack](https://github.com/xiaozai/DeT)
- [VOT22-RGBD](https://www.votchallenge.net/vot2022/dataset.html)
- [VisVent](https://github.com/wangxiao5791509/VisEvent_SOT_Benchmark)

Put the training datasets in <DATA_PATH>. It should look like:
```
$<PATH_of_tgatrack>
-- <DATA_PATH>
    -- DepthTrack/trainingset
        |-- adapter02_indoor
        |-- bag03_indoor
        |-- bag04_indoor
        ...
    -- LasHeR/trainingset
        |-- 1boygo
        |-- 1handsth
        ...
    -- VisEvent/trainingset
        |-- 00142_tank_outdoor2
        |-- 00143_tank_outdoor2
        ...
```

### Path Setting
Run the following command to set paths:
```
cd <PATH_TO_SEATRACK>
python tracking/create_default_local_file.py --workspace_dir . --data_dir <DATA_PATH> --save_dir ./output
```
You can also modify paths by these two files:
```
./lib/train/admin/local.py  # paths for training
./lib/test/evaluation/local.py  # paths for testing
```

### Training
Download the pretrained [foundation model](https://drive.google.com/drive/folders/1ttafo0O5S9DXK2PX0YqPvPrQ-HWJjhSy?usp=sharing) (OSTrack), 
put it under ```./pretrained/vitb_256_mae_32x4_ep300``` and ```./pretrained/vitb_256_mae_32x4_ep300```.
```
bash train.sh
```
You can train models with various modalities and variants by modifying ```train.sh```.

### Testing
#### For RGB-D benchmarks
[DepthTrack Test set & VOT22_RGBD]\
These two benchmarks are evaluated using [VOT-toolkit](https://github.com/votchallenge/toolkit). \
You need to put the **DepthTrack testingset** and **list.txt** we provided to ```./Depthtrack_workspace/sequences```. \
Similarly, you need put the **VOT-RGBD22** and **list.txt** we provided to ```./vot22_RGBD_workspace/sequences```.

```
bash eval_rgbd.sh
```

#### For RGB-T benchmarks
[LasHeR & RGBT234] \
Modify the <DATASET_PATH> and <SAVE_PATH> in```./RGBT_workspace/test_rgbt_mgpus.py```, then run:
```
bash eval_rgbt.sh
```
We refer you to [LasHeR Toolkit](https://github.com/BUGPLEASEOUT/LasHeR) for LasHeR evaluation, 
and refer you to [MPR_MSR_Evaluation](https://github.com/xuboyue1999/RGBT-Tracking/tree/main) for RGBT234 evaluation.


#### For RGB-E benchmark
[VisEvent]\
Modify the <DATASET_PATH> and <SAVE_PATH> in```./RGBE_workspace/test_rgbe_mgpus.py```, then run:
```
bash eval_rgbe.sh
```
We refer you to [VisEvent_SOT_Benchmark](https://github.com/wangxiao5791509/VisEvent_SOT_Benchmark) for evaluation.


## Bixtex
If you find SEATrack is helpful for your research, please consider citing:

```bibtex

```

## Acknowledgment
- This repo is based on [ViPT](https://github.com/jiawen-zhu/ViPT) which is an excellent work.
- We thank for the [PyTracking](https://github.com/visionml/pytracking) library, which helps us to quickly implement our ideas.

## Contact
If you have any question, feel free to email binbing2024@outlook.com. ^_^


