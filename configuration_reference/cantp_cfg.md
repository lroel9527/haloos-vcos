# CanTp 配置项参考文档

|容器属性|值（容器）|
|---|---|
|名称|CanTp|
|描述|Configuration of the CanTp (CAN Transport Protocol) module.|
|描述|概述：CanTp 是 AUTOSAR Communication Stack 的一部分，负责实现基于 ISO 15765-2 的 CAN 传输层协议，它支持长消息的分割和重组，确保在CAN通信时I-PDU的数据长度不大于8个字节，在CAN FD通信时I-PDU的数据不大于64个字节。|
|描述|注意：在配置 CanTp 模块时，需要确保正确设置网络层的参数，如N-PDU、定时参数和流控制策略；CanTp 配置应与 CanIf 和 PduR 的配置相匹配，以确保数据可正确传输。|
|多实例个数|0 - 1|

## 1. CanTpConfig

|容器属性|值（容器）|
|---|---|
|名称|CanTpConfig|
|描述|This container contains the configuration parameters and sub containers of the AUTOSAR CanTp module.|
|描述|概述：CanTpConfig是用于配置CAN传输层（CAN Transport Layer）的参数，该配置项下包含CanTpMainFunctionPeriod和CanTpChannel。|
|描述|在配置CanTpConfig下面的CanTpChannel时，此配置项下可根据需求添加若干连接通道（CanTpChannel），在静态配置下，每个连接通道会对应一个或一对SDU，SDU可为接收方向与发送方向；因此，CanTpChannel下有两种子容器，分别为CanTpRxNSdu和CanTpTxNSdu。|
|多实例个数|1 - 1|

### 1.1. CanTpMainFunction

|容器属性|值（容器）|
|---|---|
|名称|CanTpMainFunction|
|描述|Contains the configuration parameters of the AUTOSAR CanTp module's CanTpMainFunction.|
|描述|概述：CanSMMainFunction是一个配置项，用于定义CAN网络管理（CANSM）中的主函数，这些主函数用于taskmapping。|
|描述|注意：在配置CanTpMainFunction时，需要确保其与taskmapping功能相匹配；此外，该配置项的属性应符合AUTOSAR CP 4.4标准中对CANTP的规定。|
|多实例个数|1 - 255|

|配置项属性|值（浮点型参数配置项）|
|---|---|
|名称|CanTpMainFunctionPeriod|
|描述|Allow to configure the time for the MainFunction (as float in seconds). The CanTpMainFunctionPeriod should be assigned a value which is optimal regarding all of the timers configured for CanTp in TX and RX data transfer i.e. the differences from the configured timing should be as small as possible. Please note: This period shall be the same as call cycle time of the periodic task were CanTp Main function is called.|
|描述|概述：CanTpMainFunctionPeriod配置项指定了CAN传输协议（CAN Transport Protocol）主函数的调用周期，用于控制网络层消息的发送和接收处理的时间间隔。|
|描述|注意：此参数的值应该大于0，CanTpMainFunctionPeriod的值应根据 CanTp 在发送和接收数据传输中配置的所有计时器进行优化，即使得配置时间与实际时间的差异尽可能小，此周期应与调用 CanTp 主函数的周期性任务的调用周期时间相同,默认值5ms。|
|多实例个数|1 - 1|
|默认值|0.005|
|取值范围|0 - Inf|

### 1.2. CanTpChannel

|容器属性|值（容器）|
|---|---|
|名称|CanTpChannel|
|描述|This container contains the configuration parameters of the CanTp channel.|
|描述|概述：CanTpChannel 配置项用于定义CAN传输层的通道属性，包含的子容器有CanTpRxNSdu和CanTpTxNSdu。|
|描述|注意：在配置CanTpChannel时，需要确保通道标识符的唯一性。|
|多实例个数|1 - inf|

#### 1.2.1. CanTpRxNSdu

