# CanIf 配置项参考文档

|容器属性|值（容器）|
|---|---|
|名称|CanIf|
|描述|This container includes all necessary configuration sub-containers according the CAN Interface configuration structure.|
|描述|概述：CanIf是Controller Area Network Interface的缩写，它提供了一个抽象层，使上层软件（如应用层和网络管理）能够通过标准的API访问CAN控制器和CAN转换器。|
|描述|注意：在配置CanIf时，需要确保其与底层CAN驱动和硬件的兼容性；根据AUTOSAR CP 4.4标准，应当遵循其配置参数和初始化流程的规定；在多通道CAN系统中，正确配置每个通道的参数至关重要。|
|多实例个数|0 - 1|

## 1. CanIfCtrlDrvCfg

|容器属性|值（容器）|
|---|---|
|名称|CanIfCtrlDrvCfg|
|描述|Configuration parameters for all the underlying CAN Driver modules are aggregated under this container. For each CAN Driver module a seperate instance of this container has to be provided.|
|描述|概述：CanIfCtrlDrvCfg 是用于定义CAN接口控制器和底层驱动之间的配置关系，确保CAN通信接口的正确配置和操作。|
|描述|注意：在配置CanIfCtrlDrvCfg时，必须确保每个控制器的配置与实际硬件和驱动兼容；配置错误可能导致通信失败或系统不稳定；AUTOSAR CP 4.4标准中对此配置项的具体参数和结构有明确规定，应严格遵守。|
|多实例个数|1 - inf|

### 1.1. CanIfCtrlCfg

|容器属性|值（容器）|
|---|---|
|名称|CanIfCtrlCfg|
|描述|This container contains the configuration (parameters) of an adressed CAN controller by an underlying CAN Driver module. This container is configurable per CAN controller.|
|描述|概述：CanIfCtrlCfg 是一个配置项，用于定义CAN接口模块中的控制器配置参数，包括控制器的引用、唤醒功能和硬件对象的设置等。|
|描述|注意：在配置CanIfCtrlCfg时，需要确保控制器的ID和硬件资源匹配正确；如果启用了控制器的唤醒功能，还需要配置相应的唤醒源和唤醒事件处理；此外，要注意与CAN驱动模块的配置一致性，以保证CAN通信的正确性。|
|多实例个数|1 - inf|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|CanIfCtrlWakeupSupport|
|描述|This parameter defines if a respective controller of the referenced CAN Driver modules is queriable for wake up events.|
|描述|概述：CanIfCtrlWakeupSupport配置项用于定义CAN接口控制器是否支持唤醒功能，这决定了控制器是否能够通过网络唤醒车辆的电子控制单元（ECU）。|
|描述|注意：在配置时需确保硬件支持唤醒功能；若ECU需通过CAN网络唤醒，则此配置必须启用；不正确的配置可能导致唤醒功能不可用或系统功耗异常。|
|说明|True: Enabled False: Disabled|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CanIfCtrlId|
|描述|This parameter abstracts from the CAN Driver specific parameter Controller. Each controller of all connected CAN Driver modules shall be assigned to one specific ControllerId of the CanIf.|
|描述|概述：CanIfCtrlId 是用于标识CAN接口控制器的唯一标识符，用于配置和管理不同的CAN控制器。|
|描述|注意：确保每个CanIfCtrlId在系统中是唯一的，以避免配置冲突；正确匹配CanIfCtrlId与实际硬件控制器，以保证通信的正确性；在配置过程中应参照硬件设计文档，确保ID的正确性和有效性。|
|说明|Range: 0..number of configured controllers of all CAN Driver modules|
|多实例个数|1 - 1|
|取值范围|0 - 255|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|CanIfCtrlCanCtrlRef|
|描述|This parameter references to the logical handle of the underlying CAN controller from the CAN Driver module to be served by the CAN Interface module. The following parameters of CanController config container shall be referenced by this link: CanControllerId, CanWakeupSourceRef|
|描述|概述：CanIfCtrlCanCtrlRef 是一个配置参数，用于将CAN接口控制器（CanIfCtrl）与底层的CAN控制器（CanCtrl）关联起来，确保CAN接口层能够正确地访问和控制物理CAN控制器。|
|描述|注意：在配置时需要确保每个CanIfCtrl唯一地引用一个CanCtrl；引用的CanCtrl必须在系统中存在且已配置；如果系统中有多个CAN控制器，需要为每个控制器配置一个对应的CanIfCtrlCanCtrlRef。|
|说明|Range: 0..max. number of underlying supported CAN controllers|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Can/CanConfigSet/CanController|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|CanIfCtrlCoreRef|
|描述|This parameter references to OsPhysicalCore, indicating the core information of the CAN Controller|
|描述|CanIfCtrlCoreRef 配置项定义了CANIF控制器通道关联的核信息。|
|描述|注意：在配置CanIfCtrlCoreRef时，需要确保已配置EcuC/EcucHardware/EcucCoreDefinition。|
|说明|Range: 0..max. number of underlying supported OsPhysicalCore|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/EcuC/EcucHardware/EcucCoreDefinition|

## 2. CanIfDispatchCfg

|容器属性|值（容器）|
|---|---|
|名称|CanIfDispatchCfg|
|描述|Callback functions provided by upper layer modules of the CanIf. The callback functions defined in this container are common to all configured CAN Driver / CAN Transceiver Driver modules.|
|描述|概述：CanIfDispatchCfg 是 CAN 接口模块的配置参数之一，用于定义CAN控制器的中断和轮询机制，以及相关的回调函数。|
|描述|注意：在配置CanIfDispatchCfg时，需要确保中断和轮询机制与硬件和操作系统的能力相匹配；正确配置回调函数，以便在接收到CAN消息或发生状态变化时能够执行相应的动作；在多CAN控制器系统中，每个控制器的CanIfDispatchCfg配置必须是唯一的，以避免冲突。|
|多实例个数|1 - 1|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|CanIfDispatchUserCheckTrcvWakeFlagIndicationUL|
|描述|This parameter defines the upper layer module to which the CheckTrcvWakeFlagIndication from the Driver modules have to be routed.|
|描述|概述：CanIfDispatchUserCheckTrcvWakeFlagIndicationUL配置项用于定义用户层（UL）检查传输层唤醒标志指示的调度策略，确保在接收到唤醒标志时能够正确地通知上层用户。|
|描述|注意：该配置项需要与系统中的唤醒管理策略相匹配，确保唤醒事件能够被正确处理；在配置时需注意选择合适的用户层服务以响应唤醒标志；AUTOSAR CP 4.4标准中对唤醒管理有详细定义，需确保配置与标准一致。|
|说明|If CanIfPublicPnSupport equals False, this parameter shall not be configurable.|
|多实例个数|0 - 1|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|CanIfDispatchUserClearTrcvWufFlagIndicationUL|
|描述|This parameter defines the upper layer module to which the ClearTrcvWufFlagIndication from the Driver modules have to be routed.|
|描述|概述：CanIfDispatchUserClearTrcvWufFlagIndicationUL 是一个配置参数，用于指定当CAN转换器（Transceiver）唤醒标志被清除时，哪个上层用户（Upper Layer User）将被通知。|
|描述|注意：在配置此参数时，需要确保指定的上层用户具有处理唤醒标志清除指示的功能；此配置项应与系统中实际使用的CAN转换器和网络管理逻辑相匹配；在AUTOSAR CP 4.4标准中，确保此配置项的数据类型和使用方式符合规范要求。|
|说明|If CanIfPublicPnSupport equals False, this parameter shall not be configurable.|
|多实例个数|0 - 1|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|CanIfDispatchUserConfirmPnAvailabilityUL|
|描述|This parameter defines the upper layer module to which the ConfirmPnAvailability notification from the Driver modules have to be routed. If CanIfPublicPnSupport equals False, this parameter shall not be configurable.|
|描述|概述：CanIfDispatchUserConfirmPnAvailabilityUL 是用于配置CAN接口模块，当接收到特定网络请求时，通知上层用户（User Layer）的可用性确认。|
|描述|注意：确保该配置与上层用户的实际需求相匹配；在配置时需注意选择正确的用户层协议处理模块；此配置项应与整体网络管理策略一致，避免配置错误导致网络管理功能异常。|
|多实例个数|0 - 1|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|CanIfDispatchUserCtrlBusOffUL|
|描述|This parameter defines the upper layer (UL) module to which the notifications of all ControllerBusOff events from the CAN Driver modules have to be routed via \<User_ControllerBusOff\>.|
|描述|概述：CanIfDispatchUserCtrlBusOffUL 是一个配置参数，用于定义用户控制器的BusOff处理逻辑在CAN接口模块中的分发策略。|
|描述|注意：在配置CanIfDispatchUserCtrlBusOffUL时，需要确保它与系统中的CAN控制器和上层用户逻辑兼容；此配置项应与CAN驱动模块的BusOff处理机制相匹配；在多控制器系统中，每个控制器的BusOff分发策略可能需要独立配置。|
|说明|There is no possibility to configure no upper layer (UL) module as the provider of \<User_ControllerBusOff\>.|
|多实例个数|1 - 1|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|CanIfDispatchUserCtrlModeIndicationUL|
|描述|This parameter defines the upper layer (UL) module to which the notifications of all ControllerTransition events from the CAN Driver modules have to be routed|
|描述|概述：CanIfDispatchUserCtrlModeIndicationUL配置项用于定义用户控制模式指示的上层（Upper Layer）接口，它指定了当CAN接口的控制模式发生变化时，应通知哪个上层模块。|
|描述|注意：确保配置的上层模块接口与实际的模块接口一致，避免通知机制失效；在配置时需考虑系统的实时性和模块间的依赖关系；AUTOSAR CP 4.4标准中，对于上层模块的通知机制有明确的规范，需要确保遵循这些规范以保证系统的兼容性和稳定性。|
|说明|via \<User_ControllerModeIndication\>.|
|多实例个数|1 - 1|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|CanIfDispatchUserTrcvModeIndicationUL|
|描述|This parameter defines the upper layer (UL) module to which the notifications of all TransceiverTransition events from the CAN Transceiver Driver modules have to be routed via \<User_TrcvModeIndication\>. If no UL module is configured, no upper layer callback function will be called.|
|描述|概述：CanIfDispatchUserTrcvModeIndicationUL 是一个配置参数，用于指定CAN接口模块在收到CAN收发器模式变化指示时应通知的上层模块的名称。|
|描述|注意：在配置此参数时，需要确保指定的上层模块已经在系统中定义并且支持接收模式变化指示；此配置项的值必须与系统中实际存在的上层模块名称一致；在AUTOSAR CP 4.4标准中，确保该配置项符合CAN接口模块与上层模块之间的通信接口要求。|
|多实例个数|0 - 1|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|CanIfDispatchUserValidateWakeupEventUL|
|描述|This parameter defines the upper layer (UL) module to which the notifications about positive former requested wake up sources have to be routed via \<User_ValidateWakeupEvent\>.|
|描述|概述：CanIfDispatchUserValidateWakeupEventUL 配置项用于定义用户验证唤醒事件的上层模块(User Layer)的标识符，这允许CAN接口模块(CAN Interface module)将唤醒事件通知给相应的上层模块。|
|描述|注意：在配置CanIfDispatchUserValidateWakeupEventUL时，需要确保所指定的上层模块已经实现了唤醒事件的验证机制；此配置项应与系统中实际使用的唤醒源和上层模块保持一致；在AUTOSAR CP 4.4标准中，应当遵循模块间通信接口的规范来配置此项。|
|多实例个数|0 - 1|

