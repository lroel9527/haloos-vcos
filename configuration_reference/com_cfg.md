# Com 配置项参考文档

|容器属性|值（容器）|
|---|---|
|名称|Com|
|描述|Configuration of the AUTOSAR COM module.|
|描述|概述：Com模块是AUTOSAR通信堆栈的一部分，负责处理应用层和底层网络之间的信号传输，包括信号打包、解包、路由和过滤等功能。|
|描述|注意：在配置Com模块时，需要确保信号和PDU的映射关系符合项目要求；配置的周期性发送和接收时间参数应满足网络带宽和系统实时性要求；遵循AUTOSAR CP 4.4标准中对Com配置参数的规范，以确保模块的正确性和兼容性。|
|多实例个数|0 - 1|

## 1. ComConfig

|容器属性|值（容器）|
|---|---|
|名称|ComConfig|
|描述|This container contains the configuration parameters and sub containers of the AUTOSAR COM module.|
|描述|概述：ComConfig是AUTOSAR通信堆栈的配置容器，它包含了用于配置通信相关功能的参数，如PDU（协议数据单元）的路由策略、IPDU（交互协议数据单元）的定时参数等。|
|描述|注意：在配置ComConfig时，必须确保所有的参数与系统的通信需求相匹配，并且遵循AUTOSAR CP 4.4标准中定义的数据类型和结构；配置项的属性应当与AUTOSAR规范中的模块配置参数一致，以保证通信堆栈的正确性和可靠性；在多个ECU间共享数据时，需要特别注意PDU的一致性和同步问题。|
|多实例个数|1 - 1|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|ComDataMemSize|
|描述|Size of internal Com data in units of bytes (static memory allocation) - memory required by post-build configuration must be smaller than this constant. This parameter is needed only in case of post-build loadable implementation using static memory allocation.|
|描述|概述：ComDataMemSize配置项指定了通信堆栈中用于存储PDU（协议数据单元）的数据区域的大小，确保足够的内存空间用于数据交换。|
|描述|注意：必须确保配置的ComDataMemSize足够大，以容纳所有激活的PDU的最大数据量；过小的配置可能导致数据丢失或通信故障；在AUTOSAR CP 4.4中，该配置项的具体数值需根据系统需求和PDU大小合理计算。|
|描述|该配置项未使用|
|多实例个数|0 - 1|
|取值范围|0 - 18446744073709551615|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|ComMaxIPduCnt|
|描述|Maximum number of IPdus. This parameter is needed only in case of post-build loadable implementation using static memory allocation.|
|描述|概述：ComMaxIPduCnt 配置项定义了在AUTOSAR Communication Stack中，IPdu（即“Interaction Protocol Data Unit”，交互协议数据单元）的最大数量，这是为了限制系统中可管理的IPdu数量。|
|描述|注意：在配置ComMaxIPduCnt时，需要确保其值足以支持系统中所有的IPdu；过小的值可能导致无法配置所有必要的IPdu，而过大的值可能会浪费资源；此配置项的合理设置应基于系统需求和资源限制进行权衡。|
|描述|该配置项未使用|
|多实例个数|0 - 1|
|取值范围|0 - 18446744073709551615|

### 1.1. ComGwMapping

|容器属性|值（容器）|
|---|---|
|名称|ComGwMapping|
|描述|Each instance of this container defines one mapping of the integrated Signal Gateway.|
|描述|概述：ComGwMapping 用于定义通信网关的映射关系，它指定了如何在不同的通信对象之间转发消息。|
|描述|注意：确保映射关系不会导致数据循环或冗余传输；映射配置应符合网络带宽和延迟要求；在配置时需考虑消息的优先级和安全性要求。|
|多实例个数|0 - inf|

#### 1.1.1. ComGwDestination

|容器属性|值（容器）|
|---|---|
|名称|ComGwDestination|
|描述|Each instance of this choice container allows to define one routing destination either by reference to an already configured COM signal / group signal or by a destination description container.|
|描述|概述：ComGwDestination配置项用于定义通信网关中目的地的参数，这包括目标PDU（协议数据单元）的ID和目标PDU的类型，确保数据能正确地从源传输到预定的目标。|
|描述|注意：在配置ComGwDestination时，必须确保目标PDU的ID在整个系统中是唯一的；目标PDU类型应与系统中其他配置的PDU类型保持一致，避免类型不匹配导致的通信故障；AUTOSAR CP 4.4标准中对于通信网关的配置有详细规范，需要遵循这些规范以保证系统的兼容性和稳定性。|
|多实例个数|1 - inf|

##### 1.1.1.1. ComGwDestinationDescription

|容器属性|值（容器）|
|---|---|
|名称|ComGwDestinationDescription|
|描述|Description of a gateway destination. This container allows defining a gateway destination without the configuration of a complete COM signal. This allows adding / changing gateway relations post build without the configuration of new signals.|
|描述|概述：ComGwDestinationDescription配置项用于描述通信网关中目的地消息的详细信息，包括目标PDU的ID、目标PDU的类型等，以便正确地将源消息转发到指定的目的地。|
|描述|注意：在配置时需确保目标PDU的ID与系统中其他PDU的ID不冲突；正确指定目标PDU的类型，以匹配消息的传输协议和格式；在多目的地转发场景中，需详细规划每个目的地的配置，以避免消息转发错误或丢失。|
|描述|该配置项未使用|
|多实例个数|0 - 1|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|ComSignalEndianness|
|描述|Defines the endianness of the signal's network representation.|
|多实例个数|1 - 1|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|ComTransferProperty|
|描述|Defines if a write access to this signal can trigger the transmission of the corresponding I-PDU. If the I-PDU is triggered, depends also on the transmission mode of the corresponding I-PDU.|
|多实例个数|0 - 1|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|ComBitPosition|
|描述|Starting position within the I-PDU. This parameter refers to the position in the I-PDU and not in the shadow buffer. If the endianness conversion is configured to Opaque the parameter ComBitPosition shall define the bit0 of the first byte like in little endian byte order|
|多实例个数|1 - 1|
|取值范围|0 - 4294967295|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|ComUpdateBitPosition|
|描述|Bit position of update-bit inside I-PDU.|
|说明|If this attribute is omitted then there is no update-bit. This setting must be consistently on sender and on receiver side. Range: 0..63 for CAN and LIN, 0..511 for CAN FD, 0..2031 for FlexRay, 0..4294967295 for TP.|
|多实例个数|0 - 1|
|取值范围|0 - 4294967295|

|配置项属性|值（字符串参数配置项）|
|---|---|
|名称|ComSignalInitValue|
|描述|Initial value for this signal. In case of UINT8_N the default value is a string of length ComSignalLength with all bytes set to 0x00. In case of UINT8_DYN the initial size shall be 0.|
|说明|In case the ComSignalType is UINT8, UINT16, UINT32, UINT64, SINT8, SINT16, SINT32, SINT64 the string shall be interpreted as defined in the chapter Integer Type in the AUTOSAR EcuC specification. In case the ComSignalType is FLOAT32, FLOAT64 the string shall be interpreted as defined in the chapter Float Type in the AUTOSAR EcuC specification. In case the ComSignalType is BOOLEAN the string shall be interpreted as defined in the chapter Boolean Type in the AUTOSAR EcuC specification. In case the ComSignal is a UINT8_N, UINT8_DYN the string shall be interpreted as a decimal representation of the characters separated by blanks, e.g. "97 98 100" means a string "abd", where the char "a" is in byte 0(lowest address), "b" is in byte 1, and "d" is in byte 2 and (highest address). For the ComSignalType UINT8_DYN the dynamic length shall be set to the number of configured characters. An empty string "" shall be interpreted as 0-sized dynamic signal.|
|多实例个数|0 - 1|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|ComGwIPduRef|
|描述|Reference to an I-PDU of a Signal Gateway source or destination description.|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Com/ComConfig/ComIPdu|

###### 1.1.1.1.1. ComFilter

|容器属性|值（容器）|
|---|---|
|名称|ComFilter|
|描述|This container contains the configuration parameters of the AUTOSAR COM module's Filters.|
|说明|Note: On sender side the container is used to specify the transmission mode conditions.|
|多实例个数|0 - 1|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|ComFilterAlgorithm|
|描述|The range of values is specified in the [17] specification, chapter 2.2.2, Reception Filtering.|
|多实例个数|1 - 1|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|ComFilterMask|
|描述|The name of this attribute corresponds to the parameter name in the [17] specification of Reception Filtering.|
|多实例个数|0 - 1|
|取值范围|-2147483648 - 4294967295|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|ComFilterMax|
|描述|The name of this attribute corresponds to the parameter name in the [17] specification of Reception Filtering.|
|多实例个数|0 - 1|
|取值范围|-2147483648 - 4294967295|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|ComFilterMin|
|描述|The name of this attribute corresponds to the parameter name in the [17] specification of Reception Filtering.|
|多实例个数|0 - 1|
|取值范围|-2147483648 - 4294967295|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|ComFilterOffset|
|描述|The name of this attribute corresponds to the parameter name in the [17] specification of Reception Filtering.|
|说明|Range = 0..(ComFilterPeriod-1)|
|多实例个数|0 - 1|
|取值范围|0 - 4294967294|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|ComFilterPeriod|
|描述|This parameter defines the period of the ComFilterAlgorithm ONE_EVERY_N.|
|多实例个数|0 - 1|
|取值范围|2 - 4294967295|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|ComFilterX|
|描述|The name of this attribute corresponds to the parameter name in the [17] specification of Reception Filtering.|
|多实例个数|0 - 1|
|取值范围|-2147483648 - 4294967295|

##### 1.1.1.2. ComGwSignal

|容器属性|值（容器）|
|---|---|
|名称|ComGwSignal|
|描述|This container allows specifying a gateway source or destination respectively with a reference to a ComSignal or a ComGroupSignal.|
|多实例个数|0 - 1|

|配置项属性|值（选择引用配置项）|
|---|---|
|名称|ComGwSignalRef|
|描述|Reference to an object of a gateway relation. Either to a ComSignal or a ComGroupSignal.|
|多实例个数|1 - 1|
|目标引用|/AUTOSAR/EcucDefs/Com/ComConfig/ComSignalGroup/ComGroupSignal/AUTOSAR/EcucDefs/Com/ComConfig/ComSignal|

#### 1.1.2. ComGwSource

|容器属性|值（容器）|
|---|---|
|名称|ComGwSource|
|描述|This choice container allows the definition of the gateway source signal either by reference to an already configured COM signal / group signal or by a source description container.|
|描述|概述：ComGwSource 配置项定义了通信网关的源PDU（协议数据单元），即指定了哪些PDU将被网关模块接收并可能进行路由或转换到其他PDU。|
|描述|注意：在配置ComGwSource时，需要确保源PDU与目标PDU之间的映射关系正确无误；源PDU标识符必须在系统中是唯一的；在配置过程中应考虑PDU的大小、格式以及转换规则，以确保数据的正确传输和处理。|
|多实例个数|1 - 1|

##### 1.1.2.1. ComGwSignal

|容器属性|值（容器）|
|---|---|
|名称|ComGwSignal|
|描述|This container allows specifying a gateway source or destination respectively with a reference to a ComSignal or a ComGroupSignal.|
|描述|概述：ComGwSignal配置项用于定义网关通信中的信号转发规则，包括源信号和目标信号之间的映射关系，以实现不同网络间的数据交换。|
|描述|注意：在配置ComGwSignal时，需确保源信号和目标信号的数据类型和大小兼容；对于周期性和事件触发的信号，还需考虑转发策略以满足实时性要求；AUTOSAR CP 4.4标准中，对于网关信号的配置和管理提供了详细的规范，确保遵循这些规范以保证系统的互操作性和稳定性。|
|多实例个数|0 - 1|

|配置项属性|值（选择引用配置项）|
|---|---|
|名称|ComGwSignalRef|
|描述|Reference to an object of a gateway relation. Either to a ComSignal or a ComGroupSignal.|
|多实例个数|1 - 1|
|目标引用|/AUTOSAR/EcucDefs/Com/ComConfig/ComSignalGroup/ComGroupSignal/AUTOSAR/EcucDefs/Com/ComConfig/ComSignal|

##### 1.1.2.2. ComGwSourceDescription

