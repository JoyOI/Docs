﻿# Blob监控

Blob监控反应了状态机在执行过程中使用二进制文件的情况。

![Blob](~/images/monitor-blob.png)

二进制文件不会莫名增长，通常与同一时段状态机实例创建成正比，约为状态机实例数量的10到30倍。若超出上述范围，有可能说明系统发生异常。