# yolov5在rk3588平台上的使用方法  

## 模型训练  
训练仓：github.com/airockchip/yolov5

## 导出onnx模型  
修改./models/yolo.py--class Detect--def forward
```python
def forward(self, x):
#rknn######################################################################
    for i in range(self.nl):
        x[i] = self.m[i](x[i])  # conv
    return x
#######################################################################
```
注：在训练时屏蔽此修改
命令行运行：python export.py --rknpu 3588

## 转换rknn模型  
安装rknn-toolkit2 1.5.0+1fa95b5c
使用rknpu2-1.5.0/examples/rknn_yolov5_demo/convert_rknn_demo/yolov5/onn2rknn.py转换

## 在rk3588工控机上运行  
使用的rknpu2-1.5.0/examples/rknn_yolov5_demo/build-linux_RK3588.sh

## F&Q  
"在lpa3588平台，使用rknpu2-1.5.0运行yolov5模型有些问题。检测出的框的位置比较乱，置信度都0.51左右。训练使用的github.com/airockchip/yolov5，官方已经激活函数都是改好relu的，并用export.py生成了onnx模型，pt模型做detect.py检测正常。转换工具包安装的rknn-toolkit2 1.5.0+1fa95b5c。转换程序分别使用了rknpu2-1.5.0/examples/rknn_yolov5_demo/convert_rknn_demo/yolov5/onn2rknn.py和rknn_model_zoo/models/CV/object_detection/yolo/RKNN_model_convert/convert_yolo_ppyolo.sh。板载端使用的rknpu2-1.5.0/examples/rknn_yolov5_demo/build-linux_RK3588.sh测试的，anchor、OBJ_CLASS_NUMB等参数都改过了。"
"可以了，是export.py导出onnx的问题。教程中让用https://github.com/airockchip/yolov5仓库来训练、导出，且导出也有"--rknn"参数进去相关流程，改成./models--yolo.py--class Detect--def forward中下图的方式可在板载端正常推理。"
