---
{"dg-publish":true,"dg-path":"工具/mermaid.md","permalink":"/工具/mermaid/","dgPassFrontmatter":true,"noteIcon":"","created":"2024-04-22T22:03:17.417+08:00","updated":"2024-04-26T22:39:33.105+08:00"}
---

[官网](https://mermaid.js.org/)


```mermaid
graph LR
基本语法-->1[流程图方向] & 2[节点形状] & 3[节点之间的连接]
1--> TB从上到下 & BT从下到上 & RL从右到左 & LR从左到右
2-->id1(圆角矩形) & id2([体育场形]) & id3[[子程序]] & id4[(圆柱形)] & id5((圆形)) & id6{菱形} & id7{{六边形}}
3 --> 带箭头
3 ---  直接连接
3 --- text --- 带文本
3 ---code-->代码
```



