# CanTrcv1145 配置项参考文档

|容器属性|值（容器）|
|---|---|
|名称|CanTrcv1145|
|描述|CAN Transceiver Driver. Handles the CAN transceivers on an ECU. Upper layer is CanIf.\#CAN \#ISO11898 \#TRANSCEIVER \#Driver \#AUTOSAR|
|描述|概述：CanTrcv1145配置项用于定义CAN收发器的特定属性，如唤醒和睡眠模式的管理，确保CAN网络的通信效率和节能要求得到满足。|
|描述|注意：在AUTOSAR CP 4.4标准中，确保配置项与硬件支持的特性相匹配；适当配置唤醒和睡眠模式以优化能耗；此配置项的具体属性可能因不同硬件供应商而异，需仔细核对硬件手册。|
|CATEGORY|VENDOR_SPECIFIC_MODULE_DEFINITION|
|多实例个数|0 - 1|
|REFINED-MODULE-DEF-REF|/AUTOSAR/EcucDefs/CanTrcv1145|

## 1. CanTrcvConfigSet

|容器属性|值（容器）|
|---|---|
|名称|CanTrcvConfigSet|
|描述|This is the multiple configuration set container for CAN transceiver driver.|
|描述|概述：CanTrcvConfigSet 是一个配置集，它包含了CAN收发器模块（CAN Transceiver）的所有配置参数，用于定义CAN收发器的工作属性和行为。|
|描述|注意：在配置CanTrcvConfigSet时，需要确保所有参数与硬件特性相匹配，以避免通信问题；此外，应当注意配置集的一致性，确保在不同的ECU上，相同的配置集能够产生相同的行为；在AUTOSAR CP 4.4标准中，应当遵循其定义的模块配置参数，以确保兼容性和标准化。|
|多实例个数|1 - 1|
|POST-BUILD-CHANGEABLE|false|
|MULTIPLE-CONFIGURATION-CONTAINER|false|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CanTrcvSPICommRetries|
|描述|Not used.This value specifies the maximum number of communication retries in case of a failed SPI communication (applies both to timed-out communication and to errors/NACK in the response data). (0 ... 255 times, 0 means no retry allowed, communication must succeed at first try)|
|描述|概述：CanTrcvSPICommRetries 配置项用于定义尝试与CAN收发器通信的SPI重试次数，以确保在通信干扰或暂时性故障的情况下能够成功与CAN收发器建立通信。|
|描述|注意：在设置此配置项时，应考虑系统的容错需求和响应时间要求；重试次数不宜过高，以避免不必要的延迟；此配置项的值应与CAN收发器的特性和系统的实际环境相匹配。|
|描述|该配置项未使用|
|多实例个数|0 - 1|
|默认值|0|
|取值范围|0 - 255|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CanTrcvSPICommTimeout|
|描述|Not used.This value specifies the maximum time allowed to the CanTrcv for replying (either positively or negatively) to a SPI command. (value in ms, 0ms means no specific timeout is to be used, communication is executed at the best of the SPI HW capacity)|
|描述|概述：CanTrcvSPICommTimeout 配置项用于定义CAN收发器与SPI通信的最大超时时间，确保通信的可靠性和及时性。|
|描述|注意：超时时间应根据系统的实际需求和性能进行配置；过短的超时时间可能导致通信失败，过长的超时时间可能影响系统响应；在AUTOSAR CP 4.4中，确保该配置与CAN驱动和SPI驱动的兼容性。|
|描述|该配置项未使用|
|多实例个数|0 - 1|
|默认值|0|
|取值范围|0 - 100|

### 1.1. CanTrcvChannel