|配置项属性|值（函数名配置项）|
|---|---|
|名称|CanIfDispatchUserCheckTrcvWakeFlagIndicationName|
|描述|This parameter defines the name of \<User_CheckTrcvWakeFlagIndication\>.|
|描述|概述：CanIfDispatchUserCheckTrcvWakeFlagIndicationName 是一个配置参数，用于指定当CAN收发器检测到唤醒标志时，应该调用的上层用户回调函数的名称。|
|描述|注意：确保指定的回调函数名称在整个项目中是唯一的，并且与实际实现的用户回调函数名称相匹配；该回调函数需要由用户实现，并且应当遵循AUTOSAR规定的回调函数的原型和行为；在配置时，应当考虑到系统的唤醒策略和电源管理需求，以确保正确的唤醒事件处理。|
|说明|If CanIfDispatchUserCheckTrcvWakeFlagIndicationUL equals CAN_SM the name of \<User_CheckTrcvWakeFlagIndication\> is fixed. If it equals CDD, the name is selectable. If CanIfPublicPnSupport equals False, this parameter shall not be configurable.|
|多实例个数|0 - 1|

|配置项属性|值（函数名配置项）|
|---|---|
|名称|CanIfDispatchUserClearTrcvWufFlagIndicationName|
|描述|This parameter defines the name of \<User_ClearTrcvWufFlagIndication\>.|
|描述|概述：CanIfDispatchUserClearTrcvWufFlagIndicationName 配置项用于指定当CAN转换器唤醒标志被清除时，由CAN接口模块调用的用户回调函数的名称。|
|描述|注意：用户需要确保配置的回调函数名称在系统中是唯一的，并且与实际实现的回调函数名称相匹配；此配置项通常与特定的CAN转换器硬件和驱动有关，因此需要根据硬件的实际情况进行配置；在配置此项时，应参考硬件手册和驱动程序文档，以确保正确的集成和功能行为。|
|说明|If CanIfDispatchUserClearTrcvWufFlagIndicationUL equals CAN_SM the name of \<User_ClearTrcvWufFlagIndication\> is fixed. If it equals CDD, the name is selectable. If CanIfPublicPnSupport equals False, this parameter shall not be configurable.|
|多实例个数|0 - 1|

|配置项属性|值（函数名配置项）|
|---|---|
|名称|CanIfDispatchUserConfirmPnAvailabilityName|
|描述|This parameter defines the name of \<User_ConfirmPnAvailability\>. If CanIfDispatchUserConfirmPnAvailabilityUL equals CAN_SM the name of \<User_ConfirmPnAvailability\> is fixed. If it equals CDD, the name is selectable. If CanIfPublicPnSupport equals False, this parameter shall not be configurable.|
|描述|概述：CanIfDispatchUserConfirmPnAvailabilityName 是一个配置参数，用于指定当CAN接口模块检测到部分网络唤醒信号时，应调用的上层用户回调函数的名称。|
|描述|注意：该配置项需要与实际实现的用户回调函数名称一致；用户必须确保该回调函数遵循AUTOSAR标准中定义的原型和行为；在配置时应注意该函数的可用性，以确保在接收到部分网络唤醒信号时能够正确执行。|
|多实例个数|0 - 1|

|配置项属性|值（函数名配置项）|
|---|---|
|名称|CanIfDispatchUserCtrlBusOffName|
|描述|This parameter defines the name of \<User_ControllerBusOff\>.|
|描述|概述：CanIfDispatchUserCtrlBusOffName配置项用于指定在CAN接口发生总线关闭（Bus Off）事件时，应当调用的用户控制器的回调函数名称。|
|描述|注意：确保指定的回调函数遵循AUTOSAR标准中定义的原型和行为要求；在配置时，需要确保该回调函数已在系统中定义且可被正确调用；此配置项对于实现CAN通信的错误处理和恢复机制至关重要。|
|说明|This parameter depends on the parameter CanIfDispatchUserCtrlBusOffUL. If CanIfDispatchUserCtrlBusOffUL equals CAN_SM the name of \<User_ControllerBusOff\> is fixed. If CanIfDispatchUserCtrlBusOffUL equals CDD, the name of \<User_ControllerBusOff\> is selectable.|
|多实例个数|0 - 1|

|配置项属性|值（函数名配置项）|
|---|---|
|名称|CanIfDispatchUserCtrlModeIndicationName|
|描述|This parameter defines the name of \<User_ControllerModeIndication\>.|
|描述|概述：CanIfDispatchUserCtrlModeIndicationName 是一个配置参数，用于指定控制器模式指示（Controller Mode Indication）的用户函数名称，该函数在CAN接口模块检测到CAN控制器模式变化时被调用。|
|描述|注意：该配置项的名称应与实际实现的用户函数名称一致；用户函数需要遵循AUTOSAR规范中定义的接口和参数列表；确保在整个项目中该名称的唯一性，避免命名冲突。|
|说明|This parameter depends on the parameter CanIfDispatchUserCtrlModeIndicationUL. If CanIfDispatchUserCtrlModeIndicationUL equals CAN_SM the name of \<User_ControllerModeIndication\> is fixed. If CanIfDispatchUserCtrlModeIndicationUL equals CDD, the name of \<User_ControllerModeIndication\> is selectable.|
|多实例个数|0 - 1|

|配置项属性|值（函数名配置项）|
|---|---|
|名称|CanIfDispatchUserTrcvModeIndicationName|
|描述|This parameter defines the name of \<User_TrcvModeIndication\>.|
|描述|概述：CanIfDispatchUserTrcvModeIndicationName 配置项用于指定当CAN收发器模式改变时，哪个上层用户（如Diag或ComM）将被通知。|
|描述|注意：确保此配置正确映射到相应的用户函数，以便在CAN收发器模式变更时能正确调用用户通知函数；此配置项必须与系统中实际存在的用户和函数名相匹配；在多用户系统中，正确配置每个用户的通知函数是必要的，以避免通知遗漏。|
|说明|This parameter depends on the parameter CanIfDispatchUserTrcvModeIndicationUL. If CanIfDispatchUserTrcvModeIndicationUL equals CAN_SM the name of \<User_TrcvModeIndication\> is fixed. If CanIfDispatchUserTrcvModeIndicationUL equals CDD, the name of \<User_TrcvModeIndication\> is selectable.|
|多实例个数|0 - 1|

|配置项属性|值（函数名配置项）|
|---|---|
|名称|CanIfDispatchUserValidateWakeupEventName|
|描述|This parameter defines the name of \<User_ValidateWakeupEvent\>. This|
|描述|概述：CanIfDispatchUserValidateWakeupEventName配置项用于定义当接收到唤醒事件时，是否需要调用用户定义的验证函数来确认该唤醒事件的有效性。|
|描述|注意：在使用此配置项时，需要确保已经定义了相应的用户验证函数；此配置项在设计低功耗唤醒逻辑时尤为重要；AUTOSAR CP 4.4标准中，对于唤醒事件的处理和验证机制有明确规定，确保配置与标准一致。|
|说明|parameter depends on the parameter CanIfDispatchUserValidateWakeupEventUL. If CanIfDispatchUserValidateWakeupEventUL equals ECUM, the name of \<User_ValidateWakeupEvent\> is fixed. If CanIfDispatchUserValidateWakeupEventUL equals CDD, the name of \<User_ValidateWakeupEvent\> is selectable.|
|多实例个数|0 - 1|

## 3. CanIfInitCfg

|容器属性|值（容器）|
|---|---|
|名称|CanIfInitCfg|
|描述|This container contains the init parameters of the CAN Interface.|
|描述|概述：CanIfInitCfg 是CAN接口模块的初始化配置，它定义了CAN接口在系统启动时的配置参数，包括控制器引用、硬件对象配置以及相关的回调函数。|
|描述|注意：在配置CanIfInitCfg时，需要确保引用的CAN控制器和硬件对象与实际硬件和ECU的CAN网络结构相匹配；初始化参数必须与CAN控制器的能力和系统需求一致；在配置过程中，应遵循AUTOSAR CP 4.4标准中对初始化配置的具体要求和限制。|
|多实例个数|1 - 1|

### 3.1. CanIfBufferCfg

|容器属性|值（容器）|
|---|---|
|名称|CanIfBufferCfg|
|描述|This container contains the Txbuffer configuration. Multiple buffers with different sizes could be configured. If CanIfBufferSize (ECUC_CanIf_00834) equals 0, the CanIf Tx L-PDU only refers via this CanIfBufferCfg the corresponding CanIfHthCfg.|
|描述|概述：CanIfBufferCfg 是用于配置CAN接口模块中的缓冲区，这些缓冲区用于存储发送或接收的CAN消息，直到它们被处理。|
|描述|注意：在配置CanIfBufferCfg时，需确保缓冲区大小与消息处理速率相匹配，避免溢出；缓冲区的配置应支持系统的通信需求，并考虑优先级和消息ID的过滤；AUTOSAR CP 4.4标准可能对缓冲区的类型和数量有特定的限制或要求，需要遵守这些规范。|
|多实例个数|0 - inf|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CanIfBufferSize|
|描述|This parameter defines the number of CanIf Tx L-PDUs which can be buffered in one Txbuffer. If this value equals 0, the CanIf does not perform Txbuffering for the CanIf Tx L-PDUs which are assigned to this Txbuffer. If CanIfPublicTxBuffering equals False, this parameter equals 0 for all TxBuffer. If the CanHandleType of the referred HTH equals FULL, this parameter equals 0 for this TxBuffer.|
|描述|概述：CanIfBufferSize配置项定义了CAN接口模块中每个硬件对象（如发送或接收缓冲区）的缓冲区大小，用于存储CAN帧，直到它们被处理。|
|描述|注意：在配置CanIfBufferSize时，需要确保缓冲区大小足以容纳高峰期间的数据流量，避免数据丢失；此配置项的设置应考虑系统的内存资源限制；AUTOSAR CP 4.4标准中并未明确指定缓冲区大小的具体值，需要根据实际应用需求和硬件能力来确定。|
|多实例个数|1 - 1|
|默认值|0|
|取值范围|0 - 255|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|CanIfBufferHthRef|
|描述|Reference to HTH, that defines the hardware object or the pool of hardware objects configured for transmission. All the CanIf Tx L-PDUs refer via the CanIfBufferCfg and this parameter to the HTHs if TxBuffering is enabled, or not.|
|描述|概述：CanIfBufferHthRef 配置项是用于定义硬件传输句柄（Hardware Transmit Handle, HTH）与特定的CAN接口发送缓冲区之间的关联。|
|描述|注意：在配置CanIfBufferHthRef时，必须确保引用的HTH是存在的并且与所配置的CAN控制器相匹配；HTH的唯一性要保证，以避免在发送过程中的冲突；在配置时还应考虑到HTH的负载平衡，以优化网络的带宽利用率。|
|说明|Each HTH shall not be assigned to more than one buffer.|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/CanIf/CanIfInitCfg/CanIfInitHohCfg/CanIfHthCfg|

