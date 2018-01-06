# 状态机监控

Joy OI中所有的本地评测任务、本地Hack任务、远程题库评测、远程题库题面拉取等均有Management Service中的状态机实例承担工作。

![Count](~/images/monitor-statemachine-count.png)

在状态机监控页面中第一个折线图反应了指定时间段内的各种状态机实例创建情况。下面将对每种状态机承担的工作进行简单的描述：

| 状态机 | 说明 |
| ------ | ---- |
| JudgeStateMachine | 负责执行本地题库的评测任务 |
| VirtualJudgeStateMachine | 负责执行远程题库的评测任务 |
| HackStateMachine | 负责执行本地题库的Hack任务 |
| CompileOnlyStateMachine | 负责编译用户创建题目的自定义比较器、标程、数据范围校验器以及远程题库的选手程序 |
| HackAllStateMachine | 当在Codeforces赛制用户成功hack时，这个状态机将负责使用hack数据评测其他选手的程序 |
| BzojSyncProblemStateMachine | 负责承担拉取Bzoj题目题面的状态机 |
| CodeVSSyncProblemStateMachine | 负责承担拉取CodeVS题目题面的状态机 |
| LeetCodeSyncProblemStateMachine | 负责承担拉取LeetCode题目题面的状态机 |

您可以通过点击图例中色块右侧的状态机名称以筛选该图表中的结果。

![Lifetime](~/images/statemachine-lifetime)

第二个图表则反应了各种状态机在您指定的时间范围内，运行的时间。通常每个`JudgeStateMachine`和`HackStateMachine`会运行10秒左右，而`VirtualJudgeStateMachine`会运行10到60秒不等。若出现大量状态机运行时长超过1分钟，则表示系统可能发生故障。

对于拉取远程题库的状态机，可能运行时长会达到半个小时到一个小时，这类评测机不会被普通用户调用，并且调用时通常会有人值守，因此管理员不需要对这类评测机的运行时间过长而担心系统故障发生。