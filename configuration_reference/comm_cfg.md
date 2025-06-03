# ComM 配置项参考文档

|容器属性|值（容器）|
|---|---|
|名称|ComM|
|描述|Configuration of the ComM (Communications Manager) module.|
|描述|概述：ComM（Communication Manager）模块负责管理ECU中的通信网络接口的状态，确保根据车辆的不同操作模式调整网络接口的行为。|
|描述|注意：ComM配置必须与ECU支持的网络接口和通信协议一致；确保与Nm（网络管理）、EcuM（ECU管理）等其他管理模块的正确交互；在配置时应考虑系统的功耗和唤醒策略。|
|多实例个数|0 - 1|

## 1. ComMConfigSet

|容器属性|值（容器）|
|---|---|
|名称|ComMConfigSet|
|描述|This container contains the configuration parameters and sub containers of the AUTOSAR ComM module.|
|描述|概述：ComMConfigSet 是一个配置容器，包含了用于通信管理（ComM）模块的参数集合，这些参数定义了网络管理策略、通信模式和用户请求处理。|
|描述|注意：在配置ComMConfigSet时，必须确保所有的网络通道（Channels）和用户（Users）都被正确配置；每个ComMChannel需要至少一个ComMUser；配置参数应符合ECU的网络管理需求和硬件能力。|
|多实例个数|1 - 1|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|ComMPncEnabled|
|描述|Defines whether in this configuration set the partial networking is enabled.|
|描述|概述：ComMPncEnabled是一个配置项，用于启用或禁用部分网络集群（Partial Network Cluster）的功能，这是通信堆栈中的一个特性，用于控制ECU的网络管理行为。|
|描述|注意：在AUTOSAR CP 4.4标准中，确保在使用此配置项时，ECU的网络管理需求与部分网络集群功能相匹配；如果ECU不支持部分网络集群功能，则不应启用此配置项；在配置时，应考虑与其他网络管理配置项的兼容性和一致性。|
|说明|true: Enabled false: Disabled|
|多实例个数|0 - 1|
|默认值|false|

### 1.1. ComMChannel