### 3.2. CanIfInitHohCfg

|容器属性|值（容器）|
|---|---|
|名称|CanIfInitHohCfg|
|描述|This container contains the references to the configuration setup of each underlying CAN Driver.|
|描述|概述：CanIfInitHohCfg 是一个配置参数，用于初始化CAN接口的硬件对象句柄（HOH），它定义了CAN控制器与CAN网络之间的映射关系。|
|描述|注意：在配置CanIfInitHohCfg时，需要确保硬件对象句柄与实际的CAN控制器和网络节点正确对应；此外，每个HOH应该是唯一的，不应与其他HOH冲突；根据AUTOSAR CP 4.4标准，还需要考虑HOH的类型（如发送或接收）和相关的CAN ID过滤设置。|
|多实例个数|0 - inf|

#### 3.2.1. CanIfHrhCfg

|容器属性|值（容器）|
|---|---|
|名称|CanIfHrhCfg|
|描述|This container contains configuration parameters for each hardware receive object (HRH).|
|描述|概述：CanIfHrhCfg配置项定义了CAN接口硬件接收句柄（HRH）的属性，包括接收对象的标识符类型（标准/扩展）和过滤机制等，用于接收CAN帧。|
|描述|注意：确保每个HRH的配置与实际硬件资源和CAN网络设计相匹配；在配置标识符过滤时，考虑网络上的消息流量和处理能力，以优化性能；AUTOSAR CP 4.4标准要求支持多种消息标识符类型，包括标准ID和扩展ID，需正确配置以保证网络兼容性。|
|多实例个数|0 - inf|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|CanIfHrhSoftwareFilter|
|描述|Selects the hardware receive objects by using the HRH range/list from CAN Driver configuration to define, for which HRH a software filtering has to be performed at during receive processing.|
|描述|概述：CanIfHrhSoftwareFilter配置项用于定义是否在软件层面上对接收到的CAN消息进行过滤，以决定哪些消息将被上层应用处理。|
|描述|注意：在使用CanIfHrhSoftwareFilter时，需要确保硬件过滤器的配置与软件过滤器的配置相协调，以避免消息丢失或不必要的处理；此配置项对于系统资源和性能优化至关重要，应根据实际应用需求谨慎配置；AUTOSAR CP 4.4标准中，软件过滤的实现细节可能会根据具体的MCAL驱动和ECU硬件特性有所不同。|
|说明|True: Software filtering is enabled False: Software filtering is enabled|
|多实例个数|1 - 1|
|默认值|true|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|CanIfHrhCanCtrlIdRef|
|描述|Reference to controller Id to which the HRH belongs to. A controller can contain one or more HRHs.|
|描述|概述：CanIfHrhCanCtrlIdRef是一个配置项，用于将硬件接收句柄（HRH）与特定的CAN控制器标识符关联起来，确保接收到的CAN消息能够被正确地分配到指定的CAN控制器处理。|
|描述|注意：在配置时需确保每个HRH正确地映射到一个存在的CAN控制器ID上；不正确的映射可能导致消息处理错误；在多CAN控制器系统中，此配置尤为重要以保证消息的正确路由。|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/CanIf/CanIfCtrlDrvCfg/CanIfCtrlCfg|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|CanIfHrhIdSymRef|
|描述|The parameter refers to a particular HRH object in the CanDrv configuration (see CanHardwareObject ECUC_Can_00324).|
|描述|概述：CanIfHrhIdSymRef 是一个配置参数，用于将硬件接收句柄（Hardware Receive Handle, HRH）与符号引用（Symbolic Reference）关联起来，这样就可以通过符号名称引用特定的CAN接口接收句柄。|
|描述|注意：在配置时，确保每个HRH的符号引用是唯一的，以避免在系统中产生歧义；符号引用应与系统中使用的CAN消息标识符保持一致，以确保正确的消息处理；在配置过程中，应参照AUTOSAR CP 4.4标准中的相关规范来正确设置此参数。|
|说明|CanIf receives the following information of the CanDrv module by this reference: - CanHandleType (see ECUC_Can_00323) - CanObjectId (see ECUC_Can_00326)|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Can/CanConfigSet/CanHardwareObject|

##### 3.2.1.1. CanIfHrhRangeCfg

|容器属性|值（容器）|
|---|---|
|名称|CanIfHrhRangeCfg|
|描述|Defines the parameters required for configurating multiple CANID ranges for a given same HRH.|
|描述|概述：CanIfHrhRangeCfg 是一个配置参数，用于定义CAN接口硬件接收句柄（HRH）的接收范围，这通常涉及到接收ID的上下限，用于过滤接收到的CAN消息。|
|描述|注意：在配置CanIfHrhRangeCfg时，需要确保ID范围与实际的CAN网络消息设计相匹配；此外，要注意ID范围设置不应与其他HRH的设置冲突，以避免消息处理的不确定性；在AUTOSAR CP 4.4标准中，确保配置项符合规范的定义和约束。|
|描述|该配置项未使用|
|多实例个数|0 - inf|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|CanIfHrhRangeRxPduRangeCanIdType|
|描述|Specifies whether a configured Range of CAN Ids shall only consider standard CAN Ids or extended CAN Ids.|
|描述|概述：CanIfHrhRangeRxPduRangeCanIdType 配置项用于定义接收的CAN帧标识符的类型，这通常是标准的11位标识符或是扩展的29位标识符，用于硬件接收处理器（HRH）的接收PDU范围过滤。|
|描述|注意：在配置时需要确保CAN标识符类型与实际使用的CAN ID类型相匹配；如果配置了错误的类型，可能会导致接收处理器无法正确过滤接收到的消息；AUTOSAR CP 4.4标准中，该配置项应与CAN驱动和CAN控制器的能力相一致。|
|描述|该配置项未使用|
|多实例个数|1 - 1|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CanIfHrhRangeBaseId|
|描述|CAN Identifier used as base value in combination with CanIfHrhRangeMask for a masked ID range in which all CAN Ids shall pass the software filtering. The size of this parameter is limited by CanIfHrhRangeRxPduRangeCanIdType.|
|描述|概述：CanIfHrhRangeBaseId 用于定义接收硬件资源（HRH）的基础标识符，用于区分不同的消息范围。|
|描述|注意：确保CanIfHrhRangeBaseId与系统中其他HRH的标识符不冲突；在配置时考虑消息标识符的范围和过滤需求；AUTOSAR CP 4.4标准中，该配置项应正确映射到相应的CAN控制器和消息缓冲区。|
|描述|该配置项未使用|
|多实例个数|0 - 1|
|取值范围|0 - 536870911|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CanIfHrhRangeMask|
|描述|Used as mask value in combination with CanIfHrhRangeBaseId for a masked ID range in which all CAN Ids shall pass the software filtering. The size of this parameter is limited by CanIfHrhRangeRxPduRangeCanIdType.|
|描述|概述：CanIfHrhRangeMask 用于定义接收硬件资源（HRH）的标识符范围掩码，用于过滤接收到的CAN消息，确保只处理符合特定标识符范围的消息。|
|描述|注意：确保CanIfHrhRangeMask与HRH的配置匹配，以正确过滤消息；掩码设置应遵循CAN标准的标识符规范；在配置时需考虑消息标识符的扩展和标准格式。|
|描述|该配置项未使用|
|多实例个数|0 - 1|
|取值范围|0 - 536870911|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CanIfHrhRangeRxPduLowerCanId|
|描述|Lower CAN Identifier of a receive CAN L-PDU for identifier range definition, in which all CAN Ids shall pass the software filtering.|
|描述|概述：CanIfHrhRangeRxPduLowerCanId用于定义接收消息标识符（CAN ID）的下限，这是在配置接收硬件消息处理器（HRH）时用于过滤接收到的PDU（协议数据单元）的范围的起始值。|
|描述|注意：确保CanIfHrhRangeRxPduLowerCanId的值不超过CAN标准定义的最大值；在配置ID范围过滤时，该值应小于或等于对应的CanIfHrhRangeRxPduUpperCanId；在使用扩展CAN ID时，需注意ID的格式和长度。|
|描述|该配置项未使用|
|多实例个数|0 - 1|
|取值范围|0 - 536870911|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CanIfHrhRangeRxPduUpperCanId|
|描述|Upper CAN Identifier of a receive CAN L-PDU for identifier range definition, in which all CAN Ids shall pass the software filtering.|
|描述|概述：CanIfHrhRangeRxPduUpperCanId用于定义接收PDU的CAN ID的上限值，用于配置接收消息ID范围的上界，以便过滤接收的CAN消息。|
|描述|注意：该配置项与CanIfHrhRangeRxPduLowerCanId配合使用，以定义一个接收消息ID的范围；确保UpperCanId大于或等于LowerCanId，避免配置错误；在配置ID范围时，考虑CAN网络上的消息ID分布，以优化消息过滤效率。|
|描述|该配置项未使用|
|多实例个数|0 - 1|
|取值范围|0 - 536870911|

#### 3.2.2. CanIfHthCfg

