﻿# 特殊比较器

在题目答案不唯一时，我们允许出题人定义特殊比较器。

您可以使用C、C++、Pascal、C#等多种语言进行编写。

系统将根据比较器的返回值进行评测结果认定。

| 返回值 | 说明 |
| ------ | ---- |
|    0   | Accepted |
|    1   | Presentation Error |
|    2   | Wrong Answer |

下面给出的C++语言编写的比较器样例，这个样例是实现了去文末回车及行末空格的答案比较功能，需要您注意的是**比较器需要进行文件操作**，在运行目录下**std.txt**为答案输出，**out.txt**为选手输出。


```
#include <iostream>
#include <fstream>
#include <cstdio>
#include <algorithm>

using namespace std;

struct RetInfo{
	bool flag;
	char *ptr;
	RetInfo(){};
	RetInfo(bool f, char *p) :flag(f), ptr(p)
	{
	}
};

const int AC_CODE = 0, PE_CODE = 1, WA_CODE = 2;//return code
const int MaxSize = 100 * 1024 * 1024;//100MB
char OutData[MaxSize], StdData[MaxSize];//Data
char *OutPtr, *StdPtr;//Data pointer
int CountLine = 1;
//Var and arr
int AC();
int WA();
int PE();
//Return information
inline bool IsBlank1(const char t);
inline bool IsBlank2(const char t);
RetInfo EndOfLine(char* p);
bool EndOfFile(char* p);
char* SkipBlank(char* p);
//Functions for Judge()
int Judge();

int main(int argc, char* argv[], char* envp[])
{
	FILE *OutDataFP,*StdDataFP;
	if (argc < 3)
	{
		OutDataFP = fopen("out.txt","r");
		StdDataFP = fopen("std.txt","r");
	}
	else
    	{
        	OutDataFP = fopen(argv[1],"r");
		StdDataFP = fopen(argv[2],"r");
    	}

	fread(OutData,sizeof(char),MaxSize,OutDataFP);
	fread(StdData,sizeof(char),MaxSize,StdDataFP);
	auto RET = Judge();
	fclose(OutDataFP);
	fclose(StdDataFP);
	return RET;
}

int AC()
{
	return AC_CODE;
}

int WA()
{
	char *StdPtrT = max((char*)StdData, StdPtr - 10), *OutPtrT = max((char*)OutData, OutPtr - 10);
	int i;
	cout << "<p>第<span style='color:red'>" << CountLine << "</span>行与答案输出不匹配</p>" << endl;
	cout << "<p>答案输出：</p><pre>";
	if (StdPtrT != StdData)
		cout << "...";
	for (; StdPtrT != StdPtr; ++StdPtrT)
		cout << *StdPtrT;
	for (i = 0; i < 10 && *StdPtrT != '\0'; ++i, ++StdPtrT)
		cout << *StdPtrT;
	if (*StdPtrT != '\0')
		cout << "...";
	cout << "</pre>" << endl;
	cout << "<p>选手输出：</p><pre>";
	if (OutPtrT != OutData)
		cout << "...";
	for (; OutPtrT != OutPtr; ++OutPtrT)
		cout << *OutPtrT;
	for (i = 0; i < 10 && *OutPtrT != '\0'; ++i, ++OutPtrT)
		cout << *OutPtrT;
	if (*OutPtrT != '\0')
		cout << "...";
	cout << "</pre>" << endl;
	return WA_CODE;
}

int PE()
{
	return PE_CODE;
}

inline bool IsBlank1(const char t)
{
	return t == ' ' || t == '\r' || t == '\t';
}

inline bool IsBlank2(const char t)
{
	return t == ' ' || t == '\r' || t == '\t' || t == '\n';
}

char* SkipBlank(char* p)
{
	while (IsBlank2(*p))
	{
		if (*p == '\n')
			++CountLine;
		++p;
	}
	return p;
}

RetInfo EndOfLine(char* p)
{
	while (IsBlank1(*p))
		++p;
	return RetInfo(*p == '\n' || *p == '\0', p);
}

bool EndOfFile(char* p)
{
	while (IsBlank2(*p))
		++p;
	return *p == '\0';
}

int Judge()
{
	RetInfo ret1, ret2;
	bool Skip = false;
	StdPtr = StdData;
	OutPtr = OutData;
	while (*StdPtr != '\0' && *OutPtr != '\0')
	{
		if (*StdPtr == '\n')
			++CountLine;
		if (*StdPtr != *OutPtr)
		{
			ret1 = EndOfLine(StdPtr);
			ret2 = EndOfLine(OutPtr);
			if (ret1.flag && ret2.flag)
			{
				StdPtr = ret1.ptr;
				OutPtr = ret2.ptr;
			}
			else
			{
				StdPtr = SkipBlank(ret1.ptr);
				OutPtr = SkipBlank(ret2.ptr);
				Skip = true;
			}
			if (*StdPtr != *OutPtr && *StdPtr != '\0' && *OutPtr != '\0')
				return WA();
		}
		++StdPtr;
		++OutPtr;
	}
	if (EndOfFile(StdPtr) == false || EndOfFile(OutPtr) == false)
		return WA();
	return Skip ? PE() : AC();
}
```