|容器属性|值（容器）|
|---|---|
|名称|CanTpRxNSdu|
|描述|The following parameters needs to be configured for each CAN N-SDU that the CanTp module receives via the CanTpChannel. This N-SDU produces meta data items of type SOURCE_ADDRESS_16, TARGET_ADDRESS_16 and ADDRESS_EXTENSION_8.|
|描述|概述：CanTpRxNSdu配置中包含连接通道CAN N-SDU接收方向相关的所需的相关关键数据。|
|描述|注意：在配置CanTpRxNSdu时，必须确保PDU标识符的唯一性以避免冲突；正确设置地址信息以匹配发送方的配置；合理配置超时时间以适应网络延迟和系统性能。|
|多实例个数|0 - 1|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|CanTpRxAddressingFormat|
|描述|Declares which communication addressing mode is supported for this RxNSdu. Definition of Enumeration values:|
|描述|概述：CanTpRxAddressingFormat 配置项用于定义CAN传输层接收侧的寻址方式，包括标准寻址、扩展寻址和混合寻址。|
|描述|注意：在配置CanTpRxAddressingFormat时，需要确保它与通信矩阵中定义的寻址方式相匹配；此外，该配置项应与发送侧的CanTpTxAddressingFormat保持一致，以确保通信的一致性。|
|说明|CanTpStandard to use normal addressing format. CanTpExtended to use extended addressing format. CanTpMixed to use mixed 11 bit addressing format. CanTpNormalFixed to use normal fixed addressing format. CanTpMixed29Bit to use mixed 29 bit addressing format.|
|多实例个数|1 - 1|
|默认值|CANTP_STANDARD|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|CanTpRxPaddingActivation|
|描述|Defines if the receive frame uses padding or not. This parameter is restricted to 8 byte N-PDUs.|
|描述|概述：CanTpRxPaddingActivation 配置项用于定义接收侧的传输协议是否应该对接收到的CAN帧进行填充，以确保数据帧的长度达到预定的标准长度。|
|描述|注意：在AUTOSAR CP 4.4标准中，接收到的CAN帧可能需要填充到8字节，这取决于网络的配置；不正确的填充设置可能会导致通信不一致或数据解析错误；主要适用于适用于SF（单帧）、FC（流控制帧）和最后一个CF（连续帧）。|
|说明|Definition of enumeration values: CanTpOn: The N-PDU received uses padding for SF, FC and the last CF. (N-PDU length is always \>= 8 bytes in case of CAN 2.0) CanTpOff: The N-PDU received does not use padding for SF, CF and the last CF. (N-PDU length is dynamic - any valid DLC value). Note: The mandatory mapping to the next higher valid DLC value for N-PDUs with a length \> 8 bytes is not affected by this parameter.|
|多实例个数|1 - 1|
|默认值|CANTP_ON|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|CanTpRxTaType|
|描述|Declares the communication type of this Rx N-SDU.|
|描述|概述：CanTpRxTaType 配置项声明该Rx N-SDU的通信类型；具体可分为功能寻址或物理寻址。|
|描述|注意：在配置CanTpRxTaType时，需要确保它与系统中使用的CAN地址方案一致。|
|多实例个数|1 - 1|

|配置项属性|值（浮点型参数配置项）|
|---|---|
|名称|CanTpNar|
|描述|Value in seconds of the N_Ar timeout. N_Ar is the time for transmission of a CAN frame (any N_PDU) on the receiver side.|
|描述|概述：N_Ar超时值（以秒为单位）；CanTpNar配置项以网络层请求链路层发送（Receiver.req）为时间起点，以网络层收到链路层返回发送成功回执（Receiver.con）为时间终点。|
|描述|注意：CanTpNar参数定义了N_Ar超时时间，即CAN接收端传输CAN帧所允许的最大时间。超过这段时间如果没有完成传输，可能会导致通信超时错误。|
|多实例个数|0 - 1|
|默认值|0.025|
|取值范围|0 - Inf|

|配置项属性|值（浮点型参数配置项）|
|---|---|
|名称|CanTpNbr|
|描述|Value in seconds of the performance requirement for (N_Br + N_Ar). N_Br is the elapsed time between the receiving indication of a FF or CF or the transmit confirmation of a FC, until the transmit request of the next FC.|
|描述|概述：N_Br是从接收到FF（首帧）或CF（连续帧）的接收指示或FC（流控帧）的发送确认后，到下一FC的发送请求之间的时间。|
|描述|注意：在配置CanTpNbr时，重要的是要考虑到通信网络的实际条件和性能限制，以确保设置的时间既不会导致不必要的延迟，也不会由于过于紧迫的时间限制导致数据传输失败。|
|多实例个数|0 - 1|
|默认值|0.025|
|取值范围|0 - Inf|

|配置项属性|值（浮点型参数配置项）|
|---|---|
|名称|CanTpNcr|
|描述|Value in seconds of the N_Cr timeout. N_Cr is the time until reception of the next Consecutive Frame N_PDU.|
|描述|概述：CanTpNcr 是 AUTOSAR CP (Classic Platform) 中的配置参数，N_Cr超时的值（以秒为单位）。N_Cr是接收方动作结束到接收下一个连续帧的时长。|
|描述|注意：该参数的值必须根据网络的通信速率和性能要求来设定，以确保在规定时间内发送流控制帧。|
|多实例个数|0 - 1|
|默认值|0.15|
|取值范围|0 - Inf|

