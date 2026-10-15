嵌入式软件开发方向，关注 **FreeRTOS、STM32 外设驱动、电机控制与固件升级**。  
通过实时控制与视觉分拣项目，实践从底层驱动、任务协作到系统集成的开发过程。

## About Me

- 💻 开发方向：嵌入式软件 / RTOS / MCU 底层软件
- 🔧 项目实践：嵌入式实时控制、边缘视觉与物联网应用
- 🧭 关注实时性、资源约束、通信可靠性与故障恢复

## Technical Skills

| 方向 | 技能 |
| --- | --- |
| Programming | C、C++（Arduino）、Python / MaixPy |
| RTOS | FreeRTOS、任务调度、信号量、互斥量、中断与任务协作 |
| MCU | STM32F103 / F407、GPIO、ADC、Timer/PWM、UART、SPI、DMA |
| Control | 编码器测速、PID 闭环控制、传感器采集、任务心跳看门狗 |
| Firmware Update | Bootloader、串口 IAP、W25Q64、CRC32、HMAC-SHA256、升级回滚 |
| Tools & Testing | Keil MDK、Arduino、Python 升级工具、主机端 C 回归测试 |

## Featured Projects

### [stm32-freertos-hood-controller](https://github.com/zjw-000/stm32-freertos-hood-controller)

基于 **STM32F103 + FreeRTOS** 的嵌入式实时控制项目，包含：

- 多任务调度、共享资源互斥与中断协作
- 编码器测速、PID 调速与环境传感器处理
- DMA + 串口空闲中断接收、IAP 升级与失败回滚
- 任务心跳看门狗、主机端回归测试与模拟断电验证

### [embedded-button-defect-detection-system](https://github.com/zjw-000/embedded-button-defect-detection-system)

基于 **K210 + STM32F407 + ESP8266**，结合 YOLOv2 视觉识别、GPIO 分拣控制与 MQTT 数据上报，配套 Android 端工程。

## Development Principles

```text
明确接口 → 分层实现 → 验证功能 → 覆盖异常 → 记录边界
```
