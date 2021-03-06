---
layout: page-fullwidth
title: "测试驱动开发"
teaser: "Kent Beck先生最早在其极限编程（XP）方法论中，向大家推荐“测试驱动”这一最佳实践，还专门撰写了《测试驱动开发》一书，详细说明如何实现。经过几年的迅猛发展，测试驱动开发已经成长为一门独立的软件开发技术，其名气甚至盖过了极限编程。"
description: ""
tags: 
    - Linux
    - Docker
categories:
    - courses
permalink: /courses/test-driven-development/
header:
    image_fullwidth: "header_roadmap_3.jpg"
---
<div class="row">
<div class="medium-4 medium-push-8 columns" markdown="1">
<div class="panel radius" markdown="1">
**Table of Contents**
{: #toc }
*  TOC
{:toc}
</div>
</div><!-- /.medium-4.columns -->



<div class="medium-8 medium-pull-4 columns" markdown="1">

目前大部分内容来自百科

##  1. 概念来由

Kent Beck先生最早在其极限编程（XP）方法论中，向大家推荐“测试驱动”这一最佳实践，还专门撰写了《测试驱动开发》一书，详细说明如何实现。经过几年的迅猛发展，测试驱动开发已经成长为一门独立的软件开发技术，其名气甚至盖过了极限编程。[1] 

书籍: [测试驱动开发](http://book.douban.com/subject/1230036/)

##  2. 基本原理

*   测试驱动开发的基本思想就是在开发功能代码之前，先编写测试代码
*   然后只编写使测试通过的功能代码，从而以测试来驱动整个开发过程的进行
*   有助于编写简洁可用和高质量的代码，有很高的灵活性和健壮性
*   能快速响应变化，并加速开发过程

测试驱动开发的基本流程：

-   ①　快速新增一个测试
-   ②　运行所有的测试（有时候只需要运行一个或一部分），发现新增的测试不能通过
-   ③　做一些小小的改动，尽快地让测试程序可运行
-   ④　运行所有的测试，并且全部通过
-   ⑤　重构代码，以消除重复设计，优化设计结构

简单来说，就是不可运行/可运行/重构——这正是测试驱动开发的口号

![tdd-flowchart](/assets/Courses/tdd-flowchart.png "测试驱动开发流程")

##  3. 生动释义

*   测试驱动开发:
    -   盖房子的时候，工人师傅砌墙，<mark>会先用桩子拉上线，以使砖能够垒的笔直</mark>
    -   因为垒砖的时候都是以这根线为基准的
    -   TDD就像这样，先写测试代码，就像工人师傅先用桩子拉上线
    -   然后编码的时候以此为基准，只编写符合这个测试的功能代码

*   传统开发模式:
    -   一个新手或菜鸟级的小师傅，却可能不知道拉线   
    -   而是直接把砖往上垒，<mark>垒了一些之后再看是否笔直</mark>
    -   量一下砌好的墙是否笔直，如果不直再进行校正，敲敲打打 -- Bug?
    -   传统的软件开发过程就像这样，我们先编码，编码完成之后才写测试程序
    -   以此检验已写的代码是否正确，如果有错误再一点点修改

##  4. TDD优势

测试驱动开发不是一种测试技术，它是一种分析技术、设计技术，更是一种组织所有开发活动的技术

+   1) **TDD根据客户需求编写测试用例**

    对功能的过程和接口都进行了设计，而且这种<mark>从使用者角度对代码进行的设计</mark>通常更符合后期开发的需求。因为关注用户反馈，可以及时响应需求变更，同时因为从使用者角度出发的简单设计，也可以更快地适应变化

+   2) **出于易测试和测试独立性的要求**

    将促使我们实现松耦合的设计，并更多地依赖于接口而非具体的类，提高系统的可扩展性和抗变性。而且<mark>TDD明显地缩短了设计决策的反馈循环</mark>，使我们几秒或几分钟之内就能获得反馈。 -- 持续集成(CI)
+   3) **将测试工作提到编码之前，可频繁地运行所有测试**

    <mark>可以尽量地避免和尽早地发现错误，极大地降低了后续测试及修复的成本</mark>，提高了代码的质量。在测试的保护下，不断重构代码，以消除重复设计，优化设计结构，提高了代码的重用性，从而提高了软件产品的质量
+   4) **TDD提供了持续的回归测试，使我们拥有重构的勇气**

    因为代码的改动导致系统其他部分产生任何异常，<mark>测试都会立刻通知我们</mark>。完整的测试会帮助我们持续地跟踪整个系统的状态，因此我们就不需要担心会产生什么不可预知的副作用了</mark>
+   5) **TDD所产生的单元测试代码就是最完美的开发者文档**

    它们展示了所有的API该如何使用以及是如何运作的，<mark>而且它们与工作代码保持同步</mark>，永远是最新的
+   6) **TDD可以减轻压力、降低忧虑、提高我们对代码的信心**

    使我们拥有重构的勇气，这些都是快乐工作的重要前提
+   7) **快速的提高了开发效率**

##  5. TDD现状

1. 美国不少著名软件公司如IBM很早就开始向敏捷转型，在此过程中，TDD通常是最重要也最艰难的一个，正如IBM开发转型部门副总裁Sue Mckinney所言：*测试驱动开发前景非常诱人，但是“在这个过程中我们的付出可能也是最多的。*

2. ”Forrester的高级分析师Dave West认为，测试驱动开发（TDD）就像是“圣杯”，但是*“如果能达到这个目标，付出再多的辛苦也是值得的。”*
