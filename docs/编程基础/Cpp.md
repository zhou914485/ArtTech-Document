# C++ 编程基础

## C++ 简介

C++ 是一种通用的编程语言，由 Bjarne Stroustrup 在 1980 年代开发。它是 C 语言的扩展，支持面向对象编程，广泛应用于系统软件、游戏引擎、嵌入式系统等领域。

## 为什么学习 C++？

### 优势
- **高性能** - 编译型语言，运行效率高
- **底层控制** - 可以直接操作内存和硬件
- **跨平台** - 支持多种操作系统
- **丰富的库** - 标准库和第三方库丰富
- **工业标准** - 大型项目和游戏引擎的首选

### 应用领域
- **游戏开发** - UE、CryEngine 等游戏引擎
- **系统编程** - 操作系统、驱动程序
- **嵌入式开发** - 单片机、IoT 设备
- **高性能计算** - 科学计算、图形处理
- **金融软件** - 高频交易系统

## 开发环境搭建

### 推荐工具
- **Visual Studio** - Windows 平台首选
- **Code::Blocks** - 跨平台轻量级 IDE
- **CLion** - JetBrains 专业工具
- **Dev-C++** - 简单易用的初学者工具

### 编译器选择
- **MSVC** - Microsoft Visual C++ 编译器
- **GCC** - GNU 编译器集合
- **Clang** - LLVM 编译器

## 基础语法

### 第一个程序
```cpp
#include <iostream>
using namespace std;

int main() {
    cout << "Hello, World!" << endl;
    return 0;
}
```

### 数据类型
```cpp
// 基本数据类型
int age = 25;
float height = 1.75f;
double weight = 70.5;
bool isStudent = true;
char grade = 'A';

// 字符串
string name = "张三";

// 常量
const int MAX_SCORE = 100;
const double PI = 3.14159;
```

### 变量和指针
```cpp
// 变量声明
int score;
score = 85;

// 指针
int* ptr = &score;  // ptr 指向 score 的地址
cout << *ptr << endl;  // 输出 score 的值

// 引用
int& ref = score;  // ref 是 score 的别名
ref = 90;  // 修改 ref 就是修改 score
```

## 控制结构

### 条件语句
```cpp
// if-else 语句
if (score >= 90) {
    cout << "优秀" << endl;
} else if (score >= 80) {
    cout << "良好" << endl;
} else {
    cout << "需要努力" << endl;
}

// switch 语句
switch (grade) {
    case 'A':
        cout << "优秀" << endl;
        break;
    case 'B':
        cout << "良好" << endl;
        break;
    default:
        cout << "继续努力" << endl;
        break;
}
```

### 循环语句
```cpp
// for 循环
for (int i = 0; i < 10; i++) {
    cout << "第 " << i + 1 << " 次循环" << endl;
}

// while 循环
int count = 0;
while (count < 5) {
    cout << "计数: " << count << endl;
    count++;
}

// do-while 循环
int num;
do {
    cout << "输入一个正数: ";
    cin >> num;
} while (num <= 0);
```

## 函数

### 函数定义
```cpp
// 无返回值的函数
void sayHello() {
    cout << "Hello!" << endl;
}

// 有返回值的函数
int add(int a, int b) {
    return a + b;
}

// 带默认参数的函数
void printMessage(string message = "默认消息") {
    cout << message << endl;
}
```

### 函数重载
```cpp
// 同名函数不同参数
int add(int a, int b) {
    return a + b;
}

double add(double a, double b) {
    return a + b;
}

int add(int a, int b, int c) {
    return a + b + c;
}
```

### 函数指针
```cpp
// 函数指针声明
int (*operation)(int, int);

// 指向函数
operation = add;

// 调用函数
int result = operation(5, 3);
```

## 面向对象编程