|容器属性|值（容器）|
|---|---|
|名称|CanTrcvChannel|
|描述|This container includes CAN transceiver driver information about a single CAN channel.|
|描述|概述：CanTrcvChannel 配置项用于定义CAN传输层的通道，它指定了CAN Transceiver模块与CAN控制器之间的连接关系。|
|描述|注意：在配置CanTrcvChannel时，需要确保通道的配置与实际硬件架构相匹配；每个CAN Transceiver必须映射到唯一的CAN控制器；在多通道CAN系统中，正确的通道映射对于网络管理和诊断通信至关重要。|
|多实例个数|1 - inf|
|POST-BUILD-CHANGEABLE|false|
|MULTIPLE-CONFIGURATION-CONTAINER|false|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CanTrcvChannelId|
|描述|This value is an unique identifier of the CAN transceiver channel.|
|描述|概述：CanTrcvChannelId是用于标识CAN传输层通道的唯一标识符，确保CAN通信中每个通道的数据传输和接收能够正确地被区分和管理。|
|描述|注意：在配置CanTrcvChannelId时，必须确保其在整个项目中的唯一性；该标识符通常与物理硬件通道对应，因此在配置时应参考硬件设计文档；在AUTOSAR CP 4.4标准中，对CanTrcvChannelId的具体数值范围或格式没有特殊要求，但应遵循项目内部的命名和编号规范。|
|多实例个数|1 - 1|
|默认值|0|
|取值范围|0 - 255|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|CanTrcvChannelUsed|
|描述|This parameter defines if this CAN transceiver channel is used.|
|描述|概述：CanTrcvChannelUsed配置项用于指定是否使用CAN传输层通道，它决定了相关的CAN通道是否被激活并参与通信。|
|描述|注意：在配置时需确保所指定的通道与实际硬件资源相匹配；若设置为不使用，相关的通信功能将被禁用，可能影响系统的通信需求；AUTOSAR CP 4.4标准要求明确每个通道的使用情况，以便于系统资源的合理分配和管理。|
|多实例个数|1 - 1|
|默认值|true|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|CanTrcvControlsPowerSupply|
|描述|This parameter defines if the ECU power supply is controlled by this transceiver.TRUE = Controlled by transceiver.FALSE = Not controlled by transceiver.|
|描述|概述：CanTrcvControlsPowerSupply配置项用于指定CAN收发器是否具有控制ECU电源供应的能力，这对于节能和唤醒网络的功能特别重要。|
|描述|注意：在设计系统时，需要考虑该配置项对于电源管理策略的影响；如果CAN收发器不支持电源控制功能，该配置项应设置为false；AUTOSAR CP 4.4标准中对于电源管理有详细规定，确保配置与标准一致。|
|描述|该配置项未使用|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|CanTrcvHwPnSupport|
|描述|This parameter defines whether the CAN transceiver supports the selective wake-up function.TRUE = Selective wakeup feature is supported by the transceiver.FALSE = Selective wakeup functionality is not supported by the transceiver.|
|描述|概述：CanTrcvHwPnSupport 是一个配置项，用于指定CAN收发器硬件是否支持部分网络功能（Partial Networking），这是一种节能功能，允许在网络上只唤醒部分节点而不是整个网络。|
|描述|注意：在配置CanTrcvHwPnSupport时，需要确保硬件实际支持部分网络功能；如果硬件不支持，但软件配置错误地启用了该功能，可能会导致网络通信问题；AUTOSAR CP 4.4标准中，该配置项应与硬件规范和网络管理需求相匹配。|
|多实例个数|1 - 1|
|默认值|true|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|CanTrcvInitState|
|描述|Not used.The CanTrcv is always initialized to mode NORMAL.This parameter defines the state of the CAN transceiver after a call of CanTrcv_Init.|
|描述|概述：CanTrcvInitState 配置项用于定义CAN收发器（CAN transceiver）在系统启动时的初始状态，通常是指定为在线或离线状态。|
|描述|注意：在配置CanTrcvInitState时，需要确保它与系统的电源管理策略一致；此外，该配置项的设置应考虑到网络唤醒和诊断需求；在AUTOSAR CP 4.4标准中，应检查该配置项是否支持所有的CAN收发器模式，以确保与标准的兼容性。|
|多实例个数|1 - 1|
|默认值|CANTRCV_OP_MODE_NORMAL|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CanTrcvMaxBaudrate|
|描述|This value specifies the maximum baudrate for transceiver hardware type. The parameter is only used for validation purposes. Value shall be configured by configuration tool based on transceiver hardware type.|
|描述|概述：CanTrcvMaxBaudrate 配置项用于指定CAN收发器（CAN transceiver）支持的最大波特率，这是通信速率的一个重要参数，影响网络的数据传输效率。|
|描述|注意：在配置CanTrcvMaxBaudrate时，需要确保该值与实际硬件支持的最大波特率相匹配；超出硬件能力范围的配置可能导致通信故障；在AUTOSAR CP 4.4标准中，应当检查该配置项是否与ECU支持的CAN控制器和网络拓扑兼容。|
|多实例个数|1 - 1|
|默认值|1000|
|取值范围|0 - 1000|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|CanTrcvWakeupByBusUsed|
|描述|Defines if wake up by bus is used.|
|描述|概述：CanTrcvWakeupByBusUsed 是一个配置项，用于指示是否启用了通过CAN总线唤醒的功能，这对于实现低功耗模式下的网络管理非常关键。|
|描述|注意：在设计系统时，需要确保硬件支持通过CAN总线唤醒的功能；此配置项应与ECU的低功耗需求和唤醒策略相匹配；AUTOSAR CP 4.4标准中对此功能有明确的支持，但实现时需遵循具体的微控制器和CAN收发器的能力。|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|CanTrcvEnablePNMD|
|描述|True: PNDM in Frame Control register|
|描述|概述：CanTrcvEnablePNMD 是一个配置项，用于启用或禁用部分网络管理功能（Partial Networking Management）在CAN收发器（CAN transceiver）中的支持。|
|描述|注意：在使用该配置项时，需要确保CAN收发器硬件支持部分网络管理功能；此外，该配置项应与网络管理软件模块的要求保持一致；在配置过程中，还需注意与其他网络参与者的兼容性和网络管理策略的一致性。|
|多实例个数|1 - 1|
|默认值|true|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|CanTrcvFdTolerance|
|描述|This parameter defines whether the CanTrcv shall ignore CAN FD Frames or not.TRUE: the CanTrcv is in a FD passive mode and remains in STANDBY/SLEEP mode when CAN FD frames are recieved. CAN FD frames are never recognized as valid wakeup-frames, even if the frame contains a matching ID. After the CanTrcv receives the control field of a CAN FD frame, the CanTrcv ignores further signals until idle is detected again.FALSE: CAN FD frames are intepreted as frames with errors. When the CanTrcv is in STANDBY/SLEEP mode, every time the CanTrcv receives a CAN FD frame the error counter is incremented. If the ratio of CAN FD frames to valid CAN frames exceeds the threshhold that triggers error counter overflow the CanTrcv wakes up.RESTRICTIONS: TRUE is allowed only if the underlying CAN transceiver hardware supports FD-passive mode (such as TJA1145FD).|
|描述|概述：CanTrcvFdTolerance配置项定义了CAN收发器在CAN FD（Flexible Data-rate）模式下的容忍度，这通常涉及到时间同步和数据传输的稳定性。|
|描述|注意：在配置CanTrcvFdTolerance时，需要确保值符合CAN FD收发器的硬件规格和网络设计要求；此外，该配置项的设置必须与网络上其他节点的容忍度设置保持一致，以确保网络同步；在AUTOSAR CP 4.4标准中，如果该属性与硬件不兼容或者与网络设计不一致，可能会导致通信问题。|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|CanTrcvWakeupSourceRef|
|描述|Reference to a wakeup source in the EcuM configuration. This reference is only needed if CanTrcvWakeupByBusUsed is true.|
|描述|概述：CanTrcvWakeupSourceRef 配置项用于将CAN收发器（Transceiver）的唤醒源与ECU唤醒源进行关联，确保在CAN网络上的唤醒事件能够被系统正确识别和处理。|
|描述|注意：在配置时需确保唤醒源的引用正确指向有效的ECU唤醒源对象；如果系统中存在多个CAN收发器，每个收发器的唤醒源应当被唯一标识和配置；AUTOSAR CP 4.4标准中，唤醒源的配置应当与PNC（Partial Network Cluster）或ECU唤醒源的定义相一致。|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/EcuM/EcuMConfiguration/EcuMCommonConfiguration/EcuMWakeupSource|