|容器属性|值（容器）|
|---|---|
|名称|ComMChannel|
|描述|This container contains the configuration (parameters) of the bus channel(s). The channel parameters shall be harmonized within the whole communication stack.|
|描述|概述：ComMChannel是指通信管理模块中的通信通道，用于管理ECU内部或与其他ECU之间的网络通信状态，确保网络通信的可靠性和高效性。|
|描述|注意：在配置ComMChannel时，需要确保其与ECU支持的网络接口类型相匹配；每个ComMChannel应唯一对应一个物理或虚拟的网络通道；在AUTOSAR CP 4.4中，对ComMChannel的配置参数和行为有详细规定，需要遵循这些规定以保证兼容性和性能。|
|多实例个数|1 - 256|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|ComMFullCommRequestNotificationEnabled|
|描述|Defines if the optional SenderReceiver Port of Interface ComM_CurrentChannelRequest will be provided for this channel.|
|描述|概述：ComMFullCommRequestNotificationEnabled 是一个布尔配置项，用于启用或禁用通信管理器（ComM）模块中全通信模式请求的通知功能。|
|描述|注意：在AUTOSAR CP 4.4标准中，确保此配置项与系统设计需求一致，如果系统需要在请求全通信模式时接收通知，则应启用此功能；此配置项的默认值通常取决于具体的通信需求和ECU资源限制；在配置此项时，应考虑与其他BswM或ECUM的交互，以确保通信状态管理的正确性。|
|说明|True means enabled. False means disabled|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|ComMNoCom|
|描述|Not allowed to change state of ComM channel to COMM_SILENT_COMMUNICATION or COMM_FULL_COMMUNICATION.|
|描述|概述：ComMNoCom 是一个配置参数，用于定义通信管理模块（ComM）在无通信模式（No Communication Mode）下的行为，控制网络接口的通信能力。|
|描述|注意：确保正确配置以避免网络节点在不应该通信的时候进行数据传输；此模式通常用于降低能耗或满足特定的系统安全需求；在实施时需考虑与其他通信管理模式的协调和切换逻辑。|
|说明|true: Enabled - Not allowed to switch to Communication Modes above. false: Disabled - Allowed to switch Communication Modes above. Shall be possible to change parameter during runtime with ComM API's. ECU/All channels: ComM_LimitECUToNoComMode(). Separate channels: ComM_LimitChannelToNoComMode().|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|ComMNoWakeup|
|描述|Defines if an ECU is not allowed to wake-up the channel.|
|描述|概述：ComMNoWakeup用于指定通信管理模块（ComM）在没有唤醒事件发生时的行为，主要用于控制网络管理逻辑以减少能耗。|
|描述|注意：在配置ComMNoWakeup时，需要确保与ECU的低功耗需求相匹配；此配置项对于实现车辆的休眠模式和唤醒策略至关重要；不正确的配置可能导致网络无法按预期进入低功耗状态或唤醒。|
|说明|true: Enabled (not allowed to wake-up)) false: Disabled This is the default/init value of a runtime variable that can be changed during runtime using ComM_PreventWakeUp().|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|ComMNoWakeUpInhibitionNvmStorage|
|描述|If this parameter is set to "true", the NoWakeUp inhibition state of the channel shall be stored (in some implementation specific way) in the block pointed to by ComMGlobalNvmBlockDescriptor.|
|描述|概述：ComMNoWakeUpInhibitionNvmStorage 用于配置是否将通信管理器（ComM）的无唤醒抑制状态存储在非易失性存储器（NVM）中。|
|描述|注意：在AUTOSAR CP 4.4中，此配置项确保在系统重启后，无唤醒抑制状态能够被恢复，从而维持网络管理的连续性；正确配置此项可以避免车辆在某些情况下无法唤醒的问题；应根据项目具体需求决定是否启用此功能。|
|多实例个数|1 - 1|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|ComMBusType|
|描述|Identifies the bus type of the channel.|
|描述|概述：ComMBusType配置项用于定义通信管理模块（ComM）所管理的网络类型，例如CAN、LIN或者Ethernet，以确保正确的网络管理策略被应用。|
|描述|注意：在配置ComMBusType时，必须确保所选网络类型与实际项目中使用的网络类型一致；不同的网络类型可能需要不同的配置参数和管理策略；AUTOSAR CP 4.4标准支持多种网络类型，但具体实现细节可能因供应商而异。|
|多实例个数|1 - 1|
|默认值|COMM_BUS_TYPE_CAN|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|ComMPncGatewayType|
|描述|Identifies the Partial Network Gateway behaviour of a ComMChannel.|
|描述|概述：ComMPncGatewayType 配置项定义了部分网络（Partial Network）通信网关的类型，用于控制和管理部分网络请求和释放，以优化网络的能耗。|
|描述|注意：在配置ComMPncGatewayType时，需要确保它与系统中实际使用的部分网络类型相匹配；此配置项对于实现网络管理策略至关重要，因此需要仔细规划和验证；在AUTOSAR CP 4.4标准中，应当参照相关的通信管理模块来配置此项，以确保兼容性和正确性。|
|多实例个数|0 - 1|
|默认值|COMM_GATEWAY_TYPE_ACTIVE|

|配置项属性|值（浮点型参数配置项）|
|---|---|
|名称|ComMMainFunctionPeriod|
|描述|Specifies the period in seconds that the MainFunction has to be triggered with.|
|描述|概述：ComMMainFunctionPeriod配置项定义了通信管理主函数(ComM_MainFunction)的调用周期，单位为毫秒。这个周期决定了通信管理模块检查网络管理需求和状态变化的频率。|
|描述|注意：该值需要根据ECU的实际需求和网络管理策略来配置，以确保系统的响应性和效率；过小的周期可能会增加系统的负载，而过大的周期可能导致网络状态反应不够及时；在配置时需要考虑与其他BswM模块的周期性调用的协调。|
|说明|Comment: ComM scheduling shall be at least as fast as the communication stack and a schedule longer than 100ms makes no sense for communication.|
|多实例个数|1 - 1|
|默认值|0.01|
|取值范围|0 - Inf|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|ComMChannelId|
|描述|Channel identification number of the corresponding channel.|
|描述|概述：ComMChannelId 是一个配置项，用于唯一标识通信管理模块（ComM）中的通信通道，它关联了网络层的通道与ComM模块。|
|描述|注意：ComMChannelId 必须是唯一的，以确保每个通信通道都能被正确识别和管理；在配置时应确保其与网络层的通道配置相匹配；在整个系统中，应避免ComMChannelId的重复配置，以防止通信冲突。|
|多实例个数|1 - 1|
|取值范围|0 - 255|