### 类和对象
```cpp
class Player {
private:
    string name;
    int health;
    int level;

public:
    // 构造函数
    Player(string playerName) : name(playerName), health(100), level(1) {}
    
    // 析构函数
    ~Player() {
        cout << name << " 离开了游戏" << endl;
    }
    
    // 获取器和设置器
    string getName() const { return name; }
    int getHealth() const { return health; }
    
    void setHealth(int newHealth) {
        if (newHealth >= 0) {
            health = newHealth;
        }
    }
    
    // 成员函数
    void takeDamage(int damage) {
        health -= damage;
        if (health <= 0) {
            cout << name << " 被击败了！" << endl;
        }
    }
    
    void levelUp() {
        level++;
        health = 100;
        cout << name << " 升级到 " << level << " 级！" << endl;
    }
};
```

### 继承
```cpp
// 基类
class Animal {
protected:
    string name;
    
public:
    Animal(string animalName) : name(animalName) {}
    
    virtual void makeSound() {
        cout << "动物发出声音" << endl;
    }
    
    virtual ~Animal() = default;  // 虚析构函数
};

// 派生类
class Dog : public Animal {
public:
    Dog(string dogName) : Animal(dogName) {}
    
    void makeSound() override {
        cout << name << " 汪汪！" << endl;
    }
    
    void fetch() {
        cout << name << " 去捡球" << endl;
    }
};
```

### 多态
```cpp
// 多态示例
Animal* animals[] = {
    new Dog("小黄"),
    new Cat("小花"),
    new Dog("小黑")
};

for (int i = 0; i < 3; i++) {
    animals[i]->makeSound();  // 调用各自重写的方法
    delete animals[i];  // 释放内存
}
```

## 内存管理

### 动态内存分配
```cpp
// 使用 new 和 delete
int* ptr = new int(42);
cout << *ptr << endl;
delete ptr;  // 释放内存

// 动态数组
int* arr = new int[10];
for (int i = 0; i < 10; i++) {
    arr[i] = i * 2;
}
delete[] arr;  // 释放数组内存
```

### 智能指针 (C++11)
```cpp
#include <memory>

// unique_ptr
std::unique_ptr<Player> player = std::make_unique<Player>("玩家1");

// shared_ptr
std::shared_ptr<Player> sharedPlayer = std::make_shared<Player>("玩家2");

// 自动内存管理，不需要手动 delete
```

## 标准库

### 容器类
```cpp
#include <vector>
#include <list>
#include <map>
#include <set>

// vector - 动态数组
std::vector<int> numbers = {1, 2, 3, 4, 5};
numbers.push_back(6);

// map - 关联容器
std::map<string, int> scores;
scores["张三"] = 85;
scores["李四"] = 92;

// set - 集合
std::set<int> uniqueNumbers = {1, 2, 3, 3, 4, 5};  // 自动去重
```

### 算法
```cpp
#include <algorithm>

// 排序
std::sort(numbers.begin(), numbers.end());

// 查找
auto it = std::find(numbers.begin(), numbers.end(), 3);
if (it != numbers.end()) {
    cout << "找到了 3" << endl;
}

// 遍历
std::for_each(numbers.begin(), numbers.end(), [](int n) {
    cout << n << " ";
});
```

## 现代 C++ 特性

### auto 关键字
```cpp
auto x = 42;        // 推断为 int
auto y = 3.14;      // 推断为 double
auto name = "Tom";  // 推断为 const char*

// 用于复杂类型
auto it = numbers.begin();
```

### 范围 for 循环
```cpp
std::vector<int> numbers = {1, 2, 3, 4, 5};

// 传统方式
for (size_t i = 0; i < numbers.size(); i++) {
    cout << numbers[i] << " ";
}

// 范围 for 循环
for (int num : numbers) {
    cout << num << " ";
}

// 引用方式修改
for (int& num : numbers) {
    num *= 2;
}
```

### Lambda 表达式
```cpp
// 基本 lambda
auto add = [](int a, int b) -> int {
    return a + b;
};

int result = add(5, 3);

// 捕获外部变量
int multiplier = 2;
auto multiply = [multiplier](int x) {
    return x * multiplier;
};
```

## 模板