#### 1.1.1. CanTrcvAccess

|容器属性|值（容器）|
|---|---|
|名称|CanTrcvAccess|
|描述|This container gives CAN transceiver driver information about access to a single CAN transceiver.|
|描述|概述：CanTrcvAccess 配置项定义了对CAN收发器（CAN transceiver）硬件访问的参数，包括硬件寄存器的地址和访问方法，以便于软件层能够控制CAN收发器的状态。|
|描述|注意：在配置CanTrcvAccess时，需要确保硬件寄存器地址和访问方法与实际的硬件手册和CAN收发器规格一致；此外，应当遵循AUTOSAR CP 4.4标准中对于CAN收发器访问的规定，以保证软件的可移植性和兼容性；在多个ECU共用同一CAN收发器的情况下，还需要考虑访问同步和冲突避免的机制。|
|多实例个数|1 - 1|
|POST-BUILD-CHANGEABLE|false|

##### 1.1.1.1. CanTrcvDioAccess

|容器属性|值（容器）|
|---|---|
|名称|CanTrcvDioAccess|
|描述|This container includes the CAN transceiver driver information about accessing ports and port pins. In addition relation between CAN transceiver hardware pin names and Dio port access information is given. If a CAN transceiver hardware has no Dio interface, there is no instance of this container.|
|描述|概述：CanTrcvDioAccess 配置项用于定义CAN收发器的DIO（Direct Input/Output）访问属性，允许通过DIO接口控制CAN收发器的唤醒和睡眠状态。|
|描述|注意：在使用DIO访问CAN收发器时，需要确保硬件支持此功能，并且DIO端口已经正确配置；此配置项的使用应与CAN收发器的硬件手册和微控制器的DIO配置相匹配；在AUTOSAR CP 4.4标准中，应当遵循相关模块的配置规范，确保配置的一致性和正确性。|
|描述|该配置项未使用|
|多实例个数|0 - 1|
|POST-BUILD-CHANGEABLE|false|
|MULTIPLE-CONFIGURATION-CONTAINER|false|

