<i> Title </i>: <a href="https://arxiv.org/pdf/2301.07014.pdf"> Dataset Distillation: A Comprehensive Review  </a> (IEEE TRANSACTIONS ON PATTERN ANALYSIS AND MACHINE INTELLIGENCE 2023) <br>

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


    $$S = \mathop{argmin}\limits_{S}L(S,T)$$

    主流的 $L$ 有三种：1）Performance Matching，2）Parameter Matching，3）Distribution Matching

    有一系列工作又提出了Synthetic Data Parameterization，用function $g_\phi$ 编码的code $Z$ 来map raw iamges，在下游任务训练时，参数 $\phi$ 和 $Z$ 可以被update。

    主流的 $g_\phi(\cdot)$ 有：1）Differentiable Siamese Augmentation，2）Upsampling，3）Generators and Latent Vectors

* Experiments

    5.4  Empirical Studies总结的不错，建议读原文

* Discussion

    Computational cost仍然是个问题，有一系列工作已经在做了；Scaling up问题，在大数据集上难做，需要更高的compression rate；不同的生成模型生成能力不同，performance不同；目前只在分类任务有；安全、隐私问题

01/25/2023 By Jiaqing Zhang

<br>

----

<br>

<i> Title </i>: <a href="https://openaccess.thecvf.com/content_CVPRW_2019/papers/Weakly%20Supervised%20Learning%20for%20Real-World%20Computer%20Vision%20Applications/Xu_Missing_Labels_in_Object_Detection_CVPRW_2019_paper.pdf"> Missing Labels in Object Detection </a> (CVPR 2019) <br>

<i>Author </i>: Mengmeng Xu, Yancheng Bai,  Bernard Ghanem <br>

<i>Comments </i>:

* Background

    OB任务中，数据未必完美，会存在一些missing labels，比如一张图片有三只羊，但bbox只圈出了其中一只，这样的数据对于训练肯定是有影响的。作者的实验也证明如此

* Method

    先用一个weakly supervised od model作为teacher model，生成pseudo labels，然后把这些labels和已存在的annotations合并，然后再训练supervised od model。一旦detector的效果提升了，就会更新一遍pseudo labels，让他们更好。

    

* Discussion

    有点儿像知识蒸馏，用weakly supervised model的原因我觉得是因为相对supervised model，生成的结果更general，不会被限制住。做法不算难感觉比较有效，但是citation并不多，而且这个数据还有both image-， instance- level的labels，可能这个任务会比较简单。

01/26/2023 By Jiaqing Zhang

<br>

----

<br>


<i> Title </i>: <a href="https://www.sciencedirect.com/science/article/pii/S1361841521001080"> A survey on active learning and human-in-the-loop deep learning for medical image analysis </a> (Medical Image Analysis 2021) <br>

<i>Author </i>: Samuel Budd, Emma C. Robinson,  Bernhard Kainz <br>

<i>Comments </i>:

Human-in-the-loop的应用：1）Active Learning，2）Interaction with model outputs，人类参与prediction

* AL
    
    AL首先要考虑选哪种Query，有1）Stream-based Selective Sampling，cost低但是效果一般不好，2）Membership Query Synthesis，生成模型认为最有information的data-point，GAN在这方面表现不错，3）Pool-based Sampling，在没标注的池子里measure informativeness，然后rank，然后选出最有信息的

    AL其次要考虑怎么Evaluating informativeness，1）Uncertainty，2）Representativeness，3）GAN，4）[Learning active learning]()，用一个regression model学selection策略，Rl也可以用在AL里

    AL最后要考虑是Fine-tuning还是retraining

* Interactive refinement

    预测之后，人类来修改，然后在tune model

* Practical considerations

    Noisy oracles，大锅label，就是说让大众来label，数量多但是质量差

    弱监督学习，加入image-level的label

    Multi-task learning

    Annotation interface

这篇表面上是讲Human-in-the-loop的，实际上介绍了一大堆别的东西，虽然拉的很长，但是有用的信息还是不少的

01/31/2023 By Jiaqing Zhang

<br>

----

<br>

<i> Title </i>: <a href="https://openaccess.thecvf.com/content_cvpr_2018/papers/Konyushkova_Learning_Intelligent_Dialogs_CVPR_2018_paper.pdf"> Learning Intelligent Dialogs for Bounding Box Annotation </a> (CVPR 2021) <br>

<i>Author </i>: Ksenia Konyushkova, Vittorio Ferrari <br>

<i>Comments </i>:

* 做了啥

    训练agent to自动选择一系列动作（一共就俩：box verification，manual box drawing），使人类完成标注bbox。两种agent，一种预测box被准确verified概率，一种RL model。agent可以自适应模型的难度，提出高效的strategy，比上文俩单独的动作快，detector越强agent越牛。

* 怎么做

    * 方法1

        train一个分类器，预测这个box能不能被接受，预测的probability sort一下，然后跟$\frac{t_V}{t_D}$比较，其中$t_V$是指box verification的时间，$t_D$是指manual box drawing的时间，如果set里没有acceoted的，就直接人工标。

        怎么证明这个合理呢？他们提出了一个Theorem：如果给定acceptance的概率，strategy of动作sequence可以minimizeannotation时间，然后数学+逻辑推导了一下
    * 方法2

        RL的方法，reward是the negative time required for the chosenaction。

    还实验证明了，提升detector的performance，效果变的更好了

* 锐评一下

    肯定是google在做大规模bbox标注的时候想的点子，其实就是把box verification的工作进一步变高级了一点by加入agent来指定训练策略，想法不难，用IoU做标准

02/02/2023 By Jiaqing Zhang

<br>

----

<br>

<i> Title </i>: <a href="https://arxiv.org/abs/1810.01943"> AI Fairness 360: An Extensible Toolkit for Detecting, Understanding, and Mitigating Unwanted Algorithmic Bias </a> (Arxiv 2018) <br>

<i>Author </i>: Rachel K. E. Bellamy, Yunfeng Zhang <br>

<i>Comments </i>:

* 背景

    Fairness一直是AI中的一个重要话题，在关心model performance的同时，也不得不考虑robustness和fairness。

* 功能

    * Metrics

        * 计算Disparate impact和statisticalparity difference，分别是ratio和差值
    
    * Algorithms

        * Mitigating bias：

            * Reweighing（训练的时候加sample weights，简单粗暴），Optimized preprocessing， Learning fair representations，Disparate impact remover。分别来自于四篇工作

            * Adversarial debiasing，Prejudice remove

            * Equalized odds postprocessing（用一个模型学结果），Calibrated equalized odds post-processing（用一个模型学结果），Reject option classification（调整confiddence band）

* 评论

    集成了Fairness相关的各种个样东西，还是很好用的，但是fairness这个问题本身还没有引起过多的关注，目前这个tool有500多引。我觉得是因为大家都focus on主赛道，很多general的问题不涉及fairness，但是在医学，涉及到人类的问题上就很matters，我认为以后这个会更被重视！


02/09/2023 By Jiaqing Zhang

<br>

----

<br>

