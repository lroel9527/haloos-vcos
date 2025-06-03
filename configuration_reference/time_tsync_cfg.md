# time_tsync 配置项参考文档

|容器属性|值（容器）|
|---|---|
|名称|CanTSyn|
|描述|Configuration of the Synchronized Time-base Manager (StbM) module with respect to global time handling on CAN.|
|描述|概述：CanTSyn是用于在CAN网络上同步时间的模块，它实现了基于时间的通信和控制，以确保网络中的设备时间同步。|
|描述|注意：CanTSyn模块的配置需要与网络上其他节点的时间同步机制兼容；确保时间精度和同步周期满足系统要求；在配置时需注意与CAN驱动和操作系统的接口兼容性。|
|多实例个数|0 - 1|

## 1. CanTSynGeneral

|容器属性|值（容器）|
|---|---|
|名称|CanTSynGeneral|
|描述|This container holds the general parameters of the CAN-specific Synchronized Time-base Manager|
|描述|概述：CanTSynGeneral 用于定义时间同步(Time Synchronization)模块的一般属性，例如是否启用时间同步或者时间同步的方法。|
|描述|注意：在配置CanTSynGeneral时，需要确保选择的时间同步方法与网络的实际能力相匹配；如果网络不支持某种同步方法，配置应避免使用该方法；此外，时间同步的精度和资源消耗之间可能存在权衡，需要根据系统需求进行适当配置。|
|多实例个数|1 - 1|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|CanTSynDevErrorDetect|
|描述|Switches the development error detection and notification on or off.|
|描述|概述：CanTSynDevErrorDetect 是一个配置参数，用于启用或禁用 CAN 时间同步模块的开发错误检测功能。|
|描述|注意：开启此功能可以帮助开发者在开发阶段识别配置错误或运行时错误；错误检测功能可能会增加系统的资源消耗；在生产环境中，通常建议关闭开发错误检测以优化性能。|
|说明|\* true: detection and notification is enabled. \* false: detection and notification is disabled.|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|CanTSynVersionInfoApi|
|描述|Activate/Deactivate the version information API (CanTSyn_GetVersionInfo). True: version information API activated False: version information API deactivated.|
|描述|概述：CanTSynVersionInfoApi 用于启用或禁用 CAN 时间同步模块的版本信息API，允许用户获取模块的版本信息。|
|描述|注意：通常建议启用版本信息API以支持标准化的诊断和监控需求；如果内存或数据带宽非常受限，可能需要禁用此功能；确保在项目的需求分析阶段决定此API的启用状态。|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（浮点型参数配置项）|
|---|---|
|名称|CanTSynMainFunctionPeriod|
|描述|Schedule period of the main function cantsyn_mainfunction. Unit: [s].|
|描述|概述：CanTSynMainFunctionPeriod 配置项定义了时间同步主函数（cantsyn_mainfunction）被调用的周期，通常以时间单位毫秒（ms）表示。|
|描述|注意：该配置项的值应当与ECU的时间同步需求相匹配，确保时间同步精度；配置的周期值必须考虑到ECU的处理能力和CAN网络的负载情况；该配置项应当与系统定时器和OS任务配置保持一致，以避免时间同步功能的不准确。|
|多实例个数|1 - 1|
|取值范围|0 - Inf|

## 2. CanTSynGlobalTimeDomain

