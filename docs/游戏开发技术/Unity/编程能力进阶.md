# C# 编程能力进阶

> 本页面由[李杰](../../社团介绍/成员.md)编写并发布

本文档会提供提升C#编程能力的学习路线。


## 设计模式

在游戏开发领域，业务需求变化较快，代码迭代频繁，如何写出便于维护的代码尤为重要。

设计模式是软件开发中常用的解决方案，掌握设计模式，编写更高效、可维护的代码。

个人认为设计模式就是**SOLID**原则的具体化。

推荐的教学资源：

- [Refactoring Guru 设计模式教程](https://refactoringguru.cn/design-patterns/catalog)
- [马士兵设计模式教程 👇](https://www.bilibili.com/video/BV1osyHY3Ev8)
<div style="display: flex; justify-content: center; align-items: center; width: 100%;">
    <div style="position: relative; width: 100%; max-width: 800px; aspect-ratio: 16/9;">
        <iframe src="https://player.bilibili.com/player.html?bvid=BV1osyHY3Ev8" style="position: absolute; top: 0; left: 0; width: 100%; height: 100%; box-shadow: 0 4px 24px rgba(0,0,0,0.15);" frameborder="0" allowfullscreen></iframe>
    </div>
</div>

<br>

另外，笔者作以下提醒和总结：

1. 设计模式不是固定的代码形式，而是**构建代码的思想**。不需要死记硬背，理解其背后的意图更为重要
2. **不要过度设计**，设计模式是为了解决问题，而不是制造问题

---

## C# 进阶

如果你已经认真学习完刘铁猛老师的C#入门课程，并且完成了第一个Unity项目，那么你已经掌握了C#的基础知识。

接下来，如果想要深入学习，内容会非常多，每一点都可以展开非常多知识点，还是要结合实际项目进行学习。

具体来说剩下的二级目录内容你都可以不看（大多是笔者的杂谈，不可能在这样的篇幅把详细的内容讲清楚，但是每小节末尾会放一些学习资源），而是直接看书：[《C# in Depth》](https://zh.z-library.sk/book/4974128/045ddc/c-in-depth-fourth-edition.html)

或者直接阅读[官方文档](https://learn.microsoft.com/zh-cn/dotnet/csharp/)。

> 以下内容还在建设中……


作为进阶内容，以下是几个重要的话题：

### 异步编程

异步就是让程序在等待某些操作完成时，能够继续执行其他任务，从而提高效率。

比如，在加载资源的时候，你一定会看到加载进度条，这就是异步编程的一个应用。

然而在游戏逻辑的设计上，Unity淡化了异步的概念（后面你就会知道异步很难写对）。

你可能就要问了，“哎？教程中不是教了 `coroutine` 什么的就是可以实现让某个效果在等待特定时间后发生吗，这不是异步吗？”。

这确实是“异步”。但是是由 Unity 引擎在 **单线程(主线程)** 中通过 **“协程”** 实现的“假”异步。它并没有真正地让程序并行执行，而是通过在每一帧中分割任务来实现的。

这样极大地降低了实现异步效果的难度，让编程能力较弱的初学者也能快速上手。但是 Unity 的异步编程模型在复杂场景下可能会导致性能问题，理解异步操作我们可以更加充分地利用现代多核 CPU，写出更高效的程序。

C#是一门设计优美的语言，你可以通过简单的 `async` `await` `lock` `Task` 等来实现异步编程。

但是最基础的概念还是要理解清楚，推荐的资源：

### 反射

反射是指程序在 **运行时** 能够 **检查和修改自身结构** 的能力。如果有了解的，可以对比一下c++在**编译期**的元编程，感受二者的区别。

反射的重要性可以直接体现在隔壁的Unreal引擎。Unreal引擎通过自研的反射系统（基于宏和代码生成），让原本不具备运行时反射能力的C++（未来可能会有）也能支持蓝图等可视化脚本和动态特性。

而C#是自带反射能力的，比如你有没有想过一个问题，为什么 Unity 的 inspector 面板能够显示你写在脚本中的字段？即使字段是私有的（不使用反射，你在自己的代码中都无法访问）也能显示？这就是反射的功劳。

反射的具体形式有很多，最常见的包括 `Type` `Assembly` `Attribute` 等等。

这里举一个笔者项目中，一个自动注册ECS系统中全部System的例子：

```csharp
// 通过反射自动注册所有实现了 ISystem 接口的系统
protected override void RegisterSystems() {
    // 从当前程序集(Assembly)中获取所有类型(Type)
    foreach (var type in Assembly.GetExecutingAssembly().GetTypes()) {
        // 检查类型是否实现了 ISystem 接口且不是抽象类
        if (typeof(ISystem).IsAssignableFrom(type) && !type.IsAbstract) {
            World.SystemManager.RegisterSystem(type);
        }
    }
}
```

值得注意的是，反射的性能开销往往较大（你可以试着`ctrl + click`点开反编译出来的Type类的源码，其中会包含非常多的信息），在编写高性能代码时需要谨慎使用。

### LINQ

LINQ（Language Integrated Query）。

**LINQ！LINQ！LINQ！伟大的 LINQ！程序员的寿命延长器！**

LINQ（Language Integrated Query）是C#中极具特色的功能之一。它让你可以用类似SQL的方式**优雅**地查询、筛选、排序、分组各种集合和数据源，无论是数组、List，还是数据库、XML、JSON等 **！**

有了LINQ，很多原本需要多层循环、繁琐判断的代码都能变得**简洁、直观** **！** 它不仅提升了代码的**可读性**和**开发效率**，还能让你更专注于业务逻辑本身 **！**

如果你还没用过LINQ，强烈建议花点时间系统学习和实践。掌握LINQ，能让你的C#开发体验上一个台阶。

---

> *最后更新：2025年9月*
