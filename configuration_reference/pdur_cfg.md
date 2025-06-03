# PduR 配置项参考文档

|容器属性|值（容器）|
|---|---|
|名称|PduR|
|描述|Configuration of the PduR (PDU Router) module.|
|多实例个数|0 - 1|

## 1. PduRBswModules

|容器属性|值（容器）|
|---|---|
|名称|PduRBswModules|
|描述|Each container describes a specific BSW module (upper/CDD/lower/IpduM) that the PDU Router shall interface to.|
|说明|The reason to have it as own configuration container instead of implication of the routing path is to be able to configure CDDs properly and to force module's to be used in a post-build situation even though no routing is made to/from this module (future configurations may include these modules).|
|多实例个数|0 - 65535|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|PduRCancelReceive|
|描述|Specifies if the Transport protocol module supports the CancelReceive API or not. Value true the API is supported.|
|多实例个数|1 - 1|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|PduRCancelTransmit|
|描述|Specifies if the BSW module supports the CancelTransmit API or not. Value true the API is supported.|
|多实例个数|1 - 1|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|PduRCommunicationInterface|
|描述|Specifies if the BSW module supports the Communication Interface APIs or not. Value true the APIs are supported.|
|说明|A module can have both Communication Interface APIs and Transport Protocol APIs (e.g. the COM module).|
|多实例个数|1 - 1|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|PduRLowerModule|
|描述|The PduRLowerModule will decide who will call the APIs and who will implement the APIs.|
|说明|For example, if the CanIf module is referenced then the PDU Router module will implement the PduR_CanIfRxIndication API. And the PDUR module will call the CanIf_Transmit API. Other APIs are of course also covered. An upper module can also be an lower module (e.g. the IpduM module).|
|多实例个数|1 - 1|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|PduRRetransmission|
|描述|If set to true this means that the destination transport protocol module will use the retransmission feature. This parameter might be set to false if the retransmission feature is not used, even though the destination transport protocol is supporting it.|
|说明|This parameter is only valid for transport protocol modules and gateway operations. If transmission from a local upper layer module this module will handle the retransmission.|
|多实例个数|1 - 1|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|PduRTransportProtocol|
|描述|The PDU Router module shall use the API parameters specified for transport protocol interface.|
|多实例个数|1 - 1|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|PduRTriggertransmit|
|描述|Specifies if the BSW module supports the TriggerTransmit API or not. Value true means that the BSW module supports the TriggerTransmit interface which a lower layer module can call and also that it can call the TriggerTransmit interface of an upper layer module. Value false means that the BSW module does not support the TriggerTransmit interface which a lower layer module can call and also that it shall not call the TriggerTransmit interface of an upper layer module.|
|多实例个数|1 - 1|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|PduRTxConfirmation|
|描述|Specifies if the BSW module supports the TxConfirmation API or not. Value true the API is supported.|
|多实例个数|1 - 1|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|PduRUpperModule|
|描述|The PduRUpperModule will decide who will call the APIs and who will implement the APIs.|
|说明|For example, if the COM module is referenced then the PDU Router module will implement the PduR_Transmit API. And the PDUR module will call the Com_RxIndication API. Other APIs are of course also covered. An upper module can also be an lower module (e.g. the IpduM module).|
|多实例个数|1 - 1|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|PduRUseTag|
|描述|This parameter, if set to true, enables the usage of the tag (\<up\>) in the following API calls:|
|说明|\* PduR_\<Up\>CancelReceive \* PduR_\<Up\>CancelTransmit Example: If used by COM and the parameter is enabled the PduR_ComCancelTransmit is used. The background is that upper layer modules differ in usage of this tag (e.g. COM is using the tag, DCM is not).|
|多实例个数|1 - 1|

|配置项属性|值（外部引用配置项）|
|---|---|
|名称|PduRBswModuleRef|
|描述|This is a reference to one BSW module's configuration (i.e. not the ECUC parameter definition template).|
|说明|Example, there could be several configurations of LinIf and this reference selects one of them.|
|多实例个数|1 - 1|
|目标类型|ECUC-MODULE-CONFIGURATION-VALUES|

