# BioTL
This repository contains code for the paper *Deep Transfer Learning for Biology Cross-domain Image Classification*.

## Datasets

Five datasets used in our experiments:
- [Flowers17](http://www.robots.ox.ac.uk/~vgg/data/flowers/17/index.html)
- [Flowers102](http://www.robots.ox.ac.uk/~vgg/data/flowers/102/index.html)
- [Plant Seedlings](https://vision.eng.au.dk/plant-seedlings-dataset/)
- [PlanktonSet 1.0](https://data.nodc.noaa.gov/cgi-bin/iso?id=gov.noaa.nodc:0127422)
- [QUT Fish](https://wiki.qut.edu.au/display/cyphy/Fish+Dataset)

The scripts we used for splitting the datasets can be found in [`utils`](utils).

## How to use

System requirement:
- PyTorch>=0.3.0
- TorchVision>=0.2.0
- PyTorchNet (up to date)

Train from scratch:
```shell
DATASET='flowers17'

python main.py \
    --dataset $DATASET \
    --model alexnet \
    --lr 0.01 \
    --weight-decay 1e-4 \
    --batchsize 32 \
    --print-freq 10 \
    --expname AlexNet \
    --tensorboard \
    --gpu_ids 1 \
    --epochs 300
```

Fine-tuning on ImageNet:
```shell
DATASET='flowers17'

python main.py \
    --pretrained \
    --dataset $DATASET \
    --model alexnet \
    --lr 0.01 \
    --weight-decay 1e-4 \
    --batchsize 32 \
    --print-freq 10 \
    --expname AlexNet \
    --tensorboard \
    --gpu_ids 1 \
    --epochs 300
```

Transfer learning:
```shell
SRC_DATASET='flowers17'
DST_DATASET='flowers102'

python transfer.py \
    --src_dataset $SRC_DATASET \
    --dst_dataset $DST_DATASET \
    --model resnet18 \
    --lr 0.01 \
    --weight-decay 1e-4 \
    --batchsize 16 \
    --print-freq 10 \
    --expname ResNet-18 \
    --tensorboard \
    --gpu_ids 3 \
    --epochs 300 \
    --basemodel '/path/to/'$SRC_DATASET'_checkpoints/ResNet-18/model_best.pth.tar'
```