|配置项属性|值（浮点型参数配置项）|
|---|---|
|名称|CanTpSTmin|
|描述|Sets the duration of the minimum time the CanTp sender shall wait between the transmissions of two CF N-PDUs.|
|描述|概述：CanTpSTmin 是一个配置参数，用于定义在CAN传输层（CAN Transport Layer）中连续帧（Consecutive Frame, CF）之间的必须等待的最小间隔时间。|
|描述|注意：STmin的值必须在规定的范围内，通常是0到127毫秒或特定的微秒值；配置值过小可能导致接收端处理不及，过大可能影响通信效率；在配置STmin时，还需考虑网络的负载和性能要求。|
|说明|For further details on this parameter value see ISO 15765-2 specification.|
|多实例个数|0 - 1|
|默认值|0.025|
|取值范围|0 - Inf|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CanTpBs|
|描述|Sets the number of N-PDUs the CanTp receiver allows the sender to send, before waiting for an authorization to continue transmission of the following N-PDUs.For further details on this parameter value see ISO 15765-2 specification.|
|描述|概述：CanTpBs 配置项用于定义ISO TP（ISO 15765-2，也称为传输协议）中的块大小，即在接收方需要发送下一个流控制帧之前，发送方可以发送的连续帧的最大数量。|
|描述|注意：块大小的配置必须符合ECU的缓冲能力和网络的带宽限制；过大的块大小可能导致接收方缓冲区溢出，而过小可能影响通信效率。|
|多实例个数|0 - 1|
|默认值|8|
|取值范围|0 - 255|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CanTpRxNSduId|
|描述|Unique identifier user by the upper layer to call CanTp_CancelReceive, CanTp_ChangeParameter and CanTp_ReadParameter.|
|描述|概述：CanTpRxNSduId是用于唯一标识接收侧网络层服务数据单元（N-SDU）的配置项，它在CAN传输协议中用于区分不同的接收消息。|
|描述|注意：CanTpRxNSduId是SDU的编号，在CanTp_CancelReceive函数和CanTp_ChangeParameter函数和CanTp_ReadParameter函数调用流程中会使用。|
|多实例个数|1 - 1|
|默认值|0|
|取值范围|0 - 65535|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CanTpRxWftMax|
|描述|This parameter indicates how many Flow Control wait N-PDUs can be consecutively transmitted by the receiver. It is local to the node and is not transmitted inside the FC protocol data unit.|
|描述|概述：CanTpRxWftMax 是一个配置参数，用于指定网络层（CAN传输层）在接收ISO 15765-2多帧消息时，可以发送的最大流控制WAIT帧（WFT）的数量。|
|描述|注意：该参数的值必须根据网络的性能和通信需求来设定，以避免通信延迟和超时；过高的WFT值可能导致通信效率降低，而过低的值可能导致无法正确接收大数据包。|
|说明|CanTpRxWftMax is used to avoid sender nodes being potentially hooked-up in case of a temporarily reception inability on the part of the receiver nodes, whereby the sender could be waiting continuously.|
|多实例个数|0 - 1|
|默认值|255|
|取值范围|0 - 65535|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|CanTpRxNSduRef|
|描述|Reference to a Pdu in the COM-Stack.|
|描述|概述：CanTpRxNSduRef是一个配置项，用于引用接收侧网络层服务数据单元（NSDU），它指定了CAN传输层接收消息的标识和处理规则。|
|描述|注意：确保每个CanTpRxNSduRef正确引用了期望的PduR层的RxNSdu，以保证消息正确路由；在配置时需注意与发送侧NSdu的匹配性，避免数据传输错误；该配置项在AUTOSAR CP 4.4中是必需的，缺失会导致接收过程无法正确执行。|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/EcuC/EcucConfigSet/EcucPduCollection/Pdu|

##### 1.2.1.1. CanTpNAe

|容器属性|值（容器）|
|---|---|
|名称|CanTpNAe|
|描述|This container is required for each RxNSdu and TxNSdu with AddressingFormat CANTP_MIXED or CANTP_MIXED29BIT.|
|多实例个数|0 - 1|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CanTpNAe|
|描述|This parameter contains the transport protocol address extension value.|
|多实例个数|1 - 1|
|取值范围|0 - 255|

##### 1.2.1.2. CanTpNSa

|容器属性|值（容器）|
|---|---|
|名称|CanTpNSa|
|描述|This container is required for each RxNSdu and TxNSdu with RxTaType CANTP_PHYSICAL and CanTpAddressingFormat CANTP_EXTENDED. When DynIdSupport is enabled, this container is also required for each TxNSdu with AddressingFormat CANTP_NORMALFIXED or CANTP_MIXED29BIT. When DynIdSupport is enabled and GenericConnectionSupport is not enabled, this container is also required for each RxNSdu with AddressingFormat CANTP_NORMALFIXED or CANTP_MIXED29BIT.|
|多实例个数|0 - 1|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CanTpNSa|
|描述|This parameter contains the transport protocol source address value.|
|多实例个数|1 - 1|
|取值范围|0 - 255|

##### 1.2.1.3. CanTpNTa

|容器属性|值（容器）|
|---|---|
|名称|CanTpNTa|
|描述|This container is required for each RxNSdu and TxNSdu with AddressingFormat CANTP_EXTENDED. When DynIdSupport is enabled, this container is also required for each RxNSdu with AddressingFormat CANTP_NORMALFIXED or CANTP_MIXED29BIT. When DynIdSupport is enabled and GenericConnectionSupport is not enabled, this container is also required for each TxNSdu with AddressingFormat CANTP_NORMALFIXED or CANTP_MIXED29BIT.|
|多实例个数|0 - 1|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CanTpNTa|
|描述|This parameter contains the transport protocol target address value.|
|多实例个数|1 - 1|
|取值范围|0 - 255|

##### 1.2.1.4. CanTpRxNPdu

