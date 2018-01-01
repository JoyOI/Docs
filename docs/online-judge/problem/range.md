# 标准程序

在允许进行Hack的赛制比赛中，为比赛题目添加数据范围校验器以检查选手的Hack数据是否合法。

在系统收到Hack请求时，首先调用数据范围校验器，对数据进行校验，您在数据校验器中返回0则表示数据合法，返回1则表示不合法。

您可以使用C、C++、Pascal、C#等多种语言进行编写。

下面给出的样例为“A+B Problem”的数据范围校验器


```
using System;
using System.Collections.Generic;

namespace Range
{
    class Program
    {
        static void Main(string[] args)
        {
            string input;
            var s = new List<string>();
            while ((input = Console.ReadLine()) != null)
            {
                s.Add(input);
            }

            var full = string.Join("\r\n", s);
            if (s.Count > 1)
            {
                Console.Error.WriteLine("输入数据超过1行，不合法");
                Environment.Exit(1);
            }

            var splited = s[0].Split(' ');
            if (splited.Length != 2)
            {
                Console.Error.WriteLine($"第一行输入了{splited.Length}个数据，应当输入2个数据，不合法");
                Environment.Exit(1);
            }

            try {
                Convert.ToUInt32(splited[0]);
            }
            catch
            {
                Console.Error.WriteLine($"将{ splited[0] }转换为无符号32位整数时发生错误，不合法");
                Environment.Exit(1);
            }

            try
            {
                Convert.ToUInt32(splited[1]);
            }
            catch
            {
                Console.Error.WriteLine($"将{ splited[1] }转换为无符号32位整数时发生错误，不合法");
                Environment.Exit(1);
            }

            Console.WriteLine("恭喜，数据通过了校验");
            Environment.Exit(0);
        }
    }
}
```