|容器属性|值（容器）|
|---|---|
|名称|ComGwSourceDescription|
|描述|Description of a gateway source. This container allows defining a gateway source without the configuration of a complete COM signal. This allows adding / changing gateway relations post build without the configuration of new signals.|
|描述|概述：ComGwSourceDescription配置项用于描述通信网关（ComGw）中源PDU（协议数据单元）的属性，包括源PDU的标识符、长度等信息，以便正确处理和转发来自不同源的数据。|
|描述|注意：在配置ComGwSourceDescription时，必须确保源PDU标识符的唯一性和正确性，以防数据转发错误；源PDU的长度信息需要与实际匹配，以确保数据的完整性；AUTOSAR CP 4.4标准中对通信网关的配置和管理提供了详细的规范，需要遵循这些规范以保证系统的兼容性和稳定性。|
|描述|该配置项未使用|
|多实例个数|0 - 1|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|ComSignalEndianness|
|描述|Defines the endianness of the signal's network representation.|
|多实例个数|1 - 1|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|ComSignalType|
|描述|The AUTOSAR type of the signal. Whether or not the signal is signed or unsigned can be found by examining the value of this attribute.|
|说明|This type could also be used to reserved appropriate storage in AUTOSAR COM.|
|多实例个数|1 - 1|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|ComBitPosition|
|描述|Starting position within the I-PDU. This parameter refers to the position in the I-PDU and not in the shadow buffer. If the endianness conversion is configured to Opaque the parameter ComBitPosition shall define the bit0 of the first byte like in little endian byte order|
|多实例个数|1 - 1|
|取值范围|0 - 4294967295|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|ComBitSize|
|描述|Size in bits, for integer signal types. For ComSignalType UINT8_N and UINT8_DYN|
|说明|the size shall be configured by ComSignalLength. For ComSignalTypes FLOAT32 and FLOAT64 the size is already defined by the signal type and therefore may be omitted.|
|多实例个数|0 - 1|
|取值范围|0 - 64|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|ComSignalLength|
|描述|Description:|
|说明|For ComSignalType UINT8_N this parameter specifies the length n in bytes. For ComSignalType UINT8_DYN it specifies the maximum length in bytes. For all other types this parameter shall be ignored. The supported maximum length is restricted by the used transportation system. For non TP-PDUs the maximum size of a PDU, and therefore also of any included signal, is limited by the concrete bus characteristic. For example, the limit is 8 bytes for CAN and LIN, 64 bytes for CAN FD and 254 for FlexRay.|
|多实例个数|0 - 1|
|取值范围|0 - 4294967295|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|ComUpdateBitPosition|
|描述|Bit position of update-bit inside I-PDU.|
|说明|If this attribute is omitted then there is no update-bit. This setting must be consistently on sender and on receiver side. Range: 0..63 for CAN and LIN, 0..511 for CAN FD, 0..2031 for FlexRay, 0..4294967295 for TP.|
|多实例个数|0 - 1|
|取值范围|0 - 4294967295|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|ComGwIPduRef|
|描述|Reference to an I-PDU of a Signal Gateway source or destination description.|
|描述|概述：ComGwIPduRef 是一个配置项，用于引用在通信网关中需要路由的IPDU（即数据包单元）。|
|描述|注意：在配置通信网关时，必须确保引用的IPDU在系统中是存在且有效的；ComGwIPduRef 应该与相应的源IPDU和目标IPDU配置一致；在AUTOSAR CP 4.4标准中，通信网关的配置应遵循模块间通信原则，确保数据的正确路由和转发。|
|描述|该配置项未使用|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Com/ComConfig/ComIPdu|

### 1.2. ComIPdu

|容器属性|值（容器）|
|---|---|
|名称|ComIPdu|
|描述|Contains the configuration parameters of the AUTOSAR COM module's I-PDUs.|
|描述|概述：ComIPdu是AUTOSAR通信堆栈中的一个配置项，用于定义传输层与网络层之间的接口数据单元（PDU），它封装了网络层的数据。|
|描述|注意：确保每个ComIPdu的ID在系统中是唯一的；正确配置ComIPdu的大小和属性以匹配网络层的需求；在配置时需考虑数据的发送和接收策略，以保证数据传输的效率和可靠性。|
|多实例个数|0 - inf|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|ComIPduCancellationSupport|
|描述|Defines for I-PDUs with ComIPduType NORMAL: If the underlying IF-modul supports cancellation of transmit requests.|
|描述|概述：ComIPduCancellationSupport 配置项用于定义是否支持IPDU（协议数据单元）的取消功能，以便在网络通信中动态管理数据传输。|
|描述|注意：在AUTOSAR CP 4.4中，确保该功能与底层通信堆栈兼容；此功能可能影响系统的实时性和带宽利用率；在设计时需考虑其对系统性能的潜在影响。|
|描述|该配置项未使用|
|说明|Defines for I-PDUs with ComIPduType TP: If the underlying TP-module supports RX and TX cancellation of ongoing requests.|
|多实例个数|0 - 1|
|默认值|false|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|ComIPduDirection|
|描述|The direction defines if this I-PDU, and therefore the contributing signals and signal groups, shall be sent or received.|
|描述|概述：ComIPduDirection配置项用于定义通信接口协议数据单元（IPDU）的传输方向，指明是发送方向（发送到网络）还是接收方向（从网络接收）。|
|描述|注意：在定义ComIPdu时必须明确指定方向，因为这将影响消息处理的逻辑和配置；确保与网络管理和诊断需求相一致；AUTOSAR CP 4.4中此配置项的属性与方向定义一致，无需特别注意版本兼容性问题。|
|多实例个数|1 - 1|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|ComIPduSignalProcessing|
|描述|For the definition of the two modes Immediate and Deferred.|
|描述|概述：ComIPduSignalProcessing配置项定义了IPDU（即消息）中的信号处理模式，它决定了信号更新的时机，例如是否在发送时立即更新或者在接收时延迟更新。|
|描述|注意：在配置ComIPduSignalProcessing时，需要确保它与系统中的通信需求相匹配；选择错误的信号处理模式可能会导致通信延迟或数据一致性问题；此外，AUTOSAR CP 4.4标准中可能有特定的限制或默认值，需要根据标准文档进行正确配置。|
|多实例个数|1 - 1|
|默认值|DEFERRED|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|ComIPduType|
|描述|Defines if this I-PDU is a normal I-PDU that can be sent unfragmented or if this is a large I-PDU that shall be sent via the Transport Protocol of the underlying bus.|
|描述|概述：ComIPduType 是一个枚举类型，用于指定通信接口协议数据单元（IPDU）的类型，例如是否为正常、DM或NM消息。|
|描述|注意：在配置ComIPdu时，必须确保选择正确的ComIPduType以匹配消息的用途和行为；错误的类型可能导致消息处理不正确；AUTOSAR CP 4.4标准中可能有特定的限制和要求，需要根据标准文档进行配置。|
|多实例个数|1 - 1|
|默认值|NORMAL|

|配置项属性|值（函数名配置项）|
|---|---|
|名称|ComIPduCallout|
|描述|This parameter defines the existence and the name of a callout function for the corresponding I-PDU. If this parameter is omitted no I-PDU callout shall take place for the corresponding I-PDU.|
|描述|概述：ComIPduCallout 是一个配置项，用于定义在发送或接收IPDU（协议数据单元）时调用的用户定义函数，以实现特定的数据处理或验证逻辑。|
|描述|注意：确保定义的Callout函数符合实时性要求和数据处理安全性；该函数应避免执行过长时间的操作，以免影响系统的响应时间；在配置时应确保函数与IPDU的兼容性，避免数据类型或大小不匹配的问题。|
|多实例个数|0 - 1|

|配置项属性|值（函数名配置项）|
|---|---|
|名称|ComIPduTriggerTransmitCallout|
|描述|If there is a trigger transmit callout defined for this I-PDU this parameter contains the name of the callout function.|
|描述|概述：ComIPduTriggerTransmitCallout 是一个配置项，用于指定一个回调函数，该函数在IPDU（即消息）需要被发送之前被调用，以便动态更新IPDU的内容。|
|描述|注意：确保为每个需要此功能的IPDU正确配置了回调函数；回调函数需要遵循AUTOSAR标准中定义的原型和行为；在配置时要注意不要引入额外的延迟，以免影响消息的及时发送。|
|多实例个数|0 - 1|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|ComIPduHandleId|
|描述|The numerical value used as the ID of this I-PDU. The ComIPduHandleId is required by the API calls Com_RxIndication, Com_TpRxIndication, Com_StartOfReception and Com_CopyRxData to receive I-PDUs from the PduR (ComIP-duDirection: Receive), as well as the PduId passed to an Rx-I-PDU-callout. For Tx-I-PDUs (ComIPduDirection: Send), this handle Id is used for the APIs calls Com_TxConfirmation, Com_TriggerTransmit, Com_TriggerIPDUSend or Com_TriggerIPDUSendWithMetaData, Com_CopyTxData and Com_TpTxConfirmation to transmit respectively confirm transmissions of I-PDUs, as well as the PduId passed to the Tx-I-PDU-callout configured with ComIPduCallout and/or ComIPduTriggerTransmitCallout.|
|描述|概述：ComIPduHandleId 是用于唯一标识每个I-PDU（即“协议数据单元”）的句柄，它在AUTOSAR Communication Stack中用于访问和管理I-PDUs。|
|描述|注意：ComIPduHandleId 必须在整个项目范围内是唯一的；在配置过程中应确保没有重复的句柄ID，以避免数据传输错误；在AUTOSAR CP 4.4标准中，句柄ID通常由配置工具自动生成，以减少人为错误。|
|多实例个数|0 - 1|
|取值范围|0 - 65535|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|ComIPduGroupRef|
|描述|Reference to the I-PDU groups this I-PDU belongs to.|
|多实例个数|0 - inf|
|目标引用项的路径|/AUTOSAR/EcucDefs/Com/ComConfig/ComIPduGroup|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|ComIPduSignalGroupRef|
|描述|References to all signal groups contained in this I-Pdu|
|多实例个数|0 - inf|
|目标引用项的路径|/AUTOSAR/EcucDefs/Com/ComConfig/ComSignalGroup|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|ComIPduSignalRef|
|描述|References to all signals contained in this I-PDU.|
|多实例个数|0 - inf|
|目标引用项的路径|/AUTOSAR/EcucDefs/Com/ComConfig/ComSignal|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|ComPduIdRef|
|描述|Reference to the "global" Pdu structure to allow harmonization of handle IDs in the COM-Stack.|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/EcuC/EcucConfigSet/EcucPduCollection/Pdu|

|配置项属性|值（选择引用配置项）|
|---|---|
|名称|IPduMainFunctionRef|
|描述|Reference to the "global" Pdu structure to allow harmonization of MainFunction in the COM-Stack.|
|多实例个数|1 - 1|
|目标引用|/AUTOSAR/EcucDefs/Com/ComConfig/ComMainFunctionRx/AUTOSAR/EcucDefs/Com/ComConfig/ComMainFunctionTx|

#### 1.2.1. ComIPduCounter

|容器属性|值（容器）|
|---|---|
|名称|ComIPduCounter|
|描述|This optional container contains the configuration parameters of PDU Counter.|
|描述|概述：ComIPduCounter 是用于配置IPDU（协议数据单元）的计数器属性，这有助于确保数据传输的完整性和顺序。|
|描述|注意：确保每个IPDU配置有正确的计数器属性，以便于错误检测和重传机制的实现；计数器的大小和溢出行为应符合系统的具体需求；在配置时需考虑与接收方的兼容性。|
|描述|该配置项未使用|
|多实例个数|0 - 1|

|配置项属性|值（函数名配置项）|
|---|---|
|名称|ComIPduCounterErrorNotification|
|描述|Name of Com_CbkCounterErr callback function to be called. If this|
|描述|概述：ComIPduCounterErrorNotification用于定义一个回调函数，该函数在检测到IPDU（协议数据单元）计数器错误时被调用，用于处理或报告错误情况。|
|描述|注意：确保回调函数的实现不会引入额外的延迟，特别是在实时系统中；该回调函数应仅用于错误处理或诊断目的，避免在此函数中执行复杂逻辑；在配置时需确保该回调函数与系统中的错误处理策略一致。|
|描述|该配置项未使用|
|说明|parameter is omitted no I-PDU counter mismatch notification shall take place.|
|多实例个数|0 - 1|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|ComIPduCounterSize|
|描述|Size of PDU Counter expressed in bits|
|描述|概述：ComIPduCounterSize 配置项定义了用于AUTOSAR通信堆栈中IPDU（即消息或数据包）的计数器大小，这个计数器用于支持发送和接收消息的一致性和顺序检查。|
|描述|注意：在配置ComIPduCounterSize时，需要确保计数器大小与系统中用于消息传输的数据类型兼容；此外，计数器大小应足以支持系统预期的消息传输频率和顺序要求；在选择计数器大小时，还应考虑到内存占用和性能影响的平衡。|
|描述|该配置项未使用|
|多实例个数|1 - 1|
|取值范围|1 - 8|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|ComIPduCounterStartPosition|
|描述|Position of PDU counter expressed in bits from start position of data content|
|描述|概述：ComIPduCounterStartPosition 配置项用于指定在IPDU（即消息）中，用于传输计数器值的字节的起始位置，这有助于确保消息的一致性和顺序。|
|描述|注意：在配置时需确保计数器的位置不与其他信号或数据重叠；计数器的大小和位置应符合网络协议的要求；在配置多个计数器时，要注意它们之间的相互影响和整个消息的布局。|
|描述|该配置项未使用|
|说明|of I-PDU (SDU). Note that PDU counter is not allowed to cross a byte border. The parameter ComIPduCounterStartPosition shall define the bit0 of the first byte like in little endian byte order.|
|多实例个数|1 - 1|
|取值范围|0 - 4294967295|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|ComIPduCounterThreshold|
|描述|Threshold value of I-PDU counter algorithm, see ECUC_Com_00590.|
|描述|概述：ComIPduCounterThreshold定义了在IPDU（Internet Protocol Data Unit）中，接收到的消息计数器达到多少次后，系统认为该消息是有效的，用于防止消息丢失或错误。|
|描述|注意：该阈值应根据网络的具体情况和消息重要性来设置，以避免过高导致消息延迟处理或过低导致错误消息被误认为有效；在AUTOSAR CP 4.4中，确保该配置与PDU的类型和用途相匹配；调整此阈值时，还需考虑系统的容错能力和性能要求。|
|描述|该配置项未使用|
|多实例个数|0 - 1|
|默认值|0|
|取值范围|0 - 255|

