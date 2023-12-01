### Show-1: Marrying Pixel and Latent Diffusion Models for Text-to-Video Generation

(Paperswithcode Trending Top2)
From:Show Lab, National University of Singapore
开源时间：[10/12/2023]
代码：https://github.com/showlab/show-1
论文：https://arxiv.org/abs/2309.15818

我们组主要做 AIGC 相关的，包括图像/视频的生成和编辑。这篇文章是最近的一篇比较有影响力的工作，你可以先看看，因为你这边还有一些课业，所以咱们可以不着急哈。
大概1个月后，11月13号的时候你做一个 ppt 来做一次 paper reading，你看可以吗

### 论文标题

Show-1: Marrying Pixel and Latent Diffusion Models for Text-to-Video Generation


### 介绍

    当前文本到视频生成技术在基于像素（pixel-based）和基于潜在要素（latent-based）的视频扩散模型（VDMs）方面取得了显著进展。然而，基于像素的VDMs虽然能准确生成动作，却需消耗大量计算资源；而基于潜在要素的VDMs虽计算效率更高，但无法得到精确度高的文本-视频对齐。本文提出了一种结合像素和潜在要素的混合模型（Show-1)，先通过基于像素的VDMs生成较低分辨率但文本-视频强相关性的视频，再通过一种专家翻译方法，利用基于潜在要素的VDMs将低分辨率视频上采样到高分辨率。较于先前的工作，Show-1结合了两者的优势，在消耗更少的计算资源的情况下，保持了视频的高质量和精确的文本对齐能力。
