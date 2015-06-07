---
layout: page-fullwidth
title: "VDI4.3 测试开发总结"
teaser: "在整个VDI4.3版本中，之前提到的概念如代码审查和单元测试，因项目紧凑的原因，未能有效推广之。但扮演着SET角色，就应该尽SET的职责，在项目的开发过程中，不断地为分析、定位和技术攻坚做出贡献。能做出多大的贡献，与以下的一些因素有着强关联性质"
description: ""
tags: 
    - VDI4.3
    - SET
    - TDD
categories:
    - courses
permalink: /courses/tdd-preview1/
header:
    image_fullwidth: "unsplash_brooklyn-bridge_header.jpg"
---
<div class="row">
<div class="medium-4 medium-push-8 columns" markdown="1">
<div class="panel radius" markdown="1">
**目录**
{: #toc }
*  TOC
{:toc}
</div>
</div><!-- /.medium-4.columns -->



<div class="medium-8 medium-pull-4 columns" markdown="1">

## 碎碎语

&emsp;&emsp;在整个VDI4.3版本中，之前提到的概念如代码审查和单元测试，因项目紧凑的原因，未能有效推广之。但扮演着SET角色，就应该尽SET的职责，在项目的开发过程中，不断地为分析、定位和技术攻坚做出贡献。能做出多大的贡献，与以下的一些因素有着强关联性质：

*	1) **自身技术能力**
*	2) **项目的业务了解程度**
*	3) **Android系统知识业务了解程度**

##### 关于能力 #####

<br/>**首先，好的实践，离不开好的工作方式，在这里我选择使用VIM来编写测试代码。**

&emsp;&emsp;说明一下第一点，按我自身的情况来看，在编程技能方面并不算很特长，多是需要什么了解什么，最擅长莫过于使用VIM，还有使用Sumline Text这类编辑文本的工具，利用它们可以快速的编写出很多漂亮而稳定的测试代码。使用VIM主要是只要心想到什么，就能写出什么样子的内容（前提是自己思路足够清晰），在这里我给大家推荐几个比较好使用的插件，<mark>利用他们可以使测试编码速度提高100%~300%</mark>，并且让代码复用变得是如此的简单。

-   a) *[youcompleteme](https://valloric.github.io/YouCompleteMe/){:target="brank"}*: 使用这个自动补全的插件，写C/C++、Python、Ruby和Shell都非常方便，我平时工作无法离开它；

    ![tdd vim ycm](/assets/Courses/tdd_vim_youcompleteme.gif "VIM YouCompleteMe插件")

-   b) *[ultisnips](https://github.com/SirVer/ultisnips){:target="brank"}*: 使用这个插件，可以让我们忽略了语法的记忆，编码效率提高 200% 不是问题；

    ![tdd vim ultisnips](/assets/Courses/tdd_vim_ultisnips.gif "VIM Ultisnips插件")

    最为紧要的是，这个插件可以让我们经常使用到的代码模板，保存为模板，然后指定字符串如`if`, `switch`, `class`等等。

-   c) *[other](https://github.com/amix/vimrc){:target="brank"}*: 如`YankRing`, `nerd_tree`, `mru`, `vim-commentary`, `syntasic`等等都是不错的辅助插件，大家可以尝试学习使用一下他们。

&emsp;&emsp;如果觉得掌握不了VIM这类编辑器，也可以尝试使用平易近人的[Sumblime Text 3](https://www.sublimetext.com/3){:target="brank"}，它可以节省大量的配置时间，尤其在网页编程上我觉得使用Sublime Text是不错的选择。

&emsp;&emsp;关于代码编辑器，我觉得最重要的一些点子是，<u>尝试经常使用他们，并熟悉他们的快捷键，提高自身的测试编码能力，不要让垃圾的编辑器拖延了自己敏捷的思维。</u>

##### 熟悉业务 #####

<br/>**其次，我们要在项目组内，熟悉项目的业务**

&emsp;&emsp;作为一个测试人员，无法避免的是作为一个服务员的角色。第一个要服务的是直接的客户人员，拿一个需求时，我会尽可能想着这个需求能提供给客户什么样子的价值；第二个要服务的是是我们版本经理，完成相应的测试任务，不要漏测、识别风险；第三个要服务的是开发人员，提供一个必要的帮助给开发人员，从需求理解、测试工具、问题定位等等，简单一点，提供尽可能多的信息协助开发定位问题（前提是不要浪费过多在时间在上边）。

&emsp;&emsp;现在回顾一下，这个“服务员”的角色，不管对客户、版本经理还是开发人员，都需要对业务足够熟悉，清楚的知道自己每做一件事，它的价值体现在哪里。OK，写得太多了感觉像理论化了，来说一点具有实践意义的。

-   a)  *document*: 拿到一个需求，最好找找有没有相应的文档（包含需求文档、设计文档）等，尝试从客户角度理解一下这个需求的来源，结合文档阅读一下

-   b)  *usage*: 对一些几经修改、或大改特改的，我感觉最好的办法就是直接使用它们了；通过不断的使用，结合项目的需求很快就会熟悉了新老业务内容

