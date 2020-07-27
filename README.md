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
<div align=center>
<img width = '500' height = '300' src = "https://github.com/missFuture/zte-com2020/blob/master/images/%E4%BA%94%E5%8F%82%E6%95%B0%E6%B3%95%E8%A1%A8%E5%BE%81.png"/>
</div>

## 数据集概述
抓取检测唯一公开的是2011年康奈尔大学提出的Cornell Grasping Dataset。该数据集包含240中物品，885张图片，每一个样本中标注了若干有效抓取框和无效抓取框。部分样本可见下图：
<div align=center>
<img width = '561' height = '540' src = "https://github.com/missFuture/zte-com2020/blob/master/images/CGD_sample.png"/>
</div>

## 数据集预处理
### 数据增强
由于数据集较为匮乏，为了防止过拟合， 需要对数据集进行数据增强。主要是对原始图像进行旋转，平移，裁剪，像素级变换等处理，每一个样本经过增强后大致能得到100个样本。
### 角度变换
如果沿用将
