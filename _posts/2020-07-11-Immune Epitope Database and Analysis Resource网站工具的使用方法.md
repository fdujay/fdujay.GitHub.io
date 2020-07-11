---
layout:     post
title:      Immune Epitope Database and Analysis Resource
subtitle:   如何快捷的使用网站进行生物信息分析
date:       2020-07-11
author:     谭丹
header-img: img/post-bg-hacker.jpg
catalog: true
tags:
    - 生物信息
---

# Immune Epitope Database and Analysis Resource网站的使用方法

## 1. 背景

HLA分型技术 主要组织相容性复合体(MHC)是脊椎动物体内最复杂且具有高度多态性的基因群。1984年George Snell 首次发现小鼠MHC即H-2，1958年Dausset 发现了人的MHC即HLA(人类白细胞抗原)基因。MHC的表达产物称为主要组织相容性抗原，MHC抗原是有核细胞表面膜蛋白分子，对抗原递呈和免疫信号传递起关键作用。

## 2. 使用步骤

### 2.1 主页

链接：[http://www.iedb.org/home_v3.php](http://www.iedb.org/home_v3.php)

页面指示：

![image-20200711185651988](https://raw.githubusercontent.com/fdujay/online_img/master/img1/image-20200711185651988.png)

### 2.2 T-Cell 表位预测

点击主页右上角T Cell Epitope Predition中的[MHC I Binding](http://tools.iedb.org/mhci/)

<img src="https://raw.githubusercontent.com/fdujay/online_img/master/img1/image-20200711190232747.png" alt="image-20200711190232747" style="zoom:67%;" />

可以按照自己的需求调整选项：

- `Enter protein sequence(s) in FASTA format or as whitespace-separated sequences.` 可以粘贴序列，也可以load文件，注意不要有空格或者空白段落；
- `Prediction Method` 默认推荐选项即可；
- `MHC source species` 选择`human`
- `Show only frequently occuring alleles` 勾选`Allele`，添加`HLA-A*02:01`，配套Length选择`All lengths`。
- `Sort peptides` 选择 `Position in sequence`
- `Show` 选择 `All preditions`
- `Output format`选择 `Text file`/`HTML table`都可以

然后点击提交就可以得到分析表格了。