|容器属性|值（容器）|
|---|---|
|名称|CanTSynGlobalTimeDomain|
|描述|This represents the existence of a global time domain on CAN. The CanTSyn module can administrate several global time domains at the same time that in itself form a hierarchy of domains and sub-domains.|
|描述|概述：CanTSynGlobalTimeDomain 配置项用于定义CAN时间同步模块中全局时间域的属性，这是用于时间同步和时间戳的功能。|
|描述|注意：在配置CanTSynGlobalTimeDomain时，需要确保其值与系统中使用的时间域一致；此外，该配置项应与网络上其他节点的时间同步设置保持一致，以确保系统时间同步的准确性；应检查该配置项是否符合相关的模块和时间同步策略的要求。|
|说明|If the CanTSyn exists it is assumed that at least one global time domain exists.|
|多实例个数|1 - 1|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CanTSynGlobalTimeDomainId|
|描述|The global time domain ID.|
|描述|概述：CanTSynGlobalTimeDomainId 是用于标识CAN网络上时间同步的全局时间域ID，它允许不同的网络参与者在相同的时间基础上进行通信和同步。|
|描述|注意：在配置CanTSyn模块时，需要确保GlobalTimeDomainId的唯一性，以避免时间同步冲突；该ID应与网络中其他时间同步协议使用的时间域ID区分开来；在实施时间同步时，应考虑网络的延迟和精度要求。|
|多实例个数|1 - 1|
|取值范围|0 - 31|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|CanTSynSynchronizedTimeBaseRef|
|描述|Mandatory reference to the required synchronized time-base.|
|描述|概述：CanTSynSynchronizedTimeBaseRef 配置项用于引用同步的时间基准，它定义了CAN时间同步模块（CanTSyn）所依赖的时间基准源。|
|描述|注意：在配置CanTSyn模块时，需要确保引用的时间基准是系统中已定义的且有效的时间源；此外，时间基准的选择应支持所需的时间同步精度和性能要求；在多时间基准的系统中，还需注意时间基准之间的关系和同步策略。|
|多实例个数|1 - 1|

### 2.1. CanTSynGlobalTimeFupDataIDList

|容器属性|值（容器）|
|---|---|
|名称|CanTSynGlobalTimeFupDataIDList|
|描述|The DataIDList for FUP messages ensures the identification of data elements due to CRC calculation and message authentication process.|
|描述|概述：CanTSynGlobalTimeFupDataIDList 配置项定义了用于时间同步的CAN帧的Follow-Up数据标识符列表，这些标识符用于区分不同来源的时间信息。|
|描述|注意：在配置CanTSynGlobalTimeFupDataIDList时，需要确保列表中的数据标识符与网络上的时间同步协议一致；标识符的唯一性必须得到保证，以避免时间信息的混淆；此配置项应与实际使用的时间同步硬件和协议相匹配，以确保系统的时间同步准确性。|
|多实例个数|0 - 1|

#### 2.1.1. CanTSynGlobalTimeFupDataIDListElement

|容器属性|值（容器）|
|---|---|
|名称|CanTSynGlobalTimeFupDataIDListElement|
|描述|Element of the DataIDList for FUP messages ensures the identification of data elements due to CRC calculation and message authentication process.|
|描述|概述：CanTSynGlobalTimeFupDataIDListElement 配置项用于定义在CAN时间同步帧（Follow-Up信息）中使用的数据标识符（Data ID）列表元素，这些元素用于标识和验证同步消息。|
|描述|注意：在配置CanTSyn模块时，需要确保Data ID的唯一性和正确性，以便正确地识别和处理时间同步消息；Data ID列表应与网络上其他节点协商一致，以保证系统间的时间同步。|
|多实例个数|16 - 16|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CanTSynGlobalTimeFupDataIDListIndex|
|描述|Index of the DataIDList for FUP messages ensures the identification of data elements due to CRC calculation and message authentication process.|
|描述|概述：CanTSynGlobalTimeFupDataIDListIndex用于指定在CAN网络上发送的Follow-Up消息中全局时间同步的数据标识符（Data ID）列表的索引。|
|描述|注意：该配置项的值必须对应于实际定义的Data ID列表中的一个有效索引；在配置时需确保所选Data ID与网络上其他节点的时间同步需求兼容；不正确的配置可能导致时间同步功能失效。|
|多实例个数|1 - 1|
|取值范围|0 - 15|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CanTSynGlobalTimeFupDataIDListValue|
|描述|Value of the DataIDList for FUP messages ensures the identification of data elements due to CRC calculation and message authentication process.|
|描述|概述：CanTSynGlobalTimeFupDataIDListValue配置项用于定义在CAN网络上同步全局时间时，Follow_Up消息中使用的数据标识符（ID）列表。|
|描述|注意：该配置项的值必须与网络上其他节点使用的值保持一致，以确保时间同步的正确性；在配置此项时，应考虑网络的带宽和数据传输效率，避免因数据ID数量过多而影响网络性能。|
|多实例个数|1 - 1|
|取值范围|0 - 255|