|容器属性|值（容器）|
|---|---|
|名称|CanIfHthCfg|
|描述|This container contains parameters related to each HTH.|
|描述|概述：CanIfHthCfg 是一个配置参数，用于定义硬件传输句柄（Hardware Transmit Handle, HTH）的属性，这些属性包括用于发送CAN帧的硬件对象和相关的CAN控制器。|
|描述|注意：在配置CanIfHthCfg时，需要确保每个HTH的ID是唯一的，并且与实际的硬件资源相匹配；HTH配置必须与CAN控制器和CAN驱动的配置保持一致；在配置HTH时，还应考虑消息的优先级和发送策略，以确保消息传输的效率和可靠性。|
|多实例个数|0 - inf|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|CanIfHthCanCtrlIdRef|
|描述|Reference to controller Id to which the HTH belongs to. A controller can contain one or more HTHs.|
|描述|概述：CanIfHthCanCtrlIdRef是一个配置项，用于将硬件传输句柄（Hardware Transmit Handle, HTH）映射到特定的CAN控制器ID，确保消息的发送通过正确的CAN控制器进行。|
|描述|注意：在配置时需确保每个HTH正确地映射到一个存在的CAN控制器ID上；不同的HTH应避免映射到同一个CAN控制器ID，除非特定的应用场景需要这样做；在多CAN控制器系统中，正确的映射对于消息的准确发送和系统的稳定性至关重要。|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/CanIf/CanIfCtrlDrvCfg/CanIfCtrlCfg|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|CanIfHthIdSymRef|
|描述|The parameter refers to a particular HTH object in the CanDrv configuration (see CanHardwareObject ECUC_Can_00324).|
|描述|概述：CanIfHthIdSymRef是一个配置项，用于将硬件传输句柄（Hardware Transmit Handle, HTH）与符号引用（Symbolic Reference）关联起来，以便在发送CAN帧时引用特定的硬件资源。|
|描述|注意：在配置CanIfHthIdSymRef时，必须确保引用的HTH与CAN控制器和物理通道正确匹配；该配置项对于确保CAN接口层正确管理CAN帧的发送至关重要；在AUTOSAR CP 4.4标准中，确保该配置项的正确性对于系统的通信可靠性和性能有直接影响。|
|说明|CanIf receives the following information of the CanDrv module by this reference: - CanHandleType (see ECUC_Can_00323) - CanObjectId (see ECUC_Can_00326)|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Can/CanConfigSet/CanHardwareObject|

### 3.3. CanIfRxPduCfg

|容器属性|值（容器）|
|---|---|
|名称|CanIfRxPduCfg|
|描述|This container contains the configuration (parameters) of each receive CAN L-PDU.|
|描述|概述：CanIfRxPduCfg配置项定义了接收CAN帧的参数，包括PDU的ID、数据长度、接收处理函数等，用于指定如何处理接收到的CAN消息。|
|描述|注意：确保每个CanIfRxPduCfg配置的PDU ID在系统中是唯一的，避免消息处理冲突；配置的数据长度应与实际CAN帧数据长度匹配，以确保正确解析数据；接收处理函数需要根据实际应用需求进行配置，确保消息能被正确处理。|
|说明|The SHORT-NAME of "CanIfRxPduConfig" container itself represents the symolic name of Receive L-PDU. This L-SDU produces a meta data item of type CAN_ID_32.|
|多实例个数|0 - inf|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|CanIfRxPduDataLengthCheck|
|描述|This parameter switches the message specific data length check.|
|描述|概述：CanIfRxPduDataLengthCheck 配置项用于定义是否对接收到的CAN接口协议数据单元（PDU）的长度进行检查，以确保数据的完整性和正确性。|
|描述|注意：在AUTOSAR CP 4.4中，确保该配置项正确设置以防止数据长度错误导致的通信问题；长度检查有助于提前识别和处理可能的数据错误；不正确的数据长度设置可能会导致系统行为不符合预期。|
|说明|True: Data length check will be executed during the reception of this PDU. False: No data length check will be executed during the reception of this PDU.|
|多实例个数|1 - 1|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|CanIfRxPduCanIdType|
|描述|CAN Identifier of receive CAN L-PDUs used by the CAN Driver for CAN L-PDU reception.|
|描述|概述：CanIfRxPduCanIdType配置项用于定义接收的PDU（协议数据单元）的CAN ID类型，这决定了CAN ID是标准帧格式还是扩展帧格式。|
|描述|注意：在配置CanIfRxPduCanIdType时，必须确保所选类型与网络上实际传输的CAN帧类型一致；错误的配置可能导致接收机制无法正确识别CAN帧；AUTOSAR CP 4.4标准支持的类型包括标准、扩展和混合模式。|
|多实例个数|1 - 1|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|CanIfRxPduUserRxIndicationUL|
|描述|This parameter defines the upper layer (UL) module to which the indication|
|描述|概述：CanIfRxPduUserRxIndicationUL配置项指定了接收到特定CAN接口接收PDU（协议数据单元）后，上层（UL）模块的接收指示函数的名称，用于通知上层模块有新数据到达。|
|描述|注意：确保配置的接收指示函数名称与实际上层模块的接收处理函数名称一致；该配置项对于实现CAN通信中的数据接收流程至关重要，需要仔细配置；在AUTOSAR CP 4.4中，该配置项的命名和使用应遵循标准规范，以保证模块间的正确通信和数据处理。|
|说明|of the successfully received CANRXPDUID has to be routed via \<User_RxIndication\>. This \<User_RxIndication\> has to be invoked when the indication of the configured CANRXPDUID will be received by an Rx indication event from the CAN Driver module. If no upper layer (UL) module is configured, no \<User_RxIndication\> has to be called in case of an Rx indication event of the CANRXPDUID from the CAN Driver module.|
|多实例个数|0 - 1|

|配置项属性|值（函数名配置项）|
|---|---|
|名称|CanIfRxPduUserRxIndicationName|
|描述|This parameter defines the name of the \<User_RxIndication\>.|
|描述|概述：CanIfRxPduUserRxIndicationName 是一个配置参数，用于指定接收到特定CAN接口接收PDU（协议数据单元）时调用的上层模块的指示函数的名称。|
|描述|注意：在配置时，需要确保该名称与上层模块中定义的接收指示函数名称一致；此名称应遵循AUTOSAR命名规范；在整个项目中，每个接收PDU应该映射到唯一的接收指示函数。|
|说明|This parameter depends on the parameter CanIfRxPduUserRxIndicationUL. If CanIfRxPduUserRxIndicationUL equals CAN_TP, CAN_NM, PDUR, XCP, DLT, CAN_TSYN, J1939NM or J1939TP, the name of the \<User_RxIndication\> is fixed. If CanIfRxPduUserRxIndicationUL equals CDD, the name of the \<User_RxIndication\> is selectable.|
|多实例个数|0 - 1|
|字段长度|1-32|

|配置项属性|值（函数名配置项）|
|---|---|
|名称|CanIfRxPduUserRxCalloutName|
|描述|This parameter defines the name of the \<User_RxCalloutName\>.|
|描述|概述：CanIfRxPduUserRxCalloutName 配置项指定了接收到特定CAN接口消息后调用的用户定义函数的名称。|
|描述|注意：确保指定的函数名在项目中存在且已正确实现；函数应能处理从CAN接收的数据；在AUTOSAR CP 4.4中，此配置项的使用应符合接口模块的规范要求。|
|说明|This parameter independs on the parameter CanIfRxPduUserRxIndicationUL.|
|多实例个数|0 - 1|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CanIfRxPduCanId|
|描述|CAN Identifier of Receive CAN L-PDUs used by the CAN Interface. Exa: Software Filtering. This parameter is used if exactly one Can Identifier is assigned to the Pdu. If a range is assigned then the CanIfRxPduCanIdRange parameter shall be used.|
|描述|概述：CanIfRxPduCanId是一个配置项，用于定义CAN接口模块中接收的PDU（协议数据单元）的CAN标识符，这个标识符用于识别网络上的不同消息。|
|描述|注意：在配置CanIfRxPduCanId时，需要确保CAN ID与网络上其他消息的ID不冲突；根据CAN网络的要求，选择标准ID（11位）或扩展ID（29位）；在配置过程中，还需考虑消息的优先级，因为CAN ID的值会影响到消息在网络中的传输优先级。|
|说明|Range: 11 Bit For Standard CAN Identifier ... 29 Bit For Extended CAN identifier|
|多实例个数|1 - 1|
|取值范围|0 - 536870911|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CanIfRxPduCanIdMask|
|描述|Identifier mask which denotes relevant bits in the CAN Identifier. This parameter defines a CAN Identifier range in an alternative way to CanIfRxPduCanIdRange. It identifies the bits of the configured CAN Identifier that must match the received CAN Identifier. Range: 11 bits for Standard CAN Identifier, 29 bits for Extended CAN Identifier.|
|描述|概述：CanIfRxPduCanIdMask用于定义接收的CAN帧的CAN ID掩码，以便过滤和识别特定的CAN消息。这允许软件根据CAN ID的特定位模式接收消息，增加了灵活性和筛选能力。|
|描述|注意：在配置CanIfRxPduCanIdMask时，需要确保掩码与对应的CanIfRxPduCanId设置相匹配，以正确过滤所需的消息；掩码值的设置应考虑到实际应用中可能存在的ID变化范围；AUTOSAR CP 4.4标准中对于CAN ID掩码的使用有明确规范，需要遵循这些规范以保证兼容性。|
|描述|该配置项未使用|
|多实例个数|0 - 1|
|默认值|536870911|
|取值范围|0 - 536870911|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CanIfRxPduDataLength|
|描述|Data length of the received CAN L-PDUs used by the CAN Interface.|
|描述|概述：CanIfRxPduDataLength 定义了接收到的CAN接口协议数据单元（PDU）的数据长度。|
|描述|注意：数据长度应符合CAN网络的标准和配置要求；长度配置错误可能导致数据处理异常；确保与发送端的PDU长度匹配以保证数据的正确接收和处理。|
|说明|This information is used for Data Length Check. Additionally it might specify the valid bits in case of the discrete DLC for CAN FD L-PDUs \> 8 bytes. The data area size of a CAN L-PDU can have a range from 0 to 64 bytes.|
|多实例个数|1 - 1|
|取值范围|0 - 64|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CanIfRxPduId|
|描述|ECU wide unique, symbolic handle for receive CAN L-SDU. It shall fulfill ANSI/AUTOSAR definitions for constant defines.|
|描述|概述：CanIfRxPduId 是用于标识接收到的CAN协议数据单元（PDU）的唯一标识符。|
|描述|注意：确保每个CanIfRxPduId在系统中是唯一的，以避免数据处理上的混淆；该标识符应与ECU内部处理和诊断功能的配置相匹配；在配置过程中，应考虑PDU的优先级和处理策略。|
|说明|Range: 0..max. number of defined CanRxPduIds|
|多实例个数|1 - 1|
|取值范围|0 - 4294967295|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|CanIfRxPduHrhIdRef|
|描述|The HRH to which Rx L-PDU belongs to, is referred through this parameter.|
|描述|概述：CanIfRxPduHrhIdRef 是一个配置参数，用于将接收的CAN接口协议数据单元（PDU）与硬件接收处理句柄（HRH）关联起来，确保正确的数据流向和处理。|
|描述|注意：在配置时需确保每个CanIfRxPduHrhIdRef正确指向一个存在的HRH；HRH的配置应与实际的CAN控制器和消息缓冲区相匹配；不正确的关联可能导致接收消息处理失败或数据流向错误。|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/CanIf/CanIfInitCfg/CanIfInitHohCfg/CanIfHrhCfg|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|CanIfRxPduRef|
|描述|Reference to the "global" Pdu structure to allow harmonization of handle IDs in the COM-Stack.|
|描述|概述：CanIfRxPduRef 是一个配置参数，用于引用接收到的CAN接口协议数据单元（PDU）。|
|描述|注意：确保每个CanIfRxPduRef正确映射到相应的CAN接口PDU，以保证数据的正确接收和处理；在配置时需遵循AUTOSAR CP 4.4标准中对PDU引用的具体要求；不正确的PDU引用可能导致数据处理错误或系统功能异常。|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/EcuC/EcucConfigSet/EcucPduCollection/Pdu|

