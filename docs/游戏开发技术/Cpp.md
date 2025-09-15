# C++
> 本页面由[张大佑](../社团介绍/成员.md)编写并发布
## C++的用处
* 使你快速了解面向对象编程概念
* 刷数据结构与算法题目必备技能
* UE官方的脚本语言
* Godot的可选脚本语言
* 游戏引擎源码的编写语言(UE,Unity,Godot)
## 如何学习（以下仅凭个人经验）
### 认识CS自学社区
自学CS相关内容时，正确利用CS自学社区可以让你事半功倍。自学社区是CS自学者进行交流和资料分享的平台，笔者常用的有如下三个平台：

1. [csdiy.wiki](https://csdiy.wiki)，其中涵盖内容包括（以下内容引自该网站）：
>* 本书使用指南：由于书内涵盖资源众多，我根据不同人群的空闲时间和学习目标制定了对应的使用指南。
>* 一份供参考的 CS 学习规划：我根据自己的自学经历制定的全面的、系统化的 CS 自学规划。
必学工具：一些 CSer 效率工具介绍，例如 IDE, 翻墙, StackOverflow, Git, GitHub, Vim, LaTeX, GNU Make, Docker, 工作流 等等。
>* 经典书籍推荐：你是否苦于教材的晦涩难懂不知所云？别从自己身上找原因了，可能只是教材写得太烂。看过 CSAPP 这本书的同学一定会感叹好书的重要，我将列举推荐各个计算机领域的必看好书与资源链接。
>* 国内外高质量 CS 课程汇总：我将把我上过的以及开源社区贡献的高质量的国内外 CS 课程分门别类进行汇总，介绍其课程内容特点并给出相应的自学建议，大部分课程都会有一个独立的仓库维护相关的资源以及作业实现供大家学习参考。

2. [CS自学社区](https://www.learncs.site/docs/intro)：功能类似csdiy.wiki，但相对于前者，这个网站对于课程PPT和作业等资料都收集得更加全面，只不过收录的课程量相较于前者更少一些。可以和前者配合使用。

3. [Github](https://github.com/)：许多课程都会将维护自己的Github仓库，并且许多自学者都在这里发布自己的学习记录以及相关资源。

### 初步认识C++：Stanford CS106B
本课程主要讲授利用Stanford自己的C++库完成一些算法问题，本课程有多个Assignment，每个Assignment都有一套完整的测试框架和图形化测试界面，往往要求你根据课上学到的算法去填写框架中的关键函数。笔者自己大一的时候跟完了整个课程，并且完成了所有Assignment，受益良多。由于不同学年的作业，课程视频不同，在网上找到资源的难易程度也不同，我选择观看了2018年冬季的课程视频，做了2022年冬季的Assignment。

2022年冬季Assignment所使用的IDE是QtCreator，当时我配环境费了一番功夫，相信聪明的你可以轻松解决这个问题。你可以在[csdiy.wiki](https://csdiy.wiki/%E7%BC%96%E7%A8%8B%E5%85%A5%E9%97%A8/cpp/CS106B_CS106X/#_3)以及[2022Winter课程主页](https://web.stanford.edu/class/archive/cs/cs106b/cs106b.1224/)找到环境配置的有关信息。

另外，对于第一次学习国外课程的同学来说，可以活用AI和翻译软件，这里我推荐一款浏览器插件：[沉浸式翻译](https://immersivetranslate.cn/)，它可以让你在阅读英文文档和观看英文视频的时候如虎添翼。

课程视频：[bilibili 2018 winter](https://www.bilibili.com/video/BV1G7411k7jG/?vd_source=85e1dae5cba303a7a1d633bc7541edd2)

课程主页：[CS106B 2022 winter](https://web.stanford.edu/class/archive/cs/cs106b/cs106b.1224/) (可以在这里找到Assignment文档)

课程作业初始包：[Starter Code](https://github.com/wuzhineihan/CS106B_StarterCode)

### 了解C++现代特性：Stanford CS106L

课程介绍（转自csdiy）：

> 我从大一开始一直都是写的 C++ 代码，直到学完这门课我才意识到，我写的 C++ 代码大概只是 C 语言 + cin/cout 而已。
这门课会深入到很多标准 C++ 的特性和语法，让你编写出高质量的 C++ 代码。例如 auto binding, uniform initialization, lambda function, move semantics，RAII 等技巧都在我此后的代码生涯中被反复用到，非常实用。
值得一提的是，这门课的作业里你会实现一个 HashMap（类似于 STL 中的 unordered_map), 这个作业几乎把整个课程串联了起来，非常考验代码能力。特别是 iterator 的实现，做完这个作业我开始理解为什么 Linus 对 C/C++ 嗤之以鼻了，因为真的很难写对。
总的来讲这门课并不难，但是信息量很大，需要你在之后的开发实践中反复巩固。Stanford 之所以单开一门 C++ 的编程课，是因为它后续的很多 CS 课程 Project 都是基于 C++的。例如 CS144 计算机网络和 CS143 编译器。这两门课在本书中均有收录。

课程视频：[bilibili](https://www.bilibili.com/video/BV1K8411b7AU?vd_source=c3775a637d3254e89c728ed792770aba)

由于笔者只看了课程视频，没有写作业，因此暂无作业资源，更多内容可以自行访问课程官方网站和CS自学社区进行获取。

### C++的日常练习：[LeetCode](https://leetcode.cn/)

算法能力是CS学生就业面试时重点考察的能力，同时对于一些基本数据结构的了解是整个开发过程当中的基石。

理论上，看完CS106B就可以开始刷LeetCode了，在刷题的过程中除了STL基本用不到C++的特性，因此此课程可以和CS106L同步进行，在刷LeetCode的过程中，我认为可供新手借鉴的经验如下：

* 使用VSCode+LeetCode扩展刷题。使用VSCode的好处在于更智能的代码补全，加上LeetCode扩展之后可以实现更方便的Debug。同时如果你要使用AI辅助的话，Copilot也可以让你与AI之间的合作更加顺滑。

* [代码随想录](https://www.programmercarl.com/)：该网站提供了一套完整的刷题计划和题目讲解。跟着这套计划一天推进几道题，可以在不到三个月的时间内对算法数据结构有一个整体上的了解。

## 更多
笔者对C++的学习与了解仅限上述资料，凭借这点了解已经足够进行UE的C++开发（UE的C++相对于原生C++来说，又有许多需要学习的新知识），对于更多的高级内容则是在需要用到时才去了解。C++ Primer和C++ Primer Plus可以作为参考工具书使用，但不推荐以此入手学习C++。