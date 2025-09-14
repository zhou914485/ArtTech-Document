# AI 工具使用指北

> 本页面由[唐梓涵](https://github.com/00fish0)编辑并发布

⚠️ 本文写于 2025 年 9 月 13 日，AI 服务（尤其是大语言模型）更新飞快，本文内容随时可能过时，请读者注意甄别，灵活应对。

## 大语言模型推荐

不妨先看一眼 [Openrouter 统计的 token 使用排名](https://openrouter.ai/rankings)，一定程度上反映了当前主流大模型的热度：

![](../assets/images/Pasted%20image%2020250913150057.png)

目前市面上，ChatGPT、Claude 和 Gemini 可以说是“御三家”，知名度最高。国产模型如 Deepseek 和千问（Qwen）在中文任务上也表现优异。没有哪模型能在所有场景下通吃，建议大家多试试，按需选用。

**Claude**：专注于编程。写代码的任务，Claude 一般完成的比较好。但是也有人认为在复杂代码逻辑上 Claude 会出问题（不能充分理解业务逻辑，反复修改代码和测试，以跑通为目的，最后的结果可能和你的意图不符）。

**ChatGPT**：逻辑推理、多模态（识图、绘图）能力领先，生态成熟。ChatGPT 定位是生活中的助手，更贴近人的需求，较新的思考模型（o4, o3 等）表现不错。

**Gemini**：有人认为在语言理解方面具有优势，我个人用起来确实觉得完成翻译任务等更加符合我的想法。

国内：**Deepseek、Qwen** 等大模型都很不错，便宜大碗，Deepseek 深度思考能力做的不错。

## 如何让大模型帮你干活

### 避免 XY Problem

非常神奇的是，随着 OpenAI 提出的 Scaling Law 持续发挥效果，通过无脑堆参数量，现在的大模型已经具备了**足够的计算机专业的各种知识**，回答计算机领域的各种问题时，已经某种程度上**具有了直觉**，对于写代码的任务也有足够的能力，能写出标准、格式工整的代码。

所以，**清晰地描述问题的背景，精准、完整地告诉 LLM 你的需求。**

**尤其要注意，提问时需要避免 XY Problem。**

> 所谓 XY Problem，就是说：你其实想解决 X，但你以为 Y 能解决，结果跑去问“怎么搞 Y？”，完全没提 X。

举例：

某同学想运行一个从 GitHub 上下载的机器学习项目。项目的 `requirements.txt` 文件里写着 `pandas==1.5.0`。他的真正目标是**成功配置并运行这个机器学习项目所需要的 Python 环境**。

但他打开终端，直接运行了 `pip install -r requirements.txt`，终端冒出来一堆报错信息，最后显示：

```
ERROR: Could not find a version that satisfies the requirement pandas==1.5.0 (from versions: 2.0.0, 2.0.1, ..., 2.3.0) ERROR: No matching distribution found for pandas==1.5.0
```

看到提示，他认为自己想问的问题是**如何强制 pip 安装一个旧版本的 pandas**。

但在这个场景下，这个问题**完全无法解决这个同学的根本问题**。即使他想办法强制装上了某个版本的 Pandas，后续安装其他库（如 Numpy, scikit-learn）时，会因为 Python 版本不兼容而遇到更多、更复杂的报错，越走越偏。

正确向 LLM 的提问方式应该是：

> **我正在尝试配置一个 GitHub 上的机器学习项目。我的电脑是 macOS，安装了最新的 Python 3.13。当我使用 `pip install -r requirements.txt` 安装依赖时，遇到了 `ERROR: No matching distribution found for pandas==1.5.0` 的报错。请问我应该如何正确地为这个项目配置环境？**

这样，LLM 一看就懂了，甚至会建议你降低 Python 版本或使用虚拟环境，而不是硬装旧版 pandas。

![](../assets/images/Pasted%20image%2020250913215254.png)

### 写代码

目前大多数人认为 Claude 的代码能力最强（有足够多的代码语料训练，能够精确匹配不同函数间的 API 接口，熟悉常见的代码逻辑，能帮助写较完善的单元测试）。

**但 Prompt 写不好，再强的模型也白搭。**

#### 架构设计很重要

一个模糊的 prompt 如：

```
请帮我写一个针对AI工作负载的LLM日志分析模块。
```

如果给了一个模糊的 Prompt，让 LLM 直接开干，这样得到的代码大概率是一个玩具性质的小 demo，代码逻辑可能和你想要的相差甚远（它可能给你一笼香菜馅烧麦——虽然也是吃的，但你想要的是猪肉大葱包子😅。）。

所以，先不要让 AI 写代码，先和他多对话几轮，补充完善你的需求：

```
我想写一个针对AI工作负载的LLM日志分析模块，现有的数据是通过xxx方式收集得到的，存储在yyy,格式如zzz。你觉得这个模块可以怎么实现，包括哪几部分？
```

或者直接让 AI 反问：

```
我想写一个针对AI工作负载的LLM日志分析模块，但具体逻辑和代码架构还不清晰，我需要完善我的需求，请你不要猜测这些模糊的地方，现在直接向我提问。
```

根据回答，再提出一个完整详细的 Prompt。

一个较为完整的 prompt 应该包括技术选型（使用什么语言、什么框架？）、明确的任务（读取某个 `.csv` 文件？）、核心逻辑（使用什么平台调用 LLM 接口？还是本地部署？）、已有接口（通过哪些已有的类/获得数据？）、代码结构（细分成哪几个模块？哪部分可以使用之前的 helper function？代码主要分为哪几个抽象层？具体该使用什么特性实现？）等。

Prompt 越完整详细，得到的代码就越可控，也能让你更加地快速理解生成的代码。

#### 我是否需要看懂每一行代码？

如果你想**写小项目/快速实现 demo/写个一次性脚本/写固定模式的代码（比如发个 HTTP 请求）**：

LLM 在完成小范围的代码（可能是高度耦合，和外部关系较小的几个函数）时，只要描述清楚了要求，通常能达到非常好的效果。这种时候，如果为了快速开发，可以不管内部的实现细节。

一个函数内，几十行代码，想写出如Linus所说，有"Good Taste"的代码，现在并不难。

![](../assets/images/Pasted%20image%2020250914031826.png)

但是，如果你想**写大项目/项目的核心逻辑/写长期维护的项目/正确性要求很高**：

让 LLM 写数千行代码，完整地完成具有某个功能的项目时，如果不清晰描述对技术实现的要求，或者在生成过程中完善 Prompt（使用几层抽象实现，某一个具体部分该怎么实现等），直接多轮迭代生成，内部的架构（函数的设计等）很可能会比较混乱。

这是因为当任务变得庞大和复杂时，代码的质量不再仅仅取决于“每一行是否正确”，而更取决于**模块如何划分、职责如何分配、接口如何设计、数据如何流动**等系统架构问题。在多轮迭代中，LLM 的上下文窗口有限，很难始终保持一个清晰、统一的架构愿景。它倾向于满足你当前最具体的请求，而可能破坏之前建立好的抽象边界（比喻一下就是：原来是一坨，每生成一次，就在原来的一坨上又糊了一块）。

LLM 会生成它“见过”的最常见的模式，但这不一定是当前问题最优雅、最解耦的方案，容易生成高度耦合、重复的“胶水代码”。如果**开发者完全放弃设计职责**，盲目接受 LLM 生成的大段代码，会迅速积累巨大的技术债，使得项目后期难以维护和扩展。

即使最终的代码能完成某项功能，也会由于代码高度冗余，**不便于别人理解，也不便于后续增加新功能和维护。**

### 配环境

大模型的准确回答需要**足够的信息**。遇到环境配置问题（Python、Cuda 等），直接把报错信息完整粘贴给 AI，它通常能给出常见解决路径。如果能附上你的操作环境（是否虚拟机？执行过什么特殊操作？），回答会更准。

可以按这个流程来：

贴报错 → 问排查方法 → 尝试 → 反馈终端输出的更多信息 → 再问…

### 学会上网搜索

在“前 AI 时代”，根据计算机领域古老而神圣的传统，**程序员两大美德**是：

- **RTFM**（Read The Fucking Manual）
- **STFW**（Search The Fucking Web）

如果回答者甩出这两个缩写，意思就是认为你需要的信息非常容易获得，不应该来骚扰他。

**AI 时代，RTFM 压力小多了——很多手册内容，模型已熟记于心。**。（[如 Linux man pages 中的常见命令](https://www.man7.org/linux/man-pages/)）

而对于一些又臭又长，针对于硬件/底层开发的从业者的手册（如 [Intel 的 x86-64 架构开发手册](https://www.intel.com/content/www/us/en/developer/articles/technical/intel-sdm.html)），即使 AI 不能完全掌握其中的精髓，你也可以把手册的一部分内容喂给 AI, 让他快速地帮你找到想要的信息。

**但 STFW 在一些时候是很有必要的：** 虽然 LLM 具有足够的知识和直觉，但有一些**复杂/少见/时效性强**的问题，如：

- linux 内核具体如何对物理地址映射到 io 设备提供支持？
- bios/uefi 启动的详细区别？在电脑启动的流程中具体做了哪些事情？
- 某个包的版本不兼容安装报错，具体该如何解决？

对于这些问题，LLM 可能只会给出方法论层面的指导（如：也许你该尝试更新 xxx 包），以及报错原因的推测。

所以，有时上网搜索问题还是必要的。很有可能有人和你的环境相似，碰到了几乎一样的问题。在搜索到的结果中，**GitHub Issues、Stack Overflow、Ubuntu Forum** 等网站的信息通常认为是更加靠谱的。国内的 **CSDN、知乎** 也可以参考，但需要注意发布的时间以及可信度。

例如：

安装 gdb-dashboard 插件，使用 gdb 调试的时候，发现 Variable 一栏报错：

```python
Traceback (most recent call last):  
File "<string>", line 550, in render  
File "<string>", line 1568, in lines  
File "<string>", line 1623, in format_frame  
File "/usr/share/gdb/python/gdb/FrameDecorator.py", line 122, in frame_locals  
return args.fetch_frame_locals()  
~~~~~~~~~~~~~~~~~~~~~~~^^  
File "/usr/share/gdb/python/gdb/FrameDecorator.py", line 288, in fetch_frame_locals  
elif sym.is_artificial:  
^^^^^^^^^^^^^^^^^  
AttributeError: 'gdb.Symbol' object has no attribute 'is_artificial'
```

直接询问Claude-Sonnet-4，它只会建议“升级GDB”，并且错误地告诉我这个属性是在8.x中引入的（实际为16.x）：

![](../assets/images/Pasted%20image%2020250913160914.png)

但复制关键报错信息 `AttributeError: 'gdb.Symbol' object has no attribute 'is_artificial'`，在Google搜索，前几个结果就能找到：在gdb-dashboard项目的issue中，有人碰到了同样的问题：

通过搜索，我比询问AI更快定位到了问题（Arch Linux上我的gdb版本，与gdb-common这个包的版本不匹配）：

![](../assets/images/Pasted%20image%2020250913160206.png)

（虽然但是，我个人觉得，再过几年，LLM接收外部信息（如网络搜索）的能力进一步增强之后，这种问题对AI都不是问题）

### 提问的智慧

关于以上这部分内容，欢迎阅读[HITSZ OSA 修改版提问的智慧](https://wiki.osa.moe/guide-for-beginner/how-to-ask-questions-the-smart-way/)。

正如文中注解，**任何观点都有其时代性与文化性。你并不一定需要全盘接受作者的观点。** 但看一看怎么提问总没有坏处，无论是对人还是对AI，会提问永远都是一项重要能力，不知道什么时候就能用到呢。

## AI 服务推荐

### Github Copilot

Github Copilot的优势在于可以和VSCode紧密结合，LLM有能力读取当前项目的代码，在代码中搜索，获取Github上开源仓库的类似代码实现作为参考，以及自动生成 `tasks.json`等功能。

如果你习惯使用vscode编程，copilot的体验非常好。

**学生可白嫖**，认证后免费使用，搜索“github copilot 学生认证”即可申请。也可参考[Github官方的学生认证指南](https://docs.github.com/zh/education/about-github-education/github-education-for-students/apply-to-github-education-as-a-student)。

### Jetbrains 全家桶

Jetbrains家的各种IDE和vscode相比功能更多，对嵌入式开发（Arduino, stm32）等支持会更完善一些。**也可以白嫖。**

### Poe

Poe是一个LLM服务聚合平台，他的最大优势是多个愿望一次满足，可以直接和绝大多数大模型一站式丝滑对话。

收费形式是每个月大概120元，给一百万积分，够向LLM提问近千次。

## API Key 调用

很多工具支持通过 API Key 接入大模型，实现翻译、润色等功能——效果通常比传统机器翻译更自然。

以edge的“沉浸式翻译”插件举例：

![](../assets/images/Pasted%20image%2020250914021828.png)

国内的API KEY平台可以选择[硅基流动](https://account.siliconflow.cn/zh/login) (SiliconFlow)，注册就送14元额度，邀请其他人注册，双方也各送14元额度。

国外的API KEY 平台可以尝试[Openrouter](https://openrouter.ai/) ,但是我个人觉得延迟可能较高。

## 其他无用的小知识

- 现在的主流大模型都是transformer架构的，根据transformer架构的原理，把你的要求放在 Prompt 的最前面可能会更有用。
- 现在LLM仍然是一个黑盒，对LLM可解释性的探索一直在继续着。扩展阅读[Claude关于LLM内在原理的研究](https://transformer-circuits.pub/2025/attribution-graphs/biology.html)。