### 2.2. CanTSynGlobalTimeMaster

|容器属性|值（容器）|
|---|---|
|名称|CanTSynGlobalTimeMaster|
|描述|Configuration of the global time master. Each global time domain is required to have exactly one global time master. This master may or may not exist on the configured ECU.|
|描述|概述：CanTSynGlobalTimeMaster 配置项用于定义CAN时间同步（CAN Time Synchronization, CanTSyn）模块中的全局时间主控（Global Time Master）角色，该角色负责在网络中广播时间信息以实现网络内的时间同步。|
|描述|注意：在配置CanTSyn模块时，必须确保网络中只有一个节点被配置为Global Time Master；如果网络中存在多个时间主控，可能会导致时间同步冲突；在选择Global Time Master时，应考虑节点的可靠性和通信能力，以确保稳定的时间同步。|
|多实例个数|0 - 16|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|CanTSynImmediateTimeSync|
|描述|Enables/Disables the cyclic polling of stbm_get_time_base_update_counter() within cantsyn_mainfunction().|
|描述|概述：CanTSynImmediateTimeSync配置项用于定义是否在接收到时间同步帧后立即进行时间同步，而不是等待下一个周期性时间同步事件。|
|描述|注意：在配置此项时，需要考虑系统的实时性要求和网络负载情况；过于频繁的时间同步可能会增加网络负载，影响系统性能；此配置项在高精度时间同步需求场景下特别有用。|
|多实例个数|1 - 1|
|默认值|true|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|CanTSynGlobalTimeTxCrcSecured|
|描述|This represents the configuration of whether or not CRC is supported.|
|描述|概述：CanTSynGlobalTimeTxCrcSecured 配置项用于定义CAN时间同步消息在发送时是否使用CRC校验来保证消息的安全性。|
|描述|注意：在配置CanTSynGlobalTimeTxCrcSecured时，需要确保网络中的所有节点都支持相应的CRC校验机制；如果启用CRC校验，必须在所有相关节点上正确配置CRC参数以确保系统的一致性；需要检查该配置项是否与标准中定义的安全传输机制兼容。|
|多实例个数|1 - 1|
|默认值|CRC_SUPPORTED|

|配置项属性|值（浮点型参数配置项）|
|---|---|
|名称|CanTSynCyclicMsgResumeTime|
|描述|Defines the time where the 1st regular cycle time based message transmission takes place, after an immediate transmission before. Unit: seconds|
|描述|概述：CanTSynCyclicMsgResumeTime 配置项用于定义时间同步协议（Time Synchronization, TSync）中周期性消息的恢复时间，即在通信中断后，多长时间后恢复发送周期性的时间同步消息。|
|描述|注意：该参数的设置需要考虑网络的通信特性和时间同步的精度要求；值过小可能导致网络拥塞，值过大可能影响时间同步的准确性；需与其他网络参与者的时间同步机制保持一致，以确保系统时间同步的有效性。|
|多实例个数|1 - 1|
|默认值|0.01|
|取值范围|0 - Inf|

|配置项属性|值（浮点型参数配置项）|
|---|---|
|名称|CanTSynGlobalTimeDebounceTime|
|描述|This represents the configuration of a TX debounce time for SYNC, FUP, OFS and OFNS messages compared to a message before with the same PDU. Unit: seconds|
|描述|概述：CanTSynGlobalTimeDebounceTime配置项用于定义SYNC、FUP、OFS、OFNS报文发送的去抖时间，若设置为0则表示Debounce功能关闭。|
|描述|注意：该配置项的值应根据网络延迟和系统时间同步精度需求谨慎设置；设置过小可能导致时间同步不稳定，过大则可能影响系统对时间的快速响应；需要确保该配置项与网络性能和时间同步需求相匹配。|
|多实例个数|1 - 1|
|默认值|0.01|
|取值范围|0 - Inf|

