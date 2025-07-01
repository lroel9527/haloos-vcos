# Cdd 配置项参考文档

|容器属性|值（容器）|
|---|---|
|名称|Cdd|
|描述|The CDD module describes the minimal requirements that are necessary for the configuration of a CDD with respect to the surrounding standardized BSW modules.|
|描述|概述：Cdd（Complex Device Driver）模块是用于访问复杂外设的通用驱动程序，CDD模块虽然是属于AUTOSAR的一部分，但是该模块没有被AUTOSAR标准化。|
|描述|注意：Cdd需要遵循AUTOSAR的接口和模块规范来实现与AUTOSAR软件架构的兼容；在设计Cdd时，Cdd的开发和集成应遵循AUTOSAR的软件开发流程。|
|多实例个数|0 - 1|

## 1. CddComStackContribution

|容器属性|值（容器）|
|---|---|
|名称|CddComStackContribution|
|描述|Contribution of COM Stack modules.|
|描述|概述：CddComStackContribution配置项用于定义复杂设备驱动（Complex Device Driver, CDD）提供的服务和接口，以及它们与AUTOSAR通信栈的其他部分交互。|
|描述|注意：在配置CddComStackContribution时，需要确保CDD与通信栈其他模块的接口和服务定义清晰且一致；CDD应遵循AUTOSAR标准中定义的接口规范。|
|多实例个数|0 - 1|

### 1.1. CddComIfUpperLayerContribution

|容器属性|值（容器）|
|---|---|
|名称|CddComIfUpperLayerContribution|
|描述|Parameters that are necessary for the configuration of a Complex Driver that serves as the UpperLayer of the Com Interface module.|
|描述|概述：CddComIfUpperLayerContribution配置项用于定义复杂设备驱动（Complex Device Driver, CDD）与通信接口层（ComIf）之间的交互。|
|描述|注意：CDD的实现必须保证数据的一致性和同步；此配置项的使用应当与系统架构和通信需求紧密相关，确保正确集成CDD的功能。|
|多实例个数|0 - 1|

#### 1.1.1. CddComIfUpperLayerRxPdu

|容器属性|值（容器）|
|---|---|
|名称|CddComIfUpperLayerRxPdu|
|描述|This container specifies Rx PDUs that are exchanged between the CDD and the standardized BSW module.|
|描述|概述：CddComIfUpperLayerRxPdu 用于定义从通信驱动到上层模块的接收PDU（协议数据单元）的映射关系，确保数据能够正确地从底层传输到应用层。|
|描述|注意：确保PDU的ID和类型与系统中其他PDU的配置不冲突，应保持映射关系的一致性和准确性。|
|多实例个数|0 - 1|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CddComIfHandleId|
|描述|ECU wide unique, symbolic handle for the Pdu.|
|多实例个数|0 - 1|
|取值范围|0 - 65535|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|CddComIfPduRef|
|描述|Reference to the "global" Pdu structure to allow harmonization of handle IDs in the COM-Stack.|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/EcuC/EcucConfigSet/EcucPduCollection/Pdu|

#### 1.1.2. CddComIfUpperLayerTxPdu

|容器属性|值（容器）|
|---|---|
|名称|CddComIfUpperLayerTxPdu|
|描述|This container specifies Tx PDUs that are exchanged between the CDD and the standardized BSW module.|
|描述|概述：CddComIfUpperLayerTxPdu配置项用于定义复杂驱动设备（CDD）与通信接口层之间传输数据单元（PDU）的属性，包括PDU的标识符、大小和目标模块等信息。|
|描述|注意：在配置时需确保PDU标识符的唯一性，避免数据传输冲突。|
|多实例个数|0 - 1|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CddComIfHandleId|
|描述|ECU wide unique, symbolic handle for the Pdu.|
|描述|概述：CddComIfHandleId是用于标识Complex Device Driver (CDD)与Communication Interface之间通信的唯一标识符，确保数据传输的正确性。|
|描述|注意：CddComIfHandleId的值需要在整个项目中保持唯一。|
|多实例个数|0 - 1|
|取值范围|0 - 65535|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|CddComIfPduRef|
|描述|Reference to the "global" Pdu structure to allow harmonization of handle IDs in the COM-Stack.|
|描述|概述：CddComIfPduRef 是用于定义通信驱动设备（CDD）与PDU（协议数据单元）之间的接口引用，确保数据正确地在CDD和网络层之间传输。|
|描述|注意：确保CddComIfPduRef正确映射到相应的PDU，以保证数据传输的准确性。|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/EcuC/EcucConfigSet/EcucPduCollection/Pdu|

### 1.2. CddComMLowerLayerContribution

