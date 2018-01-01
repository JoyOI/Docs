# 标准程序

在允许进行Hack的赛制比赛中，为比赛题目添加标准程序以提供准确的答案生成器。

Hack过程中，系统将调用标程来计算出选手提供输入数据的答案，并用该答案与被Hack的程序输出的答案进行对比。

您可以使用C、C++、Pascal、C#等多种语言进行编写。

下面给出的样例为“A+B Problem”的标准程序


```
#include <iostream>

using namespace std;

int main()
{
    int a, b;
    cin >> a >> b;
    cout << a + b << endl;
}
```