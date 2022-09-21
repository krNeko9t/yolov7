# 配置环境
## 安装conda
https://anaconda.org/
用于python独立环境

## 依赖环境
- CUDA 11.3.1 (手动安装)
- Pytorch 1.21.1
- torchvision 0.13

## 克隆项目
``` shell
git clone https://github.com/WongKinYiu/yolov7.git
```

## 安装python环境
``` shell
pip install -r requirements.txt
```

## 安装pytorch (conda)
``` shell
conda install pytorch torchvision torchaudio cudatoolkit=11.3 -c pytorch
```

# 训练
## 数据集存放路径
- e
- └──datasets
     -   └──paris
         -   ├──images
         -   └──labels


## 训练数据集

``` shell
cd path/to/your/project/

# 最小规模网络
python train.py --workers 8 --device 0 --batch-size 32 --data data/facade.yaml --img 640 640 --cfg cfg/training/tiny-c.yaml --weights '' --name yolov7-custom --hyp data/hyp.scratch.p5.yaml

# 小规模网络（显存不够）
python train.py --workers 8 --device 0 --batch-size 32 --data data/facade.yaml --img 640 640 --cfg cfg/training/v7-custom.yaml --weights '' --name yolov7-custom --hyp data/hyp.scratch.p5.yaml

# 大规模网络（显存不够）
python train_aux.py --workers 8 --device 0 --batch-size 16 --data data/facade.yaml --img 1280 1280 --cfg cfg/training/w6-custom.yaml --weights 'yolov7-w6_training.pt' --name yolov7-w6-custom --hyp data/hyp.scratch.p6.yaml
```

## 测试结果
```bash
python detect.py --weights building_det.pt --conf 0.25 --img-size 640 --source e:/datasets/test/ppt-1
```