|容器属性|值（容器）|
|---|---|
|名称|CddComMLowerLayerContribution|
|描述|Parameters that are necessary for the configuration of a Complex Driver that serves as the LowerLayer of the Communication Manager module.|
|描述|概述：CddComMLowerLayerContribution配置项用于定义复杂设备驱动（Complex Device Driver, CDD）在通信管理（ComM）中的下层贡献，即CDD如何影响网络管理状态。|
|描述|注意：在AUTOSAR CP 4.4中，确保CddComMLowerLayerContribution的配置与CDD的实际功能和网络管理需求相匹配；CDD需要根据网络状态正确地报告其状态给ComM模块；在配置时，应注意与其他网络管理参与者的交互和协调。|
|描述|该配置项未使用|
|多实例个数|0 - 1|

#### 1.2.1. CddComMLowerLayerChannel

|容器属性|值（容器）|
|---|---|
|名称|CddComMLowerLayerChannel|
|描述|This container contains the network specific parameters.|
|描述|概述：CddComMLowerLayerChannel配置项用于定义复杂驱动器（Complex Device Driver, CDD）与底层通信接口之间的通道，确保CDD能够通过指定的通道与底层硬件或通信栈进行数据交换。|
|描述|注意：在配置CddComMLowerLayerChannel时，需要确保所指定的通道与CDD的功能和底层硬件接口相匹配；此配置项应与系统的通信需求和架构设计保持一致；在多通道系统中，正确的通道分配对于系统性能和可靠性至关重要。|
|描述|该配置项未使用|
|多实例个数|1 - 1|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|CddComMLowerLayerChannelRef|
|描述|Unique handle to identify one certain network. Reference to one of the network handles configured for the ComM.|
|描述|概述：CddComMLowerLayerChannelRef 是用于指定通信驱动层（CDD）与底层通信通道之间的关联，确保数据能够正确地在不同层之间传输。|
|描述|注意：在配置时需确保引用的通道与CDD兼容；该配置项对系统的通信稳定性和效率有直接影响；在多通道系统中，正确的通道引用尤为关键。|
|描述|该配置项未使用|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/ComM/ComMConfigSet/ComMChannel|

### 1.3. CddGenericNmLowerLayerContribution

|容器属性|值（容器）|
|---|---|
|名称|CddGenericNmLowerLayerContribution|
|描述|Parameters that are necessary for the configuration of a Complex Driver that serves as the LowerLayer of the Generic NM module.|
|描述|概述：CddGenericNmLowerLayerContribution配置项用于定义通用诊断网络管理（Generic Diagnostic Network Management, GenericNm）组件与下层网络管理模块之间的接口贡献，这影响了GenericNm组件的行为和网络管理消息的处理。|
|描述|注意：在配置时需确保与下层网络管理协议的兼容性和正确的接口映射；AUTOSAR CP 4.4标准中可能有具体的接口和行为规范，需要遵循这些规范来配置；如果项目中没有使用GenericNm组件，则此配置项不适用。|
|描述|该配置项未使用|
|多实例个数|0 - 1|

#### 1.3.1. CddGenericNmLowerLayerChannel

|容器属性|值（容器）|
|---|---|
|名称|CddGenericNmLowerLayerChannel|
|描述|NM Channel specific configuration parameters.|
|描述|概述：CddGenericNmLowerLayerChannel配置项用于定义通用诊断网络管理（Generic Network Management, GenericNm）模块与下层通信通道（如CAN, LIN等）之间的关联。|
|描述|注意：在配置时需确保该通道已在网络管理配置中定义；该配置项必须与实际的物理通道设置相匹配，以保证网络管理的正确性；在多通道系统中，每个GenericNm实例应正确映射到对应的物理通道。|
|描述|该配置项未使用|
|多实例个数|1 - 1|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|CddGenericNmComMNetworkHandleRef|
|描述|This reference points to the unique channel defined by the ComMChannel and provides access to the unique channel index value in ComMChannelId.|
|描述|概述：CddGenericNmComMNetworkHandleRef是一个配置项，用于指定通用诊断网络管理（Generic Network Management，简称GenericNm）与通信管理模块（Communication Manager，简称ComM）之间的网络句柄引用，确保网络管理和通信管理之间的正确关联。|
|描述|注意：在配置时需确保引用的网络句柄与实际使用的网络句柄相匹配，避免因句柄不匹配导致的通信问题；该配置项对于实现网络管理策略至关重要，应仔细配置以确保网络的正确管理和控制；在AUTOSAR CP 4.4标准中，确保使用正确的数据类型和格式符合规范要求。|
|描述|该配置项未使用|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/ComM/ComMConfigSet/ComMChannel|

### 1.4. CddJ1939RmContribution