|容器属性|值（容器）|
|---|---|
|名称|CanTpRxNPdu|
|描述|Used for grouping of the ID of a PDU and the Reference to a PDU. This N-PDU consumes a meta data item of type CAN_ID_32.|
|描述|概述：CanTpRxNPdu配置项用于定义接收侧网络层协议数据单元（N-PDU），它指定了接收CAN传输协议数据的参数和属性，如N-PDU的ID和接收消息的处理方式。|
|描述|注意：在配置CanTpRxNPdu时，必须确保N-PDU的ID在整个CAN网络中是唯一的，以避免消息冲突；此配置项应与CAN驱动和CAN接口模块的配置保持一致，以确保正确的消息接收和处理；AUTOSAR CP 4.4标准要求对接收的N-PDU进行严格的时间和资源管理，以满足实时性要求。|
|多实例个数|1 - 1|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CanTpRxNPduId|
|描述|The N-PDU identifier attached to the RxNsdu is identified by CanTpRxNSduId.|
|描述|概述：CanTpRxNPduId是用于标识接收到的网络层协议数据单元（N-PDU）的唯一标识符，它使得CAN传输层（CanTp）能够区分和处理接收到的不同N-PDU消息。|
|描述|注意：在配置CanTpRxNPduId时，必须确保其值在整个CAN网络中是唯一的，以避免消息处理的冲突；此外，该标识符的配置应与CAN驱动和网络管理配置相匹配，以确保正确的消息路由和处理；在AUTOSAR CP 4.4标准中，对CanTpRxNPduId的具体数值范围没有特殊限制，但应遵循项目或网络的具体要求。|
|说明|Each RxNsdu identifier is linked to only one SF/FF/CF N-PDU identifier. Nevertheless, in the case of extended or mixed addressing format, the same N-PDU identifier can be used for several N-SDU identifiers. The distinction is made by the N_TA or N_AE value (first data byte of SF or FF frames).|
|多实例个数|1 - 1|
|默认值|0|
|取值范围|0 - 65535|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|CanTpRxNPduRef|
|描述|Reference to a Pdu in the COM-Stack.|
|描述|概述：CanTpRxNPduRef是一个配置项，用于指定接收到的网络层协议数据单元（N-PDU）的引用，这是CAN传输协议（CanTp）模块处理接收消息所必需的。|
|描述|注意：确保每个CanTpRxNPduRef正确映射到相应的N-PDU，以保证消息的正确接收和处理；在配置时需注意与CAN驱动和PDU路由的一致性；该配置项的属性应与AUTOSAR CP 4.4标准保持一致，任何偏差都需要特别注意。|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/EcuC/EcucConfigSet/EcucPduCollection/Pdu|

##### 1.2.1.5. CanTpTxFcNPdu

|容器属性|值（容器）|
|---|---|
|名称|CanTpTxFcNPdu|
|描述|Used for grouping of the ID of a PDU and the Reference to a PDU. This N-PDU produces a meta data item of type CAN_ID_32.|
|描述|概述：CanTpTxFcNPdu 配置项用于定义CAN传输层（CAN Transport Layer）发送流控制帧的网络协议数据单元（N-PDU），它指定了发送流控制帧的CAN帧ID和DLC。|
|描述|注意：在配置CanTpTxFcNPdu时，必须确保所指定的CAN帧ID不与系统中其他N-PDU ID冲突；DLC值应符合CAN网络的数据长度要求；此配置应与接收方的期望流控制帧配置相匹配，以确保通信的正确性。|
|多实例个数|0 - 1|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CanTpTxFcNPduConfirmationPduId|
|描述|Handle Id to be used by the CanIf to confirm the transmission of the CanTpTxFcNPdu to the CanIf module.|
|描述|概述：CanTpTxFcNPduConfirmationPduId 是用于配置CAN传输层的参数，它指定了发送流控制帧N-PDU的确认消息的PDU ID。|
|描述|注意：在配置CanTpTxFcNPduConfirmationPduId时，必须确保所指定的PDU ID与系统中其他PDU ID不冲突；此ID应与发送流控制帧的N-PDU相对应；在配置时应参照ECU的CAN通信矩阵确保正确性。|
|多实例个数|1 - 1|
|默认值|0|
|取值范围|0 - 65535|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|CanTpTxFcNPduRef|
|描述|Reference to a Pdu in the COM-Stack.|
|描述|概述：CanTpTxFcNPduRef配置项用于定义传输层（CAN Transport Layer）在发送流控制帧（Flow Control Frame）时所使用的网络PDU（协议数据单元）的引用。|
|描述|注意：该配置项确保了流控制帧的正确发送，特别是在基于CAN网络的通信中；在配置时需确保引用的PDU与实际的CAN网络配置相匹配。|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/EcuC/EcucConfigSet/EcucPduCollection/Pdu|

#### 1.2.2. CanTpTxNSdu

