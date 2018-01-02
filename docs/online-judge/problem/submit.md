# 提交评测

在Joy OI的题目展示页面右侧，点击“进入编程模式”或“提交评测”即可打开代码提交窗口。

![Submit code](~/images/submit-code.png)

前者则是打开一个全屏分栏界面，左侧为题目内容，右侧为代码编辑器，鼠标移至分界区可以调整左右两边窗口大小。

![Edit mode](~/images/submit-edit-mode.png)

后者则是打开一个弹窗，进行代码粘贴。

![Submit box](~/images/submit-box.png)

Joy OI本地题库支持选手使用C、C++、Pascal、C#、VB.NET、Python 3、Java语言进行作答。下面是这些语言对应编译器的编译参数：

| 语言 | 编译参数 | 版本 |
| ---- | -------- | ---- |
|  C   | `gcc -Os -o Main.out -DONLINE_JUDGE -lm --std=c99 Main.c` | GNU GCC 4.7 |
| C++  | `g++ -Os -o Main.out -DONLINE_JUDGE -lm --std=c++98 Main.cpp` | GNU G++ 4.7 |
| Pascal | `fpc -Os -oMain.out -dONLINE_JUDGE Main.pas` | Free pascal 3.0.0 |
|  C#  | `dotnet build -o ./ -c Release` | .NET Core 2.0.4 |
|VB.NET| `dotnet build -o ./ -c Release` | .NET Core 2.0.4 |
| Java | `javac-jar Main.java Main Main.jar` | JDK 8 |
| Python 3 | `python3 Main.py` | Python 3 |

> [!NOTE]
> 上述编译参数仅为本地题库的编译参数，远程题库以实际目标平台使用的编译参数为准。

> [!NOTE]
> 对于任何一种语言，均需遵循题目的时间与空间限制，请选手谨慎选择使用的语言，如Java的运行速度明显慢于C语言，并且要消耗更多的内存。

评测机使用Ubuntu 16.04 LTS操作系统，请知晓。

在代码编辑区选择好您提交代码的语言后，点击右侧“提交评测”，Joy OI后台即为您进行评测，每道题目评测时间约为10秒钟，10秒钟后无需刷新，系统自动将评测结果展示给您。

![Submit result](~/images/submit-result.png)

在结果上点击鼠标左键，即可展开详情查看，您可以查看测试点相关的信息。