#### 3.3.1. CanIfRxPduCanIdRange

|容器属性|值（容器）|
|---|---|
|名称|CanIfRxPduCanIdRange|
|描述|Optional container that allows to map a range of CAN Ids to one PduId.|
|描述|概述：CanIfRxPduCanIdRange 配置项用于定义接收的CAN消息标识符（CAN ID）的范围，这样CAN接口（CanIf）模块可以接收一系列的CAN ID，而不是单个ID。|
|描述|注意：在配置CanIfRxPduCanIdRange时，需要确保所定义的CAN ID范围不与其他接收或发送的CAN ID冲突；范围的上下限应该符合CAN标准中ID的有效值；在配置ID范围时，还应考虑到消息过滤的硬件支持能力，以确保系统能够有效处理所接收的消息。|
|多实例个数|0 - 1|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CanIfRxPduCanIdRangeLowerCanId|
|描述|Lower CAN Identifier of a receive CAN L-PDU for identifier range definition, in which all CAN Ids are mapped to one PduId.|
|描述|概述：CanIfRxPduCanIdRangeLowerCanId 是用于定义接收的CAN帧的CAN标识符（CAN ID）的下限，这是为了支持接收ID范围内的所有消息，而不是单个ID的消息。|
|描述|注意：该配置项通常与CanIfRxPduCanIdRangeUpperCanId一起使用，以定义接收ID的范围；确保定义的范围不与其他接收或发送的CAN ID冲突；在配置ID范围时，要注意CAN控制器的过滤能力，以确保硬件能够正确处理所配置的ID范围。|
|多实例个数|1 - 1|
|取值范围|0 - 536870911|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CanIfRxPduCanIdRangeUpperCanId|
|描述|Upper CAN Identifier of a receive CAN L-PDU for identifier range definition, in which all CAN Ids are mapped to one PduId.|
|描述|概述：CanIfRxPduCanIdRangeUpperCanId 是一个配置项，用于定义接收的CAN帧的CAN标识符（CAN ID）的上限范围，这样CAN接口（CanIf）模块可以接收在指定范围内的所有CAN帧。|
|描述|注意：确保CanIfRxPduCanIdRangeUpperCanId的值高于或等于对应CanIfRxPduCanIdRangeLowerCanId值；该配置项通常与CanIfRxPduCanIdRangeLowerCanId一起使用，以定义一个有效的CAN ID范围；在配置CAN ID范围时，考虑到实际的网络通信需求和可能的ID冲突。|
|多实例个数|1 - 1|
|取值范围|0 - 536870911|

#### 3.3.2. CanIfTTRxFrameTriggering

|容器属性|值（容器）|
|---|---|
|名称|CanIfTTRxFrameTriggering|
|描述|CanIfTTRxFrameTriggering is specified in the SWS TTCAN Interface and defines Frame trigger for TTCAN reception.|
|描述|概述：CanIfTTRxFrameTriggering配置项用于定义CAN接口的时间触发接收帧的属性，这包括接收帧的标识符、数据长度代码（DLC）和引用的硬件对象等信息。|
|描述|注意：在配置CanIfTTRxFrameTriggering时，需要确保引用的硬件对象与CAN控制器和CAN驱动配置一致；此外，时间触发通信（TTCAN）的使用必须符合网络的时间同步要求；AUTOSAR CP 4.4标准中可能有特定的属性和参数要求，需要根据标准文档进行准确配置。|
|描述|该配置项未使用|
|说明|This container is only included and valid if TTCAN is supported by the controller, enabled (see CanIfSupportTTCAN, ECUC_CanIf_00675), and a joblist is used for reception.|
|多实例个数|0 - 1|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CanTTRxJoblistTimeMark|
|描述|Defines the point in time, when the joblist execution funciton (JLEF) shall be called for the referenced rx trigger. Value is given in cycle time. This parameter is only configurable if a joblist is enabled by parameter CanIfTTJobList.|
|描述|概述：CanTTRxJoblistTimeMark 配置项用于定义CAN传输层接收作业列表的时间标记，这有助于在确定的时间点同步处理接收到的消息。|
|描述|注意：在配置CanTTRxJoblistTimeMark时，需要确保时间标记与系统的时间基准同步；此配置项通常与CAN时间触发通信相关，因此需要特别注意与CAN时间触发模块的兼容性；在配置时，还需考虑到消息的接收窗口和系统的时间分辨率，以确保消息能够被正确地按照时间标记处理。|
|描述|该配置项未使用|
|多实例个数|0 - 1|
|取值范围|0 - 65535|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|CanIfTTRxHwObjectTriggerIdRef|
|描述|This parameter refers to a particular TTCAN hardware receive object Trigger of a hardware object in the TTCAN Driver Module, which is referred via plain CAN parameter CANIF_HRH_HANDLETYPE_REF. This parameter is only configurable if a joblist is enabled by parameter CanIfTTJobList.|
|描述|概述：CanIfTTRxHwObjectTriggerIdRef 是一个配置参数，用于引用CAN接口模块中的硬件对象，该硬件对象用于触发部分网络的时间触发接收操作。|
|描述|注意：在配置CanIfTTRxHwObjectTriggerIdRef时，必须确保引用的硬件对象支持时间触发的接收功能；此配置项通常与CAN部分网络的时间同步和时间触发通信机制相关联；在配置时应参考具体的CAN控制器硬件特性和网络管理需求，以确保正确的时间触发行为。|
|描述|该配置项未使用|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Can/CanConfigSet/CanHardwareObject/CanTTHardwareObjectTrigger|

### 3.4. CanIfTxPduCfg

|容器属性|值（容器）|
|---|---|
|名称|CanIfTxPduCfg|
|描述|This container contains the configuration (parameters) of a transmit CAN L-PDU. It has to be configured as often as a transmit CAN L-PDU is needed.|
|描述|概述：CanIfTxPduCfg 是一个配置参数，用于定义CAN接口层的传输协议数据单元（PDU）的属性，这些属性包括PDU的标识符、DLC、CAN ID类型等，以便正确地管理CAN消息的发送。|
|描述|注意：在配置CanIfTxPduCfg时，必须确保CAN ID与系统中其他PDU的ID不冲突；还需注意PDU的DLC值是否符合实际的数据长度要求；此外，根据AUTOSAR CP 4.4标准，还应确保配置与PDU的类型和用途相匹配，例如是否支持动态长度等。|
|说明|The SHORT-NAME of "CanIfTxPduConfig" container represents the symolic name of Transmit L-PDU. This L-SDU consumes a meta data item of type CAN_ID_32.|
|多实例个数|0 - inf|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|CanIfTxPduPnFilterPdu|
|描述|If CanIfPublicPnFilterSupport is enabled, by this parameter PDUs could be configured which will pass the CanIfPnFilter.|
|描述|概述：CanIfTxPduPnFilterPdu配置项用于定义是否对特定的CAN传输协议数据单元（PDU）应用部分网络（PN）过滤，这是为了支持部分网络功能，减少网络唤醒和通信负载。|
|描述|注意：在使用此配置项时，需要确保车辆网络配置支持部分网络功能；此配置项的使用可能会影响网络唤醒策略，因此需要仔细规划；AUTOSAR CP 4.4标准中，对于部分网络的支持和配置有明确的规范，需要确保配置与标准一致。|
|说明|If there is no CanIfTxPduPnFilterPdu configured per controller, the corresponding controller applies no CanIfPnFilter.|
|多实例个数|0 - 1|
|默认值|false|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|CanIfTxPduCanIdType|
|描述|Type of CAN Identifier of the transmit CAN L-PDU used by the CAN Driver module for CAN L-PDU transmission.|
|描述|概述：CanIfTxPduCanIdType 是一个配置项，用于定义CAN接口层传输PDU的CAN标识符类型，它决定了CAN ID是标准帧格式（11位）还是扩展帧格式（29位）。|
|描述|注意：在配置CanIfTxPduCanIdType时，需要确保它与实际的CAN网络设计一致；此外，不同的CAN控制器可能对CAN ID类型的支持有所不同，需要根据硬件能力进行配置；在AUTOSAR CP 4.4标准中，该配置项应与PDU的CAN ID长度相匹配，否则可能导致通信错误。|
|多实例个数|1 - 1|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|CanIfTxPduType|
|描述|Defines the type of each transmit CAN L-PDU.|
|描述|概述：CanIfTxPduType 是一个配置参数，用于定义CAN接口层中传输PDU（协议数据单元）的类型，这决定了PDU如何被处理和传输。|
|描述|注意：在配置CanIfTxPduType时，需要确保它与PDU的实际用途相匹配，例如静态或动态PDU；此外，该配置项应与CAN驱动层和上层服务的需求保持一致；在AUTOSAR CP 4.4标准中，应检查此配置项的属性是否支持新的或已更改的特性，以确保兼容性。|
|多实例个数|1 - 1|
|默认值|STATIC|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|CanIfTxPduUserTxConfirmationUL|
|描述|This parameter defines the upper layer (UL) module to which the confirmation of the successfully transmitted CanTxPduId has to be routed via the \<User_TxConfirmation\>.|
|描述|概述：CanIfTxPduUserTxConfirmationUL配置项定义了CAN接口层（CanIf）传输PDU（协议数据单元）时，用户传输确认上层（Upper Layer）的模块类型，用于指定哪个上层模块将接收传输确认回调。|
|描述|注意：该配置项需要与实际项目中使用的上层模块类型相匹配，以确保正确的回调机制；不正确的配置可能导致传输确认信息无法正确传递给目标上层模块；在配置时需参考AUTOSAR CP 4.4标准中对上层模块类型的定义和要求。|
|说明|This \<User_TxConfirmation\> has to be invoked when the confirmation of the configured CanTxPduId will be received by a Tx confirmation event from the CAN Driver module. If no upper layer (UL) module is configured, no \<User_TxConfirmation\> has to be called in case of a Tx confirmation event of the CanTxPduId from the CAN Driver module.|
|多实例个数|0 - 1|

