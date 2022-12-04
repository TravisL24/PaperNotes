# RepGhost: A Hardware-Efficient Ghost Module via Re-parameterization

**关键词**：可重参数（structural re-parameterization technique.），add替换concat

**思想**：<u>重新设计结构，来增加特征重用（reuse），减少推理时间</u>

## 相关工作

### 1.轻量化CNN

    -- depth-wise conv 替代 dense conv

    -- feature reuse

### 2.Structural Re-parameterization

    推理的时候，从feature space 转移到weight space

    train：3*3 conv + 1 * 1 conv  + IN + add == inference : 3 * 3 conv

    作者认为 <u>add的操作 实现了一个feature fusion</u>的效果，

### 3. RepGhost模块

<img src="https://raw.githubusercontent.com/TravisL24/pic-repo/main/picGo/2022/11/30/20221130153327.png" title="" alt="RepGhostModule.png" data-align="center">

### 网络结构

<img src="https://raw.githubusercontent.com/TravisL24/pic-repo/main/picGo/2022/11/30/20221130162004.png" title="" alt="model.png" data-align="center">