#### 1.2.2. ComIPduReplication

|容器属性|值（容器）|
|---|---|
|名称|ComIPduReplication|
|描述|This optional container contains the information needed for each I-PDU replicated.|
|描述|概述：ComIPduReplication配置项用于定义如何将传入的IPDU（协议数据单元）复制到一个或多个目标IPDU中，这在实现消息的分发和重映射时非常有用。|
|描述|注意：在使用ComIPduReplication时，需要确保源IPDU和目标IPDU之间的数据映射关系正确配置，以避免数据不一致；此外，考虑到性能和资源利用率，应谨慎选择复制的目标IPDU数量；AUTOSAR CP 4.4标准中对于IPDU复制的具体实现细节有明确规定，需要遵循这些规定以保证系统的兼容性和可靠性。|
|描述|该配置项未使用|
|多实例个数|0 - 1|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|ComIPduReplicationQuorum|
|描述|The number of identical I-PDUs needed for successful voting.|
|描述|概述：ComIPduReplicationQuorum 配置项用于定义在IPDU复制机制中所需的最小响应数（quorum），以确保数据的一致性和可靠性。|
|描述|注意：在配置ComIPduReplicationQuorum时，必须确保设置的值能够反映系统中冗余通信路径的数量和可靠性要求；该值不应超过参与复制的节点总数；在实现复制机制时，应考虑系统的性能和延迟要求。|
|描述|该配置项未使用|
|多实例个数|1 - 1|
|取值范围|1 - 3|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|ComIPduReplicaRef|
|描述|Reference to replicas PduR PDUs of this IPDU.|
|描述|概述：ComIPduReplicaRef是一个配置项，用于指定一个IPDU副本的引用，这使得原始IPDU可以有一个或多个副本，以支持不同的通信需求或数据冗余策略。|
|描述|注意：在使用ComIPduReplicaRef时，需要确保引用的IPDU副本配置正确，避免数据不一致；此配置项在设计系统通信策略时尤为重要，以确保数据的可靠性和一致性；AUTOSAR CP 4.4标准中，对IPDU副本的支持可能受限于具体的通信堆栈实现，因此在应用此配置项时应仔细检查堆栈的支持情况。|
|描述|该配置项未使用|
|多实例个数|1 - 2|
|目标引用项的路径|/AUTOSAR/EcucDefs/EcuC/EcucConfigSet/EcucPduCollection/Pdu|

#### 1.2.3. ComTxIPdu

|容器属性|值（容器）|
|---|---|
|名称|ComTxIPdu|
|描述|This container contains additional transmission related configuration parameters of the AUTOSAR COM module's I-PDUs.|
|描述|概述：ComTxIPdu是AUTOSAR通信堆栈中的配置参数，用于定义传输IPDU（即数据包）的属性，包括IPDU的标识符、大小、发送方式和发送周期等。|
|描述|注意：在配置ComTxIPdu时，必须确保IPDU标识符的唯一性，避免与其他IPDU冲突；发送周期和发送方式应根据网络带宽和系统实时性要求合理设置；在配置时还需考虑与网络管理策略的兼容性，确保数据传输的可靠性和效率。|
|多实例个数|0 - 1|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|ComTxIPduClearUpdateBit|
|描述|Defines when the update-bits of signals or signal groups, contained in this I-PDU, will be cleared.|
|描述|概述：ComTxIPduClearUpdateBit 配置项用于定义在发送IPDU（协议数据单元）后是否自动清除更新位，这有助于管理消息的发送状态。|
|描述|注意：在配置此项时，确保理解其对消息传输完整性和重复性的影响；不正确的配置可能导致接收方接收到过时或重复的数据；AUTOSAR CP 4.4标准支持此配置，无需特别注意版本兼容性问题。|
|多实例个数|0 - 1|

|配置项属性|值（浮点型参数配置项）|
|---|---|
|名称|ComMinimumDelayTime|
|描述|Defines the Minimum Delay Time (MDT) between successive transmissions of this I-PDU in seconds. The MDT is independent of the possible different transmission modes. There is only one minimum delay time parameter for one I-PDU. The minimum delay timer is not reset by changing the transmission mode. Hence, it is not allowed to violate the minimum delay time by transmission mode changes. It is not possible to monitor the minimum delay time for I-PDUs that are requested using the Com_TriggerTransmit API.|
|描述|概述：ComMinimumDelayTime 定义了在发送两个连续的IPDU之间必须等待的最小时间间隔，以防止网络拥塞和数据冲突。|
|描述|注意：该参数的设置应考虑网络的带宽和性能要求；过小的延迟时间可能导致网络冲突，过大的延迟时间可能影响消息的实时性；在配置时需遵循AUTOSAR CP 4.4标准中对时间间隔的具体要求。|
|多实例个数|0 - 1|
|取值范围|0 - 3600|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|ComTxIPduUnusedAreasDefault|
|描述|The AUTOSAR COM module fills not used areas of an I-PDU with this byte pattern. This attribute is mandatory to avoid undefined behaviour. This byte-pattern will be repeated throughout the I-PDU before any init-values or update-bits were set.|
|描述|概述：ComTxIPduUnusedAreasDefault 配置项用于定义在发送IPDU（协议数据单元）时未使用区域的默认值，确保数据的一致性和传输的可靠性。|
|描述|注意：在配置此项时，确保所设置的默认值不会与有效数据产生冲突或误解；此配置项对于避免数据在网络上的错误解释至关重要；应根据系统的安全和功能需求仔细选择默认值。|
|多实例个数|1 - 1|
|默认值|0|
|取值范围|0 - 255|

|配置项属性|值（字符串参数配置项）|
|---|---|
|名称|ComMetaDataDefault|
|描述|In case an I-PDU refers to a globally configured MetaDataType and no explicit meta data is given for a send request (e.g. by using Com_TriggerIPDUSendWithMetaData ), the AUTOSAR COM module uses this configured default meta data for sending.|
|描述|概述：ComMetaDataDefault 配置项用于定义AUTOSAR通信堆栈中的元数据默认值，这些默认值将在未明确指定元数据时使用。|
|描述|注意：在配置ComMetaDataDefault时，需要确保默认值与通信消息的设计和期望行为相匹配；元数据默认值的配置应遵循AUTOSAR CP 4.4标准中关于元数据的规范；在配置过程中，应注意不同通信接口可能需要不同的元数据默认值。|
|描述|该配置项未使用|
|说明|The configured string shall be interpreted as a decimal representation of the characters separated by blanks, e.g. "97 98 100" means a string "abd", where the char "a" is in byte 0(lowest address), "b" is in byte 1, and "d" is in byte 2 and (highest address).|
|多实例个数|0 - 1|

##### 1.2.3.1. ComTxModeFalse

|容器属性|值（容器）|
|---|---|
|名称|ComTxModeFalse|
|描述|This container contains the configuration parameters of the AUTOSAR COM module's transmission modes in the case the ComFilter evaluates to false.|
|描述|概述：ComTxModeFalse 是 AUTOSAR Communication Stack 的配置参数，用于定义PDU（Protocol Data Unit）的发送行为，当相关条件不满足时，该PDU不会被发送。|
|描述|注意：在配置ComTxModeFalse时，需要确保它与PDU的发送条件和其他ComTxMode（如ComTxModeTrue）配置一致；此外，应注意与PDU相关的其他ComSignal和ComSignalGroup配置的一致性；在配置时还应考虑系统的性能和资源限制，以免影响通信效率。|
|多实例个数|0 - 1|

###### 1.2.3.1.1. ComTxMode

|容器属性|值（容器）|
|---|---|
|名称|ComTxMode|
|描述|This container contains the configuration parameters of the AUTOSAR COM module's transmission modes.|
|多实例个数|1 - 1|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|ComTxModeMode|
|描述|The available transmission modes described in [18] shall be extended by the additional mode None.|
|说明|The transmission mode None shall not have any further sub-attributes in the ComTxMode object.|
|多实例个数|1 - 1|

|配置项属性|值（浮点型参数配置项）|
|---|---|
|名称|ComTxModeRepetitionPeriod|
|描述|Defines the repetition period in seconds of the multiple transmissions in case ComTxModeNumberOfRepetitions is configured greater than or equal to 1 and ComTxModeMode is configured to DIRECT or MIXED. In case of the mixed transmission mode only the event driven part is affected.|
|多实例个数|0 - 1|
|取值范围|0 - 3600|

|配置项属性|值（浮点型参数配置项）|
|---|---|
|名称|ComTxModeTimeOffset|
|描述|Defines the period in seconds between the start of the I-PDU by Com_IpduGroupStart and the first transmission request in case ComTxModeMode is configured to PERIODIC or MIXED. In case of the mixed transmission mode only the periodic part is affected.|
|说明|In case ComTxModeTimeOffset is omitted or configured to 0, the first periodic transmission shall be transmitted within the next invocation of Com_MainFunctionTx.|
|多实例个数|0 - 1|
|取值范围|0 - 3600|

|配置项属性|值（浮点型参数配置项）|
|---|---|
|名称|ComTxModeTimePeriod|
|描述|Defines the repetition period in seconds of the periodic transmission requests in case ComTxModeMode is configured to PERIODIC or MIXED. In case of the mixed transmission mode only the periodic part is affected.|
|多实例个数|0 - 1|
|取值范围|0 - 3600|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|ComTxModeNumberOfRepetitions|
|描述|Defines the number of repetitions for the transmission mode DIRECT and the event driven part of transmission mode MIXED.|
|多实例个数|0 - 1|
|取值范围|0 - 255|

##### 1.2.3.2. ComTxModeTrue

|容器属性|值（容器）|
|---|---|
|名称|ComTxModeTrue|
|描述|This container contains the configuration parameters of the AUTOSAR COM module's transmission modes in the case the ComFilter evaluates to true.|
|描述|概述：ComTxModeTrue 是一个配置项，用于定义AUTOSAR通信堆栈中的PDU（协议数据单元）的传输模式，当条件为真时，该模式被激活。|
|描述|注意：在配置ComTxModeTrue时，需要确保它与相关的ComTxModeFalse配置相对应，以便在不同条件下切换传输模式；此外，应当检查该模式下的传输触发条件、周期时间和最小间隔时间等属性是否符合系统要求；在AUTOSAR CP 4.4标准中，确保使用正确的数据类型和结构来配置此项，以保证与标准的兼容性。|
|多实例个数|0 - 1|

###### 1.2.3.2.1. ComTxMode

|容器属性|值（容器）|
|---|---|
|名称|ComTxMode|
|描述|This container contains the configuration parameters of the AUTOSAR COM module's transmission modes.|
|描述|概述：ComTxMode配置项定义了AUTOSAR通信堆栈中传输层的传输模式，包括周期性发送、事件触发发送等模式，用于控制消息如何在网络上发送。|
|描述|注意：在配置ComTxMode时，需要注意选择合适的传输模式以满足应用需求和网络带宽限制；周期性发送模式下，必须合理设置发送周期以避免网络拥塞；事件触发模式应确保事件定义清晰，避免不必要的网络流量。|
|多实例个数|1 - 1|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|ComTxModeMode|
|描述|The available transmission modes described in [18] shall be extended by the additional mode None.|
|描述|概述：ComTxModeMode 是 AUTOSAR Communication Stack 的配置参数，用于定义PDU（Protocol Data Unit）的发送模式，例如周期性发送、事件触发发送或者混合模式。|
|描述|注意：在配置ComTxModeMode时，需要确保它与PDU的发送需求相匹配；此外，发送模式的选择会影响网络带宽的使用和消息的时效性；在配置时还应考虑与接收端的兼容性和系统整体的通信策略。|
|说明|The transmission mode None shall not have any further sub-attributes in the ComTxMode object.|
|多实例个数|1 - 1|

