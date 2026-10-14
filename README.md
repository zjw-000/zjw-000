<div align="center">

# Hi, I'm zjw-000 👋

### Embedded Software · Edge AI · IoT

嵌入式软件开发方向｜以 MCU 控制为基础，连接边缘视觉与物联网应用

[代表项目](https://github.com/zjw-000/embedded-button-defect-detection-system) · [STM32 源码](https://github.com/zjw-000/embedded-button-defect-detection-system/tree/main/stm32) · [K210 视觉](https://github.com/zjw-000/embedded-button-defect-detection-system/tree/main/K210) · [MQTT 通信](https://github.com/zjw-000/embedded-button-defect-detection-system/tree/main/8266)

</div>

---

## About Me

- 💻 **开发方向**：嵌入式软件、MCU 外设与控制、边缘视觉应用、物联网设备通信。
- 🔧 **项目实践**：围绕纽扣缺陷检测与分拣，组织 K210 视觉识别、STM32F407 执行控制、ESP8266 数据上报与 Android 端工程。
- 🧩 **展示重点**：从外设配置、设备间通信到应用集成，让每项技术都能对应到具体源码。

## Technical Skills

以下内容以当前公开项目为依据，可通过代码入口查看实现。

| 方向 | 项目中的技术实践 | 代码入口 |
| :--- | :--- | :--- |
| Programming | C、Arduino C++、MaixPy / Python | [STM32](https://github.com/zjw-000/embedded-button-defect-detection-system/tree/main/stm32) · [ESP8266](https://github.com/zjw-000/embedded-button-defect-detection-system/tree/main/8266) · [K210](https://github.com/zjw-000/embedded-button-defect-detection-system/tree/main/K210) |
| MCU & Control | STM32F407、标准外设库、GPIO 输入输出、执行机构控制；仓库包含 Timer/PWM 与 USART 驱动模块 | [主循环](https://github.com/zjw-000/embedded-button-defect-detection-system/blob/main/stm32/MY/main.c) · [外设模块](https://github.com/zjw-000/embedded-button-defect-detection-system/tree/main/stm32/Drive/Source) |
| Edge AI | K210 KPU、YOLOv2 模型加载与推理、摄像头采集、LCD 结果显示、分类计数 | [视觉识别脚本](https://github.com/zjw-000/embedded-button-defect-detection-system/blob/main/K210/main1.py) |
| Communication | UART 数据传输、ESP8266 Wi-Fi、MQTT 发布/订阅、PubSubClient | [通信固件](https://github.com/zjw-000/embedded-button-defect-detection-system/blob/main/8266/K210_8266_MQTT_bishe/K210_8266_MQTT_bishe.ino) |
| Tools & Integration | Keil MDK、Arduino、App Inventor；MCU、视觉模块与网络模块的工程组织 | [Keil 工程](https://github.com/zjw-000/embedded-button-defect-detection-system/blob/main/stm32/Project/STM32F407.uvprojx) · [Android 端工程](https://github.com/zjw-000/embedded-button-defect-detection-system/tree/main/app) |

## Featured Repository

### [嵌入式纽扣缺陷检测与智能分拣系统](https://github.com/zjw-000/embedded-button-defect-detection-system)

**K210 + STM32F407 + ESP8266 + Android**

围绕“识别 → 分拣 → 数据上报 → 移动端应用”组织的嵌入式系统项目，包含视觉脚本、主控固件、网络固件和 App Inventor 工程。

```text
摄像头 → K210 / YOLOv2
            ├─ GPIO 控制信号 → STM32F407 → 电机 / 气泵执行机构
            └─ UART 检测数据 → ESP8266 → MQTT Broker

Android 端：App Inventor 工程与安装包见 app/ 目录
```

| 模块 | 实现内容 | 展示能力 |
| :--- | :--- | :--- |
| 视觉感知 | 摄像头采集、KPU 模型推理、检测框与类别显示 | 边缘视觉模型的应用集成 |
| 执行控制 | 读取 GPIO 控制信号，驱动电机与气泵对应输出 | MCU 外设配置与硬件控制逻辑 |
| 网络通信 | 串口接收检测统计，通过 MQTT 发布数据并订阅消息 | 设备数据传输与物联网通信 |
| 应用配套 | 提供 App Inventor 源工程与 Android 安装包 | 移动端配套与多模块工程组织 |

**阅读路径**：先看 [系统说明](https://github.com/zjw-000/embedded-button-defect-detection-system#readme)，再看 [STM32 主循环](https://github.com/zjw-000/embedded-button-defect-detection-system/blob/main/stm32/MY/main.c)、[K210 检测与上报](https://github.com/zjw-000/embedded-button-defect-detection-system/blob/main/K210/main1.py) 和 [ESP8266 MQTT 固件](https://github.com/zjw-000/embedded-button-defect-detection-system/blob/main/8266/K210_8266_MQTT_bishe/K210_8266_MQTT_bishe.ino)。

## Development Principles

以可检查的实现和清晰的边界展示工程能力：

- **从接口出发**：明确引脚、信号方向、串口参数和消息格式。
- **按模块组织**：区分外设驱动、控制逻辑、视觉推理与网络通信。
- **让描述对应代码**：说明当前实现，区分已有功能与后续扩展。
- **以验证支撑结论**：性能、稳定性和识别效果需要相应的测试条件与记录。

---

<div align="center">

**从外设到应用，把每一层连接起来。**

</div>
