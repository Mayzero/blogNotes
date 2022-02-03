# 基础知识

## 1.大括号初始化
不幸的是，直接初始化不能用于所有类型的初始化（例如用数据列表初始化对象）。为了提供更一致的初始化机制，有使用花括号的大括号初始化（也称为统一初始化或列表初始化）。

大括号初始化有三种形式：
``` c++
int width { 5 }; // direct brace initialization of value 5 into variable width (preferred)
int height = { 6 }; // copy brace initialization of value 6 into variable height
int depth {}; // value initialization (see next section)
```
直接和复制大括号初始化函数几乎相同，但通常首选直接形式。

大括号初始化具有不允许“缩小”转换的额外好处。这意味着，如果您尝试使用大括号初始化来使用无法安全保存的值来初始化变量，编译器将抛出警告或错误。例如：
``` c++
int width { 4.5 }; // error: not all double values fit into an int
```
在上面的代码片段中，我们试图将一个具有小数部分（0.5 部分）的数字（4.5）分配给一个整数变量（它只能保存没有小数部分的数字）。复制和直接初始化会删除小数部分，导致将值 4 初始化为可变宽度。但是，使用大括号初始化，这将导致编译器发出错误（这通常是一件好事，因为很少需要丢失数据）。允许在没有潜在数据丢失的情况下进行转换。

### 值初始化和零初始化
当一个变量用空括号初始化时，就会发生值初始化。在大多数情况下，值初始化会将变量初始化为零（或空，如果这更适合给定类型）。在发生归零的这种情况下，这称为归零初始化。

    int width {}; // zero initialization to value 0

## 2.iostream简介：cout、cin、endl
容易混淆 std::cin、std::cout、插入运算符 (<<) 和提取运算符 (>>)。这是一个容易记住的方法：

'std::cin' 和 'std::cout' 总是在语句的左侧。

'std::cout' 用于输出一个值（cout = 字符输出）

'std::cin' 用于获取输入值（cin = 字符输入）

'<<' 与 'std::cout' 一起使用，并显示数据移动的方向（如果 std::cout 表示控制台，则输出数据正在从变量移动到控制台）。std::cout << 4 将 4 的值移动到控制台

'>>' 与 std::cin 一起使用，并显示数据移动的方向（如果 std::cin 表示键盘，则输入数据正在从键盘移动到变量）。std::cin >> x 将用户从键盘输入的值移动到 x

### std::endl 与 '\n'
使用 std::endl 可能有点低效，因为它实际上做了两项工作：将光标移动到下一行，并“刷新”输出（确保它立即显示在屏幕上）。当使用 std::cout 将文本写入控制台时，std::cout 通常会刷新输出（如果不刷新，则通常无关紧要），因此 std::endl 刷新并不重要。

因此，通常首选使用 '\n' 字符。'\n' 字符将光标移动到下一行，但不会进行冗余刷新，因此它的性能更好。'\n' 字符也更容易阅读，因为它更短并且可以嵌入到现有文本中。

这是一个以两种不同方式使用 '\n' 的示例：
```c++
#include <iostream> // for std::cout

int main()
{
    int x{ 5 };
    std::cout << "x is equal to: " << x << '\n'; // Using '\n' standalone
    std::cout << "And that's all, folks!\n"; // Using '\n' embedded into a double-quoted piece of text (note: no single quotes when used this way)
    return 0;
}
```
!!! note "Best practice"
    将文本输出到控制台时，首选 '\n' 而不是 std::endl。

## 3.基本格式的建议
1.制表符设置为 4 个缩进空格

2.如果用运算符（例如 << 或 +）拆分长行，则应将运算符放在下一行的开头，而不是当前行的结尾
```c++
std::cout << 3 + 4
    + 5 + 6
    * 7 * 8;
```
3.通过对齐值或注释或在代码块之间添加间距，使用空格使您的代码更易于阅读。
```c++
cost          = 57;
pricePerItem  = 24;
value         = 5;
numberOfItems = 17;

std::cout << "Hello world!\n";                  // cout lives in the iostream library
std::cout << "It is very nice to meet you!\n";  // these comments are easier to read
std::cout << "Yeah!\n";                         // especially when all lined up
```

## 4.表达式
```c++
// five() is a function that returns the value 5
int five()
{
    return 5;
}
int main()
{
    int a{ 2 };             // initialize variable a with literal value 2
    int b{ 2 + 3 };         // initialize variable b with computed value 5
    int c{ (2 * 3) + 4 };   // initialize variable c with computed value 10
    int d{ b };             // initialize variable d with variable value 5
    int e{ five() };        // initialize variable e with function return value 5

    return 0;
}
```
表达式是可以执行以产生奇异值的文字、变量、运算符和函数调用的组合。执行表达式的过程称为求值，产生的单个值称为表达式的结果。

## 5.前向声明和定义向前声明和定义
前向声明允许我们在实际定义标识符之前告诉编译器标识符的存在。

对于函数，这允许我们在定义函数体之前告诉编译器函数的存在。这样，当编译器遇到对函数的调用时，它会知道我们正在调用函数，并且可以检查以确保我们正确调用函数，即使它还不知道如何或在哪里功能已定义。

要为函数编写前向声明，我们使用称为函数原型的声明语句。函数原型由函数的返回类型、名称、参数组成，但没有函数体（花括号和它们之间的所有内容），以分号结尾。