|配置项属性|值（浮点型参数配置项）|
|---|---|
|名称|CanTSynGlobalTimeTxPeriod|
|描述|This represents configuration of the TX period. Unit: seconds|
|描述|概述：CanTSynGlobalTimeTxPeriod 配置项用于定义CAN时间同步模块（CanTSyn）发送全局时间广播消息的周期，即全局时间消息在CAN网络上的发送频率。|
|描述|注意：该值应根据网络同步需求和带宽限制来配置；过高的发送频率可能导致网络拥塞，而过低的频率可能影响系统时间同步精度；需确保该配置与网络上其他节点的时间同步机制兼容。|
|多实例个数|1 - 1|
|默认值|0.5|
|取值范围|0 - Inf|

|配置项属性|值（浮点型参数配置项）|
|---|---|
|名称|CanTSynMasterConfirmationTimeout|
|描述|This represents the confirmation timeout after transmission of each Timesync message.|
|描述|概述：CanTSynMasterConfirmationTimeout 配置项用于定义时间同步主节点在发送同步消息后等待确认消息的最大时间。|
|描述|注意：该值应当根据网络延迟和系统的时间同步精度要求来设定；过小的超时时间可能导致不必要的同步失败，而过大的超时时间可能会影响系统的同步性能；在配置时需要考虑到网络的实际状况和其他节点的处理能力。|
|说明|Unit: seconds.|
|多实例个数|1 - 1|
|默认值|1|
|取值范围|0 - Inf|

#### 2.2.1. CanTSynGlobalTimeMasterPdu

|容器属性|值（容器）|
|---|---|
|名称|CanTSynGlobalTimeMasterPdu|
|描述|This container encloses the configuration of the PDU that is supposed to contain the global time information.|
|描述|概述：CanTSynGlobalTimeMasterPdu配置项用于定义通过CAN网络同步的全局时间的主时间协议数据单元（PDU），它指定了用于时间同步的PDU的属性和参数。|
|描述|注意：在配置CanTSynGlobalTimeMasterPdu时，需要确保PDU的ID、长度和格式符合网络的要求和标准；此配置项对于实现基于时间的通信和同步非常关键，应仔细设计以避免时间同步问题。|
|多实例个数|1 - 1|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CanTSynGlobalTimeMasterConfirmationHandleId|
|描述|This represents the handle ID of the PDU that contains the global time information.|
|描述|概述：CanTSynGlobalTimeMasterConfirmationHandleId是用于标识全局时间同步主确认消息的句柄ID，它关联到CAN通信中用于时间同步的特定消息。|
|描述|注意：该配置项需要确保与CAN通信中实际用于时间同步的消息ID一致；在配置时需注意不同网络上时间同步消息的ID可能会有所不同；此配置项在实现全局时间同步功能时至关重要，错误的配置可能导致时间同步功能失效。|
|多实例个数|1 - 1|
|默认值|0|
|取值范围|0 - 65535|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|CanTSynGlobalTimePduRef|
|描述|This represents the reference to the Pdu taken to transmit the global time information. The global time master of a global time domain acts as the sender of the Pdu while all the time slaves are supposed to receive the Pdu.|
|多实例个数|1 - 1|

### 2.3. CanTSynGlobalTimeSlave

|容器属性|值（容器）|
|---|---|
|名称|CanTSynGlobalTimeSlave|
|描述|Configuration of a global time slave. Each global time domain is required to have at least one time slave. The configured ECU may or may not represent a time slave.|
|描述|概述：CanTSynGlobalTimeSlave 配置项用于定义CAN网络中的时间同步从设备的行为和属性，确保网络中的时间同步精度和一致性。|
|描述|注意：确保网络中只有一个主时间同步设备和多个从设备；从设备的时间同步配置应与主设备兼容；在配置时需考虑网络延迟和设备时钟精度。|
|多实例个数|0 - 16|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|CanTSynRxCrcValidated|
|描述|Definition of whether or not validation of the CRC is supported.|
|描述|概述：CanTSynRxCrcValidated配置项用于指定是否对接收到的时间同步帧（Time Sync Frame）的CRC进行验证，以确保数据的完整性和准确性。|
|描述|注意：在启用CRC验证时，需要确保发送方和接收方的CRC算法和参数一致；关闭CRC验证可能会增加数据错误或篡改的风险。|
|多实例个数|1 - 1|
|默认值|CRC_VALIDATED|

