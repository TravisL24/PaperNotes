# Transformers in Medical Imaging

## 脑肿瘤部分

### 1.TransBTS

不需要在大型数据集上进行预训练，直接从头训练。

### 2.Bi-Transformer Unet

注意力模块 + 双ViT层 + 后处理（小于阈值的volume，众投出来的）

### 3.VT-UNet

轻量级 U型 transformer，分层方式

encoder：两个自注意力层捕捉全局 + 局部context

decoder：自注意力 + 交叉注意力 + **傅里叶位置编码**

### 4.Swim UNETR（Hatamizadeh et al.）

swim transformer encoder + CNN decoder

**shifted window partitioning scheme 来计算自注意力**

![Snipaste_2022-12-05_22-34-45.png](https://raw.githubusercontent.com/TravisL24/pic-repo/main/picGo/2022/12/05/20221205223502.png)

## 多器官分割

```
pure Transformers
```

### 1. Karimi pure Transformer

self-attention 用来 相邻线性embedding patch块(neighboring linear embedding of 3D medical image patches)

## 2. Swim UNet

-在local window中 计算自注意力 ==> 相对于输入图像时线性复杂度

-patch expanding 层 上采样解码层特征 ==> **优于常规的 双线性上采样**

```
混合模式-Encoder部分
```

### 3.TransUNet

![TranUnet.png](https://raw.githubusercontent.com/TravisL24/pic-repo/main/picGo/2022/12/06/20221206144739.png)

CNN 处理好image后，Transformer层去tokenized image patches

encoder： 12层Transformer Layers

### 4. TransFuse

BiFusion module去融合了Transformer和CNN的特征

Transfuse 和 TransUNet都需要<u>**预训练去学习位置编码</u>**

### 5. Valanrasu的优化

改良的门注意力层 ==> 不用预训练就可以学习到位置编码

local-global学习方案去优化分割结果

### 6. Swim UNETR(Tang et al.)

<u>用 有代理任务的新型自监督学习框架来预训练</u>Transformer encoder

### 7.Sobirov

<u>*用在了 头颈部肿瘤分割*</u>并且SOTA

```
即插即用，Transformer往CNN里面插入
```

### 8.TransClaw-UNet

transformer layer插入到 Claw UNet的encoder层中

### 9.LeViT-UNet

LeViT 和 CNN的混合体

```
混合模式-Transformer between Encoder and Decoder. 
    避免在下采样的过程中丢失细节
```

### 10.  TransAttUnet

guided attention + 多尺度跳跃连接 + <u>自注意力模块( 全局空间注意力 + transformer 自注意力)</u>

### 11.AFTer-UNet(Axial Fusion Transformer)

轴向融合层( axial fusion layer) ==> computationally efficent

```
混合模式- Transformer in Encoder and Decoder
```

### 12. UTNet

自注意力复杂度降低到 linear级别 + *<u>两维相对位置编码</u>*



### 13. nnFormer

cnn--空间信息，Transformer--全局context信息

自注意力 (local window计算的)  + 深监督 in decoder



### 14. DS-TransUNet(Dual Swin Transformer UNet)

--输入分割成两个不同尺度的不重叠patches

--encoder使用了Transformer 融合模块 ==> 建立不同尺度特征的long-range dependencies



```
混合模式-Transformer in Decoder
```

### 15. Li et al.

<u>window-based 自注意力机制 去上采样</u>特征图 > 双线性插值上采样

### 16.SegTran

SE Transformer + 可学习正弦位置编码

squeeze block ==> regularize the attention matrix(正则化注意力矩阵)

expansion block ==>  learn diversified representations (学习多样化表示)



## 多尺度架构

### 1.UNETR

encoder：pure transformer

decoder：cnn

缺点：计算复杂度很大

### 2.CoTr

![CoTr.png](https://raw.githubusercontent.com/TravisL24/pic-repo/main/picGo/2022/12/06/20221206204418.png)



使用了可变形自注意力模块
