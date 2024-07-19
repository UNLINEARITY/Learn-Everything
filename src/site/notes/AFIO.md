---
{"dg-publish":true,"dg-path":"MCU微控制器/STM32/AFIO.md","permalink":"/MCU微控制器/STM32/AFIO/","dgPassFrontmatter":true,"noteIcon":"","created":"2024-07-16T21:33:01.069+08:00","updated":"2024-07-19T19:31:07.398+08:00"}
---

**Alternate Function I/O**
即复用功能输入/输出

允许用户配置 [[GPIO\|GPIO]] 引脚的复用功能


主要用于引脚复用功能的选择和重定义
在STM32中，AFIO主要完成两个任务：复用功能引脚重映射、中断引脚选择


### GPIO. h

```C
//复位 AFIO外设，调用此函数，将AFIO的配置全部清除
void GPIO_AFIODeInit(void);
```

```C
void GPIO_PinRemapConfig(uint32_t GPIO_Remap, FunctionalState NewState);  //引脚重映射
```


[[STM32中断系统\|STM32中断系统]]：

```C
void GPIO_EXTILineConfig(uint8_t GPIO_PortSource, uint8_t GPIO_PinSource); // 外部中断选择，配置数据选择器来选择想要的中断引脚
```


```C
//配置事件输出功能   （一般使用的不多）
void GPIO_EventOutputConfig(uint8_t GPIO_PortSource, uint8_t GPIO_PinSource);
void GPIO_EventOutputCmd(FunctionalState NewState);
```


```C
void GPIO_ETH_MediaInterfaceConfig(uint32_t GPIO_ETH_MediaInterface);  //以太网设备
```

