前言
======

2018年3月30日，Google在加州山景城举行了第二届TensorFlow Dev Summit开发者峰会，并宣布正式发布TensorFlow 1.8版本。笔者有幸获得Google的资助亲临峰会现场，见证了这一具有里程碑式意义的新版本发布。众多新功能的加入和支持展示了TensorFlow的雄心壮志，同时早在2017年秋就开始测试的Eager Execution（动态图机制）在这一版本中终于正式加入，并成为了入门TensorFlow的官方推荐模式。

    The easiest way to get started with TensorFlow is using Eager Execution.
    
    —— https://www.tensorflow.org/get_started/

在此之前，TensorFlow所基于的传统Graph Execution的弊端，如入门门槛高、调试困难、灵活性差、无法使用Python原生控制语句等早已被开发者诟病许久。一些新的基于动态图机制的深度学习框架（如PyTorch）也横空出世，并以其易用性和快速开发的特性而占据了一席之地。尤其是在学术研究等需要快速迭代模型的领域，PyTorch等新兴深度学习框架已经成为主流。笔者所在的数十人的机器学习实验室中，竟只有笔者一人“守旧”地使用TensorFlow。然而，直到目前，市面上相关的TensorFlow相关的中文技术书籍及资料仍然基于传统的Graph Execution模式，让不少初学者（尤其是刚学过机器学习课程的大学生）望而却步。由此，在TensorFlow正式支持Eager Execution之际，有必要出现一本全新的技术手册，帮助初学者及需要快速迭代模型的研究者，以一个全新的角度快速入门TensorFlow。

同时，本手册还有第二个任务。市面上与TensorFlow相关的中文技术书籍大部分都以深度学习为主线，而将TensorFlow作为这些深度学习模型的实现方式。这样固然有体系完整的优点，然而对于已经对机器学习或深度学习理论有所了解，希望侧重于学习TensorFlow本身的读者而言，就显得不够友好。同时，虽然TensorFlow有官方的教学文档（https://tensorflow.google.cn/tutorials），然而在体例上显得逻辑性不足，缺乏一般教学文档从浅入深，层次递进的特性，而更类似于一系列技术文档的罗列。于是，笔者希望编写一本手册，以尽量精简的篇幅展示TensorFlow作为一个计算框架的主要特性，并弥补官方手册的不足，力图能让已经有一定机器学习/深度学习知识及编程能力的读者迅速上手TensorFlow，并在实际编程过程中可以随时查阅并解决实际问题。

本手册的主要特征有：

* 主要基于TensorFlow最新的Eager Execution（动态图）模式，以便于模型的快速迭代开发。但依然会包含传统的Graph Execution模式，代码上尽可能兼容两者；
* 定位以教学及工具书为主，编排以TensorFlow的各项概念和功能为核心，力求能够让TensorFlow开发者快速查阅。各章相对独立，不一定需要按顺序阅读。正文中不会出现太多关于深度学习和机器学习的理论介绍，但会提供若干阅读推荐以便初学者掌握相关基础知识；
* 代码实现均进行仔细推敲，力图简洁高效和表意清晰。模型实现均统一使用 `TensorFlow官方文档 <https://www.tensorflow.org/programmers_guide/eager#build_a_model>`_ 最新提出的继承 ``tf.keras.Model`` 和 ``tf.keras.layers.Layer`` 的方式（在其他技术文档中鲜少介绍），保证代码的高度可复用性。每个完整项目的代码总行数均不过百行，让读者可以快速理解并举一反三；
* 注重详略，少即是多，不追求巨细靡遗和面面俱到，不进行大篇幅的细节论述。

在整本手册中，带“*”的部分均为选读。

本手册的暂定名称《简单粗暴TensorFlow》是向我的好友兼同学Chris Wu编写的《简单粗暴 :math:`\text{\LaTeX}` 》（https://github.com/wklchris/Note-by-LaTeX）致敬。该手册清晰精炼，是 :math:`\text{\LaTeX}` 领域不可多得的中文资料，也是我在编写这一技术文档时所学习的对象。本手册最初是在我的好友Ji-An Li所组织的深度学习研讨小组中，由我作为预备知识的讲义而编写和使用。好友们的才学卓著与无私分享的品格也是编写此拙作的重要助力。

本手册的英文版由我的好友Zida Jin（1-4章）和Ming（5-6章）翻译，并由Ji-An Li和笔者审校。三位朋友牺牲了自己的大量宝贵时间翻译和校对本手册，同时Ji-An Li亦对本手册的教学内容和代码细节提供了诸多宝贵意见。我谨向好友们为本手册的辛勤付出致以衷心的感谢。

衷心感谢Google中国开发者关系团队和TensorFlow工程团队的成员们对本手册编写所提供的帮助。其中包括开发者关系团队的Luke Cheng在本手册写作全程提供的思路启发和持续鼓励，开发者关系团队的Rui Li, Pryce Mu和TensorFlow社群维护的小伙伴们在本手册宣发及推广上提供的大力支持，以及TensorFlow团队的Tiezhen Wang在本手册工程细节方面提供的诸多建议和补充。

关于本手册的意见和建议，欢迎在 https://github.com/snowkylin/TensorFlow-cn/issues 提交。这是一个开源项目，您的宝贵意见将促进本手册的持续更新。

|

Xihan Li（雪麒）

2018年8月于燕园