|配置项属性|值（字符串参数配置项）|
|---|---|
|名称|ComMCDDBusPrefix|
|描述|Prefix to be used for API calls to CDD.|
|描述|概述：ComMCDDBusPrefix 是一个配置参数，用于定义通信管理模块（ComM）中，与CAN数据总线相关的标识符前缀，以便在生成代码时区分不同的网络通道。|
|描述|注意：在配置时需保证前缀的唯一性，以避免在多网络环境中的命名冲突；前缀应简短且具有描述性，以便于理解和维护；在AUTOSAR CP 4.4标准中，确保该配置项符合命名规范和项目实际需求。|
|多实例个数|0 - 1|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|ComMManageReference|
|描述|Represenst the reference between a ComMChannel with role managing channel and a ComMChannel with role managed channel.|
|描述|概述：ComMManageReference配置项用于定义通信管理模块（ComM）中网络请求和释放的参考管理，确保网络通信资源的有效管理和调度。|
|描述|注意：该配置项需要与ECU的网络管理策略紧密配合，以避免资源冲突；在配置时需确保参考的网络请求和释放策略与实际的网络管理需求一致；AUTOSAR CP 4.4标准中对于网络管理的具体实现细节有严格规定，需仔细遵守以保证兼容性。|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/ComM/ComMConfigSet/ComMChannel|

#### 1.1.1. ComMNetworkManagement

|容器属性|值（容器）|
|---|---|
|名称|ComMNetworkManagement|
|描述|This container contains the configuration parameters of the networkmanagement.|
|描述|概述：ComMNetworkManagement 是一个配置项，用于定义通信管理模块（ComM）如何与网络管理（Nm）接口交互，以控制网络节点的状态和通信。|
|描述|注意：在配置ComMNetworkManagement时，需要确保它与所使用的网络管理协议（如 CAN NM, FR NM, LIN NM 等）兼容；此外，应当注意配置正确的网络通道标识符，以确保网络管理正确地控制对应的网络节点；在AUTOSAR CP 4.4标准中，应当遵循相关的模块间接口定义和行为规范。|
|多实例个数|1 - 1|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|ComMPncNmRequest|
|描述|If this parameter equals true then every time a FULL Communication is requested due to a change in the PNC state machine to COMM_PNC_REQUESTED Nm shall be called using the API Nm_NetworkRequest.|
|描述|概述：ComMPncNmRequest 配置项用于定义网络管理请求的处理方式，确保车辆网络在需要时能够快速地进行状态转换。|
|描述|注意：在配置ComMPncNmRequest时，必须确保与车辆的网络管理策略一致；此配置项应与其他网络管理配置项协同工作，以避免配置冲突；AUTOSAR CP 4.4中对此配置项的具体参数和行为有详细规定，需要仔细遵守标准。|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|ComMNmVariant|
|描述|Defines the functionality of the networkmanagement.|
|描述|概述：ComMNmVariant配置项用于定义网络管理（Nm）的变体，指定了车辆网络管理策略的类型，如是否使用CAN网络管理、GATEWAY网络管理等。|
|描述|注意：在选择ComMNmVariant时，需确保其与项目中实际使用的网络管理策略相匹配；若项目中使用了多种网络管理策略，需要为每种策略正确配置对应的变体；AUTOSAR CP 4.4标准中对网络管理的配置和实现有详细规定，需仔细遵守以保证系统的兼容性和稳定性。|
|说明|Shall be harmonized with NM configuration.|
|多实例个数|1 - 1|
|默认值|FULL|

|配置项属性|值（浮点型参数配置项）|
|---|---|
|名称|ComMNmLightTimeout|
|描述|Defines the timeout (in seconds) after COMM_FULL_COMMUNICATION sub-state COMM_FULL_COM_READY_SLEEP is left.|
|描述|概述：ComMNmLightTimeout配置项用于定义网络管理轻量级模式下，节点等待网络管理消息的超时时间，以确保网络稳定性和节点同步。|
|描述|注意：该配置项的值需根据网络的实际情况和性能要求谨慎设置，以避免因超时设置不当导致的网络通信问题；在AUTOSAR CP 4.4标准中，确保该配置项与网络管理策略和其他相关配置项协同工作；超时时间设置过短可能导致频繁的网络管理状态切换，设置过长可能影响网络的响应速度。|
|说明|The range shall be greater than 0.0 and less or equal to 255.0.|
|多实例个数|0 - 1|
|默认值|10|
|取值范围|0 - 255|

