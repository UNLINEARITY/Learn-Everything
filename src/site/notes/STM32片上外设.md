---
{"dg-publish":true,"dg-path":"MCU微控制器/STM32/STM32片上外设.md","tags":["Preipheral"],"permalink":"/MCU微控制器/STM32/STM32片上外设/","dgPassFrontmatter":true,"noteIcon":"","created":"2024-07-22T07:55:45.554+08:00","updated":"2024-09-17T00:34:38.770+08:00"}
---

(terminology::**Preipheral**)

| 英文                 | 名称            |     | 英文               | 名称        |
| ------------------ | ------------- | --- | ---------------- | --------- |
| [[NVIC\|NVIC]]     | **嵌套向量中断控制器** |     | [[USB\|USB]]     | USB通信     |
| SysTick            | 系统滴答定时器       |     | [[USART\|USART]] | 同步/异步串口通信 |
| [[RCC\|RCC]]       | 复位和时钟控制       |     | [[I2C\|I2C]]     | I2C通信     |
| [[GPIO\|GPIO]]     | 通用IO口         |     | [[SPI\|SPI]]     | SPI通信     |
| [[AFIO\|AFIO]]     | 复用IO口         |     | [[CAN\|CAN]]     | CAN通信     |
| [[EXTI\|EXTI]]     | 外部中断          |     | PWR              | 电源控制      |
| [[TIM\|TIM]]       | **定时器**       |     | BKP              | 备份寄存器     |
| [[STM32 ADC\|ADC]] | 模数转换器         |     | [[IWDG\|IWDG]]   | 独立看门狗     |
| DAC                | 数模转换器         |     | [[WWDG\|WWDG]]         | 窗口看门狗     |
| [[DMA\|DMA]]            | 直接内存访问        |     | SDIO             | SD卡接口     |
| [[RTC\|RTC]]       | 实时时钟          |     | FSMC             | 可变静态存储控制器 |
| CRC                | CRC校验         |     | USB OTG          | USB主机接口   |

### 共同代码
#### 初始化
一般都是 RCC 开启时钟，GPIO 初始化，然后再为特定外设的初始化
外设基本代码：都是使用[[结构体\|结构体]]初始化。

定义结构体、给结构体赋值、将结构体地址传递
```C
//封装的代码
void Preipheral_DeInit(void);
void Preipheral_Init(Preipheral_InitTypeDef* Preipheral_InitStruct);
void Preipheral_StructInit(Preipheral_InitTypeDef* Preipheral_InitStruct);
```

```C
//实际操作
Preipheral_InitTypeDef Preipheral_InitStruct ; //定义结构体
Preipheral_InitStruct.member1= ; 
Preipheral_InitStruct.member2= ; 
//...  引出结构体的成员，进行赋值
Preipheral_Init(&Preipheral_InitStruct); //将结构体的地址传入，进行初始化
```

#### 状态标志位
状态标志位，在状态寄存器中
```C
FlagStatus Preipheral_GetFlagStatus(USART_TypeDef* USARTx, uint16_t USART_FLAG);

void Preipheral_ClearFlag(USART_TypeDef* USARTx, uint16_t USART_FLAG);

ITStatus Preipheral_GetITStatus(USART_TypeDef* USARTx, uint16_t USART_IT);

void Preipheral_ClearITPendingBit(USART_TypeDef* USARTx, uint16_t USART_IT);
```

#### 中断配置
[[NVIC\|NVIC]]


```C

```

### 说明
>[!important] 注意
>调用初始化函数，将结构体地址传入函数时，就写入到硬件的寄存器中了
>所以可以直接更改值继续使用，初始化其他外设

```C
Preipheral_InitTypeDef Preipheral_InitStruct;
Preipheral_InitStruct.member1=x1;
Preipheral_InitStruct.member2=y1;
Preipheral1_Init(&Preipheral_InitStruct);

Preipheral_InitTypeDef Preipheral_InitStruct;
Preipheral_InitStruct.member1=x2;
Preipheral_InitStruct.member2=y2;
Preipheral2_Init(&Preipheral_InitStruct);
```

