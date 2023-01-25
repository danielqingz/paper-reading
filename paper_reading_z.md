<i>`Title `</i>: Dataset Distillation: A Comprehensive Review <a href="https://arxiv.org/pdf/2301.07014.pdf"> Token-level Adaptive Training for Neural Machine Translation </a> (IEEE TRANSACTIONS ON PATTERN ANALYSIS AND MACHINE INTELLIGENCE 2023) <br>

<i>Author </i>: Ruonan Yu, Songhua Liu,  Xinchao Wang <br>

<i>Comments </i>:

* Background

    数据太多了，负担太大了，得考虑筛选数据了。

    一个intuitive idea是选择数据中最representative or valued的samples，被称作core-set or instance selection，但是这样会discard大量数据，其实还是有用的，且会存在版权问题or隐私问题。因此 datasetdistillation (DD) or dataset condensation (DC)出现了，旨在生成数据for compression。

* Related work

    相关的方法还有knowledge distillation (Teacher model + Student model)，core-set selection，generating modeling和hyperparameter optimization。

    DD vs KD区别在于，DD aims at轻量级的数据，而KD aims at轻量级的model
    DD vs Core-set区别在于，DD基于synthesizing new data，而Core-set基于从原始数据中select；Core-set时隔HP-hard问题

* Method

    DD 做法：1）初始化生成的数据 $S$，randomly生成from Gaussion Noise；randomly从原始数据 $T$ 里sample；用Core-set方法sample。2）找一个model $M$ 优化目标函数，$L$ 是某种objective，在loop里 $M$ 和 $S$ 交替更新直到收敛，获得最终的 $S$。

    $$
        S = \argmin_{S}L(S,T)
    $$

    主流的 $L$ 有三种：1）Performance Matching，2）Parameter Matching，3）Distribution Matching

    有一系列工作又提出了Synthetic Data Parameterization，用function $g_\phi$ 编码的code $Z$ 来map raw iamges，在下游任务训练时，参数 $\phi$ 和 $Z$ 可以被update。

    主流的 $g_\phi(\cdot)$ 有：1）Differentiable Siamese Augmentation，2）Upsampling，3）Generators and Latent Vectors

* Experiments

    5.4  Empirical Studies总结的不错，建议读原文

* Discussion

    Computational cost仍然是个问题，有一系列工作已经在做了；Scaling up问题，在大数据集上难做，需要更高的compression rate；不同的生成模型生成能力不同，performance不同；目前只在分类任务有；安全、隐私问题

01/25/2023 By Jiaqing Zhang
