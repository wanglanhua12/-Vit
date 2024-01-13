# 启动项目
## 1 解压数据集
下载数据集到本地，或在云端进行解压，注意数据集解压路径。
```
!unzip -oq data/data135339/cat12_dataset.zip -d ./
```

## 2 克隆PaddleClas
```
!git clone https://gitee.com/paddlepaddle/PaddleClas.git -b release/2.3
%cd PaddleClas/
!pip install --upgrade -r requirements.txt -i https://mirror.baidu.com/pypi/simple
%cd ../
```

## 3 修改配置文件
配置文件保存在config文件夹下
- config/ViT_small_patch16_224.yaml

## 4 模型训练
`-c`指定配置文件路径，`-o`修改配置文件参数，加载预训练模型进行微调。
- ViT模型训练
```
!python PaddleClas/tools/train.py  \
    -c config/ViT_small_patch16_224.yaml  \
    -o Arch.pretrained=True  \
```

## 5 模型评估
- ViT模型评估结果：CELoss: 0.24738, loss: 0.24738, top1: 0.91183, top5: 1.00000
```
!python PaddleClas/tools/eval.py  \
    -c config/ViT_small_patch16_224.yaml  \
    -o Global.pretrained_model=output/ViT_small_patch16_224/best_model  \
```

## 模型预测
预测结果保存为CSV格式文件，替换`PaddleClas/ppcls/engine/engine.py`370行for循环代码，并在开头添加`import pandas as pd`。
- ViT模型预测
```
!python PaddleClas/tools/infer.py  \
    -c config/ViT_small_patch16_224.yaml  \
    -o Infer.infer_imgs=dataset/cat_12_test  \
    -o Global.pretrained_model=output/ViT_small_patch16_224/best_model  \
```













