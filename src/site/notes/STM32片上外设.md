---
{"dg-publish":true,"dg-path":"MCU微控制器/STM32/STM32片上外设.md","permalink":"/MCU微控制器/STM32/STM32片上外设/","dgPassFrontmatter":true,"noteIcon":"","created":"2024-07-15T11:31:20.762+08:00","updated":"2024-07-19T19:30:01.414+08:00"}
---

**Preipheral**


| 英文        | 名称        | 用途   |
| --------- | --------- | ---- |
| [[NVIC\|NVIC]]  | 嵌套向量中断控制器 |      |
| SysTick   | 系统滴答定时器   |      |
| [[RCC\|RCC]]   | 复位和时钟控制   |      |
| [[GPIO\|GPIO]]  | 通用IO口     |      |
| [[AFIO\|AFIO]]  | 复用IO口     |      |
| [[EXTI\|EXTI]]  | 外部中断      |      |
| [[TIM\|TIM]]   | 定时器       |      |
| ADC       | 模数转换器     |      |
| DMA       | 直接内存访问    |      |
| [[USART\|USART]] | 同步/异步串口通信 |      |
| [[I2C\|I2C]]   | I2C通信     | 通信协议 |
| SPI       | SPI通信     | 通信协议 |
| [[CAN\|CAN]]   | CAN通信     | 通信协议 |
| [[USB\|USB]]   | USB通信     | 通信协议 |
| [[RTC\|RTC]]   | 实时时钟      |      |
| CRC       | CRC校验     | 数据校验 |
| PWR       | 电源控制      |      |
| BKP       | 备份寄存器     |      |
| [[IWDG\|IWDG]]  | 独立看门狗     |      |
| WWDG      | 窗口看门狗     |      |
| DAC       | 数模转换器     |      |
| SDIO      | SD卡接口     |      |
| FSMC      | 可变静态存储控制器 |      |
| USB OTG   | USB主机接口   |      |


外设基本代码：
都是使用结构体初始化

定义结构体、给结构体赋值、将结构体地址传递

```C
void Preipheral_DeInit(void);

void Preipheral_Init(Preipheral_InitTypeDef* Preipheral_InitStruct);

void Preipheral_StructInit(Preipheral_InitTypeDef* Preipheral_InitStruct);
```


状态标志位，在状态寄存器中


Miscellaneous Control Register
杂项控制位的寄存器