###### 1.1.1.1.1. CanTrcvDioChannelAccess

|容器属性|值（容器）|
|---|---|
|名称|CanTrcvDioChannelAccess|
|描述|This container includes the DIO channel access by single CAN transceiver channel.|
|描述|概述：CanTrcvDioChannelAccess 配置项用于定义CAN收发器的DIO（直接I/O）通道访问属性，它允许通过DIO接口控制CAN收发器的使能和禁用状态。|
|描述|注意：在使用DIO通道控制CAN收发器时，需要确保DIO通道与CAN收发器硬件连接正确；此配置项的使用取决于硬件设计和CAN收发器是否支持DIO控制；在配置时，应参照具体的硬件手册和CAN收发器规格，确保配置的正确性和一致性。|
|描述|该配置项未使用|
|多实例个数|1 - inf|
|POST-BUILD-CHANGEABLE|false|
|MULTIPLE-CONFIGURATION-CONTAINER|false|

|配置项属性|值（字符串参数配置项）|
|---|---|
|名称|CanTrcvHardwareInterfaceName|
|描述|This parameter defines the CAN transceiver hardware interface name. It is typically the name of a pin.|
|描述|概述：CanTrcvHardwareInterfaceName 配置项用于指定CAN收发器硬件接口的名称，这有助于软件组件与特定的硬件接口进行关联。|
|描述|注意：在配置时需确保名称的唯一性和正确性，以匹配实际硬件；名称应与ECU中实际的CAN收发器硬件接口相对应；在整个项目中保持一致性，避免在不同的模块或组件中出现混淆。|
|描述|该配置项未使用|
|多实例个数|1 - 1|
|配置项属性|值（选择引用配置项）|
|---|---|
|名称|CanTrcvDioSymNameRef|
|描述|Choice Reference to a DIO Port, DIO Channel or DIO Channel Group.|
|多实例个数|1 - 1|
|目标引用|/AUTOSAR/EcucDefs/Dio/DioConfig/DioPort/DioChannel/AUTOSAR/EcucDefs/Dio/DioConfig/DioPort/DioChannelGroup/AUTOSAR/EcucDefs/Dio/DioConfig/DioPort|

##### 1.1.1.2. CanTrcvSpiSequence

|容器属性|值（容器）|
|---|---|
|名称|CanTrcvSpiSequence|
|描述|This container includes the CAN transceiver driver information about one SPI sequence. One SPI sequence used by CAN transceiver driver is in exclusive use for it. No other driver is allowed to access this sequence. CAN transceiver driver may use one sequence to access n CAN transceiver hardwares chips of the same type or n sequences are used to access one single CAN transceiver hardware chip. If a CAN transceiver hardware has no SPI interface, there is no instance of this container.|
|描述|概述：CanTrcvSpiSequence 配置项用于定义CAN收发器（Transceiver）与SPI（Serial Peripheral Interface）之间通信时所使用的序列，确保CAN收发器的正确初始化和操作。|
|描述|注意：在配置CanTrcvSpiSequence时，需要确保序列与硬件支持的SPI命令相匹配；此外，序列的配置应与CAN收发器的数据手册和初始化流程保持一致；在AUTOSAR CP 4.4标准中，如果该配置项的属性或者使用方式与标准不一致，需要检查并调整以符合标准规范。|
|多实例个数|0 - 1|
|POST-BUILD-CHANGEABLE|false|
|MULTIPLE-CONFIGURATION-CONTAINER|false|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|CanTrcvSpiAccessSynchronous|
|描述|This parameter is used to define whether the access to the Spi sequence is synchronous or asynchronous. true: SPI access is synchronous. false: SPI access is asynchronous.|
|描述|概述：CanTrcvSpiAccessSynchronous 配置项用于定义CAN收发器通过SPI接口的访问方式是否为同步。|
|描述|注意：在AUTOSAR CP 4.4中，异步SPI通信可能需要额外的配置和管理，因此确认硬件和驱动支持同步操作是必要的；同步访问通常意味着在SPI操作完成前，系统会阻塞其他操作，这可能影响系统性能；确保系统设计时考虑了这种阻塞的影响。|
|描述|该配置项未使用|
|多实例个数|0 - 1|
|默认值|false|

###### 1.1.1.2.1. CanTrcvSpiSequenceAccess

|容器属性|值（容器）|
|---|---|
|名称|CanTrcvSpiSequenceAccess|
|多实例个数|1 - inf|
|POST-BUILD-CHANGEABLE|false|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|CanTrcvSpiAccessSynchronous|
|描述|This parameter is used to define whether the access to the Spi sequence is synchronous or asynchronous.|
|多实例个数|0 - 1|
|默认值|false|