|配置项属性|值（浮点型参数配置项）|
|---|---|
|名称|CanTSynGlobalTimeFollowUpTimeout|
|描述|Rx timeout for the follow-up message. This is only relevant for selected bus systems Unit:seconds|
|描述|概述：CanTSynGlobalTimeFollowUpTimeout 配置项定义了在CAN网络上，Follow Up 消息的超时时间，这是为了确保网络参与者在规定时间内接收到时间同步信息。|
|描述|注意：该配置项的值应当根据网络的具体延迟和性能要求来设定；超时时间设置过短可能导致同步失败，设置过长可能影响系统的实时性。|
|多实例个数|1 - 1|
|取值范围|0 - Inf|

|配置项属性|值（浮点型参数配置项）|
|---|---|
|名称|CanTSynGlobalTimeMinMsgGap|
|描述|This parameter represents the configuration of a minimum message gap time for received Timesync messages compared to a message before with the same PDU. If PDUs are received more often in between than this parameter allows, they shall be ignored.|
|描述|Tags: atp.Status=draft|
|描述|概述：CanTSynGlobalTimeMinMsgGap 配置项用于定义在CAN网络上发送全局时间同步消息的最小时间间隔，以确保网络上的时间同步消息不会因为过于频繁的发送而导致网络拥堵。|
|描述|注意：该配置项的值需要根据网络的带宽和CAN控制器的性能来合理设置，以避免对网络造成不必要的负担；在设置时还需考虑到网络上其他节点的时间同步需求，确保所有节点能够有效地进行时间同步。|
|说明|Unit: seconds|
|多实例个数|1 - 1|
|默认值|0|
|取值范围|0 - Inf|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CanTSynGlobalTimeSequenceCounterJumpWidth|
|描述|The SequenceCounterJumpWidth specifies the maximum allowed gap of the Sequence Counter between two SYNC resp. two OFS messages.|
|描述|概述：CanTSynGlobalTimeSequenceCounterJumpWidth 配置项定义了在CAN网络上同步全局时间时，全局时间序列计数器（Global Time Sequence Counter）允许的最大跳变宽度。|
|描述|注意：该参数用于检测时间同步协议中的潜在错误，确保时间同步的准确性；配置值应根据网络的具体条件和时间同步的精度要求来设定；超出此跳变宽度的序列计数器值变化将被视为异常，可能会触发错误处理机制。|
|多实例个数|1 - 1|
|取值范围|1 - 15|

#### 2.3.1. CanTSynGlobalTimeSlavePdu

|容器属性|值（容器）|
|---|---|
|名称|CanTSynGlobalTimeSlavePdu|
|描述|This container encloses the configuration of the PDU that is supposed to contain the global time information.|
|描述|概述：CanTSynGlobalTimeSlavePdu配置项用于定义在CAN网络上用于时间同步的从节点的PDU（协议数据单元），它包含了必要的参数来接收和识别全局时间广播。|
|描述|注意：在配置CanTSynGlobalTimeSlavePdu时，需要确保PDU的ID和其他参数与网络上的时间同步主节点广播的PDU相匹配；此外，要注意PDU的大小和格式应符合CAN帧结构和时间同步协议要求；在多节点系统中，还需确保每个从节点的CanTSynGlobalTimeSlavePdu配置不会相互冲突。|
|多实例个数|1 - 1|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CanTSynGlobalTimeSlaveHandleId|
|描述|This represents the handle ID of the PDU that contains the global time information.|
|描述|概述：CanTSynGlobalTimeSlaveHandleId 是用于标识CAN时间同步模块中全局时间同步从站的句柄ID，它允许系统中的其他模块引用和访问该从站。|
|描述|注意：在配置CanTSyn模块时，必须确保CanTSynGlobalTimeSlaveHandleId的值在系统中是唯一的；该ID通常由系统集成者分配，以确保与其他模块的兼容性。|
|多实例个数|1 - 1|
|默认值|0|
|取值范围|0 - 65535|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|CanTSynGlobalTimePduRef|
|描述|This represents the reference to the Pdu taken to transmit the global time information. The global time master of a global time domain acts as the sender of the Pdu while all the time slaves are supposed to receive the Pdu.|
|描述|概述：CanTSynGlobalTimePduRef 是一个配置参数，用于引用在CAN时间同步模块中用于时间同步的全局时间PDU（协议数据单元）。|
|描述|注意：在配置CanTSyn模块时，需要确保引用的PDU已经在PDU Router或者相应的CAN IFrame配置中定义；此外，确保时间同步的PDU与其他PDU不会发生ID冲突；在多个网络通信中，还需注意时间同步消息的一致性和准确性。|
|多实例个数|1 - 1|

