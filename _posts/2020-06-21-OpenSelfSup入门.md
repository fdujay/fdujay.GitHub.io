---
layout:     post
title:      OpenSelfSup入门
subtitle:   如何最方便的使用自监督工具
date:       2020-06-21
author:     靳秋野
header-img: img/post-bg-re-vs-ng2.jpg
catalog: true
tags:
    - 自监督
---

> 在上一篇博客当中，我们介绍了如何安装与配置OpenSelfSup
>
> 在本片博客中，我们将介绍如何快速入门OpenSelfSup自监督库
>
> 如果你对于之前的预备工作有疑问，请参考这篇[博文](https://fdujay.github.io/2020/06/20/OpenSelfSup%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE/)

## 入门

本页提供有关OpenSelfSup用法的基本教程，如果想要了解更多内容，如在单台计算机上启动多个作业等，请参考官方文档[GETTING_STARTED.md](https://github.com/fdujay/OpenSelfSup/blob/master/docs/GETTING_STARTED.md)。

**注意**：配置文件中的默认学习率是8个GPU（`configs/linear_classification`使用1个GPU的除外）。如果使用不同数量的GPU，则总批次大小将成比例变化，您必须调整学习率`new_lr = old_lr * new_ngpus / old_ngpus`。我们建议`tools/dist_train.sh`即使在1 gpu的情况下也要使用，因为某些方法不支持非分布式训练。

### 使用单个/多个GPU进行训练

```shell
bash tools/dist_train.sh ${CONFIG_FILE} ${GPUS} [optional arguments]
```

可选参数为：

- `--resume_from ${CHECKPOINT_FILE}`：从先前的检查点文件恢复。
- `--pretrained ${PRETRAIN_WEIGHTS}`：为backbone加载预训练的权重。
- `--deterministic`：打开“确定性”模式，这会减慢训练速度，但结果可重复。
- `GPUS`是指可用显卡的块数。

一个例子：

```shell
# checkpoints and logs saved in WORK_DIR=work_dirs/selfsup/odc/r50_v1/
bash tools/dist_train.sh configs/selfsup/odc/r50_v1.py 8
```

**注意**：在训练过程中，检查点和日志与下的配置文件保存在相同的文件夹结构中`work_dirs/`。不建议使用自定义工作目录，因为评估脚本会从配置文件名推断出工作目录。如果您想将重量保存在其他地方，请使用符号链接，例如：

```
ln -s / DATA / xhzhan / openselfsup_workdirs $ {OPENSELFSUP} / work_dirs
```

## 基准测试

我们提供了几种标准基准来评估表征学习。如果要在出版物中使用此存储库，建议不要更改下面提到的用于评估的配置文件或脚本。我们希望所有方法都能得到公平的比较。

### VOC07 Linear SVM & Low-shot Linear SVM

```shell
# test by epoch
bash benchmarks/dist_test_svm_epoch.sh ${CONFIG_FILE} ${EPOCH} ${FEAT_LIST} ${GPUS}
# test pretrained model
bash benchmarks/dist_test_svm_pretrain.sh ${CONFIG_FILE} ${PRETRAIN} ${FEAT_LIST} ${GPUS}
# test random init
bash benchmarks/dist_test_svm_pretrain.sh ${CONFIG_FILE} "random" ${FEAT_LIST} ${GPUS}
```