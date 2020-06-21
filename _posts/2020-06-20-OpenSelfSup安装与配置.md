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

需要注意的是，最好把第二三步合起来，即：

```shell
conda install pytorch torchvision faiss-gpu cudatoolkit=10.0 -c pytorch
```

以免在安装的过程中，`cuda`版本先后不一致的情况出现（虽然后安装`cuda`的时候，还是会覆盖之前的版本，但还是麻烦一些）

> 另外，按照上述说明，`OpenSelfSup`是在开发人员模式`dev`下安装的，对代码进行的任何本地修改都将生效，而无需重新安装它（除非您提交了一些`commit`并希望更新版本号）。

## 数据准备

建议将数据集根目录（假设`$YOUR_DATA_ROOT`）符号链接到`$ OPENSELFSUP / data`。 如果文件夹结构不同，则可能需要更改配置文件中的相应路径。

具体的数据准备方法同样参考[INSTALL.md](https://github.com/open-mmlab/OpenSelfSup/blob/master/docs/INSTALL.md)