|配置项属性|值（字符串参数配置项）|
|---|---|
|名称|CanTrcvSpiSequenceIdentifier|
|描述|Specifies the name of the SPI sequence as used within the CanTrcv driver.|
|描述|概述：CanTrcvSpiSequenceAccess 配置项用于定义CAN收发器通过SPI接口进行通信时所使用的SPI序列，确保CAN收发器的正确初始化和操作。|
|描述|注意：在配置CanTrcvSpiSequenceAccess时，需要确保所选的SPI序列与实际的硬件连接和SPI驱动配置相匹配；此外，应当检查该SPI序列是否支持所需的所有操作，例如唤醒和休眠；在多个CAN收发器共享同一SPI接口的情况下，还需考虑SPI序列的共享和冲突管理。|
|多实例个数|1 - 1|

##### 1.1.1.3. CanTrcvSbcAccess

|容器属性|值（容器）|
|---|---|
|名称|CanTrcvSbcAccess|
|多实例个数|0 - 1|
|POST-BUILD-CHANGEABLE|false|

|配置项属性|值（选择引用配置项）|
|---|---|
|名称|CanTrcvSbcPeripheralIdRef|
|描述|Reference to the SBC peripheral that is being used by this CanTrcv channel.|
|多实例个数|1 - 1|
|目标引用|/AUTOSAR/Sbc/Sbc/SbcDevice/SbcCanTrcvPeripheral|

#### 1.1.2. CanTrcvPartialNetwork