#### 1.1.2. ComMUserPerChannel

|容器属性|值（容器）|
|---|---|
|名称|ComMUserPerChannel|
|描述|This container contains a list of identifiers that are needed to refer to a user in the system which is linked to a channel.|
|描述|概述：ComMUserPerChannel 配置项定义了通信管理器（ComM）中用户和网络通道之间的关系，用于指定哪些用户需要哪些通道来进行通信。|
|描述|注意：在配置时需要确保每个用户至少映射到一个通道；用户和通道之间的映射关系应当遵循实际的通信需求和硬件架构；在多通道系统中，正确的用户到通道的映射对于网络管理和优化资源使用至关重要。|
|多实例个数|0 - 255|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|ComMUserChannel|
|描述|Reference to the ComMUser that corresponds to this channel user.|
|描述|概述：ComMUserChannel配置项用于定义用户和网络通道之间的关系，确保通信管理模块（ComM）能够根据用户的请求管理网络通道的状态。|
|描述|注意：在配置ComMUserChannel时，必须确保每个用户至少映射到一个网络通道；用户和网络通道之间的关系应当符合实际的通信需求；在配置过程中应遵循AUTOSAR CP 4.4标准中对于用户和通道关系的规定，以确保配置的有效性和一致性。|
|说明|ImplementationType: COMM_UserHandleType|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/ComM/ComMConfigSet/ComMUser|

### 1.2. ComMPnc

|容器属性|值（容器）|
|---|---|
|名称|ComMPnc|
|描述|This container contains the configuration of the partial network cluster (PNC).|
|描述|概述：ComMPnc 配置项用于管理部分网络通信（Partial Network Communication）的设置，包括PNC的激活和去激活策略。|
|描述|注意：在配置ComMPnc时，必须确保与车辆网络的其他部分兼容，特别是与ECU的网络管理功能；PNC设置应遵循AUTOSAR CP 4.4标准中定义的网络管理策略；正确配置PNC可以帮助降低网络的能耗，提高效率。|
|多实例个数|0 - 56|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|ComMPncId|
|描述|Partial network cluster identification number.|
|描述|概述：ComMPncId是用于标识PDU（协议数据单元）中特定的部分网络通信（Partial Network Communication）的ID，它允许在AUTOSAR COM层中配置和管理基于部分网络的通信需求。|
|描述|注意：PncId的值必须在系统中唯一，以避免配置冲突；在设计时需确保PncId与系统中其他网络管理元素的标识符相协调；AUTOSAR CP 4.4标准中对PncId的具体数值范围有明确规定，需遵守这些规定以保证兼容性。|
|多实例个数|1 - 1|
|取值范围|8 - 63|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|ComMChannelPerPnc|
|描述|Reference to the ComMChannel that is required for this PNC.|
|描述|概述：ComMChannelPerPnc配置项用于定义网络管理中，每个部分网络（PNC, Partial Network Cluster）与通信通道（ComMChannel）之间的关系，确保正确的网络请求和释放策略被应用。|
|描述|注意：在配置时需确保每个PNC至少关联一个ComMChannel，以保证网络请求能够正确传递；不同PNC可以共享同一个ComMChannel，但需注意资源竞争和通信冲突；该配置项在AUTOSAR CP 4.4中是一致的，但设计时应考虑网络管理策略的复杂性和系统资源限制。|
|说明|ImplementationType: NetworkHandleType|
|多实例个数|1 - 256|
|目标引用项的路径|/AUTOSAR/EcucDefs/ComM/ComMConfigSet/ComMChannel|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|ComMPncEthIfSwitchPortGroupRef|
|描述|Reference to the PortGroups that correspond to this PNC. Note: This is only for documentation.|
|描述|概述：ComMPncEthIfSwitchPortGroupRef 是一个配置项，用于将PNC（Partial Network Cluster）与特定的以太网交换机端口组相关联，以便管理PNC的网络请求和释放。|
|描述|注意：在配置ComMPncEthIfSwitchPortGroupRef时，必须确保引用的以太网交换机端口组已经在系统中定义并且与PNC的通信需求相匹配；此配置项对于实现PNC的网络管理功能至关重要，因此需要仔细检查其正确性；AUTOSAR CP 4.4标准中，确保该配置项与其他网络管理配置项协同工作，以保证网络管理的一致性和有效性。|
|多实例个数|0 - 255|
|目标引用项的路径|/AUTOSAR/EcucDefs/EthIf/EthIfConfigSet/EthIfSwitchPortGroup|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|ComMUserPerPnc|
|描述|Reference to the ComMUsers that correspond to this PNC.|
|描述|概述：ComMUserPerPnc 配置项定义了通信管理器（ComM）中，每个部分网络（PNC）对应的用户需求，用于管理网络请求和释放。|
|描述|注意：在配置时需确保每个PNC与至少一个用户正确关联；用户和PNC之间的关系应符合实际的网络管理需求；在AUTOSAR CP 4.4标准中，应遵循PNC和用户之间的关联规则，以确保网络管理的正确性。|
|说明|ImplementationType: COMM_UserHandleType|
|多实例个数|0 - 255|
|目标引用项的路径|/AUTOSAR/EcucDefs/ComM/ComMConfigSet/ComMUser|