|配置项属性|值（浮点型参数配置项）|
|---|---|
|名称|ComTxModeRepetitionPeriod|
|描述|Defines the repetition period in seconds of the multiple transmissions in case ComTxModeNumberOfRepetitions is configured greater than or equal to 1 and ComTxModeMode is configured to DIRECT or MIXED. In case of the mixed transmission mode only the event driven part is affected.|
|描述|概述：ComTxModeRepetitionPeriod定义了在周期传输模式下，ECU发送某个PDU（协议数据单元）之间的时间间隔，用于控制数据的发送频率。|
|描述|注意：该参数的设置应考虑网络带宽和系统实时性要求，避免因频繁发送数据导致的网络拥堵；在配置时需确保该值不小于PDU的传输时间，以避免数据丢失；AUTOSAR CP 4.4标准中，该配置项的单位通常为毫秒，需确保与系统中其他时间相关配置的单位一致。|
|多实例个数|0 - 1|
|取值范围|0 - 3600|

|配置项属性|值（浮点型参数配置项）|
|---|---|
|名称|ComTxModeTimeOffset|
|描述|Defines the period in seconds between the start of the I-PDU by Com_IpduGroupStart and the first transmission request in case ComTxModeMode is configured to PERIODIC or MIXED. In case of the mixed transmission mode only the periodic part is affected.|
|描述|概述：ComTxModeTimeOffset 是用于定义AUTOSAR通信堆栈中，周期性发送的PDU（协议数据单元）的时间偏移量，这个配置项用于控制PDU发送的相对时间点，以减少网络上的冲突和提高带宽的利用率。|
|描述|注意：该值必须小于或等于PDU的发送周期；在配置时需要考虑网络上其他PDU的发送时间，以避免冲突；在多个ECU共享同一网络时，需要特别注意时间偏移量的协调。|
|说明|In case ComTxModeTimeOffset is omitted or configured to 0, the first periodic transmission shall be transmitted within the next invocation of Com_MainFunctionTx.|
|多实例个数|0 - 1|
|取值范围|0 - 3600|

|配置项属性|值（浮点型参数配置项）|
|---|---|
|名称|ComTxModeTimePeriod|
|描述|Defines the repetition period in seconds of the periodic transmission requests in case ComTxModeMode is configured to PERIODIC or MIXED. In case of the mixed transmission mode only the periodic part is affected.|
|描述|概述：ComTxModeTimePeriod 是 AUTOSAR Communication Stack 中的一个配置参数，用于定义周期性发送模式下，PDU（Protocol Data Unit）发送的时间周期。|
|描述|注意：该参数的值需要根据系统的通信需求和网络带宽来合理设置，以确保网络不会因为过高的发送频率而过载；在配置时，应考虑与其他PDU的发送周期的关系，避免可能的网络冲突；在AUTOSAR CP 4.4标准中，该参数的单位通常是时间刻度，需要确保与系统时钟和时间基准的一致性。|
|多实例个数|0 - 1|
|取值范围|0 - 3600|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|ComTxModeNumberOfRepetitions|
|描述|Defines the number of repetitions for the transmission mode DIRECT and the event driven part of transmission mode MIXED.|
|描述|概述：ComTxModeNumberOfRepetitions 配置项定义了在CAN通信中，一个IPDU（Internet Protocol Data Unit）在特定传输模式下重复发送的次数，这通常用于确保数据的可靠性。|
|描述|注意：在配置ComTxModeNumberOfRepetitions时，需要确保其值符合网络的带宽和性能要求；过多的重复发送可能导致网络拥塞；此配置项的值应与通信矩阵或系统需求文档中定义的重传策略一致。|
|多实例个数|0 - 1|
|取值范围|0 - 255|

### 1.3. ComIPduGroup

|容器属性|值（容器）|
|---|---|
|名称|ComIPduGroup|
|描述|Contains the configuration parameters of the AUTOSAR COM module's I-PDU groups.|
|描述|概述：ComIPduGroup配置项定义了一组PDU（协议数据单元）的集合，这些PDU作为通信接口的一部分，用于在AUTOSAR软件模块之间传输数据。|
|描述|注意：在配置ComIPduGroup时，需要确保每个PDU的唯一性，避免同一PDU被分配到多个PDU组中；此外，合理组织PDU组可以优化数据传输效率和系统资源利用；AUTOSAR CP 4.4标准中对PDU的管理和配置有详细规定，需要遵循相关规范以确保系统兼容性和性能。|
|多实例个数|0 - inf|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|ComIPduGroupHandleId|
|描述|The numerical value used as the ID of this I-PDU Group .|
|描述|概述：ComIPduGroupHandleId是用于标识IPDU组的唯一句柄，它允许软件组件通过这个句柄来控制IPDU组的发送和接收行为。|
|描述|注意：在配置ComIPduGroupHandleId时，必须确保每个IPDU组的句柄是唯一的，以避免数据传输中的混淆；句柄的分配应遵循AUTOSAR CP 4.4标准中对于句柄使用的具体规定；在系统设计时应考虑句柄数量的扩展性，以适应未来可能增加的IPDU组。|
|说明|The ComIPduGroupHandleId is required by the API calls to start and stop I-PDU Groups. Range: 0 .. (ComSupportedIPduGroups-1)|
|多实例个数|1 - 1|
|取值范围|0 - 65535|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|ComIPduGroupGroupRef|
|描述|References to all I-PDU groups that includes this I-PDU group. If this reference is omitted this I-PDU group does not belong to another I-PDU group.|
|描述|概述：ComIPduGroupGroupRef 是一个配置项，用于定义通信IPDU组之间的关系，允许将一个IPDU组作为另一个IPDU组的子集进行引用。|
|描述|注意：在配置ComIPduGroupGroupRef时，需要确保引用的IPDU组已经定义，避免出现无效的引用；此外，应注意组之间的包含关系，以防止循环引用或重复定义；在AUTOSAR CP 4.4标准中，应遵循其定义的模型约束和规则，确保配置的一致性和正确性。|
|描述|该配置项未使用|
|多实例个数|0 - inf|
|目标引用项的路径|/AUTOSAR/EcucDefs/Com/ComConfig/ComIPduGroup|

### 1.4. ComSignal

|容器属性|值（容器）|
|---|---|
|名称|ComSignal|
|描述|Contains the configuration parameters of the AUTOSAR COM module's signals.|
|描述|概述：ComSignal是AUTOSAR通信堆栈中的一个配置项，用于定义ECU之间交换的信号的属性，如信号大小、字节顺序、初始值等。|
|描述|注意：在配置ComSignal时，必须确保信号的大小和偏移量符合ECU的网络通信协议；字节顺序（大端或小端）需要与系统中其他ECU保持一致；为避免数据不一致，应正确设置信号的初始值。|
|多实例个数|0 - inf|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|ComInitialValueOnly|
|描述|This parameter defines that the respective signal's initial value shall be put into the respective PDU but there will not be any update of the value through the RTE. Thus the Com implementation does not need to expect any API calls for this signal (group).|
|多实例个数|0 - 1|
|默认值|false|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|ComDataInvalidAction|
|描述|This parameter defines the action performed upon reception of an invalid signal.|
|说明|Relating to signal groups the action in case if one of the included signals is an invalid signal. If Replace is used the ComSignalInitValue will be used for the replacement.|
|多实例个数|0 - 1|
|默认值|NOTIFY|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|ComRxDataTimeoutAction|
|描述|This parameter defines the action performed upon expiration of the reception deadline monitoring timer.|
|多实例个数|0 - 1|
|默认值|NONE|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|ComSignalEndianness|
|描述|Defines the endianness of the signal's network representation.|
|多实例个数|1 - 1|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|ComSignalType|
|描述|The AUTOSAR type of the signal. Whether or not the signal is signed or unsigned can be found by examining the value of this attribute.|
|说明|This type could also be used to reserved appropriate storage in AUTOSAR COM.|
|多实例个数|1 - 1|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|ComTransferProperty|
|描述|Defines if a write access to this signal can trigger the transmission of the corresponding I-PDU. If the I-PDU is triggered, depends also on the transmission mode of the corresponding I-PDU.|
|多实例个数|0 - 1|

|配置项属性|值（浮点型参数配置项）|
|---|---|
|名称|ComFirstTimeout|
|描述|Defines the length of the first deadline monitoring timeout period in seconds. This timeout is used immediately after start (or restart) of the deadline monitoring service. The timeout period of the successive periods is configured by ECUC_Com_00263.|
|多实例个数|0 - 1|
|默认值|0|
|取值范围|0 - 3600|

|配置项属性|值（浮点型参数配置项）|
|---|---|
|名称|ComTimeout|
|描述|Defines the length of the deadline monitoring timeout period in seconds. The period for the first timeout period can be configured separately by ECUC_Com_00183.|
|多实例个数|0 - 1|
|默认值|0|
|取值范围|0 - 3600|

|配置项属性|值（函数名配置项）|
|---|---|
|名称|ComErrorNotification|
|描述|Only valid on sender side: Name of Com_CbkTxErr callback function to be called.|
|说明|If this parameter is omitted no error notification shall take place.|
|多实例个数|0 - 1|

|配置项属性|值（函数名配置项）|
|---|---|
|名称|ComInvalidNotification|
|描述|Only valid on receiver side: Name of Com_CbkInv callback function to be called. Name of the function which notifies the RTE about the reception of an invalidated signal/ signal group. Only applicable if ComDataInvalidAction is configured to NOTIFY.|
|多实例个数|0 - 1|

|配置项属性|值（函数名配置项）|
|---|---|
|名称|ComNotification|
|描述|On sender side: Name of Com_CbkTxAck callback function to be called.|
|说明|On receiver side: Name of Com_CbkRxAck callback function to be called. If this parameter is omitted no notification shall take place.|
|多实例个数|0 - 1|

|配置项属性|值（函数名配置项）|
|---|---|
|名称|ComTimeoutNotification|
|描述|On sender side: Name of Com_CbkTxTOut callback function to be called.|
|说明|On receiver side: Name of Com_CbkRxTOut callback function to be called.|
|多实例个数|0 - 1|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|ComBitPosition|
|描述|Starting position within the I-PDU. This parameter refers to the position in the I-PDU and not in the shadow buffer. If the endianness conversion is configured to Opaque the parameter ComBitPosition shall define the bit0 of the first byte like in little endian byte order|
|多实例个数|1 - 1|
|取值范围|0 - 4294967295|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|ComBitSize|
|描述|Size in bits, for integer signal types. For ComSignalType UINT8_N and UINT8_DYN|
|说明|the size shall be configured by ComSignalLength. For ComSignalTypes FLOAT32 and FLOAT64 the size is already defined by the signal type and therefore may be omitted.|
|多实例个数|0 - 1|
|取值范围|0 - 64|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|ComHandleId|
|描述|The numerical value used as the ID.|
|说明|This ID identifies signals and signal groups in the COM APIs using Com_SignalIdType or Com_SignalGroupIdType parameter respectively.|
|多实例个数|0 - 1|
|取值范围|0 - 65535|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|ComSignalLength|
|描述|Description:|
|说明|For ComSignalType UINT8_N this parameter specifies the length n in bytes. For ComSignalType UINT8_DYN it specifies the maximum length in bytes. For all other types this parameter shall be ignored. The supported maximum length is restricted by the used transportation system. For non TP-PDUs the maximum size of a PDU, and therefore also of any included signal, is limited by the concrete bus characteristic. For example, the limit is 8 bytes for CAN and LIN, 64 bytes for CAN FD and 254 for FlexRay.|
|多实例个数|0 - 1|
|取值范围|0 - 4294967295|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|ComUpdateBitPosition|
|描述|Bit position of update-bit inside I-PDU.|
|说明|If this attribute is omitted then there is no update-bit. This setting must be consistently on sender and on receiver side. Range: 0..63 for CAN and LIN, 0..511 for CAN FD, 0..2031 for FlexRay, 0..4294967295 for TP.|
|多实例个数|0 - 1|
|取值范围|0 - 4294967295|

|配置项属性|值（字符串参数配置项）|
|---|---|
|名称|ComSignalDataInvalidValue|
|描述|Defines the data invalid value of the signal.|
|说明|In case the ComSignalType is UINT8, UINT16, UINT32, UINT64, SINT8, SINT16, SINT32, SINT64 the string shall be interpreted as defined in the chapter Integer Type in the AUTOSAR EcuC specification. In case the ComSignalType is FLOAT32, FLOAT64 the string shall be interpreted as defined in the chapter Float Type in the AUTOSAR EcuC specification. In case the ComSignalType is BOOLEAN the string shall be interpreted as defined in the chapter Boolean Type in the AUTOSAR EcuC specification. In case the ComSignal is a UINT8_N, UINT8_DYN the string shall be interpreted as a decimal representation of the characters separated by blanks, e.g. "97 98 100" means a string "abd", where the char "a" is in byte 0(lowest address), "b" is in byte 1, and "d" is in byte 2 and (highest address). For the ComSignalType UINT8_DYN the dynamic length shall be set to the number of configured characters. An empty string "" shall be interpreted as 0-sized dynamic signal.|
|多实例个数|0 - 1|

