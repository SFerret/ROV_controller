# 基于全志H3的水下机器人控制系统

![flow_chart](/img/flow_chart.png)

系统框图如上：

在机器人运动控制上，本控制系统以基于全志H3的nanopi开发板为核心，驱动整体系统系统。全志H3负责驱动外设，与加速度计、深度传感器及声纳等设备进行通讯，实时解析水下机器人当前的姿态、位置等信息时，再结合姿态信息与上位机发送的控制指令驱动推进器（采用多路PWM拓展IC-PCA9685），实时控制ROV的运动。

在供能系统上，本系统将逻辑部分与功率部分隔离。由于长距离能源传输的需要，本系统采用310V高压从地面站将能源输送到ROV端。对于推进器、机械臂等高功率设备供能，采用了定制大功率小型开关电源（采用隔离拓扑，约720W），将310V转为24V，再根据需要构建Buck转为7.2V。这一路电源转为功率设备设计。而在逻辑控制部分供能，采用隔离式反激式降压，将310V转为12V输出。再由板上集成Buck电路转为5V/3.3V，供传感器、交换机，NanoPi等设备使用。两路电源相互隔离，避免功率设备的浪涌损坏逻辑部分电路。

通讯系统上，为保证系统的高可拓展性，控制系统基于全志H3与控制器，引出了多样的通讯接口。在以太网通讯上，系统基于瑞昱RTL8305构建交换机，拓展多路以太网接口，为机器人系统内网络摄像头、电力载波透传、NanoPi等多个设备相互通讯。同时基于wk2132的I2C转UART，MAX485串口转RS485。为多样的传感器外设接入提供可能。

系统构建与测试
