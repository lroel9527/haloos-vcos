# CanSM 配置项参考文档

|容器属性|值（容器）|
|---|---|
|名称|CanSM|
|描述|Configuration of the CanSM module|
|多实例个数|0 - 1|

## 1. CanSMConfiguration

|容器属性|值（容器）|
|---|---|
|名称|CanSMConfiguration|
|描述|This container contains the global parameters of the CanSM and sub containers, which are for the CAN network specific configuration.|
|多实例个数|1 - 1|

|配置项属性|值（浮点型参数配置项）|
|---|---|
|名称|CanSMModeRequestRepetitionTime|
|描述|Specifies in which time duration the CanSM module shall repeat mode change requests by using the API of the CanIf module.|
|多实例个数|1 - 1|
|取值范围|0 - 65.535|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CanSMModeRequestRepetitionMax|
|描述|Specifies the maximal amount of mode request repetitions without a respective mode indication from the CanIf module until the CanSM module reports a Development Error to the Det and tries to go back to no communication.|
|多实例个数|1 - 1|
|取值范围|0 - 255|

### 1.1. CanSMManagerNetwork

|容器属性|值（容器）|
|---|---|
|名称|CanSMManagerNetwork|
|描述|This container contains the CAN network specific parameters of each CAN network|
|多实例个数|1 - inf|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|CanSMBorTxConfirmationPolling|
|描述|This parameter shall configure, if the CanSM polls the CanIf_GetTxConfirmationState API to decide the bus-off state to be recovered instead of using the CanSMBorTimeTxEnsured parameter for this decision.|
|多实例个数|1 - 1|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|CanSMEnableBusOffDelay|
|描述|This parameter defines if the \<User_GetBusOffDelay\> shall be called for this network.|
|多实例个数|0 - 1|
|默认值|false|

|配置项属性|值（浮点型参数配置项）|
|---|---|
|名称|CanSMBorTimeL1|
|描述|This time parameter defines in seconds the duration of the bus-off recovery time in level 1 (short recovery time).|
|多实例个数|1 - 1|
|取值范围|0 - 65.535|
|默认值|0.1|

|配置项属性|值（浮点型参数配置项）|
|---|---|
|名称|CanSMBorTimeL2|
|描述|This time parameter defines in seconds the duration of the bus-off recovery time in level 2 (long recovery time).|
|多实例个数|1 - 1|
|取值范围|0 - 65.535|
|默认值|1|

|配置项属性|值（浮点型参数配置项）|
|---|---|
|名称|CanSMBorTimeTxEnsured|
|描述|This parameter defines in seconds the duration of the bus-off event check. This check assesses, if the recovery has been successful after the recovery reenables the transmit path. If a new bus-off occurs during this time period, the CanSM assesses this bus-off as sequential bus-off without successful recovery. Because a bus-off only can be detected, when PDUs are transmitted, the time has to be great enough to ensure that PDUs are transmitted again (e. g. time period of the fastest cyclic transmitted PDU of the COM module / ComTxModeTimePeriodFactor).|
|多实例个数|1 - 1|
|取值范围|0 - 65.535|
|默认值|2|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CanSMBorCounterL1ToL2|
|描述|This threshold defines the count of bus-offs until the bus-off recovery switches from level 1 (short recovery time) to level 2 (long recovery time).|
|多实例个数|1 - 1|
|取值范围|0 - 255|
|默认值|5|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|CanSMComMNetworkHandleRef|
|描述|Unique handle to identify one certain CAN network. Reference to one of the network handles configured for the ComM.|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/ComM/ComMConfigSet/ComMChannel|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|CanSMTransceiverId|
|描述|ID of the CAN transceiver assigned to the configured network handle. Reference to one of the transceivers managed by the CanIf module.|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/CanIf/CanIfTrcvDrvCfg/CanIfTrcvCfg|

#### 1.1.1. CanSMController

|容器属性|值（容器）|
|---|---|
|名称|CanSMController|
|描述|This container contains the controller IDs assigned to a CAN network.|
|多实例个数|1 - 1|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|CanSMControllerId|
|描述|Unique handle to identify one certain CAN controller. Reference to one of the CAN controllers managed by the CanIf module.|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/CanIf/CanIfCtrlDrvCfg/CanIfCtrlCfg|

#### 1.1.2. CanSMDemEventParameterRefs

|容器属性|值（容器）|
|---|---|
|名称|CanSMDemEventParameterRefs|
|描述|Container for the references to DemEventParameter elements which shall be invoked using the API Dem_SetEventStatus in case the corresponding error occurs. The EventId is taken from the referenced DemEventParameter's DemEventId symbolic value. The standardized errors are provided in this container and can be extended by vendor-specific error references.|
|多实例个数|0 - 1|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|CANSM_E_BUS_OFF|
|描述|Reference to configured DEM event to report bus off errors for this CAN network.|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Dem/DemConfigSet/DemEventParameter|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|CANSM_E_MODE_REQUEST_TIMEOUT|
|描述|Reference to configured DEM event to report bus off errors for this CAN network.|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Dem/DemConfigSet/DemEventParameter|