|配置项属性|值（函数名配置项）|
|---|---|
|名称|CanIfTxPduUserTxConfirmationName|
|描述|This parameter defines the name of the \<User_TxConfirmation\>.|
|描述|概述：CanIfTxPduUserTxConfirmationName 是一个配置参数，用于指定发送CAN帧后调用的确认函数的名称，这个函数通常由上层模块实现，用以确认消息是否已经被成功发送到CAN网络。|
|描述|注意：确认函数的名称应与实际实现的函数名一致；确保该函数能够正确处理发送确认；在配置时，应注意与其他PDU的确认函数名称不冲突，以避免潜在的错误调用。|
|说明|This parameter depends on the parameter CanIfTxPduUserTxConfirmationUL. If CanIfTxPduUserTxConfirmationUL equals CAN_TP, CAN_NM, PDUR, XCP, DLT, CAN_TSYN, J1939NM or J1939TP, the name of the \<User_TxConfirmation\> is fixed. If CanIfTxPduUserTxConfirmationUL equals CDD, the name of the \<User_TxConfirmation\> is selectable.|
|多实例个数|0 - 1|
|字段长度|1-32|

|配置项属性|值（函数名配置项）|
|---|---|
|名称|CanIfTxPduUserTxCalloutName|
|描述|This parameter defines the name of the \<User_TxCalloutName\>.|
|描述|概述：CanIfTxPduUserTxCalloutName 是一个配置参数，用于指定发送CAN接口传输数据单元（PDU）时调用的用户定义函数的名称，该函数在发送操作之前或之后执行，以实现特定的用户逻辑。|
|描述|注意：用户定义的回调函数需要遵循AUTOSAR规范中定义的原型和行为；确保配置的函数名在项目中存在并且可以被正确链接；如果不需要使用用户回调，该配置项可以不设置或设置为空。|
|说明|This parameter is independent of the parameter CanIfTxPduUserTxConfirmationUL.|
|多实例个数|0 - 1|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CanIfTxPduCanId|
|描述|CAN Identifier of transmit CAN L-PDUs used by the CAN Driver for CAN L-PDU transmission.|
|描述|概述：CanIfTxPduCanId 是用于定义CAN接口层传输PDU的CAN标识符（CAN ID），它指定了发送PDU时所使用的CAN ID。|
|描述|注意：CAN ID的值必须在CAN网络中唯一，以避免冲突；根据CAN标准，标准帧格式的CAN ID为11位，扩展帧格式的CAN ID为29位；在配置时需要注意与CAN控制器和网络管理的兼容性。|
|说明|Range: 11 Bit For Standard CAN Identifier ... 29 Bit For Extended CAN identifier The CAN Identifier may be omitted for dynamic transmit L-PDUs.|
|多实例个数|1 - 1|
|取值范围|0 - 536870911|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CanIfTxPduCanIdMask|
|描述|Identifier mask which denotes relevant bits in the CAN Identifier. This parameter may be used to keep parts of the CAN Identifier of dynamic transmit L-PDUs static. Range: 11 bits for Standard CAN Identifier, 29 bits for Extended CAN Identifier.|
|描述|概述：CanIfTxPduCanIdMask用于定义发送PDU（协议数据单元）的CAN标识符掩码，以便在发送过程中对CAN ID进行过滤或匹配，确保正确的数据传输。|
|描述|注意：在配置CanIfTxPduCanIdMask时，需要确保掩码与对应的CanIfTxPduCanId设置相匹配以免影响数据的正确发送；掩码的设置应遵循CAN网络的通信协议要求；AUTOSAR CP 4.4标准中，该配置项的使用应结合具体的CAN驱动和网络管理需求进行考虑。|
|描述|该配置项未使用|
|多实例个数|0 - 1|
|默认值|3758096383|
|取值范围|0 - 3758096383|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CanIfTxPduId|
|描述|ECU wide unique, symbolic handle for transmit CAN L-SDU.|
|描述|概述：CanIfTxPduId 是用于标识传输协议数据单元（PDU）的唯一标识符，它在CAN接口模块中用于管理和映射发送的CAN消息。|
|描述|注意：确保每个CanIfTxPduId在系统中是唯一的，以避免数据传输的冲突；在配置时应与ECU的CAN驱动和网络管理配置保持一致；在使用AUTOSAR工具链时，通常这些ID由工具自动分配和管理。|
|说明|Range: 0..max. number of CantTxPduIds|
|多实例个数|1 - 1|
|取值范围|0 - 4294967295|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CanIfTxPduDataLength|
|描述|Data length of the tx CAN L-PDUs used by the CAN Interface.|
|描述|概述：CanIfTxPduDataLength配置项用于定义CAN接口层传输的PDU（协议数据单元）的数据长度，即CAN帧的DLC（Data Length Code）。|
|描述|注意：在配置CanIfTxPduDataLength时，需要确保其值不超过CAN帧允许的最大数据长度，通常为8字节（对于标准CAN）或64字节（对于CAN FD）；此外，该值应与PDU实际数据大小相匹配，避免数据截断或填充；在AUTOSAR CP 4.4标准中，应当遵循相关的PDU到CAN帧映射规则。|
|说明|This information is used for Data Length Check. Additionally it might specify the valid bits in case of the discrete DLC for CAN FD L-PDUs \> 8 bytes. The data area size of a CAN L-PDU can have a range from 0 to 64 bytes.|
|多实例个数|1 - 1|
|取值范围|0 - 64|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|CanIfTxPduBufferRef|
|描述|Configurable reference to a CanIf buffer configuration.|
|描述|概述：CanIfTxPduBufferRef 是一个配置参数，用于将CAN接口层的传输PDU（协议数据单元）关联到相应的缓冲区，以便在发送过程中存储和管理PDU。|
|描述|注意：在配置CanIfTxPduBufferRef时，必须确保引用的缓冲区已经定义并且适合于PDU的大小和类型；此外，缓冲区管理策略应当与系统的实时性和可靠性要求相匹配；在配置时还应注意PDU到缓冲区的映射是唯一的，避免不同的PDU引用相同的缓冲区。|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/CanIf/CanIfInitCfg/CanIfBufferCfg|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|CanIfTxPduRef|
|描述|Reference to the "global" Pdu structure to allow harmonization of handle IDs in the COM-Stack.|
|描述|概述：CanIfTxPduRef 是一个配置参数，用于将CAN接口层的传输PDU（协议数据单元）引用到具体的CAN驱动层的发送PDU。|
|描述|注意：在配置CanIfTxPduRef时，必须确保引用的CAN驱动层PDU已经定义且与CAN接口层的PDU匹配；此外，确保PDU的ID和类型等属性与实际的CAN网络通信要求一致；在配置过程中，还应注意避免PDU重复引用或者引用错误，以确保CAN通信的正确性。|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/EcuC/EcucConfigSet/EcucPduCollection/Pdu|

#### 3.4.1. CanIfTTTxFrameTriggering

|容器属性|值（容器）|
|---|---|
|名称|CanIfTTTxFrameTriggering|
|描述|CanIfTTTxFrameTriggering is specified in the SWS TTCAN Interface and defines Frame trigger for TTCAN transmission.|
|描述|概述：CanIfTTTxFrameTriggering配置项是用于定义CAN接口的时间触发传输帧的触发属性，这包括了帧的标识符、数据长度代码（DLC）和引用的硬件对象等信息。|
|描述|注意：在AUTOSAR CP 4.4标准中，确保配置的触发属性与系统的时间触发通信需求相匹配；如果系统不支持时间触发通信，则不应配置此项；在配置时，需要注意与CanIfTxPduConfig和CanController的配置保持一致性。|
|描述|该配置项未使用|
|说明|This container is only included and valid if TTCAN is supported by the controller, enabled (see CanIfSupportTTCAN, ECUC_CanIf_00675), and a joblist is used.|
|多实例个数|0 - 1|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CanIfTTTxJoblistTimeMark|
|描述|Defines the point in time, when the joblist execution funciton (JLEF) shall be called for the referenced tx frame trigger.|
|描述|概述：CanIfTTTxJoblistTimeMark 配置项用于定义在时间触发的CAN通信中，发送任务列表的时间标记，这有助于确保在预定的时间点发送特定的CAN帧。|
|描述|注意：在使用时间触发的CAN通信时，需要确保时间标记的准确性和一致性；该配置项应与CAN驱动和时间同步机制紧密协作，以保证时间触发传输的可靠性；在配置时需考虑系统的时间分辨率和精度要求，以避免时间偏差导致的通信问题。|
|描述|该配置项未使用|
|说明|Value is given in cycle time. This parameter is only configurable if a joblist is enabled by parameter CanIfTTJobList.|
|多实例个数|0 - 1|
|取值范围|0 - 65535|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|CanIfTTTxHwObjectTriggerIdRef|
|描述|This parameter refers to a particular TTCAN hardware transmit object Trigger of a hardware object in the TTCAN Driver Module,|
|描述|概述：CanIfTTTxHwObjectTriggerIdRef是用于引用特定的硬件对象触发器ID，这在基于时间触发的CAN通信帧传输中是必需的，以确保按时发送CAN帧。|
|描述|注意：此配置项在使用时间触发传输（TT）功能时才相关；确保引用的触发器ID与实际硬件配置相匹配；在不支持时间触发的硬件上使用此配置可能导致配置错误。|
|描述|该配置项未使用|
|说明|which is referred via plain CAN parameter CANIF_HTH_HANDLETYPE_REF. This parameter is only configurable if a joblist is enabled by parameter CanIfTTJobList.|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Can/CanConfigSet/CanHardwareObject/CanTTHardwareObjectTrigger|

## 4. CanIfPrivateCfg

|容器属性|值（容器）|
|---|---|
|名称|CanIfPrivateCfg|
|描述|This container contains the private configuration (parameters) of the CAN Interface.|
|描述|概述：CanIfPrivateCfg 是一个配置容器，包含了CAN接口模块的私有配置参数，这些参数通常不会被外部模块所访问，用于定义CAN接口模块内部的行为和属性。|
|描述|注意：在配置CanIfPrivateCfg时，需要确保所有的私有参数与项目的具体需求和CAN控制器的特性相匹配；此外，应当遵循AUTOSAR CP 4.4标准中对于私有配置参数的规定和限制；在进行配置时，还应注意与其他模块的配置参数之间的兼容性和一致性。|
|多实例个数|1 - 1|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|CanIfPrivateSoftwareFilterType|
|描述|Selects the desired software filter mechanism for reception only.|
|描述|概述：CanIfPrivateSoftwareFilterType 是一个配置参数，用于定义CAN接口模块内部软件消息过滤的类型，以确定哪些接收到的CAN消息将被上层软件处理。|
|描述|注意：在配置CanIfPrivateSoftwareFilterType时，需要确保选择的过滤类型与系统的消息处理策略相匹配；此外，过滤类型的选择可能会影响系统的性能，因为不同的过滤机制可能对CPU的负载有不同的影响；在AUTOSAR CP 4.4标准中，应当检查该配置项是否支持所有必要的过滤类型，以满足应用需求。|
|说明|Each implemented software filtering method is identified by this enumeration number. Range: Types implemented software filtering methods|
|多实例个数|1 - 1|
|默认值|LINEAR|