## 2. PduRGeneral

|容器属性|值（容器）|
|---|---|
|名称|PduRGeneral|
|描述|This container is a subcontainer of PduR and specifies the general configuration parameters of the PDU Router.|
|多实例个数|1 - 1|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|PduRDevErrorDetect|
|描述|Switches the development error detection and notification on or off.|
|说明|\* true: detection and notification is enabled. \* false: detection and notification is disabled.|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|PduRMetaDataSupport|
|描述|Enable support for MetaData handling. The MetaData is defined by the referenced MetaDataType of the global PDU definitions. This feature may be used for efficient address based routing and generic CAN-CAN-routing, where the MetaData contains the CAN ID.|
|多实例个数|0 - 1|
|默认值|false|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|PduRSpinlockRetryCounter|
|描述|Defines the number of PduR spin lock retry.|
|多实例个数|1 - 1|
|默认值|3|
|取值范围|0 - 255|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|PduRVersionInfoApi|
|描述|If true the PduR_GetVersionInfo API is available.|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|PduRZeroCostOperation|
|描述|If set the PduR configuration generator will report an error if zero-cost-operation cannot be fulfilled.|
|说明|This parameter shall be seen as an input requirement to the configuration generator.|
|多实例个数|1 - 1|

## 3. PduRRoutingPaths

|容器属性|值（容器）|
|---|---|
|名称|PduRRoutingPaths|
|描述|Represents one table of routing paths.|
|说明|This routing table allows multiple configurations that can be used to create several routing tables in the same configuration. This is mainly used for post-build (e.g. post-build selectable) but can be used by pre-compile and link-time for variant handling.|
|多实例个数|1 - 1|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|PduRConfigurationId|
|描述|Identification of the configuration of the PduR configuration. This identification can be read using the PduR API.|
|多实例个数|1 - 1|
|取值范围|0 - 65535|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|PduRMaxRoutingPathCnt|
|描述|Maximum number of RoutingPaths in all RoutingTables. This parameter is needed only in case of post-build loadable implementation using static memory allocation.|
|多实例个数|0 - 1|
|取值范围|0 - 65535|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|PduRMaxRoutingPathGroupCnt|
|描述|Maximum number of RoutingPathGroups. This parameter is needed only in case of post-build loadable implementation using static memory allocation.|
|多实例个数|0 - 1|
|取值范围|0 - 65535|

### 3.1. PduRDestPdu

|容器属性|值（容器）|
|---|---|
|名称|PduRDestPdu|
|描述|This container is a subcontainer of PduRRoutingPath and specifies one destination for the PDU to be routed.|
|多实例个数|0 - 65535|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|PduRTransmissionConfirmation|
|描述|This parameter is only for communication interfaces. Transport protocol modules will always call the TxConfirmation function.|
|说明|If set the destination communication interface module will call the TxConfirmation. However the TxConfirmation may be not called due to error. So the PduR shall not block until the TxConfirmation is called. One background for this parameter is for the PduR to know when all modules have confirmed a multicast operation.|
|多实例个数|1 - 1|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|PduRDestPduDataProvision|
|描述|Specifies how data are provided: direct (as part of the Transmit call) or via|
|说明|the TriggerTransmit callback function. Only required for non-TP gatewayed I-PDUs.|
|多实例个数|0 - 1|
|默认值|PDUR_DIRECT|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|PduRDestPduLengthHandlingStrategy|
|描述|Pdu length handling strategy while destination Pdu lengh is langer than Pdu length in EcuC|
|说明|This parameter is only used for communication interface routings. It is ignored for transmport protocol routings.|
|多实例个数|0 - 1|
|默认值|PDUR_STRATEGY_UNUSED|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|PduRDestPduHandleId|
|描述|PDU identifier assigned by PDU Router. Used by communication interface and transport protocol modules for confirmation (PduR_\<Lo\>TxConfirmation) and for TriggerTransmit (PduR_\<Lo\>TriggerTransmit).|
|多实例个数|0 - 1|
|取值范围|0 - 65535|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|PduRDestPduRef|
|描述|Destination PDU reference; reference to unique PDU identifier which shall be used by the PDU Router instead of the source PDU ID when calling the related function of the destination module.|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/EcuC/EcucConfigSet/EcucPduCollection/Pdu|