#### 1.2.1. ComMPncComSignal

|容器属性|值（容器）|
|---|---|
|名称|ComMPncComSignal|
|描述|Represents the PncComSignals which are used to communicate the EIRA and ERA status of this PNC.|
|描述|概述：ComMPncComSignal配置项用于定义参与部分网络通信（Partial Network Communication）的信号，这些信号用于控制和监视部分网络的状态。|
|描述|注意：在配置ComMPncComSignal时，确保信号与部分网络的需求相匹配；此配置项在AUTOSAR CP 4.4中可能不直接存在，因为部分网络管理通常由ComM模块处理，需要检查与ComM模块的兼容性；正确配置信号属性，如信号长度和更新周期，以满足部分网络通信的实时性要求。|
|多实例个数|0 - inf|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|ComMPncComSignalDirection|
|描述|Indicates the communication direction of this PncComSignal.|
|描述|概述：ComMPncComSignalDirection 配置项用于定义部分网络通信（Partial Network Communication）中信号的传输方向，即信号是发送还是接收。|
|描述|注意：在配置ComMPncComSignalDirection时，需要确保信号方向与实际的系统设计和网络通信需求相匹配；AUTOSAR CP 4.4标准中对于部分网络通信的支持可能有特定的限制或要求，需要参考相关文档以确保一致性；在多信号系统中，正确配置每个信号的方向对于系统的正确运行至关重要。|
|多实例个数|1 - 1|
|默认值|RX|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|ComMPncComSignalKind|
|描述|Indicates whether this PncComSignal represents EIRA or ERA PNC information.|
|描述|概述：ComMPncComSignalKind 配置项用于定义车辆网络中通信信号的类型，这有助于优化网络通信策略和资源管理。|
|描述|注意：确保每个信号类型正确匹配其功能和网络要求；不正确的配置可能导致通信效率低下或数据传输错误；在配置时需遵循AUTOSAR CP 4.4标准中对信号类型的具体定义和要求。|
|说明|This parameter ComMPncComSignalKind is optional and shall be ignored when ComMPncComSignalDirection equals TX.|
|多实例个数|0 - 1|
|默认值|EIRA|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|ComMPncComSignalChannelRef|
|描述|Reference to the ComMChannel which is used to determine whether this PncComSignal shall participate in the active or passive role (via the parameter ComMPncGatewayType of the ComMChannel).|
|描述|概述：ComMPncComSignalChannelRef 是一个配置参数，用于将部分网络请求信号（PNC信号）映射到通信信道上，以便控制网络请求消息的发送。|
|描述|注意：在配置时需确保信号与通信信道之间的映射正确无误；此配置项对于实现部分网络请求的功能至关重要；在AUTOSAR CP 4.4标准中，应遵循相关的通信管理规范来配置此参数。|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/ComM/ComMConfigSet/ComMChannel|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|ComMPncComSignalRef|
|描述|Reference to the ComSignal which is used to transport the partial network channel request information.|
|描述|概述：ComMPncComSignalRef 用于定义与部分网络集群（Partial Network Cluster）相关的通信信号引用，以便在车辆网络中管理睡眠和唤醒信号。|
|描述|注意：确保引用的信号与实际的部分网络集群配置相匹配；在配置时需考虑信号的传输和接收特性，以保证网络的稳定性和响应速度；此配置项应与车辆的网络管理策略紧密结合，以优化能耗和通信效率。|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Com/ComConfig/ComSignal|