|容器属性|值（容器）|
|---|---|
|名称|CddJ1939RmContribution|
|描述|Contribution of J1939Rm module|
|描述|概述：CddJ1939RmContribution 配置项用于定义特定通信驱动（CDD）在J1939网络管理中的角色和行为，确保网络管理的正确实施和通信的有效性。|
|描述|注意：此配置项必须与网络管理策略和其他网络参与者的配置兼容；确保配置正确反映了CDD的功能和责任；在实施此配置时，应详细测试网络的稳定性和通信的可靠性。|
|描述|该配置项未使用|
|多实例个数|0 - 1|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|CddJ1939RmAckIndication|
|描述|Defines whether the \<User\>_AckIndication callback function is implemented.|
|描述|概述：CddJ1939RmAckIndication配置项用于定义一个回调函数，该函数在接收到J1939网络上的ACK（确认）消息时被调用，用于处理确认消息的接收。|
|描述|注意：在使用此配置项时，需要确保已经在系统中实现了J1939通信协议栈，并且正确配置了相关的网络管理参数；此配置项需要与具体的应用层协议处理逻辑紧密结合，以确保正确解析和响应ACK消息；在AUTOSAR CP 4.4标准中，对于网络管理和通信服务的配置和实现有详细规范，需要遵循这些规范以保证系统的兼容性和可靠性。|
|描述|该配置项未使用|
|多实例个数|1 - 1|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|CddJ1939RmRequestIndication|
|描述|Defines whether the \<User\>_RequestIndication callback function is implemented.|
|描述|概述：CddJ1939RmRequestIndication是一个配置项，用于定义当接收到J1939网络上的请求消息时，应该调用的回调函数。|
|描述|注意：该配置项需要确保与实际的J1939请求消息处理逻辑相匹配；在配置时需注意回调函数的执行时间，以避免影响网络通信效率；此配置项在AUTOSAR CP 4.4标准中可能需要根据具体的网络管理需求进行详细配置，以确保正确的消息处理。|
|描述|该配置项未使用|
|多实例个数|1 - 1|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|CddJ1939RmRequestTimeoutIndication|
|描述|Defines whether the \<User\>_RequestTimeoutIndication callback function is implemented.|
|描述|概述：CddJ1939RmRequestTimeoutIndication配置项用于定义当J1939网络上的请求超时时触发的指示函数，确保系统能够响应网络请求超时事件。|
|描述|注意：该配置项需要与网络管理策略紧密配合，确保超时指示逻辑与系统的错误处理策略一致；在实现时需考虑网络的实际延迟和可能的重试机制；该配置项在AUTOSAR CP 4.4标准中未明确定义，需根据项目具体需求和网络管理策略自定义实现。|
|描述|该配置项未使用|
|多实例个数|1 - 1|

### 1.5. CddPduRLowerLayerContribution

|容器属性|值（容器）|
|---|---|
|名称|CddPduRLowerLayerContribution|
|描述|Parameters that are necessary for the configuration of a Complex Driver that serves as the LowerLayer of the Pdu Router module.|
|描述|概述：CddPduRLowerLayerContribution配置项定义了复杂驱动（CDD）作为下层通信模块与PduR模块交互。|
|描述|注意：在配置时需确保CDD与底层通信协议栈之间的接口匹配正确。|
|多实例个数|0 - 1|

#### 1.5.1. CddPduRLowerLayerRxPdu

|容器属性|值（容器）|
|---|---|
|名称|CddPduRLowerLayerRxPdu|
|描述|This container specifies Rx PDUs that are exchanged between the CDD and the standardized BSW module.|
|描述|概述：CddPduRLowerLayerRxPdu是一个配置项，用于定义复杂驱动器（Complex Device Driver, CDD）接收的PDU（协议数据单元）与底层通信接口之间的映射关系。|
|描述|注意：在配置CddPduRLowerLayerRxPdu时，需要确保PDU与底层通信层的兼容性和正确的映射关系。|
|多实例个数|0 - 1|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|CddPduRApiType|
|描述|This parameter configures the type of the CDD interface (IF/TP)|
|多实例个数|0 - 1|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CddPduRLowerLayerHandleId|
|描述|ECU wide unique, symbolic handle for the Pdu.|
|多实例个数|0 - 1|
|取值范围|0 - 65535|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|CddPduRLowerLayerPduRef|
|描述|Reference to the "global" Pdu structure to allow harmonization of handle IDs in the COM-Stack.|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/EcuC/EcucConfigSet/EcucPduCollection/Pdu|

#### 1.5.2. CddPduRLowerLayerTxPdu