|容器属性|值（容器）|
|---|---|
|名称|CanTrcvPartialNetwork|
|描述|This container includes the CAN transceiver driver information about the configuration of Partial Networking functionality.|
|描述|概述：CanTrcvSpiSequenceIdentifier 是用于标识CAN收发器（Transceiver）与SPI（串行外设接口）之间通信序列的唯一标识符，它确保了在配置SPI通信时，每个CAN收发器的通信序列可以被正确地识别和使用。|
|描述|注意：在配置CanTrcvSpiSequenceIdentifier时，必须确保它在整个项目中是唯一的，以避免在SPI通信中的任何冲突；该标识符通常由系统集成者或配置工具分配，以确保其唯一性和一致性；在AUTOSAR CP 4.4标准中，应检查该配置项是否与标准中定义的属性和参数相匹配，以确保兼容性。|
|多实例个数|0 - 1|
|POST-BUILD-CHANGEABLE|false|
|MULTIPLE-CONFIGURATION-CONTAINER|false|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CanTrcvBaudRate|
|描述|This value specifies the CAN Bus communication baud rate in kbps.|
|描述|概述：CanTrcvBaudRate 配置项用于定义CAN收发器（CAN transceiver）的波特率，这是通信速率的一个参数，决定了CAN网络中数据传输的速度。|
|描述|注意：在配置CanTrcvBaudRate时，必须确保波特率与网络中其他节点的波特率一致，以保证网络的正常通信；波特率的选择应考虑网络的长度和所需的数据吞吐量；在AUTOSAR CP 4.4标准中，波特率的配置应与ECU支持的硬件能力相匹配。|
|多实例个数|1 - 1|
|默认值|500|
|取值范围|0 - 1000|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|CanTrcvBusErrFlag|
|描述|NOT supported.This parameter defines if the Bus Error (BUSERR) flag is managed by the BSW. The transceiver has to set this flag if it detects a bus error.TRUE = Supported by transceiver and managed by BSW.FALSE = Not managed by BSW.|
|描述|概述：CanTrcvSbcAccess 配置项用于定义CAN收发器与系统基础芯片（SBC）之间的接口访问方式，确保CAN通信模块能够正确控制CAN收发器的状态。|
|描述|注意：在配置CanTrcvSbcAccess时，需要确保所选接口与实际硬件架构相匹配；如果硬件设计中CAN收发器直接集成于SBC，则该配置项尤为重要；AUTOSAR CP 4.4标准中可能对接口访问方式有特定的要求或限制，需要根据标准文档进行配置。|
|描述|该配置项未使用|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|CanTrcvPnCanIdIsExtended|
|描述|This parameter defines whether extended or standard identifier is used for wake-up frames.TRUE = Extended CAN identifier is used.FALSE = Standard CAN identifier is used.|
|描述|概述：CanTrcvPartialNetwork 配置项用于定义CAN收发器（Transceiver）的局部网络功能，允许在特定条件下仅激活网络的一部分，以减少能耗。|
|描述|注意：确保该功能与车辆的休眠模式和唤醒策略相兼容；在配置时需遵循ECU的硬件支持和网络需求；AUTOSAR CP 4.4标准中对局部网络管理的实现细节有严格规定，需要仔细遵守。|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|CanTrcvPnEnabled|
|描述|This parameter defines whether the selective wake-up function is enabled or disabled in HW.TRUE = Selective wakeup feature is enabled in the transceiver hardware.FALSE = Selective wakeup feature is disabled in the transceiver hardware.HINT: Make sure that you enabled CanTrcvChannel\\CanTrcvWakeupByBusUsed at this channel, when you want to use Selective wakeup at this channel.|
|描述|概述：CanTrcvBusErrFlag 是一个配置项，用于启用或禁用CAN收发器的总线错误标志，该标志指示CAN总线的错误状态。|
|描述|注意：在配置CanTrcvBusErrFlag时，需要确保它与硬件支持的功能相匹配；如果硬件不支持总线错误监控，则不应启用此功能；在AUTOSAR CP 4.4标准中，应当遵循相关模块的配置参数规范来设置此项。|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CanTrcvPnFrameCanId|
|描述|This value specifies the CAN ID of the Wake-up Frame (WUF).|
|描述|概述：CanTrcvPnFrameCanId配置项用于定义参与部分网络（Partial Networking）唤醒功能的CAN传输器所需发送的帧的CAN标识符。|
|描述|注意：该配置项的值必须确保在网络中的唯一性，避免与其他帧的CAN ID冲突；在配置时需考虑网络中所有节点的PN功能和CAN ID分配策略；该配置项在AUTOSAR CP 4.4中应与网络管理需求和配置紧密相关，确保兼容性和网络唤醒功能的正确实现。|
|多实例个数|1 - 1|
|默认值|0|
|取值范围|0 - 4294967295|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CanTrcvPnFrameCanIdMask|
|描述|This value specifies the ID Mask for the selective activation of the transceiver. It is used to configure a Wake-up frame (WUF) which consists of a group of CAN identifiers.'1': don't care'0': must matchFor example: 'CanTrcvPnFrameCanId' = 0x100 and 'CanTrcvPnFrameCanIdMask' = 0xFFIn this case any CAN message with CAN identifier: 0x100 - 0x1FF will cause a wakeup.|
|描述|概述：CanTrcvPnFrameCanIdMask 用于定义接收到的部分网络唤醒帧的CAN标识符掩码，以便过滤和识别特定的唤醒帧。|
|描述|注意：确保掩码正确匹配所需的CAN ID范围；掩码设置错误可能导致无法正确识别唤醒帧；在配置时需考虑网络上所有可能的唤醒帧ID。|
|多实例个数|1 - 1|
|默认值|0|
|取值范围|0 - 4294967295|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CanTrcvPnFrameDlc|
|描述|This value specifies the data length of the Wake-up Frame (WUF).|
|描述|概述：CanTrcvPnFrameDlc配置项用于定义参与部分网络唤醒功能的CAN传输层帧的数据长度代码（DLC），确保唤醒帧的数据长度符合网络要求。|
|描述|注意：该配置项的值必须符合CAN网络对唤醒帧DLC的具体要求；在配置时需考虑网络的实际情况和其他节点的配置，以保证唤醒功能的正常工作；AUTOSAR CP 4.4标准中未对此配置项的具体取值范围做出限制，但实际应用中应参考具体的CAN网络标准和要求。|
|多实例个数|1 - 1|
|默认值|8|
|取值范围|0 - 8|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|CanTrcvPowerOnFlag|
|描述|This parameter defines if the Power On Reset (POR) flag is available and is managed by the transceiver.TRUE = Supported by Hardware.FALSE = Not supported by Hardware.|
|描述|概述：CanTrcvPnCanIdIsExtended 配置项用于指定部分网络管理器使用的唤醒帧的CAN标识符类型，确定其是否为扩展帧（29位标识符）。|
|描述|注意：在配置此项时，必须确保与实际网络上使用的唤醒帧标识符类型相匹配；如果网络上未使用扩展帧，则不应将此属性设置为true；此配置项的设置应与CanTrcvPnCanId配置项协同工作，确保唤醒帧的标识符和类型一致。|
|多实例个数|1 - 1|
|默认值|false|

##### 1.1.2.1. CanTrcvPnFrameDataMaskSpec