### 2.4. CanTSynGlobalTimeSyncDataIDList

|容器属性|值（容器）|
|---|---|
|名称|CanTSynGlobalTimeSyncDataIDList|
|描述|The DataIDList for SYNC messages ensures the identification of data elements due to CRC calculation and message authentication process.|
|描述|概述：CanTSynGlobalTimeSyncDataIDList配置项用于定义在CAN网络上用于时间同步的消息的标识符列表，这些标识符用于识别发送或接收的时间同步消息。|
|描述|注意：在配置此项时，必须确保所有列出的标识符符合CAN网络的ID分配规则；此配置项对于实现网络上的精确时间同步至关重要，因此需要仔细规划和验证。|
|多实例个数|0 - 1|

#### 2.4.1. CanTSynGlobalTimeSyncDataIDListElement

|容器属性|值（容器）|
|---|---|
|名称|CanTSynGlobalTimeSyncDataIDListElement|
|描述|Element of the DataIDList for SYNC messages ensures the identification of data elements due to CRC calculation and message authentication process.|
|描述|概述：CanTSynGlobalTimeSyncDataIDListElement配置项用于定义在CAN网络上同步全局时间所使用的数据标识符（Data ID）列表元素，这是时间同步协议的一部分，确保网络中的所有节点可以基于相同的时间基准进行通信。|
|描述|注意：在配置此项时，必须确保所选Data ID不与网络上其他消息的标识符冲突；此配置项对于实现基于时间的操作和功能至关重要，需要仔细选择和配置。|
|多实例个数|16 - 16|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CanTSynGlobalTimeSyncDataIDListIndex|
|描述|Index for the DataIDList for SYNC messages ensures the identification of data elements due to CRC calculation and message authentication process.|
|描述|概述：CanTSynGlobalTimeSyncDataIDListIndex用于指定全局时间同步数据标识符列表中的索引，这有助于在CAN网络上同步不同节点的时间。|
|描述|注意：在配置时需确保索引值与实际的数据标识符列表相匹配；索引值的范围和有效性需要根据项目具体要求和网络设计来确定。|
|多实例个数|1 - 1|
|取值范围|0 - 15|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CanTSynGlobalTimeSyncDataIDListValue|
|描述|Value of the DataIDList for SYNC messages ensures the identification of data elements due to CRC calculation and message authentication process.|
|描述|概述：CanTSynGlobalTimeSyncDataIDListValue 是用于定义CAN时间同步（CanTSyn）模块中全局时间同步数据标识符（DataID）列表的值，这些值用于区分不同的时间同步消息。|
|描述|注意：在配置CanTSyn模块时，需要确保DataID的值是唯一的，以避免时间同步消息之间的冲突；DataID列表的值应当符合网络上其他节点的期望和配置，以确保系统间同步的一致性；在配置DataID时，还应考虑到CAN网络的负载和消息优先级，以免影响时间同步的准确性和效率。|
|多实例个数|1 - 1|
|取值范围|0 - 255|