### 3.2. PduRRoutingPath

|容器属性|值（容器）|
|---|---|
|名称|PduRRoutingPath|
|描述|This container is a subcontainer of PduRRoutingTable and specifies the routing path of a PDU.|
|多实例个数|0 - 65535|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|PduRQueueDepth|
|描述|This parameter defines the queue depth for this routing path.|
|多实例个数|0 - 1|
|取值范围|1 - 255|
|默认值|1|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|PduRTpThreshold|
|描述|This parameter is only relevant for TP routings.|
|说明|When configured, it enables on-the-fly routing and defines the number of bytes which must have been received before transmission on the destination bus may start. When omitted, direct TP routing is enforced. The PduRouter shall ensure that a buffer is allocated for this routing path which is at least as large as the threshold.|
|多实例个数|0 - 1|
|取值范围|0 - 65535|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|PduRDestPduRRef|
|多实例个数|1 - 255|
|目标引用项的路径|/AUTOSAR/EcucDefs/PduR/PduRRoutingPaths/PduRDestPdu|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|PduRDestTxBufferRef|
|描述|Reference to a buffer in the PduR. This buffer is required for communication interface gatewaying, and for transport protocol gatewaying.|
|多实例个数|0 - 65535|
|目标引用项的路径|/AUTOSAR/EcucDefs/PduR/PduRRoutingPaths/PduRTxBuffer|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|PduRSrcPduRRef|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/PduR/PduRRoutingPaths/PduRSrcPdu|

#### 3.2.1. PduRDefaultValue

|容器属性|值（容器）|
|---|---|
|名称|PduRDefaultValue|
|描述|Specifies the default value of the I-PDU. Only required for gateway operation and if at least one PDU specified by PduRDestPdu uses TriggerTransmit Data provision.|
|说明|Represented as an array of IntegerParamDef.|
|多实例个数|0 - 1|

##### 3.2.1.1. PduRDefaultValueElement

|容器属性|值（容器）|
|---|---|
|名称|PduRDefaultValueElement|
|描述|Each value element is represented by the element and the position in an array.|
|多实例个数|0 - 255|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|PduRDefaultValueElement|
|描述|The default value consists of a number of elements. Each element is one byte long and the number of elements is specified by SduLength. The position of this parameter in the container is specified by the PduRElementBytePosition parameter.|
|多实例个数|1 - 1|
|取值范围|0 - 255|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|PduRDefaultValueElementBytePosition|
|描述|This parameter specifies the byte position of the element within the default value|
|多实例个数|1 - 1|
|取值范围|0 - 4294967294|

### 3.3. PduRRoutingPathGroup

|容器属性|值（容器）|
|---|---|
|名称|PduRRoutingPathGroup|
|描述|This container groups routing path destinations. Destinations are used instead of routing paths since a routing path can be 1:n. It is desirable to be able to enable/disable a specific bus (i.e. a destination) rather than a routing path. Of course it is possible to create groups that covers specific routing paths as well.|
|说明|Enabling and disabling of routing path groups are made using the PduR API|
|多实例个数|0 - 65535|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|PduRIsEnabledAtInit|
|描述|If set to true this routing path group will be enabled after initializing the PDU Router module (i.e. enabled in the PduR_Init function).|
|多实例个数|1 - 1|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|PduRRoutingPathGroupId|
|描述|Identification of the routing group.|
|说明|The identification will be used by the disable/enable API in the PDU Router module API.|
|多实例个数|1 - 1|
|取值范围|0 - 65535|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|PduRDestPduRRef|
|多实例个数|1 - 255|
|目标引用项的路径|/AUTOSAR/EcucDefs/PduR/PduRRoutingPaths/PduRDestPdu|

### 3.4. PduRSrcPdu