|容器属性|值（容器）|
|---|---|
|名称|CanTrcvPnFrameDataMaskSpec|
|描述|This container includes the data payload mask to be used on the received payload in order to determine if the transceiver must be woken up by the received Wake-up Frame (WUF).|
|描述|概述：CanTrcvPnFrameDataMaskSpec配置项用于定义在局部网络（Partial Networking）中，CAN收发器（Transceiver）对于唤醒帧数据的掩码规范，以便正确识别和处理唤醒帧。|
|描述|注意：该配置项对于实现局部网络唤醒功能至关重要，需要确保掩码正确匹配唤醒帧的数据格式；在配置时，应考虑所有可能的唤醒源，避免遗漏；AUTOSAR CP 4.4标准中对于局部网络的支持和配置要求可能与早期版本有所不同，需要仔细核对标准文档。|
|多实例个数|0 - 8|
|POST-BUILD-CHANGEABLE|true|
|MULTIPLE-CONFIGURATION-CONTAINER|false|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CanTrcvPnFrameDataMask|
|描述|This value specifies the n byte (Byte0 = LSB) of the data payload mask to be used on the received payload in order to determine if the transceiver must be woken up by the received Wake-up Frame (WUF).|
|描述|概述：CanTrcvPnFrameDataMask 配置项用于定义在局部网络（Partial Networking）中，CAN收发器（Transceiver）用来屏蔽接收到的唤醒帧数据字节的掩码，以确定是否应唤醒网络。|
|描述|注意：该掩码应与CanTrcvPnFrameDataByte配置项一起使用，以确保正确的唤醒逻辑；掩码的设置必须符合车辆网络唤醒策略的要求；在配置时应确保掩码值正确匹配所需的数据字节，避免错误的网络唤醒。|
|多实例个数|1 - 1|
|默认值|0|
|取值范围|0 - 255|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CanTrcvPnFrameDataMaskIndex|
|描述|This value specifies the position n in frame of the mask-part.|
|描述|概述：CanTrcvPnFrameDataMaskIndex用于定义在使用部分网络功能时，CAN收发器对接收到的帧数据进行掩码处理的索引值，以便于识别和处理特定的网络管理信息。|
|描述|注意：该配置项在使用部分网络（Partial Networking）功能时非常关键，需要确保正确配置以匹配网络管理器的要求；在不同的CAN收发器硬件中，对掩码处理的支持可能有所不同，需要参考硬件手册进行配置；AUTOSAR CP 4.4标准中对该配置项的具体要求可能与硬件实现细节有所差异，务必核对标准文档和硬件手册以确保兼容性。|
|多实例个数|1 - 1|
|默认值|0|
|取值范围|0 - 7|

### 1.2. CanTrcvDemEventParameterRefs

|容器属性|值（容器）|
|---|---|
|名称|CanTrcvDemEventParameterRefs|
|描述|This container contains the references to DemEventParameter elements which shall be invoked using the API Dem_ReportErrorStatus API in case the corresponding error occurs. The EventId is taken from the referenced DemEventParameter's DemEventId value. The standardized errors are provided in the container and can be extended by vendor specific error references.|
|描述|概述：CanTrcvDemEventParameterRefs配置项用于引用与CAN收发器相关的诊断事件参数，这些参数用于报告CAN收发器的故障和状态。|
|描述|注意：确保引用的诊断事件参数与实际的故障检测和报告机制相匹配；在配置时，需遵循AUTOSAR的诊断事件管理规范；若项目未使用诊断管理模块，则此配置项可能不适用。|
|描述|该配置项未使用|
|多实例个数|0 - 1|
|POST-BUILD-CHANGEABLE|false|

## 2. CanTrcvGeneral