|容器属性|值（容器）|
|---|---|
|名称|CddPduRLowerLayerTxPdu|
|描述|This container specifies Tx PDUs that are exchanged between the CDD and the standardized BSW module.|
|描述|概述：CddPduRLowerLayerTxPdu配置项用于定义从复杂设备驱动（CDD）到底层传输层的发送PDU（协议数据单元）的映射关系，确保数据能够正确地从应用层传输到物理层。|
|描述|注意：在配置时需确保PDU的唯一性和正确的映射关系，避免数据传输错误。|
|多实例个数|0 - 1|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|CddPduRApiType|
|描述|This parameter configures the type of the CDD interface (IF/TP)|
|多实例个数|0 - 1|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CddPduRLowerLayerHandleId|
|描述|ECU wide unique, symbolic handle for the Pdu.|
|描述|概述：CddPduRLowerLayerHandleId用于标识Complex Device Driver (CDD)中PDU Router (PduR)向下层通信接口（如CAN, LIN等）发送或接收PDU时使用的唯一标识符。|
|描述|注意：该标识符必须在系统中唯一，以确保PDU的正确路由；配置时需确保与底层通信接口的配置相匹配。|
|多实例个数|0 - 1|
|取值范围|0 - 65535|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|CddPduRLowerLayerPduRef|
|描述|Reference to the "global" Pdu structure to allow harmonization of handle IDs in the COM-Stack.|
|描述|概述：CddPduRLowerLayerPduRef是一个配置项，用于将复杂设备驱动（Complex Device Driver, CDD）中定义的PDU（协议数据单元）与底层网络层的PDU关联起来。|
|描述|注意：在配置CddPduRLowerLayerPduRef时，需要确保引用的底层PDU已经在系统中定义且与CDD PDU的通信需求相匹配。|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/EcuC/EcucConfigSet/EcucPduCollection/Pdu|

### 1.6. CddPduRUpperLayerContribution

|容器属性|值（容器）|
|---|---|
|名称|CddPduRUpperLayerContribution|
|描述|Parameters that are necessary for the configuration of a Complex Driver that serves as the UpperLayer of the Pdu Router module.|
|描述|概述：CddPduRUpperLayerContribution 配置项用于定义复杂驱动（CDD）作为上层通信模块与PduR模块交互。|
|描述|注意：此配置项必须确保与系统中所有相关的上层协议和服务的兼容性。|
|多实例个数|0 - 1|

#### 1.6.1. CddPduRUpperLayerRxPdu

|容器属性|值（容器）|
|---|---|
|名称|CddPduRUpperLayerRxPdu|
|描述|This container specifies Rx PDUs that are exchanged between the CDD and the standardized BSW module.|
|描述|概述：CddPduRUpperLayerRxPdu 配置项用于定义复杂设备驱动（Complex Device Driver, CDD）接收的PDU（协议数据单元）与上层模块之间的映射关系，确保数据能够正确地从CDD传输到上层协议栈。|
|描述|注意：在配置CddPduRUpperLayerRxPdu时，必须确保PDU的标识符与系统中其他PDU的标识符不冲突。|
|多实例个数|0 - 1|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|CddPduRApiType|
|描述|This parameter configures the type of the CDD interface (IF/TP)|
|多实例个数|0 - 1|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CddPduRUpperLayerHandleId|
|描述|ECU wide unique, symbolic handle for the Pdu.|
|多实例个数|0 - 1|
|取值范围|0 - 65535|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|CddPduRUpperLayerPduRef|
|描述|Reference to the "global" Pdu structure to allow harmonization of handle IDs in the COM-Stack.|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/EcuC/EcucConfigSet/EcucPduCollection/Pdu|

#### 1.6.2. CddPduRUpperLayerTxPdu

|容器属性|值（容器）|
|---|---|
|名称|CddPduRUpperLayerTxPdu|
|描述|This container specifies Tx PDUs that are exchanged between the CDD and the standardized BSW module.|
|描述|概述：CddPduRUpperLayerTxPdu配置项用于定义复杂驱动器（Complex Device Driver, CDD）发送的PDU（协议数据单元）与PDU路由器（PduR）之间的映射关系，确保数据能够正确地从CDD传输到上层协议栈。|
|描述|注意：在配置CddPduRUpperLayerTxPdu时，需要确保PDU的标识符与系统中其他PDU的标识符不冲突；此外，应当注意PDU的大小和格式要符合上层协议的要求；最后，确保映射关系的一致性，以便PduR能够正确地处理来自CDD的数据。|
|多实例个数|0 - 1|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|CddPduRApiType|
|描述|This parameter configures the type of the CDD interface (IF/TP)|
|多实例个数|0 - 1|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CddPduRUpperLayerHandleId|
|描述|ECU wide unique, symbolic handle for the Pdu.|
|描述|概述：CddPduRUpperLayerHandleId是用于标识复杂驱动设备（CDD）与PDU路由器（PduR）之间通信的上层处理标识符，确保数据能够正确地在CDD和PduR之间传输。|
|描述|注意：该标识符必须在系统中唯一，以避免数据传输的混淆。|
|多实例个数|0 - 1|
|取值范围|0 - 65535|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|CddPduRUpperLayerPduRef|
|描述|Reference to the "global" Pdu structure to allow harmonization of handle IDs in the COM-Stack.|
|描述|概述：CddPduRUpperLayerPduRef 配置项用于定义复杂设备驱动（Complex Device Driver, CDD）与PDU路由器（PduR）之间的上层PDU引用，确保数据能够在CDD和PDU路由器之间正确传输。|
|描述|注意：在配置CddPduRUpperLayerPduRef时，需要确保引用的上层PDU与CDD的接口匹配；此配置项应与系统中的通信矩阵和PDU路由策略保持一致。|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/EcuC/EcucConfigSet/EcucPduCollection/Pdu|