### 1.2. CanSMMainFunction

|容器属性|值（容器）|
|---|---|
|名称|CanSMMainFunction|
|描述|Contains the configuration parameters of the AUTOSAR CanSM module's CanSMMainFunction.|
|描述|概述：CanSMMainFunction是一个配置项，用于定义CAN网络管理（CANSM）中的主函数，这些主函数用于taskmapping。在未添加本项实例时，生成的默认主函数周期为10ms|
|描述|注意：在配置CanSMMainFunction时，需要确保其与taskmapping功能相匹配；此外，该配置项的属性应符合AUTOSAR CP 4.4标准中对CANSM的规定。|
|多实例个数|1 - 255|

|配置项属性|值（浮点型参数配置项）|
|---|---|
|名称|CanSMMainFunctionPeriod|
|描述|Call cycle in seconds of CanSM_MainFunction.|
|描述|概述：CanSMMainFunctionPeriod配置项指定了CAN状态管理主函数（CanSM_MainFunction）的调用周期，这个周期决定了CAN状态管理功能的执行频率。|
|描述|注意：该值必须与系统定时器和OS任务调度配置相匹配，以确保准确的时间行为；过小的周期可能导致系统过载，而过大的周期可能导致网络管理响应不及时；在配置时需要考虑到ECU的性能和网络的实时性要求。|
|多实例个数|0 - 1|
|默认值|0.005|
|取值范围|0 - 65.535|

## 2. CanSMGeneral

|容器属性|值（容器）|
|---|---|
|名称|CanSMGeneral|
|描述|Container for general pre-compile parameters of the CanSM module|
|多实例个数|1 - 1|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|CanSMDevErrorDetect|
|描述|Switches the development error detection and notification on or off.|
|说明|\* true: detection and notification is enabled. \* false: detection and notification is disabled.|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|CanSMIcomSupport|
|描述|Selects support of Pretended Network features in CanSM.|
|说明|True: Enabled False: Disabled|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|CanSMPncSupport|
|描述|Enables or disables support of partial networking.|
|说明|False: Partial Networking is disabled True: Partial Networking is enabled|
|多实例个数|0 - 1|
|默认值|false|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|CanSMSetBaudrateApi|
|描述|The support of the Can_SetBaudrate API is optional. If this parameter is set to true the Can_SetBaudrate API shall be supported. Otherwise the API is not supported.|
|多实例个数|0 - 1|
|默认值|false|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|CanSMTxOfflineActiveSupport|
|描述|Determines whether the ECU passive feature is supported by CanSM.|
|说明|True: Enabled False: Disabled|
|多实例个数|0 - 1|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|CanSMVersionInfoApi|
|描述|Activate/Deactivate the version information API (CanSM_GetVersionInfo).|
|说明|true: version information API activated false: version information API deactivated|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（函数名配置项）|
|---|---|
|名称|CanSMGetBusOffDelayFunction|
|描述|This parameter configures the name of the \<User_GetBusOffDelay\> callout function, which is used by CanSM to acquire an additional L1/L2 delay time. This function is only called for channels where CanSMEnableBusOffDelay is enabled.|
|多实例个数|0 - 1|

|配置项属性|值（函数名配置项）|
|---|---|
|名称|BusOffBeginFunction|
|描述|Name of Com_CbkCounterErr callback function to be called. If this|
|说明|parameter is omitted no I-PDU counter mismatch notification shall take place.|
|多实例个数|0 - 1|

|配置项属性|值（函数名配置项）|
|---|---|
|名称|BusOffEndFunction|
|描述|Name of Com_CbkCounterErr callback function to be called. If this|
|说明|parameter is omitted no I-PDU counter mismatch notification shall take place.|
|多实例个数|0 - 1|

|配置项属性|值（字符串参数配置项）|
|---|---|
|名称|CanSMGetBusOffDelayHeader|
|描述|This parameter configures the header file containing the prototype of the \<User_GetBusOffDelay\> callout function.|
|多实例个数|0 - 1|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CanSMSpinlockRetryCounter|
|描述|The maximal retry counter when trying to get spinlock. When empty the maximal counter is 255|
|描述|自旋锁尝试最大次数，不配置时默认为255|
|多实例个数|0 - 1|
|默认值|255|
|取值范围|0 - 65535|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CanSMInitFastExecuteThreshold|
|描述|The maximal loop counter when invoke state machine execution function during init process. The Threshold will be 3 if empty|
|描述|初始化阶段允许快速切换机制最大循环次数，不配置时默认为3|
|多实例个数|0 - 1|
|默认值|3|
|取值范围|1 - 255|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CanSMMainFuncFastExecuteThreshold|
|描述|The maximal loop counter when invoke state machine execution function during main function process. The Threshold will be 3 if empty|
|描述|周期函数阶段允许快速切换机制最大循环次数，不配置时默认为3|
|多实例个数|0 - 1|
|默认值|3|
|取值范围|1 - 255|
