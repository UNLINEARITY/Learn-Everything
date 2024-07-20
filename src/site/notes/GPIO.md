---
{"dg-publish":true,"dg-path":"MCU微控制器/STM32/GPIO.md","permalink":"/MCU微控制器/STM32/GPIO/","dgPassFrontmatter":true,"noteIcon":"","created":"2024-05-21T15:20:27.754+08:00","updated":"2024-07-20T11:33:13.346+08:00"}
---

**General Purpose Input Output** 
通用输入输出口
引脚电平：0V~3.3V    
部分 FT  Five Tolerate 可容忍 5V

### 操作步骤

1. 使用 [[RCC\|RCC]] 开启 GPIO 时钟
	所有 GPIO 都挂载在 APB2  总线上
	**开启 APB2时钟**

2. 使用 GPIO_Init 函数初始化 GPIO

3. 使用输出或输入的函数控制 GPIO 口

### GPIO. h
```C
//复位外设
void GPIO_DeInit(GPIO_TypeDef* GPIOx);
```

```C
//GPIO 初始化
void GPIO_Init(GPIO_TypeDef* GPIOx, GPIO_InitTypeDef* GPIO_InitStruct);//初始化端口，使用结构体变量初始化

void GPIO_StructInit(GPIO_InitTypeDef* GPIO_InitStruct);//给结构体变量赋一个默认值
```

```C
//GPIO 读取函数
uint8_t GPIO_ReadInputDataBit(GPIO_TypeDef* GPIOx, uint16_t GPIO_Pin);
//读取输入数据寄存器某一个端口的输入值  返回读取端口的高低电平

uint16_t GPIO_ReadInputData(GPIO_TypeDef* GPIOx);
//读取整个输入数据寄存器的输入值  返回16位数据

uint8_t GPIO_ReadOutputDataBit(GPIO_TypeDef* GPIOx, uint16_t GPIO_Pin);
//读取输出数据寄存器某一个端口的输出值  返回读取端口的高低电平

uint16_t GPIO_ReadOutputData(GPIO_TypeDef* GPIOx);
//读取整个输出数据寄存器的输出值  返回16位数据
```

```C
//GPIO 写入函数

void GPIO_SetBits(GPIO_TypeDef* GPIOx, uint16_t GPIO_Pin);
//将指定端口设为高电平

void GPIO_ResetBits(GPIO_TypeDef* GPIOx, uint16_t GPIO_Pin);
//将指定端口设为低电平

void GPIO_WriteBit(GPIO_TypeDef* GPIOx, uint16_t GPIO_Pin, BitAction BitVal);
//对位操作，写高电平或低电平

void GPIO_Write(GPIO_TypeDef* GPIOx, uint16_t PortVal);
//同时写入16个端口
```


```C
//锁定GPIO引脚配置，防止以外更改
void GPIO_PinLockConfig(GPIO_TypeDef* GPIOx, uint16_t GPIO_Pin);
```
### 基本结构
所有 GPIO 都挂载在APB2  总线上，见 [[STM32F103C8T6\|系统结构图]]
#### 总体结构图

![Pasted image 20240318151746.png](/img/user/%E5%8A%9F%E8%83%BD%E6%80%A7%E6%96%87%E4%BB%B6%E5%A4%B9/%E8%BD%BD%E5%85%A5%E7%9A%84%E5%AA%92%E4%BD%93%E8%B5%84%E6%BA%90/Pasted%20image%2020240318151746.png)


#### 位结构图

![Pasted image 20240318152503.png](/img/user/%E5%8A%9F%E8%83%BD%E6%80%A7%E6%96%87%E4%BB%B6%E5%A4%B9/%E8%BD%BD%E5%85%A5%E7%9A%84%E5%AA%92%E4%BD%93%E8%B5%84%E6%BA%90/Pasted%20image%2020240318152503.png)


•**输出模式**
下可控制端口输出高低电平，
用以驱动 LED、控制蜂鸣器、模拟通信协议输出时序等

•**输入模式**
下可读取端口的高低电平或电压
用于读取按键输入、外接模块电平信号输入、ADC 电压采集、模拟通信协议接收数据等


### 输入

避免引脚悬空而导致的输入数据不确定
加上拉/下拉电阻（阻值都比较大，尽量不影响正常的输入操作）
- 上拉电阻
	保证引脚高电平，默认高电平的输入模式
- 下拉电阻
	保证引脚低电平，默认低电平的输入模式

