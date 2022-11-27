# CoTr: Efficiently Bridging CNN and Transformer for 3D Medical Image Segmentation

**关键词**：Conv + Transformer(defomable)，deformable self-attention mechanism, 多尺度

![模型图.png](https://raw.githubusercontent.com/TravisL24/pic-repo/main/picGo/2022/11/27/20221127200808.png)

**主要思路**：

1. conv 和 transformer混合处理3D图像

2. 用deformable 自注意力机制来减少复杂度

## 模块细节

### 1.CNN encoder

3D conv + IN + ReLU（3，3，2）

### 2.DeTrans encoder

多尺度的来捕获long-range context 信息

**细节**：

1. <u>flatten 特征图 变成 1D序列</u>（空间信息损失的问题怎么处理？）
   
   用3D位置编码序列去处理空间信息损失问题
   
   ![位置编码.png](https://raw.githubusercontent.com/TravisL24/pic-repo/main/picGo/2022/11/27/20221127204100.png)

2. MS-DMSA，多头注意力机制只关注部分samling locations（这个部分是怎么去找到的呢?）
   
   ![head公式.png](https://raw.githubusercontent.com/TravisL24/pic-repo/main/picGo/2022/11/27/20221127211544.png)
   
   1 - attention 权重
   2 - 用 $P_q$ 去re-scale 特征
   3 - 采样点偏移 <-- 这个偏移的作用是？

3. DeTrans Layer
   
   MS-DMSA layer + FFN + layer normalization

### 3.Decoder

      output sequece 要 reshape成对应尺寸的feature maps

       解码部分全部是<u>CNN部分</u>，添加了 **深监督**

## 实验部分

![实验结果.png](https://raw.githubusercontent.com/TravisL24/pic-repo/main/picGo/2022/11/27/20221127221524.png)
