<div align="center">

# Hi, I'm zjw-000 👋

### Embedded Software · FreeRTOS · Motor Control · Firmware Update

嵌入式软件开发方向｜聚焦实时任务协作、电机控制与固件升级可靠性

[烟机主控系统](https://github.com/zjw-000/stm32-freertos-hood-controller) · [RTOS 任务](https://github.com/zjw-000/stm32-freertos-hood-controller/blob/master/APP_TASK/app_tasks.c) · [Bootloader](https://github.com/zjw-000/stm32-freertos-hood-controller/tree/master/Bootloader) · [视觉分拣系统](https://github.com/zjw-000/embedded-button-defect-detection-system)

</div>

---

## About Me

- 💻 **开发方向**：STM32 底层软件、FreeRTOS 多任务、电机闭环控制、Bootloader 与串口 IAP（应用内固件升级）。
- 🔧 **核心项目**：基于 STM32F103C8T6 + FreeRTOS 的智能烟机主控，覆盖传感器采集、运行模式控制、串口升级与故障恢复。
- 👁️ **拓展实践**：K210 视觉检测、STM32F407 分拣执行、ESP8266 / MQTT 数据通信与 Android 端配套工程。
- 🧩 **工程关注**：任务与中断协作、共享资源互斥、数据有效期、升级状态一致性，以及异常路径的可验证性。

## Technical Skills

以下内容以当前公开项目为依据，可通过代码入口查看实现。

| 方向 | 项目中的技术实践 | 代码入口 |
| :--- | :--- | :--- |
| C & MCU | C、STM32F103 / F407、标准外设库、GPIO、ADC、Timer/PWM、编码器、USART、SPI、Flash | [烟机 BSP](https://github.com/zjw-000/stm32-freertos-hood-controller/tree/master/BSP) |
| FreeRTOS | 任务划分与优先级、互斥量、二值信号量、中断到任务同步、状态快照、堆栈监测与故障钩子 | [任务实现](https://github.com/zjw-000/stm32-freertos-hood-controller/blob/master/APP_TASK/app_tasks.c) |
| Motor Control | 编码器测速、位置式 PID、积分与输出限幅、PWM 调速、模式切换与控制状态复位 | [电机驱动](https://github.com/zjw-000/stm32-freertos-hood-controller/blob/master/BSP/MOTOR/motor.c) · [PID](https://github.com/zjw-000/stm32-freertos-hood-controller/blob/master/BSP/PID/pid.c) |
| Sensors & Concurrency | DHT11、MQ2 / ADC、数据有效期与故障隔离、LCD 显示、LCD / W25Q64 共用 SPI 总线互斥 | [传感器与控制任务](https://github.com/zjw-000/stm32-freertos-hood-controller/blob/master/APP_TASK/app_tasks.c) · [SPI 总线](https://github.com/zjw-000/stm32-freertos-hood-controller/blob/master/BSP/SPI/SPI.c) |
| DMA & Protocol | USART IDLE + DMA 半传输/传输完成中断、循环 DMA、软件环形缓冲、流式拆包、CRC32 与超时重试 | [接收通道](https://github.com/zjw-000/stm32-freertos-hood-controller/blob/master/BSP/DMA/dma.c) · [流解析器](https://github.com/zjw-000/stm32-freertos-hood-controller/blob/master/Shared/iap_stream.h) |
| Bootloader & IAP | APP / Bootloader 分区、W25Q64 暂存、A/B 元数据、试运行确认、备份回滚、黄金镜像恢复、HMAC-SHA256 镜像认证 | [升级状态机](https://github.com/zjw-000/stm32-freertos-hood-controller/blob/master/Shared/boot_flow.h) · [镜像认证](https://github.com/zjw-000/stm32-freertos-hood-controller/blob/master/Shared/boot_auth.h) |
| Reliability & Testing | 任务心跳看门狗、升级进度监督、主机端 C 回归测试、模拟断电注入、Python 固件发送与结果查询 | [主机测试](https://github.com/zjw-000/stm32-freertos-hood-controller/tree/master/tools/host_tests) · [升级工具](https://github.com/zjw-000/stm32-freertos-hood-controller/blob/master/tools/send_firmware.py) |
| Edge AI & IoT | MaixPy / Python、K210 KPU / YOLOv2、Arduino C++、ESP8266 Wi-Fi、MQTT / PubSubClient | [视觉识别](https://github.com/zjw-000/embedded-button-defect-detection-system/tree/main/K210) · [MQTT 固件](https://github.com/zjw-000/embedded-button-defect-detection-system/tree/main/8266) |

## Featured Projects

### 01 · [智能烟机嵌入式主控系统](https://github.com/zjw-000/stm32-freertos-hood-controller)

**核心项目｜STM32F103C8T6 · FreeRTOS · PID · DMA · Bootloader / IAP · W25Q64**

围绕烟机的待机、手动、自动和防回流模式，组织实时控制、传感器处理、显示交互与固件升级，重点展示 MCU 底层开发和系统可靠性设计。

```text
按键 / DHT11 / MQ2 → FreeRTOS 采集与模式管理 → 电机控制任务 → PWM / 电机
编码器 ───────────→ 定时测速 + 信号量 ───────→ PID 转速反馈
共享状态 ─────────→ 互斥保护 / 快照 ────────→ LCD 显示

Python 上位机 → USART + 循环 DMA → 环形缓冲 / 流式协议 → W25Q64 下载区
                                                        ↓
                   Bootloader：认证 → 备份 → 安装 → APP 试运行确认
                                      失败 → 上一稳定版 / 黄金镜像恢复
```

- **RTOS 任务协作**：按键、采集、测速、电机、显示、升级与看门狗分工；定时中断通过信号量通知测速任务，共享状态采用互斥保护，外设等待移出状态锁。
- **电机与传感器控制**：手动及防回流模式采用编码器反馈 + PID；自动模式根据温湿度、气体数据融合调节 PWM，包含数据过期停机、迟滞判断和模式状态复位。
- **串口流式接收**：IDLE 与 DMA 半传输/传输完成中断共同搬运接收数据，环形缓冲衔接任务解析，处理半包、粘包、坏帧重同步及重传。
- **升级与恢复**：片内 8KB Bootloader + 56KB APP；片外 Flash 保存下载镜像、稳定版备份与黄金镜像，通过 A/B 元数据记录阶段，支持试运行确认与失败回滚。
- **运行监督**：独立看门狗检查任务心跳和升级进度；升级期间立即停机，健康观察通过后确认新固件，提供堆与任务栈水位观测入口。

**验证记录（仓库文档）**：控制逻辑覆盖 7 组主机回归测试；升级链路覆盖 346 个模拟断电检查点，以及认证、协议解析和 ACK 丢失重试。真实硬件时序、电机响应与断电恢复仍需实板验证，详见[控制验证记录](https://github.com/zjw-000/stm32-freertos-hood-controller/blob/master/docs/plans/05_运行控制四项修复.md)和[升级验证记录](https://github.com/zjw-000/stm32-freertos-hood-controller/blob/master/docs/plans/04_升级可靠性整改.md)。

> 当前升级通道为串口 IAP；认证使用可替换的开发密钥，尚未建立硬件信任根。恢复镜像均不可用时停留在 Bootloader，需通过 SWD 检修。

**源码阅读路径**：[任务与控制](https://github.com/zjw-000/stm32-freertos-hood-controller/blob/master/APP_TASK/app_tasks.c) → [DMA 接收](https://github.com/zjw-000/stm32-freertos-hood-controller/blob/master/BSP/DMA/dma.c) → [IAP 服务](https://github.com/zjw-000/stm32-freertos-hood-controller/blob/master/Shared/iap_service.h) → [启动与回滚](https://github.com/zjw-000/stm32-freertos-hood-controller/blob/master/Shared/boot_flow.h) → [回归测试](https://github.com/zjw-000/stm32-freertos-hood-controller/tree/master/tools/host_tests)。

---

### 02 · [嵌入式纽扣缺陷检测与智能分拣系统](https://github.com/zjw-000/embedded-button-defect-detection-system)

**拓展项目｜K210 · STM32F407 · ESP8266 · MQTT · Android**

围绕“识别 → 分拣 → 数据上报 → 移动端应用”组织的嵌入式系统项目，包含视觉脚本、主控固件、网络固件和 App Inventor 工程。

```text
摄像头 → K210 / YOLOv2
            ├─ GPIO 控制信号 → STM32F407 → 电机 / 气泵执行机构
            └─ UART 检测数据 → ESP8266 → MQTT Broker

Android 端：App Inventor 工程与安装包见 app/ 目录
```

- **视觉感知**：摄像头采集、KPU 模型推理、检测框与类别显示。
- **执行与通信**：STM32 GPIO 控制电机与气泵，ESP8266 接收串口统计并通过 MQTT 发布数据、订阅消息。
- **应用配套**：提供 App Inventor 源工程与 Android 安装包。

**阅读路径**：先看 [系统说明](https://github.com/zjw-000/embedded-button-defect-detection-system#readme)，再看 [STM32 主循环](https://github.com/zjw-000/embedded-button-defect-detection-system/blob/main/stm32/MY/main.c)、[K210 检测与上报](https://github.com/zjw-000/embedded-button-defect-detection-system/blob/main/K210/main1.py) 和 [ESP8266 MQTT 固件](https://github.com/zjw-000/embedded-button-defect-detection-system/blob/main/8266/K210_8266_MQTT_bishe/K210_8266_MQTT_bishe.ino)。

## Development Principles

以可检查的实现和清晰的边界展示工程能力：

- **从接口出发**：明确引脚、信号方向、串口参数和消息格式。
- **按模块组织**：区分外设驱动、控制逻辑、视觉推理与网络通信。
- **覆盖异常路径**：关注共享状态一致性、传感器失效、通信超时、升级中断和恢复失败。
- **让描述对应代码**：说明当前实现，区分已有功能与后续扩展。
- **以验证支撑结论**：性能、稳定性和识别效果需要相应的测试条件与记录。

---

<div align="center">

**从外设到应用，把每一层连接起来。**

</div>