### 1.3. ComMUser

|容器属性|值（容器）|
|---|---|
|名称|ComMUser|
|描述|This container contains a list of identifiers that are needed to refer to a user in the system which is designated to request Communication modes.|
|描述|概述：ComMUser配置项定义了通信管理模块（ComM）中用户的属性和行为，它指定了用户请求通信模式的能力和方式，以及用户与通信通道（ComMChannel）之间的关联。|
|描述|注意：确保每个ComMUser正确映射到至少一个ComMChannel，以保证通信需求得到满足；用户请求的通信模式应与系统的能力和策略相匹配；在配置ComMUser时，应考虑系统的功耗和网络带宽需求。|
|多实例个数|0 - 255|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|ComMUserIdentifier|
|描述|An identifier that is needed to refer to a user in the system which is designated to request Communication Modes.|
|描述|概述：ComMUserIdentifier 是一个用于唯一标识通信管理器（ComM）用户的配置项，它将用户实体与其请求的通信服务关联起来。|
|描述|注意：在配置过程中，每个ComM用户必须分配一个唯一的标识符；这个标识符通常由系统设计者或配置工具分配，以确保系统中的一致性；在整个项目中，应保持ComMUserIdentifier的一致性，避免在不同的上下文中重复使用相同的标识符。|
|说明|ImplementationType: ComM_UserHandleType|
|多实例个数|1 - 1|
|取值范围|0 - 254|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|ComMUserEcucPartitionRef|
|描述|Denotes in which "EcucPartition" the requester is executed. When the partition is stopped, the communication request shall be cancelled in the ComM|
|描述|概述：ComMUserEcucPartitionRef配置项用于指定通信管理模块（ComM）用户所属的ECU配置分区引用，确保系统中的通信请求能够被正确管理和分配到相应的分区。|
|描述|注意：在多核或多分区系统中使用时，正确配置此项对于确保通信管理的隔离性和安全性至关重要；该配置项必须与系统分区设计一致，避免跨分区通信管理错误；AUTOSAR CP 4.4标准中对于分区的管理和配置有详细规定，需要确保与标准一致。|
|说明|to avoid a stay-awake situation of the bus due to a stopped partition.|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/EcuC/EcucPartitionCollection/EcucPartition|

## 2. ComMGeneral