### 1.7. CddSoAdUpperLayerContribution

|容器属性|值（容器）|
|---|---|
|名称|CddSoAdUpperLayerContribution|
|描述|Parameters that are necessary for the configuration of a Complex Driver that serves as the UpperLayer of the SoAd module.|
|描述|概述：CddSoAdUpperLayerContribution配置项用于定义复杂设备驱动（Complex Device Driver, CDD）作为上层模块与SoAd模块交互。|
|描述|注意：在配置CddSoAdUpperLayerContribution时，需要确保CDD与SoAd模块之间的接口和数据流向正确定义，以保证网络通信的正确性。|
|多实例个数|0 - 1|

#### 1.7.1. CddSoAdUpperLayerRxPdu

|容器属性|值（容器）|
|---|---|
|名称|CddSoAdUpperLayerRxPdu|
|描述|This container specifies Rx PDUs that are exchanged between the CDD and the standardized BSW module.|
|描述|概述：CddSoAdUpperLayerRxPdu配置项用于定义复杂设备驱动（Complex Device Driver, CDD）与Socket Adaptor（SoAd）模块之间接收路径的参数，这包括PDU的标识符、长度和连接到的上层协议。|
|描述|注意：在配置CddSoAdUpperLayerRxPdu时，需要确保PDU标识符的唯一性，以避免数据传输中的冲突；PDU长度应与实际数据包大小相匹配。|
|多实例个数|0 - 1|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|CddPduRApiType|
|描述|This parameter configures the type of the CDD interface (IF/TP)|
|多实例个数|0 - 1|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CddSoAdUpperLayerHandleId|
|描述|ECU wide unique, symbolic handle for the Pdu.|
|多实例个数|1 - 1|
|取值范围|0 - 65535|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|CddSoAdUpperLayerPduRef|
|描述|Reference to the "global" Pdu structure to allow harmonization of handle IDs in the COM-Stack.|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/EcuC/EcucConfigSet/EcucPduCollection/Pdu|

#### 1.7.2. CddSoAdUpperLayerTxPdu

|容器属性|值（容器）|
|---|---|
|名称|CddSoAdUpperLayerTxPdu|
|描述|This container specifies Tx PDUs that are exchanged between the CDD and the standardized BSW module.|
|描述|概述：CddSoAdUpperLayerTxPdu配置项用于定义复杂设备驱动（Complex Device Driver, CDD）与Socket Adaptor（SoAd）模块之间的上行传输协议数据单元（PDU），即CDD发送数据时使用的PDU。|
|描述|注意：在配置CddSoAdUpperLayerTxPdu时，需要确保PDU的标识与系统中其他PDU的标识符不冲突。|
|多实例个数|0 - 1|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|CddPduRApiType|
|描述|This parameter configures the type of the CDD interface (IF/TP)|
|描述|概述：CddPduRApiType配置项用于定义Complex Device Driver (CDD)与PDU Router之间通信时使用的API类型，分为Tp和If类型。|
|描述|注意：API的类型必须保持一致。|
|多实例个数|0 - 1|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CddSoAdUpperLayerHandleId|
|描述|ECU wide unique, symbolic handle for the Pdu.|
|描述|概述：CddSoAdUpperLayerHandleId是用于标识Complex Device Driver (CDD)与Socket Adaptor (SoAd)之间通信的上层协议处理模块的唯一标识符。|
|描述|注意：在配置时需确保每个CDD与SoAd之间的通信通道的CddSoAdUpperLayerHandleId是唯一的。|
|多实例个数|0 - 1|
|取值范围|0 - 65535|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|CddSoAdUpperLayerPduRef|
|描述|Reference to the "global" Pdu structure to allow harmonization of handle IDs in the COM-Stack.|
|描述|概述：CddSoAdUpperLayerPduRef 是一个配置参数，用于将Complex Device Driver (CDD)中处理的PDU与Socket Adaptor (SoAd)层的上层PDU关联起来，确保数据正确地在CDD和SoAd之间传输。|
|描述|注意：在配置CddSoAdUpperLayerPduRef时，必须确保引用的PDU与CDD所处理的PDU匹配。|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/EcuC/EcucConfigSet/EcucPduCollection/Pdu|