|容器属性|值（容器）|
|---|---|
|名称|CanTpTxNSdu|
|描述|The following parameters needs to be configured for each CAN N-SDU that the CanTp module transmits via the CanTpChannel. This N-SDU consumes meta data items of type SOURCE_ADDRESS_16, TARGET_ADDRESS_16 and ADDRESS_EXTENSION_8.|
|描述|概述：CanTpTxNSdu配置中包含连接通道CAN N-SDU发送方向相关的所需的相关关键数据。|
|描述|注意：在配置CanTpTxNSdu时，必须确保NSDU的标识符在整个系统中是唯一的；根据AUTOSAR CP 4.4标准，需要正确设置地址信息和传输属性，以保证数据的正确发送和接收；配置时应注意与接收端的配置相匹配，避免通信错误。|
|多实例个数|0 - 1|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|CanTpTc|
|描述|Switch for enabling Transmit Cancellation.|
|描述|概述：CanTpTc是一个配置项，用于指定CAN传输层（CAN Transport Layer）是否支持传输控制，即是否允许对CAN消息的发送进行管理和控制。|
|描述|注意：在AUTOSAR CP 4.4标准中，确保在启用CanTpTc时，网络层已经配置为支持相应的传输控制功能；此配置项对于实现高级数据传输管理功能至关重要；不当的配置可能会影响网络通信的效率和可靠性。|
|多实例个数|1 - 1|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|CanTpTxAddressingFormat|
|描述|Declares which communication addressing format is supported for this TxNSdu. Definition of Enumeration values:|
|描述|概述：CanTpTxAddressingFormat配置项用于定义CAN传输层（CanTp）在发送帧的寻址方式。|
|描述|注意：在配置CanTpTxAddressingFormat时，需要确保它与网络上其他节点的寻址格式兼容；AUTOSAR CP 4.4标准支持标准寻址、扩展寻址和混合寻址模式；选择错误的寻址格式可能导致通信失败或数据解析错误。|
|说明|CanTpStandard to use normal addressing format. CanTpExtended to use extended addressing format. CanTpMixed to use mixed 11 bit addressing format. CanTpNormalFixed to use normal fixed addressing format. CanTpMixed29Bit to use mixed 29 bit addressing format.|
|多实例个数|1 - 1|
|默认值|CANTP_STANDARD|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|CanTpTxPaddingActivation|
|描述|Defines if the transmit frame use padding or not. This parameter is restricted to 8 byte N-PDUs.|
|描述|概述：CanTpTxPaddingActivation 是一个配置项，用于定义在使用CAN传输层进行发送操作时，是否激活填充功能，控制该通道报文是否填充。|
|描述|注意：在AUTOSAR CP 4.4标准中，确保此配置与PDU的长度和CAN控制器的填充功能设置相匹配。|
|说明|Definition of Enumeration values: CanTpOn The transmit N-PDU uses padding for SF, FC and the last CF. (N-PDU length is always 8 bytes in case of CAN 2.0) CanTpOff The transmit N-PDU does not use padding for SF, CF and the last CF. (N-PDU length is dynamic - any valid DLC value). Note: The mandatory mapping to the next higher valid DLC value for N-PDUs with a length \> 8 bytes is not affected by this parameter.|
|多实例个数|1 - 1|
|默认值|CANTP_ON|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|CanTpTxTaType|
|描述|Declares the communication type of this TxNsdu.|
|描述|概述：CanTpTxTaType配置项用于定义CAN传输层（CanTp）中发送端的地址类型，它决定了如何处理发送帧的地址信息。|
|描述|注意：在配置CanTpTxTaType时，需要确保它与网络上其他节点的地址类型兼容；此外，选择错误的地址类型可能导致通信失败或数据错误；AUTOSAR CP 4.4标准支持多种地址类型，包括物理地址和功能地址，需要根据实际应用场景选择合适的类型。|
|说明|Enumeration values: CanTpPhysical. Used for 1:1 communication. CanTpFunctional. Used for 1:n communication.|
|多实例个数|1 - 1|

|配置项属性|值（浮点型参数配置项）|
|---|---|
|名称|CanTpNas|
|描述|Value in second of the N_As timeout. N_As is the time for transmission of a CAN frame (any N_PDU) on the part of the sender.|
|描述|概述：CanTpNas 是用于定义 CAN 传输层的网络层服务数据单元（N-PDU）的发送确认超时时间，发送方发送任意类型数据帧（首帧、连续帧）的时长。|
|描述|注意：该值必须根据网络的实际条件和性能要求进行配置；超时时间设置过短可能导致在网络拥堵时无法正确确认消息，设置过长可能影响系统响应时间；在配置时需遵循相关的网络通信标准和协议要求。|
|多实例个数|1 - 1|
|默认值|0.025|
|取值范围|0 - Inf|

|配置项属性|值（浮点型参数配置项）|
|---|---|
|名称|CanTpNbs|
|描述|Value in seconds of the N_Bs timeout. N_Bs is the time of transmission until reception of the next Flow Control N_PDU.|
|描述|概述：CanTpNbs配置项定义了发送方任意动作结束到收到流控帧的时长。|
|描述|注意：N_Ar以网络层请求链路层发送（Receiver.req）为时间起点，以网络层收到链路层返回发送成功回执（Receiver.con）为时间终点；N_Bs可以以链路层返回首帧或连续帧发送成功（Sender.con）为时间起点，以链路层返回收到新的流控帧提示（Sender.ind）为时间终点；N_Bs可以以链路层返回连续帧发送成功（Sender.con）为时间起点，以链路层返回收到新的流控帧提示（Sender.ind）为时间终点；N_Bs可以以收到流控帧的提示（Sender.con）为时间起点，以链路层返回收到新的流控帧提示（Sender.ind）为时间终点。|
|多实例个数|0 - 1|
|默认值|0.075|
|取值范围|0 - Inf|