这是 add 函数的函数原型：
```c++
int add(int x, int y); // function prototype includes return type, name, parameters, and semicolon.  No function body!
```
现在，这是我们没有编译的原始程序，使用函数原型作为函数 add 的前向声明：
```c++
#include <iostream>

int add(int x, int y); // forward declaration of add() (using a function prototype)

int main()
{
    std::cout << "The sum of 3 and 4 is: " << add(3, 4) << '\n'; // this works because we forward declared add() above
    return 0;
}

int add(int x, int y) // even though the body of add() isn't defined until here
{
    return x + y;
}
```
值得注意的是，函数原型不需要指定参数的名称。在上面的代码中，您还可以像这样转发声明您的函数：
```c++
int add(int, int); // valid function prototype
```
但是，我们更喜欢给我们的参数命名（使用与实际函数相同的名称），因为它可以让您通过查看原型来了解函数参数是什么。否则，您必须找到函数定义。

!!! note "转发声明一个函数但没有定义它会发生什么。"
    视情况而定。如果进行了前向声明，但从未调用过该函数，则程序将编译并运行良好。但是，如果进行了前向声明并调用了该函数，但程序从未定义该函数，则程序将正常编译，但链接器会抱怨它无法解析函数调用。

## 6. 包含多个文件的程序
main.cpp（带有前向声明）：
```c++
#include <iostream>

int add(int x, int y); // needed so main.cpp knows that add() is a function declared elsewhere

int main()
{
    std::cout << "The sum of 3 and 4 is: " << add(3, 4) << '\n';
    return 0;
}
```
add.cpp（保持不变）：
```c++
int add(int x, int y)
{
    return x + y;
}
```
当编译器编译 main.cpp 时，它会知道 add 是什么标识符并得到满足。链接器会将 main.cpp 中的 add 函数调用连接到 add.cpp 中的函数 add 定义。

使用这种方法，我们可以让文件访问存在于另一个文件中的函数。

## 7.Header files 头文件
随着程序变得越来越大（并使用更多文件），必须转发声明您要使用的每个在不同文件中定义的函数变得越来越乏味。如果您可以将所有前向声明放在一个地方，然后在需要时导入它们，那不是很好吗？

>头文件允许我们将声明放在一个位置，然后在需要它们的地方导入它们。这可以节省大量在多文件程序中的输入。

### Using standard library header files
```c++
#include <iostream>

int main()
{
    std::cout << "Hello, world!";
    return 0;
}
```
答案是 std::cout 已在“iostream”头文件中前向声明。当我们#include，我们要求预处理器将所有内容（包括 std::cout 的前向声明）从名为“iostream”的文件复制到执行#include 的文件中。

> 当#include 文件时，包含文件的内容将插入到包含点。这提供了一种从另一个文件中提取声明的有用方法。

当涉及到函数和变量时，值得记住的是，头文件通常只包含函数和变量声明，而不包含函数和变量定义（否则可能导致违反单一定义规则）

### 编写自己的头文件
头文件只包含两部分:
1. A header guard 头文件保护符
2. 头文件的实际内容，应该是我们希望其他文件能够看到的所有标识符的前向声明。

### 源文件应该包括它们的配对头文件
something.h:
```c++
int something(int); // return type of forward declaration is int
```
something.cpp:
```c++
#include "something.h"

void something(int) // error: wrong return type
{
}
```
因为 something.cpp #includes something.h，编译器会注意到函数 something() 的返回类型不匹配，并给我们一个编译错误。如果something.cpp 没有#include something.h，我们必须等到链接器发现差异，这会浪费时间。对于另一个示例，请参阅此评论。

### 尖括号与双引号
当我们使用尖括号时，我们是在告诉预处理器这是一个不是我们自己编写的头文件。编译器将仅在包含目录指定的目录中搜索头文件。包含目录配置为项目/IDE 设置/编译器设置的一部分，通常默认为包含编译器和/或操作系统附带的头文件的目录。编译器不会在项目的源代码目录中搜索头文件。

当我们使用双引号时，我们是在告诉预处理器这是我们编写的头文件。编译器将首先在当前目录中搜索头文件。如果在那里找不到匹配的标头，它将搜索包含目录。

!!! Note
    使用双引号来包含您已编写或预期在当前目录中找到的头文件。使用尖括号来包含您的编译器、操作系统或您在系统其他地方安装的第三方库附带的头文件。
### Header file best practices
- 始终包括头守卫（我们将在下一课中介绍这些内容）。

- 不要在头文件中定义变量和函数（全局常量是一个例外——我们稍后会介绍）

- 为您的头文件提供与它们关联的源文件相同的名称（例如，grades.h 与grades.cpp 配对）。

- 每个头文件都应该有一个特定的工作，并且尽可能独立。例如，您可以将所有与功能 A 相关的声明放在 Ah 中，将所有与功能 B 相关的声明放在 Bh 中。这样，如果您以后只关心 A，则可以只包含 Ah 而不会获得与 B 相关的任何内容.

- 请注意您需要为您在代码文件中使用的功能显式包含哪些标头

- 您编写的每个标头都应该自己编译（它应该#include它需要的每个依赖项）

- 仅 #include 您需要的内容（不要仅仅因为可以包含所有内容）。

- 不要#include .cpp 文件。