|容器属性|值（容器）|
|---|---|
|名称|ComMGeneral|
|描述|General configuration parameters of the Communication Manager.|
|描述|概述：ComMGeneral是AUTOSAR通信管理模块的一般配置容器，包含了影响整个通信管理模块行为的全局配置参数。|
|描述|注意：在配置ComMGeneral时，需要确保参数设置与系统的通信需求相匹配；某些参数可能会影响到网络管理策略和ECU的唤醒行为；AUTOSAR CP 4.4标准中，确保使用正确的数据类型和取值范围以避免配置错误。|
|多实例个数|1 - 1|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|ComM0PncVectorAvoidance|
|描述|This parameter avoids sending of 0-PNC-Vectors in case ComMPncGatewayEnabled is enabled.|
|描述|概述：ComM0PncVectorAvoidance 是一个配置项，用于指定是否启用部分网络请求（PNC）的向量避免机制，以减少网络请求的总线负载。|
|描述|注意：在AUTOSAR CP 4.4标准中，确保此配置项与网络管理需求相匹配；如果启用，需要仔细配置以避免不必要的网络唤醒；此配置项的使用可能会受到具体项目或硬件平台的限制。|
|多实例个数|0 - 1|
|默认值|false|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|ComMDevErrorDetect|
|描述|Switches the development error detection and notification on or off.|
|描述|概述：ComMDevErrorDetect是一个配置参数，用于启用或禁用通信管理模块（ComM）的开发错误检测功能，以便在软件开发阶段识别和报告潜在的错误。|
|描述|注意：在生产代码中通常禁用此功能以优化性能；确保在开发和测试阶段启用以捕获和修正错误；与AUTOSAR标准一致，但需注意资源消耗和性能影响。|
|说明|\* true: detection and notification is enabled. \* false: detection and notification is disabled.|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|ComMDirectUserMapping|
|描述|If this parameter is set to true the configuration tool shall automatically create a ComMUser per ComMPnc and a ComMUser per ComMChannel.|
|描述|概述：ComMDirectUserMapping 用于定义用户与通信管理模块之间的直接映射关系，确保正确的用户能够访问特定的通信服务。|
|描述|注意：在配置ComMDirectUserMapping时，必须确保用户与服务之间的映射关系符合系统的安全和权限要求；该映射应遵循AUTOSAR CP 4.4的标准，以保证兼容性和系统的稳定性；配置错误可能导致通信服务的访问权限问题或数据安全风险。|
|说明|The shortName of the generated ComMUsers shall follow the following naming convention: PNCUser_ComMPncId, e.g. PNCUser_13 ChannelUser_ComMChannelId, e.g. ChannelUser_25 Restriction: ComMUser, which are created due to this configuration parameter, shall not be used by SWCs (only available for BswM).|
|多实例个数|0 - 1|
|默认值|false|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|ComMModeLimitationEnabled|
|描述|true if mode limitation functionality shall be enabled.|
|描述|概述：ComMModeLimitationEnabled 是一个配置参数，用于启用或禁用通信管理模块（ComM）的模式限制功能，该功能允许限制ECU进入某些通信模式。|
|描述|注意：在配置此参数时，确保理解其对系统行为的影响；不正确的配置可能导致网络管理异常；此参数在AUTOSAR CP 4.4中是可选的，根据项目需求决定是否启用。|
|说明|true: Enabled false: Disabled|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|ComMPncGatewayEnabled|
|描述|Enables or disables support of Partial Network Gateway.|
|描述|概述：ComMPncGatewayEnabled配置项用于启用或禁用部分网络通信（PNC）网关功能，这是控制ECU间通信的重要机制，特别是在AUTOSAR的通信管理模块中。|
|描述|注意：在AUTOSAR CP 4.4标准中，确保在使用此配置项时已经定义了网络通信需���和PNC的配置；此配置项对于实现网络分段和优化网络带宽非常关键；不正确的配置可能导致网络通信故障或性能下降。|
|说明|False: Partial Networking Gateway is disabled True: Partial Networking Gateway is enabled|
|多实例个数|0 - 1|
|默认值|false|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|ComMPncSupport|
|描述|Enables or disables support of partial networking.|
|描述|概述：ComMPncSupport 配置项用于指定是否启用部分网络集群（Partial Network Cluster）支持，这是一个用于优化网络管理策略的功能，允许部分网络节点处于低功耗模式以节省能源。|
|描述|注意：在使用ComMPncSupport时，需要确保网络管理需求与AUTOSAR CP 4.4标准中定义的部分网络功能兼容；此外，相关的BswM配置也需要正确设置以支持PNC功能；最后，确保硬件和底层通信堆栈支持PNC特性。|
|说明|False: Partial Networking is disabled True: Partial Networking is enabled|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|ComMResetAfterForcingNoComm|
|描述|ComM shall perform a reset after entering "No Communication" mode because of an active mode limitation to "No Communication" mode.|
|描述|概述：ComMResetAfterForcingNoComm是一个配置项，用于指定通信管理模块（ComM）在强制进入No Communication状态后是否应该在下一个主周期自动重置状态。|
|描述|注意：在AUTOSAR CP 4.4标准中，需要确保此配置项与系统的通信需求相一致；如果系统需要在某些情况下保持No Communication状态，不应启用自动重置；此配置项的使用应结合诊断和网络管理需求仔细考虑。|
|说明|true: Enabled false: Disabled|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|ComMSynchronousWakeUp|
|描述|Wake up of one channel shall lead to a wake up of all channels if true.|
|描述|概述：ComMSynchronousWakeUp 配置项用于定义通信管理模块是否应在网络唤醒信号到达时立即唤醒ECU。|
|描述|注意：在AUTOSAR CP 4.4标准中，此配置项确保了网络管理的及时响应性和系统的低延迟；配置时需考虑ECU的功耗和唤醒策略；不适当的配置可能导致ECU响应延迟或过度消耗电源。|
|说明|true: Enabled false: Disabled|
|多实例个数|1 - 1|
|默认值|true|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|ComMVersionInfoApi|
|描述|Switches the possibility to read the published information with the service ComM_GetPublishedInformation().|
|描述|概述：ComMVersionInfoApi 用于启用或禁用通信管理模块的版本信息API，允许用户获取模块的版本信息。|
|描述|注意：在AUTOSAR CP 4.4中，通常建议启用此API以支持标准化的诊断和监控需求；确保在配置时正确设置此API以避免软件兼容性问题；在生产环境中，应仔细考虑是否公开版本信息，以防止潜在的安全风险。|
|说明|true: Enabled false: Disabled|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|ComMWakeupInhibitionEnabled|
|描述|true if wake up inhibition functionality enabled.|
|描述|概述：ComMWakeupInhibitionEnabled 是一个配置参数，用于启用或禁用通信管理器（ComM）中的唤醒抑制功能，该功能允许系统在特定条件下抑制唤醒信号，以减少不必要的网络活动和功耗。|
|描述|注意：在配置此参数时，需要确保它与系统的功耗和唤醒策略相匹配；如果启用唤醒抑制，必须仔细定义抑制条件以避免影响系统的响应性；在AUTOSAR CP 4.4标准中，确保使用正确的模块和接口来配置和管理唤醒抑制功能。|
|说明|true: Enabled false: Disabled|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（浮点型参数配置项）|
|---|---|
|名称|ComMPncPrepareSleepTimer|
|描述|Time in seconds the PNC state machine shall wait in COMM_PNC_PREPARE_SLEEP.|
|描述|概述：ComMPncPrepareSleepTimer配置项用于定义在部分网络控制器（PNC）进入准备睡眠状态之前需要等待的时间，以确保网络上的所有节点都有足够的时间来完成数据交换。|
|描述|注意：该配置项的值应根据网络的实际需求和性能来设置，以避免不必要的延迟或数据丢失；在设置时需考虑网络的拓扑结构和通信协议的特性；在AUTOSAR CP 4.4标准中，该配置项的单位通常是毫秒，确保与系统的时间管理策略一致。|
|多实例个数|0 - 1|
|取值范围|0 - 63|

