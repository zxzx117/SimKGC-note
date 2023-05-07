---


---

<p>#SimKGC的阅读笔记</p>
<p>与之前的KGC方法的不同：<br>
SimKGC是基于文本的，相较于基于嵌入的方法，它所携带的信息更多，对于每个实体都有对应的描述。基于嵌入的方法是transductive，而simKGC是inductive,更适用于构建一个通用的KG。<br>
所以基于文本理应优于基于嵌入的方法，但事实不是如此，因为基于嵌入的方法不涉及文本，所以可以有效训练大量负样本，而基于文本就不行，这就要求有新的负采样策略来满足对比学习。本文采用了in-batch negatives、pre-batch negatives、self-negatives(hard negatives mining)三种负采样策略来弥补因为基于文本而产生的负采样不足的问题。</p>
<p>##re-rank<br>
基于文本的模型很依赖文本对于实体的描述，而忽略了邻居的关联，所以提出了re-rank策略，来提高head的邻居分数。但其实本文在实验和源码部分提及，加入re-rank并不一定会使它更优秀，在代码注释中也写到了默认情况下不使用re-rank策略。</p>
<p>以往KGC的链路预测任务推测三元组，tail需要对给给定的head和relation排序，head也同样如此，SimKGC提出了将所有的三元组进行一个逆向的操作，这样就不再需要预测head，转而将链接预测任务全部变成tail。</p>
<p>模型的主要架构是一个双Bert的编码器，对于Bert我还在了解，关于Bert的部分，在学习完之后会更新过来。![输入图片说明](/imgs/2023-05-07/cx1Mt1lRuPiHYLil.png</p>