|配置项属性|值（字符串参数配置项）|
|---|---|
|名称|ComSignalInitValue|
|描述|Initial value for this signal. In case of UINT8_N the default value is a string of length ComSignalLength with all bytes set to 0x00. In case of UINT8_DYN the initial size shall be 0.|
|说明|In case the ComSignalType is UINT8, UINT16, UINT32, UINT64, SINT8, SINT16, SINT32, SINT64 the string shall be interpreted as defined in the chapter Integer Type in the AUTOSAR EcuC specification. In case the ComSignalType is FLOAT32, FLOAT64 the string shall be interpreted as defined in the chapter Float Type in the AUTOSAR EcuC specification. In case the ComSignalType is BOOLEAN the string shall be interpreted as defined in the chapter Boolean Type in the AUTOSAR EcuC specification. In case the ComSignal is a UINT8_N, UINT8_DYN the string shall be interpreted as a decimal representation of the characters separated by blanks, e.g. "97 98 100" means a string "abd", where the char "a" is in byte 0(lowest address), "b" is in byte 1, and "d" is in byte 2 and (highest address). For the ComSignalType UINT8_DYN the dynamic length shall be set to the number of configured characters. An empty string "" shall be interpreted as 0-sized dynamic signal.|
|多实例个数|0 - 1|

|配置项属性|值（字符串参数配置项）|
|---|---|
|名称|ComTimeoutSubstitutionValue|
|描述|The signal substitution value will be used in case of a timeout and ComRxDataTimeoutAction is set to SUBSTITUTE.|
|说明|In case of UINT8_N the default value is a string of length ComSignalLength with all bytes set to 0x00. In case ofUINT8_DYN the initial size shall be 0. In case the ComSignalType is UINT8, UINT16, UINT32, UINT64, SINT8, SINT16, SINT32, SINT64 the string shall be interpreted as defined in the chapter Integer Type in the AUTOSAR EcuC specification. In case the ComSignalType is FLOAT32, FLOAT64 the string shall be interpreted as defined in the chapter Float Type in the AUTOSAR EcuC specification. In case the ComSignalType is BOOLEAN the string shall be interpreted as defined in the chapter Boolean Type in the AUTOSAR EcuC specification. In case the ComSignal is a UINT8_N, UINT8_DYN the string shall be interpreted as a decimal representation of the characters separated by blanks, e.g. "97 98 100" means a string "abd", where the char "a" is in byte 0(lowest address), "b" is in byte 1, and "d" is in byte 2 and (highest address). For the ComSignalType UINT8_DYN the dynamic length shall be set to the number of configured characters. An empty string "" shall be interpreted as 0-sized dynamic signal.|
|多实例个数|0 - 1|

|配置项属性|值（外部引用配置项）|
|---|---|
|名称|ComSystemTemplateSystemSignalRef|
|描述|Reference to the ISignalToIPduMapping that contains a reference to the ISignal (System Template) which this ComSignal (or ComGroupSignal) represents.|
|多实例个数|0 - 1|
|目标类型|I-SIGNAL-TO-I-PDU-MAPPING|

#### 1.4.1. ComFilter

|容器属性|值（容器）|
|---|---|
|名称|ComFilter|
|描述|This container contains the configuration parameters of the AUTOSAR COM module's Filters.|
|说明|Note: On sender side the container is used to specify the transmission mode conditions.|
|多实例个数|0 - 1|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|ComFilterAlgorithm|
|描述|The range of values is specified in the [17] specification, chapter 2.2.2, Reception Filtering.|
|多实例个数|1 - 1|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|ComFilterMask|
|描述|The name of this attribute corresponds to the parameter name in the [17] specification of Reception Filtering.|
|多实例个数|0 - 1|
|取值范围|-2147483648 - 4294967295|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|ComFilterMax|
|描述|The name of this attribute corresponds to the parameter name in the [17] specification of Reception Filtering.|
|多实例个数|0 - 1|
|取值范围|-2147483648 - 4294967295|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|ComFilterMin|
|描述|The name of this attribute corresponds to the parameter name in the [17] specification of Reception Filtering.|
|多实例个数|0 - 1|
|取值范围|-2147483648 - 4294967295|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|ComFilterOffset|
|描述|The name of this attribute corresponds to the parameter name in the [17] specification of Reception Filtering.|
|说明|Range = 0..(ComFilterPeriod-1)|
|多实例个数|0 - 1|
|取值范围|0 - 4294967294|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|ComFilterPeriod|
|描述|This parameter defines the period of the ComFilterAlgorithm ONE_EVERY_N.|
|多实例个数|0 - 1|
|取值范围|2 - 4294967295|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|ComFilterX|
|描述|The name of this attribute corresponds to the parameter name in the [17] specification of Reception Filtering.|
|多实例个数|0 - 1|
|取值范围|-2147483648 - 4294967295|

### 1.5. ComSignalGroup

|容器属性|值（容器）|
|---|---|
|名称|ComSignalGroup|
|描述|Contains the configuration parameters of the AUTOSAR COM module's signal groups.|
|描述|概述：ComSignalGroup 是 AUTOSAR Communication Stack 中的一个配置项，用于定义一组信号（ComSignals），这些信号作为一个整体被发送和接收，以优化网络带宽和消息处理。|
|描述|注意：在配置ComSignalGroup时，需要确保组内所有信号的更新和传输作为一个原子操作处理；组内信号的打包和解包策略应当一致，以避免数据不一致的问题；在定义信号组时，还需考虑网络带宽和ECU处理能力，以确保信号组的有效管理和传输。|
|多实例个数|0 - inf|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|ComInitialValueOnly|
|描述|This parameter defines that the respective signal's initial value shall be put into the respective PDU but there will not be any update of the value through the RTE. Thus the Com implementation does not need to expect any API calls for this signal (group).|
|描述|概述：ComInitialValueOnly 配置项用于指定是否仅在通信系统初始化时发送初始值，而在后续的通信周期中不再发送该值，除非该值发生变化。|
|描述|注意：在使用ComInitialValueOnly时，需要确保系统设计可以容忍在通信周期中不接收到静态值的更新；此配置项可能会影响系统的诊断和监控策略，因为某些监控系统可能依赖于定期接收的更新；在配置此项时，应仔细考虑与网络管理和唤醒信号的交互，以避免意外的网络行为。|
|多实例个数|0 - 1|
|默认值|false|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|ComSignalGroupArrayAccess|
|描述|Defines whether the uint8-array based access shall be used for this ComSignalGroup.|
|描述|概述：ComSignalGroupArrayAccess 配置项用于定义信号组数组的访问机制，允许对信号组中的信号数组进行索引访问，从而简化对复杂信号组的处理。|
|描述|注意：在配置时需确保信号组中的信号确实是数组类型，以便可以通过索引进行访问；此配置项需要与ComSignalGroup的定义一致，以保证正确的数据访问；在AUTOSAR CP 4.4标准中，应当注意信号组数组访问的内存对齐和数据一致性要求。|
|描述|该配置项未使用|
|多实例个数|0 - 1|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|ComDataInvalidAction|
|描述|This parameter defines the action performed upon reception of an invalid signal.|
|描述|概述：ComDataInvalidAction配置项用于定义当接收到无效或未定义的信号数据时，通信堆栈应采取的动作，例如可以配置为保持最后有效值或设置为默认值。|
|描述|注意：在配置ComDataInvalidAction时，需要确保所选动作与系统的容错需求相匹配；对于关键信号，考虑使用保持最后有效值以避免因数据无效导致的系统行为不确定；AUTOSAR CP 4.4标准中明确支持此配置项，但实现细节可能因AUTOSAR版本和供应商实现而异。|
|说明|Relating to signal groups the action in case if one of the included signals is an invalid signal. If Replace is used the ComSignalInitValue will be used for the replacement.|
|多实例个数|0 - 1|
|默认值|NOTIFY|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|ComRxDataTimeoutAction|
|描述|This parameter defines the action performed upon expiration of the reception deadline monitoring timer.|
|描述|概述：ComRxDataTimeoutAction配置项定义了接收信号在发生超时情况时的处理动作，例如将信号值设置为默认值或者不更新。|
|描述|注意：在配置ComRxDataTimeoutAction时，需要确保所选择的动作与系统的安全要求相符；超时处理策略应当在系统设计阶段就明确规划；在AUTOSAR CP 4.4标准中，应当检查该配置项是否支持所有预定义的动作类型，以确保与标准的兼容性。|
|多实例个数|0 - 1|
|默认值|NONE|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|ComTransferProperty|
|描述|Defines if a write access to this signal can trigger the transmission of the corresponding I-PDU. If the I-PDU is triggered, depends also on the transmission mode of the corresponding I-PDU.|
|多实例个数|0 - 1|

|配置项属性|值（浮点型参数配置项）|
|---|---|
|名称|ComFirstTimeout|
|描述|Defines the length of the first deadline monitoring timeout period in seconds. This timeout is used immediately after start (or restart) of the deadline monitoring service. The timeout period of the successive periods is configured by ECUC_Com_00263.|
|描述|概述：ComFirstTimeout 配置项用于定义在通信接口模块（Com）中，PDU（协议数据单元）的首次发送超时时间，即在发送第一个PDU副本之前等待的时间。|
|描述|注意：ComFirstTimeout 的值应当根据系统的通信需求和性能指标来设定；超时时间设置过短可能导致系统无法在规定时间内完成数据的准备和发送；在AUTOSAR CP 4.4标准中，确保该配置项的数据类型和单位符合规范要求。|
|多实例个数|0 - 1|
|默认值|0|
|取值范围|0 - 3600|

|配置项属性|值（浮点型参数配置项）|
|---|---|
|名称|ComTimeout|
|描述|Defines the length of the deadline monitoring timeout period in seconds. The period for the first timeout period can be configured separately by ECUC_Com_00183.|
|描述|概述：ComTimeout 配置项用于定义通信接口中消息的超时时间，确保系统能够在预定时间内检测到消息丢失或延迟。|
|描述|注意：设置合理的超时时间以避免过早或过晚地报告通信错误；超时设置应考虑网络的实际延迟和系统的性能要求；在AUTOSAR CP 4.4中，确保与ComStack配置的兼容性和一致性。|
|多实例个数|0 - 1|
|默认值|0|
|取值范围|0 - 3600|

|配置项属性|值（函数名配置项）|
|---|---|
|名称|ComErrorNotification|
|描述|Only valid on sender side: Name of Com_CbkTxErr callback function to be called.|
|描述|概述：ComErrorNotification是一个配置项，用于定义在AUTOSAR通信中间件（Com层）发生错误时所调用的回调函数，以便于系统可以对错误进行处理。|
|描述|注意：在配置ComErrorNotification时，需要确保回调函数符合AUTOSAR CP 4.4标准中定义的接口规范；回调函数应当能够处理所有预期的错误类型；在实际部署时，应当考虑回调函数的执行时间对系统性能的影响。|
|说明|If this parameter is omitted no error notification shall take place.|
|多实例个数|0 - 1|

|配置项属性|值（函数名配置项）|
|---|---|
|名称|ComInvalidNotification|
|描述|Only valid on receiver side: Name of Com_CbkInv callback function to be called. Name of the function which notifies the RTE about the reception of an invalidated signal/ signal group. Only applicable if ComDataInvalidAction is configured to NOTIFY.|
|描述|概述：ComInvalidNotification是一个配置参数，用于指定当接收到无效或未启用的信号时，应该调用的回调函数。|
|描述|注意：在配置ComInvalidNotification时，需要确保所引用的回调函数符合AUTOSAR标准中定义的原型和行为；此配置项通常与信号的数据无效或数据更新状态有关；在设计系统时，应考虑如何处理无效信号的情况，以确保系统的鲁棒性。|
|多实例个数|0 - 1|

|配置项属性|值（函数名配置项）|
|---|---|
|名称|ComNotification|
|描述|On sender side: Name of Com_CbkTxAck callback function to be called.|
|描述|概述：ComNotification 用于定义在接收到特定的通信消息后触发的回调函数，这些回调函数用于处理接收到的消息或执行相关的动作。|
|描述|注意：确保回调函数的实现符合实时性和资源消耗的要求；回调函数应避免执行复杂或耗时的操作，以免影响消息处理的效率；在配置ComNotification时，应确保消息标识符与回调函数正确匹配，避免错误触发。|
|说明|On receiver side: Name of Com_CbkRxAck callback function to be called. If this parameter is omitted no notification shall take place.|
|多实例个数|0 - 1|