|容器属性|值（容器）|
|---|---|
|名称|PduRSrcPdu|
|描述|This container is a subcontainer of PduRRoutingPath and specifies the source of the PDU to be routed.|
|多实例个数|0 - 65535|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|PduRSrcPduUpTxConf|
|描述|When enabled, the TxConfirmation will be|
|说明|forwarded to the upper layer. Prerequisites: Lower layer and upper layer support TxConfirmation.|
|多实例个数|1 - 1|
|默认值|true|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|PduRSourcePduBlockSize|
|描述|Minimum amount of buffer space required by receiving transport protocol layer to continue reception.|
|多实例个数|0 - 1|
|取值范围|1 - 4294967295|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|PduRSourcePduHandleId|
|描述|PDU identifier assigned by PDU Router.|
|多实例个数|1 - 1|
|取值范围|0 - 65535|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|PduRSrcPduRef|
|描述|Source PDU reference; reference to unique PDU identifier which shall be used for the requested PDU Router operation.|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/EcuC/EcucConfigSet/EcucPduCollection/Pdu|

### 3.5. PduRTxBuffer

|容器属性|值（容器）|
|---|---|
|名称|PduRTxBuffer|
|描述|Specifies a buffer used for gatewaying via communication interfaces or transport protocols.|
|多实例个数|0 - 65535|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|PduRPduMaxLength|
|描述|Length of the Tx buffer in bytes. This parameter limits the size of buffered routed PDUs.|
|多实例个数|1 - 1|
|取值范围|1 - 65535|

### 3.6. PduRBufferPool

|容器属性|值（容器）|
|---|---|
|名称|PduRBufferPool|
|描述|Specifies a buffer used for event cache situation.|
|多实例个数|0 - 255|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|PduRBufferPoolBlockSize|
|描述|Length of buffer poll block.|
|多实例个数|1 - 1|
|默认值|8|
|取值范围|1 - 65535|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|PduRBufferPoolBlockNumber|
|描述|Number of buffer poll block.|
|多实例个数|1 - 1|
|默认值|10|
|取值范围|1 - 65535|

## 4. PduRMainFunction

|容器属性|值（容器）|
|---|---|
|名称|PduRMainFunction|
|描述|Contains the configuration parameters of the AUTOSAR PduR module's PduRMainFunction.|
|描述|概述：PduRMainFunction是一个配置项，用于定义PduR模块的主函数，这些主函数用于taskmapping。在未添加本项实例时，生成的默认主函数周期为1ms|
|描述|注意：在配置PduRMainFunction时，需要确保其与taskmapping功能相匹配；此外，该配置项的属性应符合AUTOSAR CP 4.4标准中对PduR的规定。|
|多实例个数|0 - 255|

|配置项属性|值（浮点型参数配置项）|
|---|---|
|名称|PduRMainFunctionPeriod|
|描述|Call cycle in seconds of PduRMainFunction.|
|描述|概述：PduRMainFunctionPeriod配置项指定了CAN状态管理主函数（PduRMainFunction）的调用周期，这个周期决定了PduR跨核路由时异步跨核传输的执行频率。|
|描述|注意：该值必须与系统定时器和OS任务调度配置相匹配，以确保准确的时间行为；在配置时需要考虑到ECU的性能和网络的实时性要求。|
|多实例个数|0 - 1|
|默认值|0.001|
|取值范围|0 - 65.535|

## 5. PduRInterruptServiceRoutine

|容器属性|值（容器）|
|---|---|
|名称|PduRInterruptServiceRoutine|
|描述|Contains the configuration parameters of the AUTOSAR PduR module's PduRMainFunction.|
|描述|概述：PduRInterruptServiceRoutine是一个配置项，用于IF类消息跨核路由的目的核触发功能|
|描述|注意：在配置PduRInterruptServiceRoutine时，需要确保会关联到正确的中断上。|
|多实例个数|0 - 255|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|PduROsIsrRef|
|描述|Destination PDU reference; reference to unique PDU identifier which shall be used by the PDU Router instead of the source PDU ID when calling the related function of the destination module.|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Os/OsIsr|
