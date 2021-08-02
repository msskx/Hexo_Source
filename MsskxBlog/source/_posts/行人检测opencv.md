---
title: 行人检测 OpenCV
date: 2021-07-24 22:06:00
updated:
tags: python
categories: python
description: 基于opencv的python实现行人检测 
---


```python
# python detect.py --images images
````
```python
# 导入必要的包
from __future__ import print_function
from imutils.object_detection import non_max_suppression
from imutils import paths
import numpy as np
import argparse
import imutils
import cv2
```

```python
# 构造参数parse并解析参数，处理解析我们的命令行参数。我们这里只需要一个开关，--images ，这是包含我们要执行行人检测的图像列表的目录的路径。
ap = argparse.ArgumentParser()
ap.add_argument("-i", "--images", required=True, help="path to images directory")
args = vars(ap.parse_args())

```

```python
# 初始化描述器/人检测器
# 初始化我们的行人检测器。首先，我们调用hog = cv2.HOGDescriptor() 它初始化了定向梯度直方图描述符。
# 然后，我们调用设置SVM检测器 将支持向量机设置为预训练的行人检测器，
# 通过 cv2.HOGDescriptor_getDefaultPeopleDetector()功能。
hog = cv2.HOGDescriptor()
hog.setSVMDetector(cv2.HOGDescriptor_getDefaultPeopleDetector())
```

```python
# 在图像路径上循环
# 我们开始循环遍历我们的图像-images 目录。这篇报告中的示例（以及本文源代码中包含的其他图像）
imagePaths = list(paths.list_images(args["images"]))
```
```python
for imagePath in imagePaths:
	# 加载图像并调整其大小以（1）减少检测时间和（2）提高检测精度
	image = cv2.imread(imagePath)
	image = imutils.resize(image, width=min(400, image.shape[1]))
	orig = image.copy()
```
```python
# 检测图像中的人
	(rects, weights) = hog.detectMultiScale(image, winStride=(4, 4),
		padding=(8, 8), scale=1.05)
```

```python
# 绘制原始边界框
# 获取我们的初始边界框并将它们绘制在我们的图像上
	for (x, y, w, h) in rects:
		cv2.rectangle(orig, (x, y), (x + w, y + h), (0, 0, 255), 2)
```
```python
	# 使用相当大的重叠阈值对边界框应用非最大值抑制，以尝试保持仍然是人的重叠框
	# 对于某些图像，每个人检测到多个重叠的边界框
	# 在这种情况下，我们有两个选择。我们可以检测一个边界框是否完全包含在另一个边界框内。
	# 或者我们可以应用非最大值抑制并抑制与重要阈值重叠的边界框——如下
	rects = np.array([[x, y, x + w, y + h] for (x, y, w, h) in rects])
	pick = non_max_suppression(rects, probs=None, overlapThresh=0.65)
```
```python

	# 绘制最终边界框
	for (xA, yA, xB, yB) in pick:
		cv2.rectangle(image, (xA, yA), (xB, yB), (0, 255, 0), 2)
	
	# 显示有关边界框数量的一些信息
	filename = imagePath[imagePath.rfind("/") + 1:]
	print("[INFO] {}: {} original boxes, {} after suppression".format(
		filename, len(rects), len(pick)))
```
```python
	# 显示输出图像
	cv2.imshow("Before NMS", orig)
	cv2.imshow("After NMS", image)
	cv2.waitKey(0)
```