|配置项属性|值（函数名配置项）|
|---|---|
|名称|ComTimeoutNotification|
|描述|On sender side: Name of Com_CbkTxTOut callback function to be called.|
|描述|概述：ComTimeoutNotification 是一个配置项，用于定义在AUTOSAR通信管理模块中，当某个PDU（协议数据单元）的接收超时事件发生时，需要调用的回调函数。|
|描述|注意：确保为每个需要超时通知的PDU正确配置了ComTimeoutNotification；回调函数需要遵循AUTOSAR规定的接口和行为模式；在配置时要注意系统资源和性能影响，避免因超时处理导致的系统延迟。|
|说明|On receiver side: Name of Com_CbkRxTOut callback function to be called.|
|多实例个数|0 - 1|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|ComHandleId|
|描述|The numerical value used as the ID.|
|说明|This ID identifies signals and signal groups in the COM APIs using Com_SignalIdType or Com_SignalGroupIdType parameter respectively.|
|多实例个数|0 - 1|
|取值范围|0 - 65535|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|ComUpdateBitPosition|
|描述|Bit position of update-bit inside I-PDU.|
|描述|概述：ComUpdateBitPosition 配置项用于定义信号或信号组的更新位在IPDU（即消息帧）中的位置，这个更新位用于指示数据是否已经被更新。|
|描述|注意：在配置ComUpdateBitPosition时，需要确保更新位的位置不与IPDU中其他信号的数据位重叠；更新位的使用应遵循AUTOSAR规范中关于信号更新的机制；在设计IPDU布局时，应考虑到所有信号的更新位位置，以确保数据的一致性和准确性。|
|说明|If this attribute is omitted then there is no update-bit. This setting must be consistently on sender and on receiver side. Range: 0..63 for CAN and LIN, 0..511 for CAN FD, 0..2031 for FlexRay, 0..4294967295 for TP.|
|多实例个数|0 - 1|
|取值范围|0 - 4294967295|

|配置项属性|值（外部引用配置项）|
|---|---|
|名称|ComSystemTemplateSignalGroupRef|
|描述|Reference to the ISignalToIPduMapping that contains a reference to the ISignalGroup (SystemTemplate) which this ComSignalGroup represents.|
|描述|概述：ComSystemTemplateSignalGroupRef是一个配置项，用于引用在通信系统模板中定义的信号组，以便在AUTOSAR通信管理模块中使用这些信号组进行数据交换。|
|描述|注意：在配置ComSystemTemplateSignalGroupRef时，必须确保引用的信号组已在系统模板中定义；引用的信号组ID和名称需要与系统模板中的定义完全一致，以保证数据交换的准确性；此配置项对于实现基于信号组的数据交换至关重要，因此需要仔细检查其正确性和一致性。|
|描述|该配置项未使用|
|多实例个数|0 - 1|
|目标类型|I-SIGNAL-TO-I-PDU-MAPPING|

#### 1.5.1. ComGroupSignal

|容器属性|值（容器）|
|---|---|
|名称|ComGroupSignal|
|描述|This container contains the configuration parameters of group signals. I.e. signals that are included within a signal group.|
|描述|概述：ComGroupSignal用于定义一组信号（Signals）的集合，这些信号作为一个整体在通信接口中进行管理和传输。|
|描述|注意：在定义ComGroupSignal时，确保所有包含的信号兼容并符合传输协议要求；组内信号的更新策略应统一管理，以避免数据不一致；AutoSAR CP 4.4标准中对信号组的具体实现和限制应详细参考相关通信协议章节。|
|多实例个数|0 - inf|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|ComSignalEndianness|
|描述|Defines the endianness of the signal's network representation.|
|描述|概述：ComSignalEndianness 配置项用于定义通信信号的字节序，指定信号在网络消息中的表示方式是大端（Big Endian）还是小端（Little Endian）。|
|描述|注意：在定义信号的字节序时，必须确保与网络上其他系统或组件的字节序兼容；错误的字节序配置可能导致数据解析错误，影响系统间的数据交换；AUTOSAR CP 4.4标准支持配置每个信号的字节序，以适应不同网络要求。|
|多实例个数|1 - 1|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|ComSignalType|
|描述|The AUTOSAR type of the signal. Whether or not the signal is signed or unsigned can be found by examining the value of this attribute.|
|描述|概述：ComSignalType 是用于定义通信信号的数据类型，这个配置项指定了信号可以携带的数据类型，如整型、浮点型或布尔型等。|
|描述|注意：在定义ComSignalType时，需要确保数据类型与应用层期望的数据类型一致；数据类型的选择会影响信号的编码、解码以及传输效率；在AUTOSAR CP 4.4标准中，应遵循定义的数据类型枚举，不应使用非标准的数据类型。|
|说明|This type could also be used to reserved appropriate storage in AUTOSAR COM.|
|多实例个数|1 - 1|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|ComTransferProperty|
|描述|Optionally defines whether this group signal shall contribute to the TRIGGERED_ON_CHANGE transfer property of the signal group. If at least one group signal of a signal group has the "ComTransferProperty" configured all other group signals of that signal group shall have the attribute configured as well.|
|描述|概述：ComTransferProperty 是一个配置项，用于定义AUTOSAR通信堆栈中的PDU（协议数据单元）传输属性，例如是否是触发传输、周期传输还是直接传输。|
|描述|注意：在配置ComTransferProperty时，需要确保它与PDU的发送策略相匹配；不同的传输属性可能会影响消息的延迟和带宽需求；在配置周期性传输属性时，还需注意周期时间的设置以满足系统的实时性要求。|
|多实例个数|0 - 1|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|ComBitPosition|
|描述|Starting position within the I-PDU. This parameter refers to the position in the I-PDU and not in the shadow buffer. If the endianness conversion is configured to Opaque the parameter ComBitPosition shall define the bit0 of the first byte like in little endian byte order|
|描述|概述：ComBitPosition用于定义信号在消息中的起始位位置，这对于确保信号正确打包和解包至网络消息中至关重要。|
|描述|注意：在配置ComBitPosition时，必须确保它与信号的长度和消息的大小相兼容，避免信号溢出消息边界；此外，考虑到不同网络的字节序，需要确保位位置的配置与网络的字节序一致；AUTOSAR CP 4.4中并未对ComBitPosition的具体实现细节做出改变，但在实际应用中应注意其与其他配置项的关联性和一致性。|
|多实例个数|1 - 1|
|取值范围|0 - 4294967295|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|ComBitSize|
|描述|Size in bits, for integer signal types. For ComSignalType UINT8_N and UINT8_DYN|
|描述|概述：ComBitSize 配置项用于定义AUTOSAR通信堆栈中，特定信号的大小，以位为单位。|
|描述|注意：在配置ComBitSize时，必须确保其值与信号实际的大小相匹配；超出信号实际大小的配置可能导致数据截断；在信号映射和打包过程中，应考虑端对端保护的需求。|
|说明|the size shall be configured by ComSignalLength. For ComSignalTypes FLOAT32 and FLOAT64 the size is already defined by the signal type and therefore may be omitted.|
|多实例个数|0 - 1|
|取值范围|0 - 64|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|ComHandleId|
|描述|The numerical value used as the ID.|
|描述|概述：ComHandleId 是用于唯一标识 AUTOSAR Communication Stack 中的 PDU（Protocol Data Unit）或信号（Signal）的一个配置参数，它确保了系统中数据传输的唯一性和可追踪性。|
|描述|注意：ComHandleId 的值必须在整个系统中是唯一的，以避免数据传输的冲突；在配置过程中应确保 ComHandleId 与实际的 PDU 或信号相匹配；在系统的生命周期内，一旦分配，ComHandleId 应保持不变以维护系统的稳定性和数据一致性。|
|说明|This ID identifies signals and signal groups in the COM APIs using Com_SignalIdType or Com_SignalGroupIdType parameter respectively.|
|多实例个数|0 - 1|
|取值范围|0 - 65535|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|ComSignalLength|
|描述|Description:|
|描述|概述：ComSignalLength 定义了通信信号的长度，以位为单位，用于指定在通信接口中传输的数据大小。|
|描述|注意：确保ComSignalLength与实际数据类型大小匹配，避免数据截断或溢出；在配置时考虑网络带宽和传输效率；长度设置应符合AUTOSAR CP 4.4标准中对信号大小的规定。|
|说明|For ComSignalType UINT8_N this parameter specifies the length n in bytes. For ComSignalType UINT8_DYN it specifies the maximum length in bytes. For all other types this parameter shall be ignored. The supported maximum length is restricted by the used transportation system. For non TP-PDUs the maximum size of a PDU, and therefore also of any included signal, is limited by the concrete bus characteristic. For example, the limit is 8 bytes for CAN and LIN, 64 bytes for CAN FD and 254 for FlexRay.|
|多实例个数|0 - 1|
|取值范围|0 - 4294967295|

|配置项属性|值（字符串参数配置项）|
|---|---|
|名称|ComSignalDataInvalidValue|
|描述|Defines the data invalid value of the signal.|
|描述|概述：ComSignalDataInvalidValue用于定义在通信信号无效或未接收到更新时所采用的默认值，确保系统的健壮性和数据的一致性。|
|描述|注意：该值需要根据信号的数据类型和应用场景仔细选择，以避免误操作或逻辑错误；在配置时需确保与信号的有效值范围不冲突，以免引起数据处理异常；AUTOSAR CP 4.4标准中，对于某些信号类型可能不支持设置无效值，需要根据具体信号属性决定是否配置。|
|说明|In case the ComSignalType is UINT8, UINT16, UINT32, UINT64, SINT8, SINT16, SINT32, SINT64 the string shall be interpreted as defined in the chapter Integer Type in the AUTOSAR EcuC specification. In case the ComSignalType is FLOAT32, FLOAT64 the string shall be interpreted as defined in the chapter Float Type in the AUTOSAR EcuC specification. In case the ComSignalType is BOOLEAN the string shall be interpreted as defined in the chapter Boolean Type in the AUTOSAR EcuC specification. In case the ComSignal is a UINT8_N, UINT8_DYN the string shall be interpreted as a decimal representation of the characters separated by blanks, e.g. "97 98 100" means a string "abd", where the char "a" is in byte 0(lowest address), "b" is in byte 1, and "d" is in byte 2 and (highest address). For the ComSignalType UINT8_DYN the dynamic length shall be set to the number of configured characters. An empty string "" shall be interpreted as 0-sized dynamic signal.|
|多实例个数|0 - 1|

|配置项属性|值（字符串参数配置项）|
|---|---|
|名称|ComSignalInitValue|
|描述|Initial value for this signal. In case of UINT8_N the default value is a string of length ComSignalLength with all bytes set to 0x00. In case of UINT8_DYN the initial size shall be 0.|
|描述|概述：ComSignalInitValue 配置项用于定义通信信号的初始值，这个值将在系统启动或通信控制器重置后被设置到信号中。|
|描述|注意：在配置初始值时，需要确保值符合信号的数据类型和取值范围；如果信号用于诊断通信，初始值可能需要遵循特定的诊断协议要求；在AUTOSAR CP 4.4标准中，应当确保配置工具或开发环境正确支持ComSignalInitValue的配置，以避免系统启动时的数据不一致问题。|
|说明|In case the ComSignalType is UINT8, UINT16, UINT32, UINT64, SINT8, SINT16, SINT32, SINT64 the string shall be interpreted as defined in the chapter Integer Type in the AUTOSAR EcuC specification. In case the ComSignalType is FLOAT32, FLOAT64 the string shall be interpreted as defined in the chapter Float Type in the AUTOSAR EcuC specification. In case the ComSignalType is BOOLEAN the string shall be interpreted as defined in the chapter Boolean Type in the AUTOSAR EcuC specification. In case the ComSignal is a UINT8_N, UINT8_DYN the string shall be interpreted as a decimal representation of the characters separated by blanks, e.g. "97 98 100" means a string "abd", where the char "a" is in byte 0(lowest address), "b" is in byte 1, and "d" is in byte 2 and (highest address). For the ComSignalType UINT8_DYN the dynamic length shall be set to the number of configured characters. An empty string "" shall be interpreted as 0-sized dynamic signal.|
|多实例个数|0 - 1|

|配置项属性|值（字符串参数配置项）|
|---|---|
|名称|ComTimeoutSubstitutionValue|
|描述|The signal substitution value will be used in case of a timeout and ComRxDataTimeoutAction is set to SUBSTITUTE.|
|描述|概述：ComTimeoutSubstitutionValue 是用于定义在通信接口（Com）层中，当超时事件发生时所采用的替代值，这个值将被用于替换未成功更新的信号或信号组的数据。|
|描述|注意：在配置ComTimeoutSubstitutionValue时，需要确保该值与信号的数据类型和取值范围兼容；此外，应当考虑到替代值对系统行为的潜在影响，避免因不当的替代值导致系统异常行为；在AUTOSAR CP 4.4标准中，应当遵循相关规范来配置超时替代值，以确保系统的健壮性和一致性。|
|描述|该配置项未使用|
|说明|In case of UINT8_N the default value is a string of length ComSignalLength with all bytes set to 0x00. In case ofUINT8_DYN the initial size shall be 0. In case the ComSignalType is UINT8, UINT16, UINT32, UINT64, SINT8, SINT16, SINT32, SINT64 the string shall be interpreted as defined in the chapter Integer Type in the AUTOSAR EcuC specification. In case the ComSignalType is FLOAT32, FLOAT64 the string shall be interpreted as defined in the chapter Float Type in the AUTOSAR EcuC specification. In case the ComSignalType is BOOLEAN the string shall be interpreted as defined in the chapter Boolean Type in the AUTOSAR EcuC specification. In case the ComSignal is a UINT8_N, UINT8_DYN the string shall be interpreted as a decimal representation of the characters separated by blanks, e.g. "97 98 100" means a string "abd", where the char "a" is in byte 0(lowest address), "b" is in byte 1, and "d" is in byte 2 and (highest address). For the ComSignalType UINT8_DYN the dynamic length shall be set to the number of configured characters. An empty string "" shall be interpreted as 0-sized dynamic signal.|
|多实例个数|0 - 1|