TTL 肖特基触发器实际上为： [[施密特触发器\|施密特触发器]]
对输入信号整流消抖
### 输出
**输出数据寄存器**
普通的 IO 口输出，**只能整体读写**
可同时控制十六个端口，对哪一个端口写 1，就对应哪一个输出

**位设置/位清除寄存器**
对某一位操作，而不影响其他位
位设置，写 1
位清除，写 1

#### 推挽输出 
高低电平均有较强的驱动能力
STM32 对高低电平的输出有绝对控制权

P-MOS N-MOS 都工作
输出数据寄存器为 1  P-MOS 导通 N-MOS 关断，输出高电平
输出数据寄存器为 0 P-MOS 关断  N-MOS导通，输出低电平

#### 开漏输出


低电平有较强的驱动能力
高电平无驱动能力

N-MOS 工作，P-MOS 断开
输出数据寄存器为 1  P-MOS N-MOS 断开，相当于输出断开，高阻模式
输出数据寄存器为 0 P-MOS 关断  N-MOS 导通，输出低电平

[[通信协议\|通信协议]]的驱动方式，例如 [[I2C\|I2C]]，多机通信避免各个设备的干扰
也可设置 5V 的输出电平信号
在 IO 引脚拉 5V 的高电平
输出数据寄存器为 1 时，输出 5V
#### 输出关闭
P-MOS N-MOS 都无效
端口的电平由外部信号控制


###  8 种输入输出模式

| 模式名称   | 库函数定义                   | 性质   | 特征                        |
| ------ | ----------------------- | ---- | ------------------------- |
| 浮空输入   | IN_FLOATING             | 数字输入 | 可读取引脚电平，若引脚悬空，则电平不确定      |
| 上拉输入   | IPU (In Pull UP)        | 数字输入 | 可读取引脚电平，内部连接上拉电阻，悬空时默认高电平 |
| 下拉输入   | IPD (In Pull DOWN)      | 数字输入 | 可读取引脚电平，内部连接下拉电阻，悬空时默认低电平 |
| 模拟输入   | AIN ( Analog IN)        | 模拟输入 | GPIO无效，引脚直接接入内部ADC        |
| 开漏输出   | OUT_OD (Out Open Drain) | 数字输出 | 可输出引脚电平，高电平为高阻态，低电平接VSS   |
| 推挽输出   | OUT_PP (Out Push Pull)  | 数字输出 | 可输出引脚电平，高电平接VDD，低电平接VSS   |
| 复用开漏输出 | AF_OD                   | 数字输出 | 由片上外设控制，高电平为高阻态，低电平接VSS   |
| 复用推挽输出 | AD_PP                   | 数字输出 | 由片上外设控制，高电平接VDD，低电平接VSS   |
|        |                         |      |                           |

#### 浮空/上拉/下拉输入

![Pasted image 20240715171532.png](/img/user/%E5%8A%9F%E8%83%BD%E6%80%A7%E6%96%87%E4%BB%B6%E5%A4%B9/%E8%BD%BD%E5%85%A5%E7%9A%84%E5%AA%92%E4%BD%93%E8%B5%84%E6%BA%90/Pasted%20image%2020240715171532.png)

输入模式下，输出功能无效
#### 模拟输入

![Pasted image 20240715171541.png](/img/user/%E5%8A%9F%E8%83%BD%E6%80%A7%E6%96%87%E4%BB%B6%E5%A4%B9/%E8%BD%BD%E5%85%A5%E7%9A%84%E5%AA%92%E4%BD%93%E8%B5%84%E6%BA%90/Pasted%20image%2020240715171541.png)

[[ADC\|ADC]] 模数转换专属模式


#### 开漏/推挽输出
![Pasted image 20240715171553.png](/img/user/%E5%8A%9F%E8%83%BD%E6%80%A7%E6%96%87%E4%BB%B6%E5%A4%B9/%E8%BD%BD%E5%85%A5%E7%9A%84%E5%AA%92%E4%BD%93%E8%B5%84%E6%BA%90/Pasted%20image%2020240715171553.png)

输出的引脚由输出数据寄存器控制

#### 复用开漏/推挽输出

![Pasted image 20240715171559.png](/img/user/%E5%8A%9F%E8%83%BD%E6%80%A7%E6%96%87%E4%BB%B6%E5%A4%B9/%E8%BD%BD%E5%85%A5%E7%9A%84%E5%AA%92%E4%BD%93%E8%B5%84%E6%BA%90/Pasted%20image%2020240715171559.png)

输出的引脚由[[STM32片上外设\|片上外设]] 控制

