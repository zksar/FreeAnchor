## FreeAnchor

The Code for "FreeAnchor: Learning to Match Anchors for Visual Object Detection" \[[arxiv](https://arxiv.org/abs/1909.02466)\]. 

![architecture](architecture.png)

## Installation 
Check [INSTALL.md](INSTALL.md) for installation instructions.

## Usage
You will need to download the COCO dataset and configure your own paths to the datasets.

For that, all you need to do is to modify `maskrcnn_benchmark/config/paths_catalog.py` to point to the location where your dataset is stored.

#### Config Files
We provide four configuration files in the configs directory.

| Backbone | Iteration | Scale jittering<br>train / test | Config File |  
| :-----: | :---: | :---: | :----------: |
| ResNet-50-FPN    |   90k |   N / N  | configs/free_anchor_R-50-FPN_1x.yaml      | 
| ResNet-101-FPN   |   90k |   N / N  | configs/free_anchor_R-101-FPN_1x.yaml     | 
| ResNet-101-FPN   |  135k |   N / N  | configs/free_anchor_R-101-FPN_1.5x.yaml   | 
| ResNeXt-101-FPN  |  135k |   Y / N  | configs/free_anchor_X-101-FPN_j1.5x.yaml  | 


#### Training with 4 GPUs (4 images per GPU)

```bash
cd path_to_free_anchor
export NGPUS=4
python -m torch.distributed.launch --nproc_per_node=$NGPUS tools/train_net.py --config-file "path/to/config/file.yaml"
```

#### Training with 8 GPUs (2 images per GPU)

```bash
cd path_to_free_anchor
export NGPUS=8
python -m torch.distributed.launch --nproc_per_node=$NGPUS tools/train_net.py --config-file "path/to/config/file.yaml"
```

#### Test on MS-COCO test-dev

```bash
cd path_to_free_anchor
python -m torch.distributed.launch --nproc_per_node=$NGPUS tools/test_net.py --config-file "path/to/config/file.yaml" MODEL.WEIGHT "path/to/.pth file" DATASETS.TEST "('coco_test-dev',)"
```

#### Evaluate NMS Recall

```bash
cd path_to_free_anchor
python  -m torch.distributed.launch --nproc_per_node=$NGPUS tools/eval_NR.py --config-file "path/to/config/file.yaml" MODEL.WEIGHT "path/to/.pth file"
```
## Citations
Please consider citing our paper in your publications if the project helps your research.
```
@inproceedings{zhang2019freeanchor,
  title   =  {{FreeAnchor}: Learning to Match Anchors for Visual Object Detection},
  author  =  {Zhang, Xiaosong and Wan, Fang and Liu, Chang and Ji, Rongrong and Ye, Qixiang},
  booktitle =  {Neural Information Processing Systems},
  year    =  {2019}
}
```
