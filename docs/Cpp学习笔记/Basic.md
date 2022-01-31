# 基础知识

## 大括号初始化
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

###　值初始化和零初始化
当一个变量用空括号初始化时，就会发生值初始化。在大多数情况下，值初始化会将变量初始化为零（或空，如果这更适合给定类型）。在发生归零的这种情况下，这称为归零初始化。

    int width {}; // zero initialization to value 0

## iostream简介：cout、cin、endl
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
!!! Best practice
    将文本输出到控制台时，首选 '\n' 而不是 std::endl。

## 基本格式的建议
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