## 2. CddEcucPartitionInteraction

|容器属性|值（容器）|
|---|---|
|名称|CddEcucPartitionInteraction|
|描述|This optional container holds the partition interaction configuration.|
|描述|概述：CddEcucPartitionInteraction配置项定义了复杂设备驱动（Complex Device Driver, CDD）与ECU配置单元（ECUC）分区间的交互方式，这涉及到CDD如何与AUTOSAR软件架构中的其他部分进行通信和数据交换。|
|描述|注意：在配置CddEcucPartitionInteraction时，需要确保CDD与ECU分区间的交互符合AUTOSAR CP 4.4的通信机制要求；此配置项的设置应与系统的安全和隔离级别要求相匹配；在多核或多分区系统中，还需考虑跨分区或跨核心的交互策略。|
|描述|该配置项未使用|
|多实例个数|0 - 1|

|配置项属性|值（函数名配置项）|
|---|---|
|名称|CddPartitionStoppedFunctionName|
|描述|Function name to be called when the partition which is triggering the Complex Driver is stopped.|
|描述|概述：CddPartitionStoppedFunctionName 配置项指定了在分区停止时调用的复杂驱动设备（CDD）的函数名称。|
|描述|注意：确保指定的函数符合实际的CDD实现并且已经定义；函数应当能够处理分区停止时的资源释放和状态保存；在配置时需遵循AUTOSAR CP 4.4的命名和实现规范。|
|描述|该配置项未使用|
|多实例个数|1 - 1|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|CddEcucPartitionRef|
|描述|Reference to the "EcucPartition" which executes the software which triggers the CDD.|
|描述|概述：CddEcucPartitionRef配置项用于指定复杂设备驱动（Complex Device Driver，CDD）所属的ECU配置分区引用，确保CDD与特定的ECU分区关联，以便于管理和配置。|
|描述|注意：在多核或多分区系统中，正确配置CddEcucPartitionRef至关重要，以确保CDD运行在正确的ECU分区上；该配置项在AUTOSAR CP 4.4中可能受限于特定的模块或组件支持情况；用户需确保分区配置与系统架构设计一致，避免资源冲突或访问违规。|
|描述|该配置项未使用|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/EcuC/EcucPartitionCollection/EcucPartition|

## 3. CddGeneral

|容器属性|值（容器）|
|---|---|
|名称|CddGeneral|
|描述|Contains the general configuration parameters of the module.|
|描述|概述：CddGeneral是一个配置容器，它包含了用于Complex Device Driver (CDD)的通用配置参数，这些参数用于定义CDD的基本属性和行为。|
|描述|注意：在AUTOSAR CP 4.4标准中，CddGeneral的配置应当与CDD模块的实现和集成需求相匹配；确保CddGeneral的参数设置不会与其他BSW模块的配置发生冲突；在配置CDD时，应遵循AUTOSAR的模块化和接口标准，以确保模块间的兼容性和系统的可维护性。|
|描述|该配置项未使用|
|多实例个数|0 - 1|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CddInstanceId|
|描述|Specifies the InstanceId of this module instance. If only one instance is present it shall have the Id 0.|
|描述|概述：CddInstanceId 是一个配置项，用于为复杂设备驱动（Complex Device Driver，简称CDD）实例分配一个唯一的标识符，以便在AUTOSAR软件架构中进行区分和管理。|
|描述|注意：在配置CddInstanceId时，必须确保在整个AUTOSAR项目中该标识符的唯一性；该标识符通常由系统集成者分配，以确保与其他软件组件的标识符不冲突；在AUTOSAR CP 4.4标准中，CddInstanceId的配置应符合标准规定的数据类型和取值范围。|
|描述|该配置项未使用|
|多实例个数|1 - 1|
|取值范围|0 - 255|

## 4. CddGlobalTimeContribution

|容器属性|值（容器）|
|---|---|
|名称|CddGlobalTimeContribution|
|描述|Contribution of Global Time modules.|
|描述|概述：CddGlobalTimeContribution配置项用于定义复杂设备驱动（Complex Device Driver, CDD）对全局时间同步机制的贡献，即指定CDD是否提供时间信息以支持系统的时间同步。|
|描述|注意：在配置CddGlobalTimeContribution时，需要确保CDD能够提供准确和可靠的时间信息；此配置项通常与全局时间同步服务（Global Time Synchronization Services）相关联，因此需要与其他时间同步相关的配置项协同工作；在AUTOSAR CP 4.4标准中，如果系统不使用全局时间同步服务，该配置项可能不适用或需要特别注意其默认值和行为。|
|描述|该配置项未使用|
|多实例个数|0 - 1|

