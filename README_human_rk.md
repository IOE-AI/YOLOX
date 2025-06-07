# YOLOX_HUMAN_RK

## 安装依赖

```
pip install -r requirements.txt
```

## 安装 yolox

```
pip install -v -e . 
```

## 准备数据集

先使用 obs://obs2learn/dataset/person_5k/hunman_voc_format_5k.zip

## 训练

```
YOLOX_DATADIR=datasets/pascal_voc_format python tools/train.py -f exps/example/yolox_voc/yolox_voc_s_human.py -d 0 -b 64 --fp16 -o 
```

## 增量训练

```
YOLOX_DATADIR=datasets/pascal_voc_format python tools/train.py -f exps/example/yolox_voc/yolox_voc_s_human.py -c weights/best_ckpt.pth -d 0 -b 64 --fp16 -o 
```

## 验证检测模型

```
python tools/demo.py image -f exps/example/yolox_voc/yolox_voc_s_human.py -c YOLOX_outputs/yolox_voc_s_human/best_ckpt.pth --path assets/human.jpg --conf 0.7 --nms 0.65 --tsize 320 --save_result --device gpu
```

## 模型转换

### pt --> onnx

```
python tools/export_onnx.py -h
python3 tools/export_onnx.py --output-name yolox_s_human.onnx -n yolox-s -f exps/example/yolox_voc/yolox_voc_s_human.py -c YOLOX_outputs/yolox_voc_s_human/best_ckpt.pth --rknpu 
```

### onnx --> pt

使用 python3.6、rknn-toolkit2 1.4.0-22dcfef4 进行转换，同时进行量化 