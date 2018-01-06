# Hack记录监控

Hack记录监控页面中反应了Online Judge系统评测结果在一段时间内的状态。

![Hack](~/images/monitor-hack.png)

若一段时间内没有任何Hack记录，或System Error的状态暴增，则说明`Management Service`系统有可能发生了故障。

管理员应当按如下情况考虑并排查问题：

- Management Service无法连接到数据库
- Management Service的Blob过多，导致数据库已满
- System Error的评测记录系远程评测端故障
- 前端Web页面发生BUG导致无法提交Hack