### 4.1. CddGlobalTimeDomain

|容器属性|值（容器）|
|---|---|
|名称|CddGlobalTimeDomain|
|描述|This represents the existence of a CDD global time domain. The CddGlobalTimeContribution can administrate several global time domains at the same time that in itself form a hierarchy of domains and sub-domains.|
|描述|概述：CddGlobalTimeDomain配置项用于定义通用诊断组件（CDD）所使用的全局时间域，确保时间敏感的诊断服务能够在正确的时间域内执行。|
|描述|注意：在配置CddGlobalTimeDomain时，需要确保所选时间域与系统中其他组件的时间域一致，以避免时间同步问题；此配置项对于实现时间同步的诊断服务尤为重要；AUTOSAR CP 4.4标准中并未明确定义此配置项，因此具体实现可能会依赖于供应商的实现。|
|描述|该配置项未使用|
|多实例个数|1 - 1|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CddGlobalTimeDomainId|
|描述|The global time domain ID.|
|描述|概述：CddGlobalTimeDomainId是用于标识Complex Device Driver（CDD）所属的全局时间域的唯一标识符，确保CDD在正确的时间域中执行其操作。|
|描述|注意：在配置CddGlobalTimeDomainId时，必须确保其与系统中定义的时间域ID匹配；不同的CDD如果操作在相同的时间域中，应该使用相同的时间域ID；在AUTOSAR CP 4.4标准中，对时间域的概念和管理有明确规定，需要遵守这些规定以保证系统的时间一致性和准确性。|
|描述|该配置项未使用|
|多实例个数|1 - 1|
|取值范围|0 - 31|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|CddSynSynchronizedTimeBaseRef|
|描述|Mandatory reference to the required synchronized time-base.|
|描述|概述：CddSynSynchronizedTimeBaseRef 是一个配置参数，用于引用一个同步的时间基准，这通常是由通用诊断模块（CDD）提供的，以确保时间同步。|
|描述|注意：在配置CddSynSynchronizedTimeBaseRef时，需要确保引用的时间基准是有效的，并且与系统中其他模块的时间同步需求兼容；此外，该时间基准应当由一个可靠的时间源提供，以保证时间同步的准确性；在AUTOSAR CP 4.4标准中，如果时间同步的概念在项目中不适用或未被使用，那么这个配置项可能不会出现。|
|描述|该配置项未使用|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/StbM/StbMSynchronizedTimeBase|

#### 4.1.1. CddGlobalTimeMaster

|容器属性|值（容器）|
|---|---|
|名称|CddGlobalTimeMaster|
|描述|Configuration of the global time master. Each global time domain is required to have exactly one global time master. This master may or may not exist on the configured ECU.|
|描述|概述：CddGlobalTimeMaster配置项用于定义一个通信驱动模块（Complex Device Driver, CDD）作为全局时间的主控，负责管理和维护系统中的全局时间同步。|
|描述|注意：该配置项需要确保系统中只有一个CddGlobalTimeMaster被指定，以避免时间同步冲突；在分布式系统中，选择CddGlobalTimeMaster时要考虑网络延迟和精确度要求；AUTOSAR CP 4.4标准中并未直接定义CddGlobalTimeMaster，此配置可能属于特定实现或扩展，需参考具体的供应商文档。|
|描述|该配置项未使用|
|多实例个数|0 - 1|

|配置项属性|值（浮点型参数配置项）|
|---|---|
|名称|CddGlobalTimeTxPeriod|
|描述|This represents configuration of the TX period. Unit: seconds|
|描述|概述：CddGlobalTimeTxPeriod 配置项用于定义Complex Device Driver (CDD) 发送全局时间信息的周期，即CDD多久发送一次时间同步信息。|
|描述|注意：该配置项的值应当与系统中时间同步的要求相匹配；在配置时需要考虑网络带宽和系统负载，以免造成不必要的网络拥塞；如果配置的周期与AUTOSAR CP 4.4标准中推荐的时间同步周期不一致，需要确保系统中其他组件能够适应这一变化。|
|描述|该配置项未使用|
|多实例个数|1 - 1|
|取值范围|0 - Inf|

##### 4.1.1.1. CddGlobalTimeMasterPdu