|配置项属性|值（外部引用配置项）|
|---|---|
|名称|ComSystemTemplateSystemSignalRef|
|描述|Reference to the ISignalToIPduMapping that contains a reference to the ISignal (System Template) which this ComSignal (or ComGroupSignal) represents.|
|描述|概述：ComSystemTemplateSystemSignalRef 是一个配置项，用于在AUTOSAR通信管理模块中引用系统信号，确保正确的信号映射和数据交换。|
|描述|注意：在配置ComSystemTemplateSystemSignalRef时，必须确保引用的系统信号已经在系统信号字典中定义；引用的系统信号应与期望的通信对象匹配，以保证数据一致性；在配置过程中，应遵循AUTOSAR CP 4.4标准中对于系统信号引用的规范和约束。|
|描述|该配置项未使用|
|多实例个数|0 - 1|
|目标类型|I-SIGNAL-TO-I-PDU-MAPPING|

##### 1.5.1.1. ComFilter

|容器属性|值（容器）|
|---|---|
|名称|ComFilter|
|描述|This container contains the configuration parameters of the AUTOSAR COM module's Filters.|
|描述|概述：ComFilter配置项用于定义PDU（Protocol Data Unit）的过滤机制，它决定了哪些PDU可以被接收或发送，基于特定的规则和条件。|
|描述|注意：在AUTOSAR CP 4.4中，ComFilter的属性应与通信堆栈的需求相匹配，确保正确的PDU过滤；过滤规则的配置需要考虑系统的性能和资源限制；不同的ComFilter类型对应不同的过滤逻辑，因此选择合适的过滤类型对于系统的正确性至关重要。|
|描述|该配置项未使用|
|说明|Note: On sender side the container is used to specify the transmission mode conditions.|
|多实例个数|0 - 1|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|ComFilterAlgorithm|
|描述|The range of values is specified in the [17] specification, chapter 2.2.2, Reception Filtering.|
|描述|概述：ComFilterAlgorithm 配置项用于定义AUTOSAR通信堆栈中消息过滤算法的类型，它决定了如何根据预设的规则对传入的消息进行筛选。|
|描述|注意：在配置ComFilterAlgorithm时，需要确保选择的过滤算法与系统需求相匹配；不同的过滤算法可能会影响消息处理的性能和效率；在AUTOSAR CP 4.4标准中，应当参照标准中定义的过滤算法类型来配置，以保证兼容性和标准的一致性。|
|描述|该配置项未使用|
|多实例个数|1 - 1|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|ComFilterMask|
|描述|The name of this attribute corresponds to the parameter name in the [17] specification of Reception Filtering.|
|描述|概述：ComFilterMask用于定义通信消息过滤器中的掩码值，该值与接收到的消息数据进行按位与操作，以确定是否接受或拒绝该消息。|
|描述|注意：掩码值的设置需要根据实际的消息格式和过滤需求仔细设计；在配置时需确保掩码与消息长度一致，避免数据截断或过滤错误；AUTOSAR CP 4.4标准中对于ComFilterMask的具体使用和配置应遵循通信管理模块的规范要求。|
|描述|该配置项未使用|
|多实例个数|0 - 1|
|取值范围|-2147483648 - 4294967295|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|ComFilterMax|
|描述|The name of this attribute corresponds to the parameter name in the [17] specification of Reception Filtering.|
|描述|概述：ComFilterMax是AUTOSAR通信堆栈中的一个配置参数，用于定义接收信号的最大过滤阈值，以确定是否接受或拒绝传入的信号。|
|描述|注意：在配置ComFilterMax时，需要确保其值不超过信号数据类型所能表示的最大值；此外，该值应与信号的物理范围和应用需求相匹配；在配置过滤器时，还应考虑与其他相关过滤参数（如ComFilterMin）的关系，以确保过滤逻辑的正确性。|
|描述|该配置项未使用|
|多实例个数|0 - 1|
|取值范围|-2147483648 - 4294967295|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|ComFilterMin|
|描述|The name of this attribute corresponds to the parameter name in the [17] specification of Reception Filtering.|
|描述|概述：ComFilterMin 是用于定义接收信号的最小阈值，确保只有满足最小值条件的信号才会被处理。|
|描述|注意：在设置ComFilterMin时，确保其值适当以避免丢失重要信号；该值应小于或等于对应信号的最大值ComFilterMax，以保持有效的过滤范围；在多信号系统中，每个信号的ComFilterMin应独立设置以满足特定需求。|
|描述|该配置项未使用|
|多实例个数|0 - 1|
|取值范围|-2147483648 - 4294967295|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|ComFilterOffset|
|描述|The name of this attribute corresponds to the parameter name in the [17] specification of Reception Filtering.|
|描述|概述：ComFilterOffset 是 AUTOSAR Communication Stack 中的一个配置参数，用于定义信号或信号组过滤算法中的偏移量，该偏移量用于确定过滤器的参考值。|
|描述|注意：在配置ComFilterOffset时，需要确保其值与信号的大小和类型相匹配，避免数据溢出或不正确的过滤行为；此外，该参数应与ComFilterMask参数一起使用，以定义过滤器的完整行为；在配置过滤器时，应仔细考虑过滤条件，以确保系统的正确性和性能。|
|描述|该配置项未使用|
|说明|Range = 0..(ComFilterPeriod-1)|
|多实例个数|0 - 1|
|取值范围|0 - 4294967294|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|ComFilterPeriod|
|描述|This parameter defines the period of the ComFilterAlgorithm ONE_EVERY_N.|
|描述|概述：ComFilterPeriod 是用于定义通信消息过滤的时间周期，用于确定消息是否满足特定的时间间隔条件后才被接收或发送。|
|描述|注意：该配置项的设置应确保与系统的实时性和通信需求相匹配；过滤周期设置不当可能导致消息延迟或丢失；在配置时需考虑消息的优先级和重要性。|
|描述|该配置项未使用|
|多实例个数|0 - 1|
|取值范围|2 - 4294967295|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|ComFilterX|
|描述|The name of this attribute corresponds to the parameter name in the [17] specification of Reception Filtering.|
|描述|概述：ComFilterX 是 AUTOSAR Communication Stack 中的一个配置参数，用于定义PDU（Protocol Data Unit）的过滤机制，以确定哪些PDU应该被传递给上层软件组件。|
|描述|注意：在配置ComFilterX时，需要确保过滤条件与系统的通信需求相匹配；过滤器设置错误可能导致必要的数据被错误地过滤掉；在配置过滤器时，应当参照AUTOSAR CP 4.4标准中对应的通信管理模块的规范来确保兼容性和正确性。|
|描述|该配置项未使用|
|多实例个数|0 - 1|
|取值范围|-2147483648 - 4294967295|

### 1.6. ComMainFunctionTx

|容器属性|值（容器）|
|---|---|
|名称|ComMainFunctionTx|
|描述|Contains the configuration parameters of the AUTOSAR COM module's ComMainFunctionTx|
|描述|概述：ComMainFunctionTx是一个配置项，用于定义通信堆栈中传输管理模块的主函数调用周期，即指定ComTxIPdu（传输协议数据单元）的处理频率。|
|描述|注意：该配置项的值应当与ECU的发送需求和网络带宽相匹配，以避免网络拥塞或数据发送延迟；在配置时需考虑与其他通信相关功能（如Nm或PduR）的调用周期的协调；在AUTOSAR CP 4.4标准中，应确保该配置项的周期设置符合系统定时要求，并与其他BswM模块的调度协同工作。|
|多实例个数|0 - inf|

|配置项属性|值（浮点型参数配置项）|
|---|---|
|名称|MainTxTimeBase|
|描述|The period between successive calls to ComMainFunctionTx in seconds. This parameter may be used by the COM generator to transform the values of the transmission related timing configuration parameters of the COM module to internal implementation specific counter or tick values. The COM module's internal timing handling is implementation specific.|
|描述|概述：MainTxTimeBase 配置项用于定义发送消息的主时间基准，它决定了消息发送的时间间隔。|
|描述|注意：确保MainTxTimeBase的设置与系统的时间管理和调度策略相匹配；不正确的时间基准设置可能导致消息发送不及时或冲突；在分布式系统中，需要同步不同节点的时间基准以保证消息的一致性。|
|说明|The COM module (generator) may rely on the fact that ComMainFunctionTx is scheduled according to the value configured here.|
|多实例个数|0 - 1|
|取值范围|0 - Inf|

### 1.7. ComMainFunctionRx

|容器属性|值（容器）|
|---|---|
|名称|ComMainFunctionRx|
|描述|Contains the configuration parameters of the AUTOSAR COM module's ComMainFunctionRx|
|描述|概述：ComMainFunctionRx 是 AUTOSAR Communication Stack 中的一个配置参数，用于定义接收通信任务的周期性调用时间。|
|描述|注意：该配置项的周期设置应考虑系统的实时性要求和网络负载，以避免数据延迟或丢失；周期过短可能会增加系统负载，过长可能影响消息的及时处理；应与其他网络管理和通信服务的周期性调用相协调。|
|多实例个数|0 - inf|

|配置项属性|值（浮点型参数配置项）|
|---|---|
|名称|MainRxTimeBase|
|描述|The period between successive calls to ComMainFunctionRx in seconds. This parameter may be used by the COM generator to transform the values of the transmission related timing configuration parameters of the COM module to internal implementation specific counter or tick values. The COM module's internal timing handling is implementation specific.|
|描述|概述：MainRxTimeBase配置项定义了接收主时间基准，用于确定接收消息的时间精度和处理周期。|
|描述|注意：该配置项对于确保消息接收和处理的实时性至关重要；必须与系统中的其他时间基准配置保持一致，以避免时间同步问题；在配置时需考虑实际的网络延迟和处理能力，以设置合理的时间基准。|
|说明|The COM module (generator) may rely on the fact that ComMainFunctionRx is scheduled according to the value configured here.|
|多实例个数|0 - 1|
|取值范围|0 - Inf|

### 1.8. ComMainFunctionGw

|容器属性|值（容器）|
|---|---|
|名称|ComMainFunctionGw|
|描述|Contains the configuration parameters of the AUTOSAR COM module's ComMainFunctionGw|
|描述|概述：ComMainFunctionGw 是 AUTOSAR Communication Stack 中的一个配置项，用于控制网关通信任务的调度周期。|
|描述|注意：该配置项的周期设置应与系统的通信需求和性能指标相匹配；不正确的周期设置可能导致数据延迟或丢失；在多任务环境中，确保该函数的调度不会与其他关键任务冲突。|
|多实例个数|0 - inf|

|配置项属性|值（浮点型参数配置项）|
|---|---|
|名称|MainGwTimeBase|
|描述|The period between successive calls to ComMainFunctionGw in seconds. This parameter may be used by the COM generator to transform the values of the transmission related timing configuration parameters of the COM module to internal implementation specific counter or tick values. The COM module's internal timing handling is implementation specific.|
|描述|概述：MainGwTimeBase配置项用于定义网关模块的主时间基准，这是一个用于时间同步和调度的关键参数，它决定了网关任务的触发周期。|
|描述|注意：在配置MainGwTimeBase时，需要确保它与系统中其他模块的时间基准保持一致，以便于实现精确的时间同步；此外，该时间基准应该符合系统的实时性要求，以及满足网关数据处理和转发的性能需求；在AUTOSAR CP 4.4标准中，应当遵循时间和调度管理相关的规范来配置此项。|
|说明|The COM module (generator) may rely on the fact that ComMainFunctionGw is scheduled according to the value configured here.|
|多实例个数|0 - 1|
|取值范围|0 - Inf|

### 1.9. ComTxSignalFifo

