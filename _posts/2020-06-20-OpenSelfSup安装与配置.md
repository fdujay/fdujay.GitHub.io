---
layout:     post
title:      OpenSelfSup的安装与配置
subtitle:   如何最方便的使用自监督工具
date:       2020-06-20
author:     靳秋野
header-img: img/post-bg-re-vs-ng2.jpg
catalog: true
tags:
    - 自监督
---

> 如今，自监督学习逐渐成为计算机视觉领域的热门
>
> 为了更好的使用自监督技术，MMLab最新开源了开源自监督库：[OpenSelfSup](https://github.com/open-mmlab/OpenSelfSup)
>
> 那么我们就一起看看如何更好的站在巨人肩膀上进行自监督学习的研究


## 环境配置

首先，官方提供了环境配置的文件[INSTALL.md](https://github.com/open-mmlab/OpenSelfSup/blob/master/docs/INSTALL.md)，跟着说明一步一步来即可。

### Requirements

- Linux (Windows is not officially supported)
- Python 3.5+
- PyTorch 1.1 or higher
- CUDA 9.0 or higher
- NCCL 2
- GCC 4.9 or higher
- [mmcv](https://github.com/open-mmlab/mmcv)

We have tested the following versions of OS and softwares:

- OS: Ubuntu 16.04/18.04 and CentOS 7.2
- CUDA: 9.0/9.2/10.0/10.1
- NCCL: 2.1.15/2.2.13/2.3.7/2.4.2
- GCC(G++): 4.9/5.3/5.4/7.3

### Install openselfsup

a. 创建`conda`虚拟环境并激活.

```shell
conda create -n open-mmlab python=3.7 -y
conda activate open-mmlab
```

b. 安装PyTorch和torchvision（根据 the [official instructions](https://pytorch.org/)）, e.g.,

```shell
conda install pytorch torchvision -c pytorch
```

c. 安装其他第三方库.

```shell
conda install faiss-gpu cudatoolkit=10.0 -c pytorch # optional for DeepCluster and ODC, assuming CUDA=10.0
```

d. 克隆.

```shell
git clone https://github.com/open-mmlab/openselfsup.git
cd openselfsup
```

e. 安装.

```shell
pip install -v -e .  # or "python setup.py develop"
```

**需要注意的是，最好把第bc两步合起来，即：**

```shell
conda install pytorch torchvision faiss-gpu cudatoolkit=10.0 -c pytorch
```

以免在安装的过程中，`cuda`版本先后不一致的情况出现（虽然后安装`cuda`的时候，还是会覆盖之前的版本，但还是麻烦一些）

> 另外，按照上述说明，`OpenSelfSup`是在开发人员模式`dev`下安装的，对代码进行的任何本地修改都将生效，而无需重新安装它（除非您提交了一些`commit`并希望更新版本号）。

## 数据准备

建议将数据集根目录（假设`$YOUR_DATA_ROOT`）符号链接到`$ OPENSELFSUP / data`。 如果文件夹结构不同，则可能需要更改配置文件中的相应路径。

具体的数据准备方法同样参考[INSTALL.md](https://github.com/open-mmlab/OpenSelfSup/blob/master/docs/INSTALL.md)，文档中`PASCAL VOC`是可以自动配置的，`ImageNet`和`Places205`需要自己下载，并自行按照指示配置。

### 准备PASCAL VOC

假设您通常将数据集存储在`$ YOUR_DATA_ROOT`中（例如，对我来说是`/home/davis/data/`）。该脚本将自动将PASCAL VOC 2007下载到​`$ YOUR_DATA_ROOT`中，准备所需的文件，在`$ OPENSELFSUP`下创建一个文件夹`data`，并创建一个符号链接`VOCdevkit`。