|容器属性|值（容器）|
|---|---|
|名称|CddGlobalTimeMasterPdu|
|描述|This container encloses the configuration of the PDU that is supposed to contain the global time information.|
|描述|概述：CddGlobalTimeMasterPdu配置项用于定义Complex Device Driver (CDD) 模块作为全局时间主节点时发送的PDU（协议数据单元）。|
|描述|注意：在配置CddGlobalTimeMasterPdu时，需要确保PDU与CDD模块的时间同步功能兼容；此配置项通常与网络管理和时间同步相关的其他配置项紧密相关，因此需要仔细协调这些配置以确保系统的时间同步准确性；AUTOSAR CP 4.4标准中可能有特定的属性和参数要求，需要根据标准文档进行准确配置。|
|描述|该配置项未使用|
|说明|Please note that the configuration of CddGlobalTimeMasterPdu is optional and shall only be used for Complex Drivers that are using Pdus for carrying timeSync information.|
|多实例个数|0 - 1|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|CddGlobalTimeMasterPduRef|
|描述|This represents the reference to the Pdu taken to transmit the global time information. The global time master of a global time domain is the sender of this Pdu.|
|描述|概述：CddGlobalTimeMasterPduRef是一个配置项，用于指定Complex Device Driver (CDD) 作为全局时间主节点时所使用的PDU（协议数据单元）引用。|
|描述|注意：在配置CddGlobalTimeMasterPduRef时，需要确保引用的PDU与CDD的时间同步功能兼容；此配置项通常与时间同步相关的模块一起使用，如同步以太网通信；在AUTOSAR CP 4.4标准中，确保配置项符合PDU的定义和使用要求。|
|描述|该配置项未使用|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Cdd/CddComStackContribution/CddComIfUpperLayerContribution/CddComIfUpperLayerTxPdu|

#### 4.1.2. CddGlobalTimeSlave

|容器属性|值（容器）|
|---|---|
|名称|CddGlobalTimeSlave|
|描述|Configuration of a global time slave. Each global time domain is required to have at least one time slave. The configured ECU may or may not represent a time slave.|
|描述|概述：CddGlobalTimeSlave配置项用于定义通用设备驱动（Complex Device Driver，CDD）中的全局时间同步从设备的属性和行为，确保系统中的多个组件可以基于统一的时间基准进行同步操作。|
|描述|注意：在配置CddGlobalTimeSlave时，需要确保系统中有一个明确的全局时间主设备（GlobalTimeMaster）配置，以便从设备能够同步到正确的时间基准；此配置项在AUTOSAR CP 4.4标准中可能不直接提及，因为全局时间同步功能的实现细节可能依赖于具体的AUTOSAR BSW模块或CDD实现；在实现时，应考虑网络延迟和时钟偏差补偿机制，以提高时间同步的准确性。|
|描述|该配置项未使用|
|多实例个数|0 - 1|

##### 4.1.2.1. CddGlobalTimeSlavePdu

|容器属性|值（容器）|
|---|---|
|名称|CddGlobalTimeSlavePdu|
|描述|This container encloses the configuration of the PDU that is supposed to contain the global time information.|
|描述|概述：CddGlobalTimeSlavePdu配置项用于定义通信数据诊断（CDD）模块中全局时间同步协议的从设备协议数据单元（PDU），它指定了用于时间同步的数据传输对象。|
|描述|注意：在配置CddGlobalTimeSlavePdu时，需要确保PDU的ID和大小符合网络通信要求；此配置项对于实现基于时间的服务和功能至关重要，因此需要精确配置；AUTOSAR CP 4.4标准中未明确列出此配置项，可能属于特定实现或扩展，因此在标准AUTOSAR环境中使用时应谨慎。|
|描述|该配置项未使用|
|说明|Please note that the configuration of CddGlobalTimeSlavePdu is optional and shall only be used for Complex Drivers that are using Pdus for carrying timeSync information.|
|多实例个数|0 - 1|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|CddGlobalTimeSlavePduRef|
|描述|This represents the reference to the Pdu taken to transmit the global time information. All the time slaves are supposed to receive the Pdu.|
|描述|概述：CddGlobalTimeSlavePduRef是一个配置项，用于引用Complex Device Driver (CDD) 模块中用于同步全局时间的从节点PDU（协议数据单元）。|
|描述|注意：在配置CddGlobalTimeSlavePduRef时，必须确保引用的PDU与CDD模块的全局时间同步功能相匹配；此配置项通常与全局时间同步服务相关联，因此需要在实现时间敏感网络时特别注意；在AUTOSAR CP 4.4标准中，确保该配置项与其他网络管理配置项协同工作，以保证网络时间同步的准确性。|
|描述|该配置项未使用|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Cdd/CddComStackContribution/CddComIfUpperLayerContribution/CddComIfUpperLayerRxPdu|