-   c)  *communication*: 交流也是很重要的，不懂就问，找模板负责人来问，直到清楚的理解为止。 [小黄鸭调试法](http://blog.jobbole.com/85719/){:target="brank"}

-   d)  *expand*: 有些时候拓展、发散一下也是必须的，不要局限在一小部分，尝试考虑一下关联的内容，由点及面，再扩充到一个整体。发散也是有根有据的，[Android Internal](http://sangfor.linkscue.com/courses/android-internal/){:target="brank"}。

##### 了解行业 #####

<br/>**最后，还要亮相的是Android系统知识的理解程度**

&emsp;&emsp;这里不是来说明我对Android系统知识有多了解、多牛逼，而是来提供一些学习方法。有句话这么说的，想做出改变任何时候都不会晚。我们也一样，学习是一个积累的过程，付出行动，努力向前迈出一小步。

&emsp;&emsp;上一次SSLT测试交流分享会上，我把我熟悉的Android系统知识简单分享了一下，虽然大家听着觉得相对痛苦，但是大家还是大概知道Android系统结构会是什么样子的。我们很多核心业务，与Android系统底层是无法分开的，如图形处理`surfaceflinger`，多媒体相关的知识`gpu, ipp, egl, ffmpeg, jpeg, omx, vpu, media, surfaceflinger, performance, codec, decodec, mali, light, hwcomposer, gralloc`，他们连环套连环、环环相扣（ [Android系统文件<sup>beta</sup>](http://sangfor.linkscue.com/courses/android-system-files/){:target="brank"} ），想要理解它们并发现一些潜在影响我们客户体验的问题，还需要对Android系统进行有力的剖析。

&emsp;&emsp;OK，阐述了那么多了，大家或许对于怎么学习这么多的Android系统知识有一定的兴趣了吧。那先说说我这一个学习历程吧。

######（一）学习历程

-   a)  *<u>初识Android、与折腾的心</u>*: 2010年Android手机刚刚出来的时候，它很卡，很慢，内置的应用程序又多；

    从这时起，就开始反复折腾Android手机，从Root开始，删除垃圾应用程序，改善GPS定位，调整Android UserData分区空间大小等等，那时候起，每天逛论坛，见识着国内外的大牛们如何修改Android ROM，如经常逛的国外论坛[XDA Developers](http://forum.xda-developers.com/){:target="brank"}。

-   b)  *<u>开始接触源代码</u>*: 感觉很多东西并非能按照自己的心意去做事，于是似就想到从源代码入手

    以前多是按照别人的教程来修改Android ROM，或是通过反编译其中的Apk来增加、修改其中的功能，感觉很多东西并非能按照自己的心意去做事，于是似就想到从源代码入手。最早开始于2013年，在Ubuntu环境下，成功编译了 CyanogenMod 源代码，用于Android手机上，这个时候感觉很多东西都是属于自己可以控制的，感觉很不同。这个时候开始接触了 [CyanogenMod](http://www.cyanogenmod.org/) 和 [Github](http://github.com){:target="brank"}，这个时候就会尝试和大神们一样，移植系统到Android手机上。

-   c) *<u>开始关注开发者博客</u>*: 有些时候不期望在某一块技能继续提升时，而仅仅是想看盾这一个行业的发展状态；

    学习技能是无穷无尽的，尤其是IT行业，日新月异每天都会有无穷无尽的新知识诞生。在知识海洋里边，我们要学习筛选和保持与这个社区思想同步的状态。这时候开始关注的博客有:

    +   Google Android开发者官方博客: [Android Developers Blog<sup>(需要穿墙)</sup>](http://android-developers.blogspot.com/){:target="brank"}
    +   CyanogenMod 开发者博客: [CyanogenMod Blog](http://www.cyanogenmod.org/blog){:target="brank"}

    如果这时候还有余力，大家可以关注一下他们的Google Plus和Facebook，这些大神们的社区帐号通常都是比较活跃的

-   d)  *<u>关注国内大神们的博客</u>*: 也许你看着国外的文章逐渐疲惫了，这时候我建议大家看看一些国内一些大神们的博客文章，有一些作者的著作内容都还是比较好的，比如 [老罗的Android之旅](http://blog.csdn.net/Luoshengyang/article/list/1){:target="brank"}， [Android系统移植与平台开发](http://blog.csdn.net/column/details/androidporting.html){:target="brank"}，阅读这些文章，结合源代码来学习效果会很好。

######（二）小结

-   社区论坛是与大神们零距离接触的地方
-   尝试自己去修改一些东西，试图让它们按你的思维去工作
-   关注国内外开发者的博客，学习他们查看、分析和解决问题的思维

## VDI4.3版本总结

&emsp;&emsp;先来看维基百科对[SET的定义](https://zh.wikipedia.org/wiki/SDET){:target="brank"}: SDET，是软件测试开发工程师（英语：Software Design Engineer in Test）的简称，该词据信来源于微软。SDET在敏捷软件流程中起着越来越关键的作用，既要快速了解各项知识，又要对业务能够快速上手。SDET是为了解决在推行敏捷过程中，软件测试效率无法突破，并且在快速迭代中测试无法面面俱到，而产生的一种保证开发与测试过程之间无缝转换的一种角色。

&emsp;&emsp;结合我们项目来讲，特点是需求相对较多、时间相对紧凑，在预研也不到位的情况下，更需要SET角色来辅助开发，来协助问题分析与定位，做好技术攻坚，保证项目质量及进度。

### 1. 问题分析与定位

&emsp;&emsp;协助开发分析与定位问题，有些时候是必要的，开发人员一般情况下压力会比较大，考虑的问题也不能面面俱到，这时候我们可以去做一些辅助性的工作，如提供自检工具、提供一些开源项目比较好的工具，并运用到项目上来，提升团队效率。

##### 提升交付质量 #####

<br/>通过提供工具，提升开发提交给测试的包质量提升。

+   提供给开发自检、调试使用的工具: `master_env.sh`，初衷是让开发调试和一些简单的自检更加愉快、见效

    先来一个简单的演示:
    
    -   mkgrep: 搜索一个模块在何处被编译
    -   check_string_res: 检查一个App项目，是否缺少翻译（避免Bug: 37265）<br/><br/>

    <ul class="clearing-thumbs small-block-grid" data-clearing>
        <li><a href="/assets/Courses/tdd_master_env_demo.gif"><img data-caption="VDI4.3 提供开发快速调试和自检小工具" src="/assets/Courses/tdd_master_env_demo.gif"></a></li>
    </ul>

    <br/>文档下载：[〖aDesk〗提供给开发测试人员调试、自检的工具.doc](/assets/Courses/tdd_〖aDesk〗提供给开发测试人员调试、自检的工具.doc)

    &emsp;&emsp;关于这类自测工具，我觉得还是相对缺少的，它类似于代码扫描工具，目的是为了显著的提升开发提交包的质量，尽可能减少低级错误。展望: [PMD](http://pmd.sourceforge.net/){:target="brank"}, [FindBugs](http://findbugs.sourceforge.net/){:target="brank"}, [Lint](http://tools.android.com/tips/lint/){:target="brank"}等，结合以我们业务进行代码扫描，当这些工具不能满足时再适当的编写一些检查工具。

##### 提升分析能力 #####

<br/>参考开源项目的做法，提供工具方便开发人员分析和定位问题的能力。

+   源码索引平台: [VDI4.3 Android Source Index<sup><mark>(仅对部分人开放访问权限)</mark></sup>](http://sangfor.linkscue.com:8080/source/){:target="brank"}

    有这么一个源码索引平台，我们可以方便的查找代码、阅读代码，和定位问题，无论测试人员，还是开发人员，都可以利用它得到很好的锻炼与实践。

    -   演示通过指定文本来搜索Kernel上的内容
    -   演示通过指定Symbol搜索自己想要的代码片段 <br/><br/>

    <ul class="clearing-thumbs small-block-grid" data-clearing>
      <li><a href="/assets/Courses/tdd_opengrok_demo.gif"><img data-caption="VDI4.3 OpenGrok 建立的Android源代码索引平台" src="/assets/Courses/tdd_opengrok_demo.gif"></a></li>
    </ul>

    <br/>相关链接: [〖aDesk〗Android源代码快速索引OpenGrok环境搭建和使用](http://200.200.0.17/cms/supesite/?action-model-name-creative-itemid-14798){:target="brank"}

####小结

&emsp;&emsp;在上边罗列出来的协助开发分析和定位问题上，除了提供必要的提升代码质量工具以外，还提供代码索引工具，在这一个过程中，作为项目的一员，我觉得<mark>持续学习开源项目的做法</mark>是很有必要的。在没有找到OpenGrok之前，我还尝试使用了[LXR](http://sourceforge.net/projects/lxr/){:target="brank"}和[Source Insight](http://www.sourceinsight.com/){:target="brank"}来尝试建立源码索引，都不理想。后来，通过经微博一个朋友介绍使用了[OpenGrok](https://github.com/OpenGrok/OpenGrok/tree/0.12-stable)，最后花上一些时间才搭建好这个Android源码索引平台，现在使用起来挺顺手的。

&emsp;&emsp;由引可见，与开源项目保持同步的思维是多么的重要，闭门造车很容易让我们走弯路。建立大家都多去关注一下大型的开源项目，Follow下他们，应该会有不少的收获，模仿他们的作风往往也会让自信心受到鼓舞。

### 2. 协助技术攻坚

&emsp;&emsp;大家也许对于技术攻坚也相当地感兴趣，每当协助开发成功突破一个个难关的时候，一种成就感就会油然升起。俗话说，付出总会有相应的回报，我们的付出也会同时体现在这里协助攻克难题上。虽然我们测试部门，还没能够像 [Google软件测试之道<sub>:像google一样进行软件测试</sub>](http://book.douban.com/subject/25742200/){:target="brank"} 这里介绍的测试人员角色分工那么精细，但我们也在积极探索符合我们自身敏捷流程的一种SET测试模式，这种模式，除了提供工具、代码审查<sup><mark>(推广难度与项目时间松紧相关)</mark></sup>等以外，我觉得还会包含一种职能——<span style="color:#DF4949;">协助攻克技术难题</span>。

在VDI4.3版本中，我协助技术攻坚包含:

+   1) [Android升降级](http://200.200.0.17/cms/supesite/?action-model-name-creative-itemid-14146){:target="brank"}: 源自于对Android系统知识、OTA原理的了解，加快项目发布速度
+   2) [Android四核Adb、串口调试](http://200.200.0.17/cms/supesite/?action-model-name-creative-itemid-14971){:target="brank"}: 方便杰微四核的调试，为解决问题和定位问题提供帮助
+   3) [双核、四核源码对比](http://200.200.0.17/cms/supesite/?action-model-name-creative-itemid-14973){:target="brank"}: 从结果导向和源码上做对比，分析四核需重点测试的地方
+   4) [协助解决四核黑屏](http://200.200.0.17/cms/supesite/?action-model-name-creative-itemid-14975){:target="brank"}: 由Parameters各升降级导致的黑屏问题，协助解决风险
+   5) [协助解决分辨率缩放问题](http://200.200.0.17/cms/supesite/?action-model-name-creative-itemid-14978){:target="brank"}: 源自于对Android系统知识的了解，协助解决这个阻碍；

&emsp;&emsp;从表面上看，这些都涉及到Android系统知识，关于Android系统知识的[学习历程](http://sangfor.linkscue.com/courses/tdd-preview1/#section-4){:target="brank"}已有阐述，与这里产出最相关的内容应该是参与论坛上修改和定制Android ROM、及学习博客知识等。从博客上领悟的，以及自己动手查阅代码的，可以获得不少的帮助。只有对这一整个系统有一定的了解，结合自身业务知识的积累，才能把众多难关一点点的啃下。

&emsp;&emsp;关于协助技术攻坚的，要在项目组时间相对空闲的状态下做的，比如我在VDI4.3负责四核模块时，因为开发的预研不充分，遇到了不少的麻烦，直接合并四核、双核源代码，出现了很多之前未预料的问题。此外，我觉得这类<mark>介入开发</mark> 应该只能算是**问题驱动型**，而我觉得更好的应该是**直接介入开发**，毕竟现在敏捷和[TDD<sub><mark>(测试驱动开发)</mark></sub>](http://sangfor.linkscue.com/courses/test-driven-development/){:target="brank"}会是未来软件开发流程的主流，理论上，我们应该是 <span style="color:#DF4949;">先拉好垂直线，再垒砖，而非先垒砖，再拉垂直线</span>。

&emsp;&emsp;提到测试驱动开发，要求拿到一个需求之后，就能够依据需求直接编写对应的测试套件，像 [测试驱动开发基本流程](/assets/Courses/tdd-flowchart.png){:target="brank"} 所描述一样，我觉得以我们现状，这暂时只能是一个愿景，在熟悉业务、软件代码和软件架构上，以目前现状来看，还需要更多的努力。

##### 可实践的内容 #####

<br/>&emsp;&emsp;暂时避开谈[TDD](http://sangfor.linkscue.com/courses/test-driven-development/){:target="brank"}不谈，我们可以来一些可以付诸以实践的内容，我们还是可以像[Microsoft公司的SDET一样](http://microsoftjobsblog.com/ireland-based-ankur-gives-5-truths-in-testing/){:target="brank"}，要求自己、强化自身的能力，<u>结合我们现在情况来讲，可以这么做</u>：

+   1) 学习一些编程基础，以最简练的语言写好测试代码，会写代码也是TDD的前提；
+   2) 熟悉业务知识，并熟悉开发人员提供的软件/模块设计方案（仔细阅读文档）；
+   3) 尽可能从客户角度出发，客户才是最终使用人；
+   4) 给自己更高的定位: <b>SDET = Project Management + Passion for Customer Experience + Engineering Skills</b>；
+   5) 了解行业动态，包括: <span style="color:blue;">开源项目的作法，SDET行业发展，模块相关的系统知识<span style="color:black;"><sup>(<u>多阅读一下大神们的博客</u>)</sup></span></span>，并尝试运用它们<sup>([链接](http://www.zhihu.com/question/19636213){:target="brank"})</sup>；

##### 小结 #####

<br/>&emsp;&emsp;回归谈谈协助技术攻坚的内容，前边已提到了，协助技术攻坚可以让项目风险把握、项目进度和测试质量都有所提升，但目前来讲，还是问题驱动型的介入开发，而非能够直接驱动型，现在我们离TDD测试驱动开发模型还有一定的差距，但不代表没有可实践的内容。我们可以尝试多学习一些编程语言，多关注一下行业动态，写好测试代码，这为以后单元测试、走敏捷、走TDD测试驱动开发提供保障。

## 