### 函数模板
```cpp
template<typename T>
T maximum(T a, T b) {
    return (a > b) ? a : b;
}

// 使用
int maxInt = maximum(5, 3);
double maxDouble = maximum(3.14, 2.71);
```

### 类模板
```cpp
template<typename T>
class Stack {
private:
    std::vector<T> elements;
    
public:
    void push(T element) {
        elements.push_back(element);
    }
    
    T pop() {
        if (elements.empty()) {
            throw std::runtime_error("Stack is empty");
        }
        T element = elements.back();
        elements.pop_back();
        return element;
    }
    
    bool empty() const {
        return elements.empty();
    }
};

// 使用
Stack<int> intStack;
Stack<string> stringStack;
```

## 异常处理

### try-catch 语句
```cpp
try {
    int result = 10 / 0;  // 可能引发异常
} catch (const std::exception& e) {
    cout << "发生异常: " << e.what() << endl;
} catch (...) {
    cout << "发生未知异常" << endl;
}
```

### 自定义异常
```cpp
class CustomException : public std::exception {
private:
    std::string message;
    
public:
    CustomException(const std::string& msg) : message(msg) {}
    
    const char* what() const noexcept override {
        return message.c_str();
    }
};

// 抛出自定义异常
throw CustomException("这是一个自定义异常");
```

## UE 中的 C++

### 基本类结构
```cpp
// .h 文件
UCLASS()
class MYGAME_API AMyActor : public AActor
{
    GENERATED_BODY()

public:
    AMyActor();

protected:
    virtual void BeginPlay() override;

    UPROPERTY(EditAnywhere, BlueprintReadWrite, Category = "Stats")
    int32 Health;

    UFUNCTION(BlueprintCallable, Category = "Actions")
    void TakeDamage(int32 Damage);

public:
    virtual void Tick(float DeltaTime) override;
};

// .cpp 文件
AMyActor::AMyActor()
{
    PrimaryActorTick.bCanEverTick = true;
    Health = 100;
}

void AMyActor::BeginPlay()
{
    Super::BeginPlay();
}

void AMyActor::TakeDamage(int32 Damage)
{
    Health -= Damage;
    if (Health <= 0)
    {
        UE_LOG(LogTemp, Warning, TEXT("Actor destroyed!"));
        Destroy();
    }
}

void AMyActor::Tick(float DeltaTime)
{
    Super::Tick(DeltaTime);
}
```

## 最佳实践

### 编码规范
- **变量命名**: 使用有意义的名称
- **常量**: 使用 const 和 constexpr
- **内存管理**: 使用智能指针
- **异常安全**: 使用 RAII 原则

### 性能优化
- **避免不必要的拷贝**: 使用引用和移动语义
- **内联函数**: 简单函数使用 inline
- **编译器优化**: 使用 -O2 或 -O3 选项

## 学习资源

### 官方文档
- [C++ 参考手册](https://en.cppreference.com/)
- [ISO C++ 标准](https://isocpp.org/)

### 在线教程
- [菜鸟教程 C++](https://www.runoob.com/cplusplus/cpp-tutorial.html)
- [C++ Primer Plus](https://book.douban.com/subject/10789789/)

### 推荐书籍
- 《C++ Primer》
- 《Effective C++》
- 《More Effective C++》

## 常见问题

### Q: C++ 和 C 的区别？
A: C++ 是 C 的超集，增加了面向对象、模板、异常处理等特性。

### Q: 如何避免内存泄漏？
A: 使用智能指针、RAII 原则，每个 new 都要有对应的 delete。

### Q: 什么时候使用指针，什么时候使用引用？
A: 引用用于别名，指针用于动态内存分配和可能为空的情况。

## 下一步

掌握 C++ 基础后，可以：
- 深入学习 [UE 进阶](../UE/进阶.md)
- 学习 [算法数据结构](算法.md)
- 参与 [项目开发](../项目信息/蜀祭·太初.md)

---

*需要帮助？查看 [项目信息](../项目信息/食几何时.md) 或联系社团导师*