|容器属性|值（容器）|
|---|---|
|名称|ComTxSignalFifo|
|描述|Contains the configuration parameters of the AUTOSAR COM module's ComTxSignalFifo|
|描述|概述：ComTxSignalFifo配置项用于定义通信堆栈中传输信号的FIFO（First-In-First-Out）缓冲区，多核重入调用Com_SendSignal时使用。|
|描述|注意：在AUTOSAR CP 4.4标准中，需要确保FIFO缓冲区的大小和管理策略符合系统的内存和性能要求；FIFO机制应当与通信接口的传输能力相匹配，避免数据溢出或延迟；配置时应注意与ComSignal和Pdu相关配置的一致性和兼容性。|
|多实例个数|0 - 1|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|ComSupportedTxSignalProx|
|描述|If this Parameter is set to true, TxSignalProx is enabled. If this Parameter is not present, TxSignalProx is assumed.|
|描述|概述：ComSupportedTxSignalProx配置项用于定义在AUTOSAR通信堆栈中，哪些发送信号支持代理（Proxies）功能，即允许通过网络管理器或其他机制代理发送信号。|
|描述|注意：在AUTOSAR CP 4.4标准中，对于使用代理发送机制的信号，需要确保网络管理策略与代理发送策略兼容；代理发送功能主要用于网络管理和节能策略，因此需要谨慎配置；此配置项在设计时需考虑系统的实时性和网络带宽限制。|
|多实例个数|0 - 1|
|默认值|true|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|MaxDequeueCntOneCycle|
|描述|Defines the MaxDequeueCntOneCycle of Fifo.|
|描述|概述：MaxDequeueCnt配置项用于定义用户配置单次最大的出队次数（当该值配置小于200次 会默认使用200作为单次出队的阈值）|
|描述|注意：用户需要考虑单次出队次数越多 runable执行时间越长 该次数需要用户自己测试评估|
|多实例个数|1 - 1|
|取值范围|0 - 65535|
|默认值|0|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|Uint8FifoDepth|
|描述|Defines the Depth of Uint8 Type Fifo.|
|描述|概述：Uint8FifoDepth配置项用于定义UINT8类型的FIFO（可存放1字节数据）队列的深度，即队列可以存储的元素数量上限，常用于缓冲区大小的设置。|
|描述|注意：在设置Uint8FifoDepth时，需要确保其值不超过数据类型允许的最大值，即255；过小的FifoDepth可能导致数据溢出，过大的FifoDepth可能会导致不必要的内存消耗；在AUTOSAR CP 4.4中，确保该配置项与实际应用场景的内存管理策略相匹配。|
|多实例个数|1 - 1|
|取值范围|0 - 65535|
|默认值|0|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|Uint16FifoDepth|
|描述|Defines the Depth of Uint16 Type Fifo.|
|描述|概述：Uint16FifoDepth 配置项用于定义一个UINT16类型的FIFO（可存放2字节数据）缓冲区的深度，即缓冲区可以存储的元素数量。|
|描述|注意：在配置Uint16FifoDepth时，需要确保缓冲区深度与系统内存资源和性能要求相匹配；过大的FIFO深度可能会导致不必要的内存消耗，而过小可能导致数据溢出或丢失；此配置项应与相关的数据处理速率和任务调度策略相协调。|
|多实例个数|1 - 1|
|取值范围|0 - 65535|
|默认值|0|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|Uint32FifoDepth|
|描述|Defines the Depth of Uint32 Type Fifo.|
|描述|概述：Uint32FifoDepth 配置项用于定义一个UINT32类型的FIFO（可存放4字节数据）缓冲区的深度，即缓冲区可以存储的元素数量。|
|描述|注意：在配置Uint32FifoDepth时，需要确保队列深度与系统内存和性能要求相匹配；过大的队列深度可能会导致不必要的内存消耗；此配置项在AUTOSAR CP 4.4标准中未明确定义，具体实现可能依赖于软件架构或组件的具体要求。|
|多实例个数|1 - 1|
|取值范围|0 - 65535|
|默认值|0|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|Uint8_NFifoDepth|
|描述|Defines the Depth of Uint8_N Type Fifo.|
|描述|概述：Uint8_NFifoDepth 是一个配置项，用于指定Uint8_N（用户可自定义大小）队列的深度，这个队列用于存储等待传输的网络帧。|
|描述|注意：该配置项的值必须根据系统的缓冲需求和内存限制来设定；过大的值可能会导致不必要的内存消耗，而过小的值可能导致网络帧丢失；在AUTOSAR CP 4.4标准中，该值应该是一个8位无符号整数，确保配置值在0到255的范围内。|
|多实例个数|1 - 1|
|取值范围|0 - 65535|
|默认值|0|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|Uint8_NFifoSize|
|描述|Defines the Size of Uint8_N Type Fifo.|
|描述|概述：Uint8_NFifoSize 是一个配置项，用于指定Uint8_N（用户可自定义）队列的的大小，这个大小是以字节为单位的，用于存储接收到的网络帧。|
|描述|注意：在配置Uint8_NFifoSize时，需要确保FIFO的大小足以容纳预期的网络流量，避免数据丢失；此外，FIFO大小的配置应考虑到系统内存资源的限制，以免造成内存溢出；根据AUTOSAR CP 4.4标准，该配置项的数据类型应为无符号8位整数，如果配置的数据类型与此不符，需要进行调整。|
|多实例个数|1 - 1|
|取值范围|0 - 65535|
|默认值|0|

|配置项属性|值（浮点型参数配置项）|
|---|---|
|名称|ProxyPeriodicTime|
|描述|The period between successive calls to ProxyPeriodicTime in seconds.|
|描述|概述：ProxyPeriodicTime 配置项用于指定AUTOSAR软件组件中的代理端口（Proxy Port）发送周期性数据的时间间隔，确保周期性数据按照预定的时间间隔发送。|
|描述|注意：ProxyPeriodicTime 的值必须与系统的时间基准和调度策略相匹配；在配置周期性发送时间时，应考虑系统的实时性要求和网络带宽限制；如果配置的周期时间与实际的任务调度周期不一致，可能会导致数据发送不准确或者丢失。|
|说明|The COM module (generator) may rely on the fact that ProxyPeriodicTime is scheduled according to the value configured here.|
|多实例个数|1 - 1|
|取值范围|0 - Inf|
|默认值|0.005|

## 2. ComGeneral

|容器属性|值（容器）|
|---|---|
|名称|ComGeneral|
|描述|Contains the general configuration parameters of the module.|
|描述|概述：ComGeneral是AUTOSAR通信堆栈的一部分，它定义了通用的配置参数，这些参数影响整个通信堆栈的行为，如模块的激活状态、版本信息等。|
|描述|注意：在配置ComGeneral时，需要确保所选参数与系统需求相匹配；注意版本兼容性，确保配置项符合AUTOSAR CP 4.4标准；某些参数可能会影响通信性能，因此需要仔细评估。|
|多实例个数|1 - 1|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|ComCancellationSupport|
|描述|This parameter enables/disables the cancellation feature:|
|描述|概述：ComCancellationSupport 配置项用于指定通信堆栈是否支持IPDU（即消息或数据包）的取消传输功能，这允许在传输过程中停止IPDU的发送。|
|描述|注意：在配置ComCancellationSupport时，需要确保底层的通信硬件和驱动支持取消传输的功能；如果启用了取消传输，可能会对系统的实时性和带宽有影响；AUTOSAR CP 4.4标准中，该配置项应与其他相关配置项（如ComTxIPdu）保持一致性。|
|描述|该配置项未使用|
|说明|true: enabled false: disabled|
|多实例个数|0 - 1|
|默认值|true|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|ComConfigurationUseDet|
|描述|The error hook shall contain code to call the Det.|
|描述|概述：ComConfigurationUseDet 是一个配置项，用于指定是否在通信堆栈中启用开发错误检测（Development Error Tracer, Det）。|
|描述|注意：在AUTOSAR CP 4.4标准中，开发者需要根据系统的诊断需求决定是否启用Det；如果启用，必须确保Det模块已经集成到系统中；在生产代码中通常会禁用Det以节省资源和提高性能。|
|说明|If this parameter is configured COM_DEV_ERROR_DETECT shall be set to ON as output of the configuration tool. (as input for the source code).|
|多实例个数|0 - 1|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|ComEnableMDTForCyclicTransmission|
|描述|Enables globally for the whole Com module the minimum delay time monitoring for cyclic and repeated transmissions (ComTxModeMode=PERIODIC or ComTxModeMode=MIXED for the cyclic transmissions, ComTxModeNumberOfRepetitions \> 0 for repeated transmissions).|
|描述|概述：ComEnableMDTForCyclicTransmission 配置项用于启用或禁用最小延迟时间（Minimum Delay Time, MDT）机制，该机制用于循环传输的消息，以防止网络上的拥塞。|
|描述|注意：在配置最小延迟时间时，需要确保设置的MDT值不会违反网络的带宽限制；MDT设置应考虑到所有周期性消息的传输需求，以避免对实时性能的影响；在AUTOSAR CP 4.4标准中，该配置项应与网络管理和通信堆栈的其他部分协同工作，以确保整体系统的稳定性和性能。|
|描述|该配置项未使用|
|多实例个数|0 - 1|
|默认值|true|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|ComEnableSignalGroupArrayApi|
|描述|Activate/Deactivate the signal group array access APIs (Com_SendSignalGroupArray, Com_ReceiveSignalGroupArray).|
|描述|概述：ComEnableSignalGroupArrayApi 是一个配置项，用于启用或禁用 AUTOSAR Communication Stack 中的 Signal Group Array API 功能，该功能允许用户以数组的形式访问信号组中的所有信号。|
|描述|注意：在使用此配置项时，需要确保应用层确实需要通过数组的方式访问信号组；此外，启用此API可能会对系统资源和性能产生影响，因此在资源受限的系统中使用时应谨慎；最后，根据AUTOSAR CP 4.4标准，应检查相关模块是否支持此API，以保证配置的兼容性。|
|描述|该配置项未使用|
|说明|true: signal group array access APIs activated false: signal group array access APIs deactivated|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|ComMetaDataSupport|
|描述|This parameter enables/disables the support of meta-data feature including the API Com_TriggerIPDUSendWithMetaData.|
|描述|概述：ComMetaDataSupport配置项用于定义是否在通信堆栈中支持元数据的传输，允许在发送或接收消息时附加额外的信息，如消息的发送者或时间戳。|
|描述|注意：在AUTOSAR CP 4.4标准中，元数据的支持是可选的，需要根据项目需求决定是否启用；如果启用，需确保所有相关组件和模块都支持元数据处理；配置时应注意元数据的大小和格式，以避免影响消息传输效率。|
|描述|该配置项未使用|
|说明|true: enabled false: disabled|
|多实例个数|0 - 1|
|默认值|false|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|ComRetryFailedTransmitRequests|
|描述|If this Parameter is set to true, retry of failed transmission requests is enabled. If this Parameter is not present, the default value is assumed.|
|描述|概述：ComRetryFailedTransmitRequests 是一个配置项，用于指定是否应该重试传输失败的通信请求。|
|描述|注意：在AUTOSAR CP 4.4标准中，确保此配置项与系统的错误处理策略和通信需求相一致；重试机制可能会影响系统的实时性和带宽，因此需要谨慎配置；此配置项的使用应当考虑到网络的拥塞管理和错误恢复策略。|
|多实例个数|0 - 1|
|默认值|false|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|ComVersionInfoApi|
|描述|Activate/Deactivate the version information API (Com_GetVersionInfo).|
|描述|概述：ComVersionInfoApi 配置项用于启用或禁用通信堆栈的版本信息API，这允许软件组件获取通信模块的版本信息。|
|描述|注意：在AUTOSAR CP 4.4标准中，通常建议在生产代码中禁用版本信息API，以减少内存占用和避免潜在的安全问题；如果启用，需要确保对应的API函数符合AUTOSAR标准的命名和实现规范；在开发或测试阶段，可以启用此功能以帮助诊断和验证软件版本。|
|描述|该配置项未使用|
|说明|True: version information API activated False: version information API deactivated|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|ComSupportedIPduGroups|
|描述|Defines the maximum number of supported I-PDU groups.|
|描述|概述：ComSupportedIPduGroups 配置项定义了通信堆栈中支持的IPDU（协议数据单元）组，这些组用于管理IPDU的传输属性和状态。|
|描述|注意：在配置ComSupportedIPduGroups时，需要确保每个IPDU组的标识符是唯一的；此外，应当注意IPDU组与具体的IPDU之间的关联关系，以保证正确的数据传输和接收；根据AUTOSAR CP 4.4标准，还需要考虑IPDU组的激活和停用机制，确保在运行时可以控制IPDU的传输。|
|多实例个数|1 - 1|
|取值范围|0 - 65535|

|配置项属性|值（字符串参数配置项）|
|---|---|
|名称|ComUserCbkHeaderFile|
|描述|Defines the header files for callback functions which shall be included by the COM module.|
|描述|概述：ComUserCbkHeaderFile是一个配置参数，用于指定用户定义的回调函数的头文件名称，该文件包含了由COM模块调用的回调函数的声明。|
|描述|注意：文件名应确保与实际的头文件名匹配，以便正确地包含所需的回调函数声明；路径应正确设置以确保编译器可以找到该头文件；在AUTOSAR CP 4.4标准中，应遵循命名和路径约定以保持一致性。|
|多实例个数|0 - inf|