|配置项属性|值（浮点型参数配置项）|
|---|---|
|名称|CanTpNcs|
|描述|Value in seconds of the performance requirement of (N_Cs + N_As). N_Cs is the time in which CanTp is allowed to request the Tx data of a Consecutive Frame N_PDU.|
|描述|概述：CanTpNcs配置项定义了发送方动作结束到发送下一个连续帧的时长。|
|描述|注意：N_Cs可以以链路层提示收到流控帧（Sender.ind）为时间起点，以网络层请求链路层发送连续帧（Sender.req）为时间终点；N_Cs可以以返回连续帧发送成功（Sender.con）为时间起点，以网络层请求链路层发送新的连续帧（Sender.req）为时间终点。|
|多实例个数|0 - 1|
|默认值|0.05|
|取值范围|0 - Inf|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CanTpTxNSduId|
|描述|Unique identifier to a structure that contains all useful information to process the transmission of a TxNsdu.|
|描述|概述：CanTpTxNSduId是用于标识CAN传输层（CanTp）中特定发送NSDU（网络服务数据单元）的唯一标识符。|
|描述|注意：该SDU的编号，在CanTp_Transmit函数和CanTp_CancelTransmit函数调用流程中会使用。|
|多实例个数|1 - 1|
|默认值|0|
|取值范围|0 - 65535|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|CanTpTxNSduRef|
|描述|Reference to a Pdu in the COM-Stack.|
|描述|概述：CanTpTxNSduRef是一个配置项，用于引用发送端网络层服务数据单元（NSDU），它指定了CAN传输层（CanTp）用于发送数据的特定NSDU。|
|描述|注意：确保CanTpTxNSduRef正确引用了期望的NSDU配置，以保证数据能够正确发送；在配置时需注意与接收端NSDU的匹配性，避免数据发送到错误的目标；此配置项缺失会导致发送功能不可用。|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/EcuC/EcucConfigSet/EcucPduCollection/Pdu|

##### 1.2.2.1. CanTpNAe

|容器属性|值（容器）|
|---|---|
|名称|CanTpNAe|
|描述|This container is required for each RxNSdu and TxNSdu with AddressingFormat CANTP_MIXED or CANTP_MIXED29BIT.|
|多实例个数|0 - 1|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CanTpNAe|
|描述|This parameter contains the transport protocol address extension value.|
|描述|概述：CanTpNAe是用于定义网络地址扩展（Network Address Extension）的配置参数，它允许在CAN传输层（CAN Transport Layer）中支持多个网络地址，从而实现对不同节点的通信。|
|描述|注意：在使用CanTpNAe时，需要确保网络中的每个节点都支持网络地址扩展功能；此配置项在配置CAN通信时非常重要，以确保消息正确路由；AUTOSAR CP 4.4标准中并未直接提及CanTpNAe，因此具体实现可能会依赖于供应商的实现细节。|
|描述|该配置项未使用|
|多实例个数|1 - 1|
|取值范围|0 - 255|

##### 1.2.2.2. CanTpNSa

|容器属性|值（容器）|
|---|---|
|名称|CanTpNSa|
|描述|This container is required for each RxNSdu and TxNSdu with RxTaType CANTP_PHYSICAL and CanTpAddressingFormat CANTP_EXTENDED. When DynIdSupport is enabled, this container is also required for each TxNSdu with AddressingFormat CANTP_NORMALFIXED or CANTP_MIXED29BIT. When DynIdSupport is enabled and GenericConnectionSupport is not enabled, this container is also required for each RxNSdu with AddressingFormat CANTP_NORMALFIXED or CANTP_MIXED29BIT.|
|多实例个数|0 - 1|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CanTpNSa|
|描述|This parameter contains the transport protocol source address value.|
|描述|概述：CanTpNSa 配置项指定了用于CAN传输层的网络源地址，这是ISO-TP（ISO 15765-2）协议中的一部分，用于标识发送节点的地址信息。|
|描述|注意：在配置CanTpNSa时，需要确保地址值与网络中其他节点的源地址不冲突；此外，该值通常与车辆网络的地址分配方案一致；在AUTOSAR CP 4.4标准中，确保此配置项符合CAN传输层模块的要求。|
|描述|该配置项未使用|
|多实例个数|1 - 1|
|取值范围|0 - 255|

##### 1.2.2.3. CanTpNTa

|容器属性|值（容器）|
|---|---|
|名称|CanTpNTa|
|描述|This container is required for each RxNSdu and TxNSdu with AddressingFormat CANTP_EXTENDED. When DynIdSupport is enabled, this container is also required for each RxNSdu with AddressingFormat CANTP_NORMALFIXED or CANTP_MIXED29BIT. When DynIdSupport is enabled and GenericConnectionSupport is not enabled, this container is also required for each TxNSdu with AddressingFormat CANTP_NORMALFIXED or CANTP_MIXED29BIT.|
|多实例个数|0 - 1|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CanTpNTa|
|描述|This parameter contains the transport protocol target address value.|
|描述|概述：CanTpNTa 配置项定义了CAN传输层中的网络目标地址，用于区分不同的网络节点，确保CAN消息能够被正确地发送到预定的目标节点。|
|描述|注意：在配置CanTpNTa时，需要确保地址与网络中其他节点的地址不冲突；根据CAN网络的实际架构和通信需求来设置此地址；在AUTOSAR CP 4.4标准中，此配置应与PDU层的地址信息保持一致，以确保消息的正确路由。|
|描述|该配置项未使用|
|多实例个数|1 - 1|
|取值范围|0 - 255|