### 4.1. CanIfTTGeneral

|容器属性|值（容器）|
|---|---|
|名称|CanIfTTGeneral|
|描述|CanIfTTGeneral is specified in the SWS TTCAN Interface and defines if and in which way TTCAN is supported.|
|描述|概述：CanIfTTGeneral是AUTOSAR CAN接口模块的配置参数之一，用于定义CAN接口的传输层（Transfer Layer）的一般性配置，如是否启用特定的传输层功能。|
|描述|注意：在配置CanIfTTGeneral时，需要确保所选功能与硬件能力和项目需求相匹配；此配置项在AUTOSAR CP 4.4标准中可能没有直接对应，因为标准主要定义接口和功能模块的抽象层，具体实现细节可能因供应商而异；务必参考具体的AUTOSAR实现文档和硬件手册以确保正确配置。|
|描述|该配置项未使用|
|说明|This container is only included and valid if TTCAN is supported by the controller, enabled (see CanIfSupportTTCAN, ECUC_CanIf_00675), and used.|
|多实例个数|0 - 1|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|CanIfTTJoblist|
|描述|Defines whether TTCAN is processed via a joblist.|
|描述|概述：CanIfTTJoblist 配置项用于定义CAN接口模块中的触发传输作业列表，这些作业列表指定了在特定条件下需要发送的CAN消息的顺序和时间。|
|描述|注意：在配置CanIfTTJoblist时，需要确保列表中的CAN消息符合网络的时间触发传输要求；此外，要注意与CAN驱动和网络管理模块的兼容性；在配置时还应考虑系统的实时性和消息优先级。|
|描述|该配置项未使用|
|说明|TRUE: Joblist is used. FALSE: No joblist is used. This parameter is only configurable if TTCAN is enabled by parameter CanIfSupportTTCAN.|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CanIfTTMaxIsrDelay|
|描述|Defines the maximum delay for the execution of the joblist execution function JLEF. This parameter is only configurable if a joblist is enabled by parameter CanIfTTJobList.|
|描述|概述：CanIfTTMaxIsrDelay 配置项定义了CAN接口模块中，从接收到中断信号到开始处理该中断的最大延迟时间，这个时间用于确保CAN通信的实时性和可靠性。|
|描述|注意：该参数的设置需要考虑系统的实时性要求和中断服务例程(ISR)的优先级；过高的延迟时间可能会导致CAN消息处理不及时，影响系统性能；在配置时需要确保与实际硬件和操作系统的中断响应能力相匹配。|
|描述|该配置项未使用|
|多实例个数|1 - 1|
|取值范围|0 - 65535|

#### 4.1.1. CanIfTTDemEventParameterRefs

|容器属性|值（容器）|
|---|---|
|名称|CanIfTTDemEventParameterRefs|
|描述|Container for the references to DemEventParameter elements which shall be invoked using the API Dem_SetEventStatus in case the corresponding error occurs. The EventId is taken from the referenced DemEventParameter's DemEventId symbolic value. The standardized errors are provided in this container and can be extended by vendor-specific error references.|
|描述|概述：CanIfTTDemEventParameterRefs配置项用于引用CAN接口模块中传输层错误检测管理（TTDem）事件的参数，允许CAN接口模块报告传输层的错误事件给诊断事件管理器（Dem）。|
|描述|注意：确保引用的Dem事件参数与实际的诊断需求相匹配；在配置时需遵循AUTOSAR的标准数据模型，以确保兼容性；该配置项在AUTOSAR CP 4.4中可能需要根据具体的实现和版本进行适当调整，以确保与最新的诊断管理策略一致。|
|描述|该配置项未使用|
|多实例个数|0 - 1|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|CANIF_TT_E_JLE_SYNC|
|描述|Reference to configured DEM event to report that the JLEF lost synchronization to the local time of the TTCAN controller.|
|描述|概述：CANIF_TT_E_JLE_SYNC是一个配置项，用于定义CAN接口模块中，针对J1939 Link Error (JLE) 错误的同步传输触发机制。|
|描述|注意：该配置项在AUTOSAR CP 4.4标准中未明确提及，因此在实施时需要依据具体的项目需求和CAN接口模块的实现细节来定义；确保与项目中使用的CAN驱动和网络管理模块兼容；在配置时应考虑网络的错误处理策略和性能影响。|
|描述|该配置项未使用|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Dem/DemConfigSet/DemEventParameter|

## 5. CanIfPublicCfg

|容器属性|值（容器）|
|---|---|
|名称|CanIfPublicCfg|
|描述|This container contains the public configuration (parameters) of the CAN Interface.|
|描述|概述：CanIfPublicCfg是CAN接口模块的公共配置参数集合，用于定义CAN接口模块的基本行为和功能，如控制器模式设置、通道定义和消息过滤策略等。|
|描述|注意：在配置CanIfPublicCfg时，需要确保与项目中使用的CAN控制器和网络管理策略相兼容；配置参数应遵循AUTOSAR CP 4.4标准中对CAN接口模块的要求和约束；对于多CAN通道的项目，需要为每个通道仔细配置相应的参数，避免配置错误导致通信故障。|
|多实例个数|1 - 1|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|CanIfDevErrorDetect|
|描述|Switches the development error detection and notification on or off.|
|描述|概述：CanIfDevErrorDetect 是一个配置参数，用于启用或禁用 CAN 接口 (CanIf) 模块的开发错误检测和报告机制。|
|描述|注意：在生产代码中通常会禁用此功能以节省资源，因为它主要用于开发和测试阶段；如果启用，需确保与 DEM (Diagnostic Event Manager) 模块的集成正确配置以处理错误报告；在配置此参数时，应遵循项目的错误处理策略和性能要求。|
|说明|\* true: detection and notification is enabled. \* false: detection and notification is disabled.|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|CanIfPublicDebugSupport|
|描述|trun on canif cmd.|
|描述|CanIfPublicDebugSupport 配置项定义了CANIF维测变量是否参与编译。|
|描述|注意：在配置CanIfPublicDebugSupport时，需要确保为CANIF维测变量预留足够的RAM大小。|
|说明|TRUE: Enabled FALSE: Disabled|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|CanIfPublicPnSupport|
|描述|Selects support of Partial Network features in CanIf.|
|描述|概述：CanIfPublicPnSupport配置项用于启用或禁用部分网络（Partial Networking）支持，允许在CAN接口级别上实现网络管理策略，以减少车辆休眠时的能耗。|
|描述|注意：在使用此配置项时，必须确保底层CAN驱动和网络管理模块支持部分网络特性；此配置项对于实现低功耗模式的车辆网络管理至关重要；在AUTOSAR CP 4.4标准中，此配置项的使用应与其他网络管理配置项协同考虑，以确保网络管理策略的一致性和有效性。|
|说明|True: Enabled False: Disabled|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|CanIfPublicTxBuffering|
|描述|Enables and disables the buffering of transmit L-PDUs (rejected by the CanDrv) within the CAN Interface module.|
|描述|概述：CanIfPublicTxBuffering 配置项用于定义是否启用CAN接口的公共发送缓冲区，以便管理多个发送请求并优化网络带宽使用。|
|描述|注意：在启用此配置时，需要确保缓冲区大小和管理策略适当配置以避免数据丢失；此配置项在高负载CAN网络中尤为重要，以保持数据传输的效率和可靠性；AUTOSAR CP 4.4标准支持此配置，但具体实现细节可能因供应商而异。|
|说明|True: Enabled False: Disabled|
|多实例个数|1 - 1|
|默认值|true|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|CanIfPublicTxBufferMaxDepthFetchSupport|
|描述|After enabling the CanIfPublicTxBufferMaxDepthFetchSupport configuration item, the maximum usage depth of each CanIfTxBuffer queue will be monitored and recorded during runtime and stored in the RAM resource named CanIfTxBufferMaxDepth, which is helpful for users to reasonably adjust CanIfTxBufferSize according to the actual caniftxbuffer queue usage.|
|描述|启用CanIfPublicTxBufferMaxDepthFetchSupport配置项后，将在runtime过程中监测并记录每个CanIfTxBuffer队列的最大使用深度，并存储在RAM资源CanIfTxBufferMaxDepth中，使用户能够根据实际的缓存队列使用情况合理地调整CanIfTxBufferSize。|
|描述|注意：此配置仅在CanIfPublicTxBuffering配置为true时可以启用。此外，为了得到合理可靠的最大使用深度，用户需要进行一段时间的长稳维测。|
|说明|True: Enabled False: Disabled|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|CanIfPublicWakeupCheckValidByNM|
|描述|If enabled, only NM messages shall validate a detected wake-up event in CanIf.|
|描述|概述：CanIfPublicWakeupCheckValidByNM 是一个配置参数，用于决定是否通过网络管理（NM）检查唤醒源的有效性。|
|描述|注意：在使用此配置时，必须确保网络管理功能已经集成并正确配置在系统中；此配置项对于实现车辆网络唤醒功能的可靠性至关重要；在AUTOSAR CP 4.4标准中，此配置应与其他唤醒相关配置项协同工作，以确保系统的正确响应。该配置项置true时，CanIfPublicWakeupCheckValidSupport也会置为true，并且置灰；当该配置项由true置为false时，CanIfPublicWakeupCheckValidSupport默认保留为true，并取消置灰。|
|说明|If disabled, all received messages corresponding to a configured Rx PDU shall validate such a wake-up event. This parameter depends on CanIfPublicWakeupCheckValidSupport and shall only be configurable, if it is enabled. True: Enabled False: Disabled|
|多实例个数|0 - 1|
|默认值|false|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|CanIfPublicWakeupCheckValidSupport|
|描述|Selects support for wake up validation|
|描述|概述：CanIfPublicWakeupCheckValidSupport 是一个配置参数，用于启用或禁用 CAN 接口 (CanIf) 模块中的唤醒验证支持功能，以检查接收到的唤醒事件是否有效。|
|描述|注意：在配置此参数时，需要确保它与系统中实际的硬件支持和唤醒源需求相匹配；如果硬件不支持唤醒验证，那么启用该功能可能会导致不必要的复杂性或功能不一致；在设计低功耗模式和唤醒逻辑时，应考虑此配置项的设置。|
|说明|True: Enabled False: Disabled|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|CanIfWakeupSupport|
|描述|Enables the CanIf_CheckWakeup API at Pre-Compile-Time. Therefore, this parameter defines if there shall be support for wake-up.|
|描述|概述：CanIfWakeupSupport 是一个配置项，用于指定CAN接口模块是否支持唤醒功能，这决定了CAN控制器是否能够在网络唤醒事件发生时唤醒ECU。|
|描述|注意：在配置CanIfWakeupSupport时，需要确保硬件支持唤醒功能；此外，应当与ECU的低功耗模式和网络管理需求相协调；如果设置为不支持唤醒，那么在网络唤醒事件发生时，ECU将不会被唤醒。|
|说明|TRUE: Enabled FALSE: Disabled|
|多实例个数|1 - 1|
|默认值|true|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|CanIfUserTxCalloutSupport|
|描述|Enables the Appl_CanIf_Tx_Callout API at Pre-Compile-Time. Therefore, this parameter defines if there shall be support for canif tx callout.|
|描述|概述：CanIfUserTxCalloutSupport 是一个配置项，用于启用或禁用用户定义的发送回调函数，该函数在CAN接口层发送CAN消息之后被调用。|
|描述|注意：在使用此配置项时，需要确保已经实现了相应的用户定义回调函数；此配置项的使用可能会影响系统的性能，因为额外的回调函数调用可能会增加系统的处理时间；在配置此项时，应当考虑与其他CAN接口层配置项的兼容性和整体系统设计。|
|说明|TRUE: Enabled FALSE: Disabled|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|CanIfUserTxConfirmationCalloutSupport|
|描述|Enables the Appl_CanIf_TxConfirmation_Callout API at Pre-Compile-Time. Therefore, this parameter defines if there shall be support for canif txconfirmation callout.|
|描述|概述：CanIfUserTxConfirmationCalloutSupport 是一个配置项，用于启用或禁用用户定义的发送确认回调函数，这些回调函数在CAN接口层发送成功后被调用。|
|描述|注意：在使用此配置项时，需要确保已经定义了相应的用户回调函数；此配置项的使用应与系统的实际需求相匹配，避免不必要的开销；如果启用此功能，需要在整个系统中保持一致性，以确保所有相关的发送确认都能得到处理。|
|说明|TRUE: Enabled FALSE: Disabled|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|CanIfUserRxIndicationCalloutSupport|
|描述|Enables the Appl_CanIf_RxIndication_Callout API at Pre-Compile-Time. Therefore, this parameter defines if there shall be support for canif rxIndication callout.|
|描述|概述：CanIfUserRxIndicationCalloutSupport 是一个配置项，用于启用或禁用用户定义的接收指示回调函数，这些回调函数在接收到CAN帧时由CAN接口模块调用。|
|描述|注意：在使用此配置项时，需要确保已经定义了相应的用户回调函数；此配置项的启用可能会影响系统的响应时间和性能；如果项目中不需要处理接收到的CAN消息，则可以禁用此功能以节省资源。|
|说明|TRUE: Enabled FALSE: Disabled|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（函数名配置项）|
|---|---|
|名称|CanIfMapMcalApiPrefix|
|描述|This configuration item maps the driver interfaces of different chips|
|描述|概述：CanIfMapMcalApiPrefix用于定义CAN接口模块中MCAL层API函数的前缀，以便在上层模块中调用这些底层驱动函数时，能够正确地引用它们。|
|描述|注意：前缀的定义必须与实际MCAL驱动的命名约定一致，以确保正确的函数调用；在多个CAN驱动共存的系统中，正确的前缀映射尤为关键；该配置项在整个项目中应保持一致，避免引用混乱。|
|说明|This configuration item maps the driver interfaces of different chips|
|多实例个数|1 - 1|