|容器属性|值（容器）|
|---|---|
|名称|CanTrcvGeneral|
|描述|General configuration parameters of the CANTRCV.|
|描述|概述：CanTrcvGeneral 是一个配置容器，包含了用于CAN收发器驱动模块的通用配置参数，例如用于定义硬件相关的属性和CAN收发器的通用功能。|
|描述|注意：在配置CanTrcvGeneral时，需要确保所有的参数设置与硬件规格相匹配；此外，应当遵循AUTOSAR CP 4.4标准中对于CAN收发器模块的配置要求和限制；在多个CAN网络中使用时，每个网络的CanTrcvGeneral配置可能会有所不同，需要分别配置。|
|多实例个数|1 - 1|
|POST-BUILD-CHANGEABLE|false|
|MULTIPLE-CONFIGURATION-CONTAINER|false|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|CanTrcvDevErrorDetect|
|描述|This parameter switches the Development Error Detection and Notification ON or OFF.true: Development error detection is enabled.false: Development error detection is disabled.Note: In general, the development error detection is recommended during pre-test phase. It is not recommended to enable the development error detection in production code due to increased runtime and ROM consumption needs.|
|描述|概述：CanTrcvDevErrorDetect 是一个配置参数，用于启用或禁用CAN收发器（Transceiver）的开发错误检测功能，以便在开发和测试阶段识别潜在的错误。|
|描述|注意：在生产代码中通常禁用此功能以节省资源；确保在开发和测试阶段根据需要启用以便进行故障诊断；在AUTOSAR CP 4.4标准中，此配置应与系统和模块的诊断策略保持一致。|
|多实例个数|1 - 1|
|默认值|true|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|CanTrcvGetVersionInfo|
|描述|This parameter enables/disables the function CanTrcv_GetVersionInfo() to get major, minor and patch version information.|
|描述|概述：CanTrcvGetVersionInfo 是一个配置项，用于启用或禁用 CAN 收发器模块的版本信息API，该API允许用户获取模块的版本信息，包括主版本号、次版本号和补丁版本号。|
|描述|注意：在AUTOSAR CP 4.4标准中，如果启用了该配置项，必须实现相应的GetVersionInfo API；如果不需要版本信息，可以禁用以节省空间；确保在配置时遵循项目的规范和需求。|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CanTrcvSPICommRetries|
|描述|Not used.This value specifies the maximal number of communication retries in case of failed SPI communication (applies both to timed out communication and to errors/NACK in the response data).|
|多实例个数|0 - 1|
|默认值|0|
|取值范围|0 - 255|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CanTrcvSPICommTimeout|
|描述|Not used.This value specifies the maximal time allowed to the transceiver in order to reply (either positively or negatively) to a SPI command. (value in ms, 0ms means no specific timeout is to be used, communication is executed at the best of the SPI HW capacity)|
|多实例个数|0 - 1|
|默认值|0|
|取值范围|0 - 100|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CanTrcvWaitCount|
|描述|Not used.This value specifies the number of wait states to change the transceiver operation mode. Transceiver hardware may need wait states for some transitions. Please refer to the technical reference of this module.|
|描述|概述：CanTrcvWaitCount是用于定义在CAN收发器（Transceiver）从睡眠模式唤醒到正常模式转换过程中，软件需要等待的最大循环次数。|
|描述|注意：该参数的设置需要根据具体的CAN收发器硬件特性和系统的响应时间要求来确定；过小的值可能导致系统未能成功唤醒CAN收发器，而过大的值可能导致系统响应延迟；在AUTOSAR CP 4.4标准中，确保该配置项与硬件手册和系统性能要求相匹配。|
|描述|该配置项未使用|
|多实例个数|0 - 1|
|默认值|0|
|取值范围|0 - 4294967295|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|CanTrcvWakeUpSupport|
|描述|Defines whether wake up polling or not|
|描述|概述：CanTrcvWakeUpSupport 是一个配置项，用于指定CAN收发器是否支持唤醒功能，这决定了CAN网络节点是否能够在网络空闲时进入低功耗模式，并在检测到网络活动时唤醒。|
|描述|注意：在配置CanTrcvWakeUpSupport时，需要确保硬件支持唤醒功能；如果硬件不支持，该配置应设置为不支持以避免功能异常；此外，该配置项的设置应与整个系统的低功耗策略和唤醒逻辑相协调。|
|多实例个数|1 - 1|
|默认值|CANTRCV_WAKEUP_BY_POLLING|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CanTrcvIndex|
|描述|This value specifies the InstanceId of this module instance. If only one instance is present it shall have the Id 0.|
|描述|概述：CanTrcvIndex是用于标识特定CAN收发器（Transceiver）的索引，它在配置CAN通信堆栈时用于区分连接到同一CAN网络上的多个收发器。|
|描述|注意：在配置多个CAN收发器时，每个收发器的CanTrcvIndex必须是唯一的，以避免配置冲突；确保索引与实际硬件连接和软件驱动匹配，以保证通信的正确性；在AUTOSAR CP 4.4标准中，对CanTrcvIndex的具体数值范围没有特别限制，但应根据实际项目需求合理分配。|
|多实例个数|1 - 1|
|默认值|0|
|取值范围|0 - 255|

|配置项属性|值（浮点型参数配置项）|
|---|---|
|名称|CanTrcvMainFunctionPeriod|
|描述|This parameter specifies the period for cyclic call of CanTrcv_MainFunction. EcuC unit is seconds.|
|描述|概述：CanTrcvMainFunctionPeriod配置项定义了CAN收发器主函数的调用周期，即主函数被周期性调度执行的时间间隔，用于处理CAN收发器的状态和诊断信息。|
|描述|注意：该配置项的值应当与系统的实时性要求和CAN网络的通信需求相匹配；过短的周期可能导致CPU负载过高，而过长的周期可能影响通信效率和诊断能力；在AUTOSAR CP 4.4标准中，确保该配置项的设置符合ECU的实际硬件能力和网络需求。|
|多实例个数|1 - 1|
|默认值|0.01|
|取值范围|0.001 - 1|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CanTrcvWaitTime|
|描述|Wait time for transceiver state changes in micro-seconds.|
|描述|概述：CanTrcvWaitTime配置项定义了CAN收发器从睡眠状态唤醒到正常状态所需等待的时间，以确保CAN网络的稳定性和可靠性。|
|描述|注意：该配置项的时间单位和具体值需根据硬件手册和CAN网络的实际需求来设置；过长的等待时间可能会影响系统的响应速度，而过短的等待时间可能导致网络未能稳定即开始通信，引发错误。|
|多实例个数|0 - 1|
|默认值|0|
|取值范围|0 - 255|
