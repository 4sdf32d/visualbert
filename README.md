# 中文多模态bert

bert的提出极大得推动了NLP的发展，但随着多模态任务的增多（这在很多企业中已经成为一种常见的任务），单纯的NLPBert已经无法满足需求。

后续看到了很多的paper也陆续都采用了transformer预训练多模态bert，但都基本是英文领域。

该项目主要是预训练中文的多模态Bert，也是为了以后的多模态任务提供基本的模型

## 相关paper
[参考](https://mp.weixin.qq.com/s/THxlQX2MPXua0_N0Ug0EWA)

1. VisualBERT 


论文标题：VisualBERT: A Simple and Performant Baseline for Vision and Language
论文链接：https://arxiv.org/abs/1908.03557
源码链接：https://github.com/uclanlp/visualbert

和 BERT 类似，VisualBERT 在结构上采用了堆叠的 Transformer。其在一开始就将文字和图片信息通过 Transformer 的自注意力机制进行对齐融合。

其文字部分的输入为原始的 BERT 文字输入（词向量+位置编码+片段编码）加上 Token/Image 编码来表示其是图片或文字，而图片部分的输入则是采用通过 Faster-RCNN 提取的图片区域特征加上相应的位置编码，片段编码和 Token/Image 编码（如下图右侧所示）。



VisualBERT 遵循 BERT 一样的流程，先进行预训练然后在相应的任务上进行微调，其采用了两个预训练任务：第一个是和 BERT 一样的语言掩码，第二个则是句子-图像预测 （即判断输入的句子是否为相应图片的描述）。

作者在 VQA，VCR，NLVR2 和 Flickr30k 四个视觉语言任务上进行了测试，结果表明 VisualBERT 在四个任务中都达到了最好的表现或和已知最好表现相近的表现。进一步的消融实验表明 VisualBERT 可以有效地学习到语言和相应图像区域的联系，同时也具有一定的句法敏感性。


## 实现逻辑
上述的paper都基本采用了COCO数据集，但中文领域很难找到能达到COCO规模的数据，因此打算将COCO的英文标注翻译为中文即可得到中文领域的数据集，会存在些翻译导致的偏差。

