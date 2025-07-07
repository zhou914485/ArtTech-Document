# C# 编程基础

## C# 简介

C# 是一种现代的、面向对象的编程语言，由微软开发。它是 Unity 游戏开发的主要编程语言，也是 .NET 平台的核心语言。

## 为什么学习 C#？

### 优势
- **易学易用** - 语法简洁，容易上手
- **强类型** - 编译时检查，减少运行时错误
- **面向对象** - 支持封装、继承、多态
- **跨平台** - 支持 Windows、macOS、Linux
- **丰富的库** - 庞大的 .NET 生态系统

### 应用领域
- **游戏开发** - Unity 游戏引擎
- **Web 开发** - ASP.NET Core
- **桌面应用** - WPF、WinForms
- **移动开发** - Xamarin
- **云服务** - Azure 云平台

## 开发环境搭建

### 推荐工具
- **Visual Studio** - 微软官方 IDE
- **Visual Studio Code** - 轻量级编辑器
- **JetBrains Rider** - 专业开发工具

### 安装步骤
1. 下载 [Visual Studio Community](https://visualstudio.microsoft.com/zh-hans/vs/community/)
2. 安装时选择 ".NET 桌面开发" 工作负载
3. 创建新的控制台应用项目
4. 编写第一个 Hello World 程序

## 基础语法

### 第一个程序
```csharp
using System;

namespace HelloWorld
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("Hello, World!");
        }
    }
}
```

### 数据类型
```csharp
// 基本数据类型
int age = 25;
float height = 1.75f;
double weight = 70.5;
bool isStudent = true;
char grade = 'A';
string name = "张三";

// 常量
const int MAX_SCORE = 100;
```

### 变量和常量
```csharp
// 变量声明
int score;
score = 85;

// 同时声明和初始化
int level = 1;
string playerName = "玩家1";

// 隐式类型
var health = 100;  // 编译器推断为 int
var message = "游戏开始";  // 编译器推断为 string
```

## 控制结构

### 条件语句
```csharp
// if-else 语句
if (score >= 90)
{
    Console.WriteLine("优秀");
}
else if (score >= 80)
{
    Console.WriteLine("良好");
}
else
{
    Console.WriteLine("需要努力");
}

// switch 语句
switch (grade)
{
    case 'A':
        Console.WriteLine("优秀");
        break;
    case 'B':
        Console.WriteLine("良好");
        break;
    default:
        Console.WriteLine("继续努力");
        break;
}
```

### 循环语句
```csharp
// for 循环
for (int i = 0; i < 10; i++)
{
    Console.WriteLine($"第 {i + 1} 次循环");
}

// while 循环
int count = 0;
while (count < 5)
{
    Console.WriteLine($"计数: {count}");
    count++;
}

// foreach 循环
int[] numbers = {1, 2, 3, 4, 5};
foreach (int num in numbers)
{
    Console.WriteLine(num);
}
```

## 方法和函数

### 方法定义
```csharp
// 无返回值的方法
public void SayHello()
{
    Console.WriteLine("Hello!");
}

// 有返回值的方法
public int Add(int a, int b)
{
    return a + b;
}

// 带默认参数的方法
public void PrintMessage(string message = "默认消息")
{
    Console.WriteLine(message);
}
```

### 方法重载
```csharp
public class Calculator
{
    public int Add(int a, int b)
    {
        return a + b;
    }
    
    public double Add(double a, double b)
    {
        return a + b;
    }
    
    public int Add(int a, int b, int c)
    {
        return a + b + c;
    }
}
```

## 面向对象编程

### 类和对象
```csharp
public class Player
{
    // 字段
    private string name;
    private int health;
    private int level;
    
    // 属性
    public string Name
    {
        get { return name; }
        set { name = value; }
    }
    
    public int Health
    {
        get { return health; }
        set 
        { 
            if (value >= 0)
                health = value;
        }
    }
    
    // 构造函数
    public Player(string playerName)
    {
        name = playerName;
        health = 100;
        level = 1;
    }
    
    // 方法
    public void TakeDamage(int damage)
    {
        health -= damage;
        if (health <= 0)
        {
            Console.WriteLine($"{name} 被击败了！");
        }
    }
    
    public void LevelUp()
    {
        level++;
        health = 100;
        Console.WriteLine($"{name} 升级到 {level} 级！");
    }
}
```

### 继承
```csharp
// 基类
public class Animal
{
    public string Name { get; set; }
    
    public virtual void MakeSound()
    {
        Console.WriteLine("动物发出声音");
    }
}

// 派生类
public class Dog : Animal
{
    public override void MakeSound()
    {
        Console.WriteLine("汪汪！");
    }
    
    public void Fetch()
    {
        Console.WriteLine($"{Name} 去捡球");
    }
}
```

### 多态
```csharp
Animal[] animals = 
{
    new Dog { Name = "小黄" },
    new Cat { Name = "小花" },
    new Dog { Name = "小黑" }
};

foreach (Animal animal in animals)
{
    animal.MakeSound();  // 调用各自重写的方法
}
```

## 集合和数组

### 数组
```csharp
// 声明和初始化
int[] scores = new int[5];
int[] numbers = {1, 2, 3, 4, 5};
string[] names = new string[] {"张三", "李四", "王五"};

// 访问数组元素
scores[0] = 95;
Console.WriteLine(numbers[2]);  // 输出: 3
```

### 列表 (List)
```csharp
using System.Collections.Generic;

// 创建列表
List<string> fruits = new List<string>();

// 添加元素
fruits.Add("苹果");
fruits.Add("香蕉");
fruits.Add("橙子");

// 访问元素
Console.WriteLine(fruits[0]);  // 输出: 苹果

// 遍历列表
foreach (string fruit in fruits)
{
    Console.WriteLine(fruit);
}
```

### 字典 (Dictionary)
```csharp
// 创建字典
Dictionary<string, int> playerScores = new Dictionary<string, int>();

// 添加键值对
playerScores.Add("张三", 85);
playerScores.Add("李四", 92);
playerScores["王五"] = 78;

// 访问值
Console.WriteLine(playerScores["张三"]);  // 输出: 85

// 检查键是否存在
if (playerScores.ContainsKey("李四"))
{
    Console.WriteLine($"李四的分数: {playerScores["李四"]}");
}
```

## 异常处理

### try-catch 语句
```csharp
try
{
    int result = 10 / 0;  // 会引发异常
}
catch (DivideByZeroException ex)
{
    Console.WriteLine("除零错误: " + ex.Message);
}
catch (Exception ex)
{
    Console.WriteLine("发生错误: " + ex.Message);
}
finally
{
    Console.WriteLine("无论是否发生异常都会执行");
}
```

### 抛出异常
```csharp
public void SetAge(int age)
{
    if (age < 0)
    {
        throw new ArgumentException("年龄不能为负数");
    }
    
    this.age = age;
}
```

## 文件操作

### 读写文件
```csharp
using System.IO;

// 写入文件
string content = "这是要写入的内容";
File.WriteAllText("example.txt", content);

// 读取文件
string readContent = File.ReadAllText("example.txt");
Console.WriteLine(readContent);

// 逐行读取
string[] lines = File.ReadAllLines("example.txt");
foreach (string line in lines)
{
    Console.WriteLine(line);
}
```

## Unity 中的 C#

### MonoBehaviour 基类
```csharp
using UnityEngine;

public class PlayerController : MonoBehaviour
{
    public float speed = 5f;
    
    void Start()
    {
        // 游戏开始时调用
    }
    
    void Update()
    {
        // 每帧调用
        float horizontal = Input.GetAxis("Horizontal");
        transform.Translate(Vector3.right * horizontal * speed * Time.deltaTime);
    }
}
```

### Unity 特有的数据类型
```csharp
// Vector3 - 三维向量
Vector3 position = new Vector3(0, 5, 0);
Vector3 movement = Vector3.up * 2f;

// Quaternion - 旋转
Quaternion rotation = Quaternion.Euler(0, 90, 0);

// Color - 颜色
Color red = Color.red;
Color customColor = new Color(1f, 0.5f, 0.3f, 1f);
```

## 最佳实践

### 命名规范
- **类名**: PascalCase (PlayerController)
- **方法名**: PascalCase (MovePlayer)
- **变量名**: camelCase (playerHealth)
- **常量名**: UPPER_CASE (MAX_HEALTH)

### 代码组织
```csharp
// 使用命名空间
namespace GameLogic
{
    public class GameManager
    {
        // 私有字段
        private int score;
        
        // 公共属性
        public int Score => score;
        
        // 公共方法
        public void AddScore(int points)
        {
            score += points;
        }
    }
}
```

## 学习资源

### 官方文档
- [C# 编程指南](https://docs.microsoft.com/zh-cn/dotnet/csharp/)
- [Unity 脚本参考](https://docs.unity3d.com/ScriptReference/)

### 在线教程
- [菜鸟教程 C#](https://www.runoob.com/csharp/csharp-tutorial.html)
- [微软 C# 学习路径](https://docs.microsoft.com/zh-cn/learn/paths/csharp-first-steps/)

### 练习项目
- 计算器程序
- 文字冒险游戏
- 简单的管理系统

## 常见问题

### Q: C# 和 C++ 有什么区别？
A: C# 是托管语言，有自动内存管理；C++ 是非托管语言，需要手动管理内存。

### Q: 如何调试 C# 代码？
A: 使用 Visual Studio 的调试器，设置断点，逐步执行代码。

### Q: Unity 中的 C# 版本？
A: Unity 支持 C# 8.0 及更高版本（取决于 Unity 版本）。

## 下一步

掌握 C# 基础后，可以：
- 学习 [Unity 入门](../Unity/入门.md)
- 了解 [UE 编程](../UE/入门.md)
- 参与 [项目开发](../项目信息/蜀祭·太初.md)

---

*需要帮助？查看 [项目信息](../项目信息/食几何时.md) 或联系社团导师*