|配置项属性|值（浮点型参数配置项）|
|---|---|
|名称|ComMTMinFullComModeDuration|
|描述|Minimum time duration in seconds, spent in the COMM_FULL_COMMUNICATION sub-state COMM_FULL_COM_NETWORK_REQUESTED.|
|描述|概述：ComMTMinFullComModeDuration 是一个配置参数，用于定义ECU在全通信模式（Full Communication Mode）下必须保持的最小时间，以确保网络上的其他节点有足够的时间来识别ECU的存在。|
|描述|注意：该参数的设置需要考虑网络的总体性能和其他节点的需求；设置过短可能导致网络管理问题，设置过长可能影响系统的响应时间；在AUTOSAR CP 4.4标准中，该配置应与网络管理需求和ECU的唤醒/睡眠行为相协调。|
|多实例个数|1 - 1|
|默认值|5|
|取值范围|0.001 - 65|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|ComMEcuGroupClassification|
|描述|Defines whether a mode inhibition affects the ECU or not.|
|描述|概述：ComMEcuGroupClassification 配置项用于定义ECU组的分类，这有助于管理ECU间的通信和确保网络上不同ECU组之间的数据交换满足特定的分类要求。|
|描述|注意：在配置ComMEcuGroupClassification时，需要确保ECU组分类与系统设计和网络管理策略一致；分类应当反映出ECU之间的通信关系和数据交换的安全级别；在AUTOSAR CP 4.4标准中，应当遵循预定义的分类枚举值，不应随意定义新的分类。|
|说明|Examples: 000: No mode inhibition can be activated 001: Wake up inhibition can be enabled|
|多实例个数|1 - 1|
|默认值|3|
|取值范围|0 - 255|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|ComMGlobalNvMBlockDescriptor|
|描述|Reference to NVRAM block containing the none volatile data. If this parameter is not configured it means that no NVRam is used at all.|
|描述|概述：ComMGlobalNvMBlockDescriptor是用于描述通信管理模块（ComM）与非易失性内存管理模块（NvM）之间数据块的关联信息，它指定了用于存储ComM相关数据的NvM块。|
|描述|注意：在配置时需确保指定的NvM块ID与实际NvM配置中的块ID一致；该配置项对于实现ComM模块的NvM数据持久化至关重要；在多个ComM通道共享同一NvM块时，需要特别注意数据的读写冲突和同步问题。|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/NvM/NvMBlockDescriptor|