|配置项属性|值（字符串参数配置项）|
|---|---|
|名称|CanIfPublicCddHeaderFile|
|描述|Defines header files for callback functions which shall be included in case of CDDs. Range of characters is 1.. 32.|
|描述|概述：CanIfPublicCddHeaderFile 配置项用于指定Complex Device Driver (CDD) 的头文件名称，该文件包含了CDD所需的类型定义和函数原型，以便于CAN Interface模块能够与CDD进行交互。|
|描述|注意：在配置CanIfPublicCddHeaderFile时，需要确保文件名与实际CDD头文件的名称相匹配；头文件应当包含所有必要的声明，以供CAN Interface模块正确调用CDD的接口；如果项目中没有使用CDD，该配置项可能不需要设置或者应该保持为空。|
|多实例个数|0 - inf|

|配置项属性|值（字符串参数配置项）|
|---|---|
|名称|CanIfPublicUserCbkHeaderFile|
|描述|Defines header files for user callback functions which shall be included in case of CanIfCallout. Range of characters is 1.. 32.|
|描述|概述：CanIfPublicUserCbkHeaderFile 配置项用于指定用户定义的CAN接口回调函数的头文件名称，这使得用户可以在该头文件中声明自己的回调函数，以便在CAN接口接收或发送消息时被调用。|
|描述|注意：确保指定的头文件存在且包含了所有必要的用户回调函数声明；头文件的命名和路径应符合项目的文件组织结构和编码规范；在AUTOSAR CP 4.4标准中，该配置项应与其他CAN接口模块配置保持一致性，避免命名冲突或路径错误。|
|多实例个数|0 - inf|

## 6. CanIfTrcvDrvCfg

|容器属性|值（容器）|
|---|---|
|名称|CanIfTrcvDrvCfg|
|描述|This container contains the configuration (parameters) of all addressed CAN transceivers by each underlying CAN Transceiver Driver module. For each CAN transceiver Driver a seperate instance of this container shall be provided.|
|描述|概述：CanIfTrcvDrvCfg 是用于定义CAN接口传输层驱动配置的参数，包括传输层驱动的标识符和相关属性。|
|描述|注意：确保每个传输层驱动配置与其对应的硬件和网络管理需求相匹配；在配置时需遵循AUTOSAR CP 4.4标准中对CAN接口的具体要求；适当的配置可以优化网络性能和可靠性。|
|多实例个数|0 - inf|

### 6.1. CanIfTrcvCfg

|容器属性|值（容器）|
|---|---|
|名称|CanIfTrcvCfg|
|描述|This container contains the configuration (parameters) of one addressed CAN transceiver by the underlying CAN Transceiver Driver module. For each CAN transceiver a seperate instance of this container has to be provided.|
|描述|概述：CanIfTrcvCfg 是一个配置项，用于定义CAN接口层中CAN收发器的配置参数，包括收发器的模式设置、唤醒和睡眠功能等。|
|描述|注意：在配置CanIfTrcvCfg时，需要确保收发器的参数与实际硬件特性相匹配；根据AUTOSAR CP 4.4标准，应当遵循其定义的属性和数据结构；在多个CAN网络中，每个网络的收发器配置应该是唯一的，以避免配置冲突。|
|多实例个数|1 - inf|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|CanIfTrcvWakeupSupport|
|描述|This parameter defines if a respective transceiver of the referenced CAN Transceiver Driver modules is queriable for wake up events.|
|描述|概述：CanIfTrcvWakeupSupport 配置项用于定义CAN接口传输层是否支持唤醒功能，这决定了传输层是否能够管理和识别网络唤醒事件。|
|描述|注意：在设计系统时，需要确认硬件支持唤醒功能；此配置应与ECU的低功耗模式和网络管理需求相匹配；AUTOSAR CP 4.4标准中，确保此配置与Can Transceiver Driver的能力相一致。|
|说明|True: Enabled False: Disabled|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CanIfTrcvId|
|描述|This parameter abstracts from the CAN Transceiver Driver specific parameter Transceiver. Each transceiver of all connected CAN Transceiver Driver modules shall be assigned to one specific TransceiverId of the CanIf.|
|描述|概述：CanIfTrcvId 是一个配置参数，用于标识CAN接口层中的CAN收发器（Transceiver）设备的唯一标识符。|
|描述|注意：在配置时，确保每个CAN收发器有一个唯一的CanIfTrcvId；该标识符通常与CAN驱动层中定义的收发器标识符相对应；在整系统中，CanIfTrcvId 必须保持一致，以便于系统的诊断和管理。|
|说明|Range: 0..number of configured transceivers of all CAN Transceiver Driver modules|
|多实例个数|1 - 1|
|取值范围|0 - 255|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|CanTrcvType|
|描述|This parameter defines the trcv type.|
|描述|概述：CanTrcvType配置项用于定义收发器类型。|
|描述|注意：非Autosar标准|
|说明|If CanIfTrcvCfg be configed, this parameter shall be configurable.|
|多实例个数|0 - 1|

|配置项属性|值（收发器通道名称定义）|
|---|---|
|名称|CanIfTrcvCanTrcv|
|描述|This configuration is trcv channel name|
|描述|概述：CanIfTrcvCanTrcv用于定义收发器通道名称。|
|描述|注意：需要用户自己手动填写，和自己手动开发收发器对应上。|
|说明|This configuration is trcv channel name|
|多实例个数|0 - 1|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|CanTrcvWakeupSourceRef|
|描述|Reference to a wakeup source in the EcuM configuration. This reference is only needed if CanTrcvWakeupByBusUsed is true.|
|描述|概述：CanTrcvWakeupSourceRef 配置项用于将CAN收发器（Transceiver）的唤醒源与ECU唤醒源进行关联，确保在CAN网络上的唤醒事件能够被系统正确识别和处理。|
|描述|注意：在配置时需确保唤醒源的引用正确指向有效的ECU唤醒源对象；如果系统中存在多个CAN收发器，每个收发器的唤醒源应当被唯一标识和配置；AUTOSAR CP 4.4标准中，唤醒源的配置应当与PNC（Partial Network Cluster）或ECU唤醒源的定义相一致。|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/EcuM/EcuMConfiguration/EcuMCommonConfiguration/EcuMWakeupSource|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|CanIfTrcvChnlToCanIfCtrlChnlRef|
|描述|This parameter references to the logical handle of the underlying CAN|
|描述|概述：CanIfTrcvChnlToCanIfCtrlChnlRef 配置项用于映射CAN接口的收发器通道到CAN接口控制器通道，确保正确的通信路径和数据流。|
|描述|注意：在配置时需确保每个收发器通道正确对应到唯一的控制器通道；不遵循此映射规则可能导致数据传输错误或通信失败；在多通道CAN系统中，此配置尤为关键以保证通道间的正确数据隔离和处理。|
|说明|transceiver from the CAN transceiver driver module to be served by the CAN Interface module. Range: 0..max. number of underlying supported CAN transceivers|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/CanIf/CanIfCtrlDrvCfg/CanIfCtrlCfg|
