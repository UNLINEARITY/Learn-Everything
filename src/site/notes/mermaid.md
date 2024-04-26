---
{"dg-publish":true,"dg-path":"工具/mermaid.md","permalink":"/工具/mermaid/","dgPassFrontmatter":true,"noteIcon":"","created":"2024-04-22T22:03:17.417+08:00","updated":"2024-04-26T21:05:10.065+08:00"}
---

[官网](https://mermaid.js.org/)



```mermaid  
graph LR
	test--> id[结束] & 开始
	结束-->世界
```

```mermaid  
flowchart TD
	Start --> Stop
```


```mermaid  
timeline
	title History of Social Media Platform
	  2002 : LinkedIn
	  2004 : Facebook : Google
	  2005 : Youtube
	  2006 : Twitter
	  2007 : Tumblr
	  2008 : Instagram
	  2010 : Pinterest
```

```mermaid  
 pie showdata
        title /r/obsidianmd posts by type
        "Graphs" : 85
        "Dashboards" : 14
        "Tips" : 1
```


```mermaid
graph LR
	项目现金流量--> 初始现金流量 & 营业净现金流量 & 终结现金流量
	初始现金流量-->id2[现金流出]-->固定资产投资 & 流动资金投资 & 其他投资
	营业净现金流量--> 现金流入 & 现金流出
	现金流入-->营业收入
	现金流出-->经营成本 & 税金及附加 & 所得税
	终结现金流量-->id1[现金流入]-->固定资产预计净残值 & 流动资金投资回收
	
```

```mermaid
graph LR
项目现金流量--> 初始现金流量 & 营业净现金流量 & 终结现金流量
初始现金流量-->id2[现金流出]-->固定资产投资 & 流动资金投资 & 其他投资
营业净现金流量--> 现金流入 & 现金流出
现金流入-->营业收入
现金流出-->经营成本 & 税金及附加 & 所得税
终结现金流量-->id1[现金流入]-->固定资产预计净残值 & 流动资金投资回收
	
```


```mermaid
graph LR
项目现金流量--> 初始现金流量 & 营业净现金流量 & 终结现金流量
初始现金流量-->id2[现金流出]-->固定资产投资 & 流动资金投资 & 其他投资

```
