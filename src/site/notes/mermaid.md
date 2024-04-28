---
{"dg-publish":true,"dg-path":"工具/mermaid.md","permalink":"/工具/mermaid/","dgPassFrontmatter":true,"noteIcon":"","created":"2024-04-22T22:03:17.417+08:00","updated":"2024-04-28T18:56:07.854+08:00"}
---

[官网](https://mermaid.js.org/)

```mermaid
graph LR
	begin --> en
```


### 基本语法
```
---
title: name
---
```
#### 方向
direction 
TB/TD  自上而下
BT  自下而上
RL  从右到左
LR  从左到右
#### 基本图形
`[]`   方框（默认）
`()`  圆角框
`[[]]`  子程序
`[()]` 圆柱体
`(())`  单圆
`((()))` 双圆
`{}`  菱形
`{{}}`  六边形
`[//]  [\\]`  平行四边形
`[/\] [\/]`  梯形
#### 节点之间链接
```
-->
---
--text---
--text-->
-.->
-.text.->
==> 
~~~
--o
--x
o--o
x--x
<-->
```

```mermaid
graph LR
1 ==> 2 ---->3 -.....->4
```

subgraph one 
direction RL
a1-->a2 
end
### 状态图
stateDiagram
`[*]` 开始和结束
`state id{  }`   复合体

### 思维导图
mindmap

`))((`    Bang
`)(`  Cloud

```mermaid
mindmap
root((本网站))
	数学
		微积分
		概率论
		数理统计
		复变函数
		积分变换
	自动控制原理
		经典控制理论
			传递函数
			根轨迹分析
		现代控制理论
			状态空间
	物理
		力学
		电磁学
		热学
		光学
		量子力学
	计算机
		编程语言
			MATLAB
			Python
			C++
		单片机
	电力拖动
		直流拖动系统
		交流拖动系统
	技术经济与工程管理
		
```

### 桑基图
sankey-beta

```mermaid
sankey-beta
world,test,100

world,qus,10

world,ome,40
```




```mermaid
quadrantChart
    title Reach and engagement of campaigns
    x-axis Low Reach --> High Reach
    y-axis Low Engagement --> High Engagement
    quadrant-1 We should expand
    quadrant-2 Need to promote
    quadrant-3 Re-evaluate
    quadrant-4 May be improved
    Campaign A: [0.3, 0.6]
    Campaign B: [0.45, 0.23]
    Campaign C: [0.57, 0.69]
    Campaign D: [0.78, 0.34]
    Campaign E: [0.40, 0.34]
    Campaign F: [0.35, 0.78]

```
```mermaid
stateDiagram-v2
        [*] --> Active
    
        state Active {
            [*] --> NumLockOff
            NumLockOff --> NumLockOn : EvNumLockPressed
            NumLockOn --> NumLockOff : EvNumLockPressed
            --
            [*] --> CapsLockOff
            CapsLockOff --> CapsLockOn : EvCapsLockPressed
            CapsLockOn --> CapsLockOff : EvCapsLockPressed
            --
            [*] --> ScrollLockOff
            ScrollLockOff --> ScrollLockOn : EvScrollLockPressed
            ScrollLockOn --> ScrollLockOff : EvScrollLockPressed
        }

```




