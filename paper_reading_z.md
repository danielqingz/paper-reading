<i>Title</i>: <a href="https://arxiv.org/pdf/2010.04380v1.pdf">Token-level Adaptive Training for Neural Machine Translation</a> (EMNLP 2020) <br>

<i>Author</i>: Shuhao Gu, Jinchao Zhang<br>

<i>Comments</i>: 
这也是一篇探讨低频词的工作，强调了低频词在翻译任务中的重要性，还是从loss function下手，通过修改权重的方式改变model对不同频率词的注意力。

本文讨论了两个通过修改权重解决高低频token不平衡问题的工作，Focal Loss和Linear weight function<a href="https://dl.acm.org/doi/pdf/10.1145/3308558.3313415">Improving Neural Response Diversity with Frequency-Aware Cross-Entropy Loss</a>，分析这两个工作效果不好的原因都是在于强行修改loss权重导致损害了模型对高频词的学习。

之后提出了自己的方法，实际上就是把“惩罚”loss改进为“奖励”loss，低频token给予更高的权重，整体权重>=1，然后在数学上提出两个权重公式分别乘在loss上，一个是随着token频率的增加权重指数递减，另一个是考虑了noisy token的问题，将特别低频的token权重反而降低。

进入实验部分，这个工作做了n个实验：base model；base model基础上fine-tune（fine-tune所用的数据是训练base model的数据，及额外的包含有更多低频token的数据集）；设计了一个function使模型在epoch中能更多的见到包含低频词的例子；利用Linear weight function的例子；以及利用上述两种方法的实验，其中这两个都是先训练一段时间，然后再以新方法在低学习率上继续train。为了验证效果，该工作用multi-bleu作为评测标准，还sample一些翻译例子，证明自己的模型能翻译出低频词；还分析了词的diversity，进一步佐证生成了更多的低频词。

在这个工作中存在一些问题：1）测试的数据集，该工作自己分了一个low一个high的测试集，描述为：一个包含更多的低频tokens，另一个包含更多的高频tokens，但没有明确的分布。2）还是没有具体分析低频词在模型学习过程中的作用。

By Jiaqing Zhang
