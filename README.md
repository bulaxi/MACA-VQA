## News

- This paper has been accepted by IEEE ICME 2025.
- Paper PDF (Baidu Netdisk): https://pan.baidu.com/s/1Eauk4dfI0GnGHrM8cZ92Rw?pwd=55wc
- Extraction code: 55wc

MACA-VQA: Quality Assessment of UGC Videos via Multi-level Distortion Adaptation and Spatiotemporal Cross-Attention Fusion

### Reproduction Environment

- OS: Linux
- Python: 3.8.19

### Install Requirements

For this reproduction, package versions were pinned and verified as follows:

Core versions used in reproduction:

```text
torch==2.2.2
torchvision==0.17.2
numpy==1.24.3
scipy==1.10.1
pandas==2.0.3
opencv-python==4.9.0.80
pytorchvideo==0.1.5
clip==1.0
einops==0.8.0
torch-geometric==2.5.3
```

Full environment export used during reproduction was saved as:

```text
/data/user/wjp/requirements.txt
```

### Train And Test

#### 1. Extract video frames

```
python extract_frame/extract_frame_*.py
```

#### 2. Extract VideoMAE features

Use [VideoMae V2](https://github.com/OpenGVLab/VideoMAEv2/blob/master/extract_tad_feature.py) to extract motion features.

#### 3. Extract distortion features

Use [Re-IQA](https://github.com/avinabsaha/ReIQA/blob/main/demo_quality_aware_feats.py) to extract distortion features.

#### 4. Train the model

##### 4.1 train on LSVQ

```shell
python -u train_baseline_modular.py --database LSVQ
```

##### 4.2 fine-tune on other datasets

```shell
python -u train_other_modular.py
```

##### 4.3 test on other datasets

```shell
python -u test_baseline_modular.py
```

Example:

```bash
python -u test_baseline_modular.py \
	--database KoNViD-1k \
	--trained_model ckpts_modular/YOUR_TRAINED_MODEL.pth
```

Replace `ckpts_modular/YOUR_TRAINED_MODEL.pth` with your own trained checkpoint path.

Supported test datasets in `test_baseline_modular.py`:

- LiveVQC
- KoNViD-1k
- CVD2014
- youtube_ugc
- LIVEYTGaming
- LBVD
- LIVE-Qualcomm

### Acknowledgement
The basic code is partially from the below repos.
- [ModularVQA](https://github.com/winwinwenwen77/ModularBVQA)
- [Re-IQA](https://github.com/avinabsaha/ReIQA)
- [VideoMae V2](https://github.com/OpenGVLab/VideoMAEv2)



