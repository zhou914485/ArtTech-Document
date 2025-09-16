# Unity 入门

> 本页面由[李杰](../../社团介绍/成员.md)编写并发布

本文档旨在提供 Unity 引擎的入门路线，帮助初学者快速上手并掌握基本技能。

## 前置工具栈

此处列举的工具非必须项，但推荐学习以提升开发，以及日后学习的效率：

1. **版本控制**：Git
    - GitHub（验证学生身份，可以免费使用很多东西）、GitLab、Gitee 等代码托管平台
2. **网络工具**，获取国外高质量学习资源
    - Youtube 有机翻字幕，推荐使用（当然更推荐直接能听懂外文）
3. **AI** 辅助工具。和代码编辑器结合使用的 AI agents。加快问题排查，解决学习上的疑惑都很有帮助
4. **笔记工具**，学习过程中，保持记录可以提高学习的质量
    - Obisidian、Notion、Onenote 等主流笔记工具
    - 笔者个人推荐开源项目 Trilium Notes，但是需要自己折腾一下

## 安装 Unity

1. 访问 [Unity 官方网站](https://unity.com/)
2. 下载并安装 Unity Hub
3. 通过 Unity Hub 安装 LTS（长期支持） 版本的 Unity 编辑器

## 安装心仪的代码编辑器

推荐使用 Visual Studio，VSCode 或 JetBrains Rider
Visual Studio 和 Rider 都可以享受学生优惠，免费使用绝大多数功能，对 Unity 开发的支持相当不错

笔者更常用 VSCode。但是需要自行安装需要的插件以及 [dotnet SDK](https://dotnet.microsoft.com/zh-cn/)。

## 跟随教程开始第一个项目

这一步过后，你将创建一个简单的 3D 游戏项目，了解 Unity 的基本界面和功能。
注意不要单纯地复制教程的内容，而是尽可能理解每一步的意义所在，必要时添加自己的理解，为游戏添加个性化内容。

推荐的教程：

- [B站 MStudio 教程](https://space.bilibili.com/370283072)
- [Unity 官方入门教程](https://learn.unity.com/)
- [Brackeys YouTube 频道](https://www.youtube.com/user/Brackeys)

## C# 基础

在完成你的第一个项目之后，想必已经了解了Unity的基本操作和界面。像Unity和Unreal这样的游戏引擎，都会提供不用写代码的可视化脚本工具，但是想要成为优秀的游戏开发者，必要的编程能力是不可或缺的。

C#作为一门自带GC的面向对象编程语言，具有简洁的语法和强大的功能，非常适合初学者学习。

强烈推荐 刘铁猛老师的入门教程：

<div style="display: flex; justify-content: center; align-items: center; width: 100%;">
    <div style="position: relative; width: 100%; max-width: 800px; aspect-ratio: 16/9;">
        <iframe src="https://player.bilibili.com/player.html?bvid=BV13b411b7Ht" style="position: absolute; top: 0; left: 0; width: 100%; height: 100%; box-shadow: 0 4px 24px rgba(0,0,0,0.15);" frameborder="0" allowfullscreen></iframe>
    </div>
</div>

该课程涵盖了大部分需要的知识，虽然不够全面，但是对简单的开发足够使用了。如果想要更加深入地学习C#，建议购买课程中提到过的 [《C# in Depth》](https://zh.z-library.sk/book/4974128/045ddc/c-in-depth-fourth-edition.html) 深入学习。

## OOP 思想

面向对象编程（OOP）是一种编程范式，使用“对象”来表示数据和行为。也是当下游戏编程的主流编程范式。

> *同时也存在函数式编程（FP），面向过程（PP），面向切片（SP）等等其他编程范式，可作为拓展内容自行了解*
> *值得注意的是，现在各种编程语言的设计都会借鉴各种编程思想的优点，这一点多写一些代码自有体会*

详细的教程这里不做推荐，各种各样网上都有。

下面几点是笔者学习中体会深刻的一些道理，日后可以参考：

- **SOLID**原则
- 以业务维度划分代码，然后才是技术角度
- 简单性是一切可靠性的前提
- 优先使用对象**组合**，而非类**继承**（这一点略显暴论）

---

> *最后更新：2025年9月*