##### 1.2.2.4. CanTpRxFcNPdu

|容器属性|值（容器）|
|---|---|
|名称|CanTpRxFcNPdu|
|描述|Used for grouping of the ID of a PDU and the Reference to a PDU. This N-PDU consumes a meta data item of type CAN_ID_32.|
|描述|概述：CanTpRxFcNPdu 配置项为该路连接通道配置流控帧所需PDU引用，其中包括PduId和引用信息。|
|描述|注意：在配置CanTpRxFcNPdu时，PduId在普通寻址方式时与NSduId挂接，但是在扩展寻址等其他方式中，可能会存在多路复用的情况，需要同时考虑N_TA。|
|多实例个数|0 - 1|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CanTpRxFcNPduId|
|描述|N-PDU identifier attached to the FC N-PDU of this TxNsdu identified by CanTpTxNSduId.|
|描述|概述：CanTpRxFcNPduId是用于定义接收流控制帧的网络层协议数据单元（N-PDU）的标识符，它是CAN传输层配置中的一个元素，用于确保正确接收流控制信息。|
|描述|注意：该标识符必须是唯一的，以避免在网络上的冲突；在配置时需确保与发送流控制帧的N-PDU ID相匹配；在AUTOSAR CP 4.4标准中，确保该配置项符合网络管理和诊断消息的要求。|
|说明|Each TxNsdu identifier is linked to one Rx FC N-PDU identifier only. However, in the case of extended addressing format, the same FC N-PDU identifier can be used for several N-SDU identifiers. The distinction is made by means of the N_TA value (first data byte of FC frames).|
|多实例个数|1 - 1|
|默认值|0|
|取值范围|0 - 65535|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|CanTpRxFcNPduRef|
|描述|Reference to a Pdu in the COM-Stack.|
|描述|概述：CanTpRxFcNPduRef配置项用于定义接收流控制帧的网络层协议数据单元（N-PDU）的引用，确保在CAN传输层正确处理接收到的流控制帧。|
|描述|注意：该配置项必须确保引用的N-PDU与实际接收流控制帧的N-PDU匹配；在配置时需注意与其他N-PDU的唯一性和区分性，避免冲突；AUTOSAR CP 4.4标准中，确保该配置项的正确性对于实现基于CAN的网络通信的流控制至关重要。|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/EcuC/EcucConfigSet/EcucPduCollection/Pdu|

##### 1.2.2.5. CanTpTxNPdu

|容器属性|值（容器）|
|---|---|
|名称|CanTpTxNPdu|
|描述|Used for grouping of the ID of a PDU and the Reference to a PDU. This N-PDU produces a meta data item of type CAN_ID_32.|
|描述|概述：CanTpTxNPdu 配置项用于定义CAN传输层（CAN Transport Layer）中用于发送网络层协议数据单元（NPDU）的参数，这些参数包括PDU的ID、类型以及与之关联的CAN控制器等信息。|
|描述|注意：在配置CanTpTxNPdu时，必须确保PDU的ID在整个CAN网络中是唯一的，以避免冲突；需要与CAN驱动和网络管理配置相匹配，以确保正确的数据传输和网络行为；在配置过程中，应参照AUTOSAR CP 4.4标准中的相关规范来设置参数，确保配置的兼容性和标准性。|
|多实例个数|1 - 1|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CanTpTxNPduConfirmationPduId|
|描述|Handle Id to be used by the CanIf to confirm the transmission of the CanTpTxNPdu to the CanIf module.|
|描述|概述：CanTpTxNPduConfirmationPduId 是用于配置CAN传输层的参数，它指定了用于确认传输NPDU（网络协议数据单元）的PDU ID。|
|描述|注意：在配置CanTpTxNPduConfirmationPduId时，必须确保它与实际的CAN驱动层中定义的PDU ID相匹配；此ID应唯一地标识一个特定的确认PDU；在配置过程中，应避免与其他PDU ID发生冲突。|
|多实例个数|1 - 1|
|默认值|0|
|取值范围|0 - 65535|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|CanTpTxNPduRef|
|描述|Reference to a Pdu in the COM-Stack.|
|描述|概述：CanTpTxNPduRef是一个配置项，用于指定CAN传输层（CanTp）中用于网络层协议数据单元（NPDU）传输的引用，主要用于发送操作。|
|描述|注意：确保CanTpTxNPduRef正确指向有效的NPDU配置，以保证数据能够正确发送；在配置时需注意与接收NPDU的匹配和兼容性；此配置项在AUTOSAR CP 4.4中应与CAN驱动和网络管理模块的配置保持一致，以避免通信问题。|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/EcuC/EcucConfigSet/EcucPduCollection/Pdu|

