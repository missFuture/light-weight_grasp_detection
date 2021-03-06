# light-weight_grasp_detection
一种轻量型的抓取检测网络模型，基于康奈尔抓取检测数据集，平均准确率90%，速度70FPS
## 抓取检测概述
本课题主要研究复杂场景下的多目标机器人抓取检测问题,抓取检测指的是给定一个物体,找到一种满足抓取任务需求的夹具抓取配置。该课题属于计算机视觉中目标检测范围，大部分目标检测研究的是物体
种类以及物体的具体位置信息， 抓取检测一般不需要对物体进行识别，给出有效的抓取框即可，该抓取框一般是带有角度（见下图所标注）。抓取配置可以由五参数法表示：
<p align="center">
<font face="黑体" size=15>
g = {θ, x, y, w, h}
</font>
</p>
具体的示意图可参考：
<p align="center">
<img width = '500' height = '300' src = "https://github.com/missFuture/zte-com2020/blob/master/images/five_para.png"/>
</p>

## 数据集概述
抓取检测唯一公开的是2011年康奈尔大学提出的Cornell Grasping Dataset。该数据集包含240中物品，885张图片，每一个样本中标注了若干有效抓取框和无效抓取框。部分样本可见下图：
<p align="center">
<img width = '250' height = '250' src = "https://github.com/missFuture/zte-com2020/blob/master/images/CGD_sample.png"/>
</p>

## 数据集预处理
### 数据增强
由于数据集较为匮乏，为了防止过拟合， 需要对数据集进行数据增强。主要是对原始图像进行旋转，平移，裁剪，像素级变换等处理，每一个样本经过增强后大致能得到100个样本。
### 角度变换
如果沿用直接回归五参数的方法，模型的泛化性能收到很大影响。同时，考虑到抓取检测模型对角度的要求并非十分苛刻，角度相差一点还可以正常进行抓取，然后对于位置信息却不行，所以对角度信息做了分类处理。
<p align="center">
<img width = '600' height = '200' src = "https://github.com/missFuture/zte-com2020/blob/master/images/degree_cls.png"/>
</p>

## 抓取检测模型
采用一种轻量型目标识别网络[SqueezeNet](https://arxiv.org/abs/1602.07360).该网络的特点在于：采用模块化的设计思想，模块有Squeeze层和Expand层，极大的减少参数量。设计原则如下：
- 1.使用1∗11∗1卷积代替3∗33∗3 卷积：参数减少为原来的1/9 
- 2.减少输入通道数量：这一部分使用squeeze layers来实现 
- 3.将欠采样操作延后，可以给卷积层提供更大的激活图：更大的激活图保留了更多的信息，可以提供更高的分类准确率
<br/>抓取模型如图所示：</br>
<p align="center">
<img width = '468' height = '400' src = "https://github.com/missFuture/zte-com2020/blob/master/images/squeezenet.png"/>
</p>

## 抓取检测结果
在CGD上面进行测试，得到最后的平均准确率是90%， 速度超过50帧（GTX Titanx）。部分测试结果如图所示（**左侧：正确，右侧：错误**）。
<p align="center">
<img width = '1000' height = '500' src = "https://github.com/missFuture/zte-com2020/blob/master/images/single_object_result.png"/>
</p>