## 2. CanTpGeneral

|容器属性|值（容器）|
|---|---|
|名称|CanTpGeneral|
|描述|This container contains the general configuration parameters of the CanTp module.|
|描述|概述：CanTpGeneral 是一个配置容器，为CanTp模块的通用配置项。|
|描述|注意：在配置CanTpGeneral时，需要确保参数设置符合网络的通信需求和性能指标。|
|多实例个数|1 - 1|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|CanTpChangeParameterApi|
|描述|This parameter, if set to true, enables the CanTp_ChangeParameterRequest Api for this Module.|
|描述|概述：CanTpChangeParameterApi 是一个配置项，此配置项允许在运行时更改参数，通过API调用。|
|描述|注意：类型为Boolean，控制是否使能CanTp_ChangeParameterRequest函数。|
|多实例个数|1 - 1|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|CanTpDevErrorDetect|
|描述|Switches the development error detection and notification on or off.|
|描述|概述：CanTpDevErrorDetect 是一个配置参数，类型为Boolean，控制是否使能本模块开发错误追踪问题。|
|描述|注意：true: 启用检测及通知；false: 禁用检测及通知；此功能用于支持开发阶段的问题定位，在正式版本中建议关闭。|
|说明|\* true: detection and notification is enabled. \* false: detection and notification is disabled.|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|CanTpDynIdSupport|
|描述|Enable support for dynamic ID handling via N-PDU MetaData.|
|描述|概述：CanTpDynIdSupport 配置项用于指定CAN传输层（CanTp）是否支持动态定义CAN标识符，这允许在运行时改变用于诊断或数据传输的CAN ID。|
|描述|注意：在AUTOSAR CP 4.4标准中，动态CAN ID支持是可选的，需要根据项目需求决定是否启���；如果启用此功能，需要确保上层服务和应用能够适应动态ID的变化；在配置时，应检查ECU硬件和CAN驱动是否支持动态ID的配置和更改。|
|描述|该配置项未使用|
|多实例个数|0 - 1|
|默认值|false|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|CanTpFlexibleDataRateSupport|
|描述|Enable support for CAN FD frames.|
|描述|概述：CanTpFlexibleDataRateSupport配置项用于指定CAN传输层（CanTp模块）启用对CAN FD帧的支持。|
|描述|注意：类型为Boolean，控制是否支持CAN FD（Flexible Data-Rate）。|
|多实例个数|0 - 1|
|默认值|true|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|CanTpGenericConnectionSupport|
|描述|Enable support for the handling of generic connections using N-SDUs with MetaData. Requires CanTpDynIdSupport.|
|描述|概述：CanTpGenericConnectionSupport 是一个配置项，用于指定CAN传输层（CanTp模块）是否支持泛型连接管理，这可以提高模块的灵活性，允许它处理不同类型的通信连接。|
|描述|注意：在AUTOSAR CP 4.4标准中，确保在使用泛型连接支持时，相关的PDU路由配置正确；此功能可能会增加模块的复杂性和资源消耗；如果应用场景不需要泛型连接，可以关闭此功能以节省资源。|
|描述|该配置项未使用|
|多实例个数|0 - 1|
|默认值|false|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|CanTpEnableSynchronousTransmit|
|描述|If this option is enabled, the CanTp will try to get a buffer and to transmit the FF or SF directly from the context of CanTp_Transmit. Otherwise, buffer request and transmission will be done during the next CanTp_MainFunction call.|
|描述|概述：CanTpEnableSynchronousTransmit 配置项用于确定CAN传输层（CanTp）是否支持同步发送功能。|
|描述|注意：该配置项为非标配置项，类型为Boolean，控制是否支持同步发送。|
|多实例个数|1 - 1|
|默认值|true|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|CanTpReadParameterApi|
|描述|This parameter, if set to true, enables the CanTp_ReadParameterApi for this module.|
|描述|概述：CanTpReadParameterApi 配置项用于启用或禁用传输层读取参数的API。|
|描述|注意：类型为Boolean，控制是否使能CanTp_ReadParameter函数。|
|多实例个数|1 - 1|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|CanTpVersionInfoApi|
|描述|The function CanTp_GetVersionInfo is configurable (On/Off) by this configuration parameter.|
|描述|概述：CanTpVersionInfoApi 配置项用于启用或禁用 CAN 传输层的版本信息API，该API允许用户获取CAN传输层模块的版本信息。|
|描述|注意：在AUTOSAR CP 4.4标准中，版本信息API的使用是可选的；如果启用，必须确保模块实现了相应的API函数；在发布产品时，出于节省资源的考虑，通常建议禁用此API。|
|描述|该配置项未使用|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CanTpPaddingByte|
|描述|Used for the initialization of unused bytes with a certain value|
|描述|概述：CanTpPaddingByte 是用于定义在传输层（CAN Transport Layer）发送CAN帧时，填充剩余字节的值。|
|描述|注意：类型为Int，用于填充的数据，ISO-15765-2默认配置为0xCC。|
|多实例个数|1 - 1|
|默认值|85|
|取值范围|0 - 255|
