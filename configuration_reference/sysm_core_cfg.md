# BswM 配置项参考文档

|容器属性|值（容器）|
|---|---|
|名称|BswM|
|描述|Configuration of the BswM (Basic SW Mode Manager) module.|
|描述|概述：BswM (Bsw Mode Manager) 是负责管理基础软件模块（Bsw）模式之间切换的组件，它根据来自应用层或其他Bsw模块的模式请求，控制Bsw模块间的模式切换。|
|描述|注意：在配置BswM时，需要确保所有模式请求的来源和目标模式都被正确定义；BswM的配置应遵循AUTOSAR CP 4.4标准中对模式管理逻辑的要求；在多模式复杂系统中，设计BswM逻辑时要特别注意避免模式切换的死锁情况。|
|多实例个数|0 - 1|

## 1. BswMConfig

|容器属性|值（容器）|
|---|---|
|名称|BswMConfig|
|描述|This container contains the configuration parameters and sub containers of the AUTOSAR BswM module. This container exists once per partition.|
|描述|概述：BswMConfig 是用于定义基本软件模块管理（BswM）的配置参数，它包括模块的功能和行为配置，如模式管理、规则和动作列表等。|
|描述|注意：在配置BswMConfig时，必须确保所有的模式请求、规则和动作都已经正确定义并且相互匹配；BswMConfig的配置应该与系统的功能需求和依赖关系保持一致；在AUTOSAR CP 4.4标准中，BswM的配置可能需要与新的功能和改进的标准兼容。|
|多实例个数|1 - inf|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|BswMPartitionRef|
|描述|This references the partition the BswM shall run inside.|
|描述|概述：BswMPartitionRef是一个配置项，用于指定基本软件模块（BswM）的分区引用，确保模块能够在指定的内存分区中运行。|
|描述|注意：在配置BswMPartitionRef时，需要确保引用的分区符合AUTOSAR的内存分区规范；分区配置应与ECU的内存管理策略相匹配；在多核或多分区系统中，应注意不同分区间的数据共享和同步机制。|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/EcuC/EcucPartitionCollection/EcucPartition|

### 1.1. BswMRteModeDclGroup

|容器属性|值（容器）|
|---|---|
|名称|BswMRteModeDclGroup|
|描述|This container describes a ModeDeclarationGroup which is created by the BswM.|
|描述|概述：BswMRteModeDclGroup是用于声明BSW模块模式的一组配置，它允许定义模块在不同操作模式下的行为。|
|描述|注意：在定义BswMRteModeDclGroup时，需要确保模式声明与BSW模块的实际行为一致；每个BSW模块应有其对应的模式声明，以便于系统管理和模式切换；AUTOSAR CP 4.4标准要求模式管理机制明确，因此在配置时应注意满足标准的要求。|
|说明|The following elements are created in the BswM_swc.arxml: - ModeDeclarationGroup with the name of this container. - ModeSwitchInterface which uses the ModeDeclarationGroup as its ModeDeclarationGroupPrototpye - ImplementationType with a CompuMethod which contains all Modes of the ModeDeclarationGroup - DataTypeMappingSet which maps the Mode Declaration Group to the ImplementationType|
|多实例个数|0 - inf|
|POST-BUILD-CHANGEABLE|false|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|BswMInitMode|
|描述|Reference to a Mode of this ModeDeclarationGroup. Target is used as InitalMode of the ModeDeclarationGroup.|
|描述|概述：BswMInitMode配置项定义了基本软件模块管理（BswM）的初始化模式，这是BswM模块在系统启动时的行为配置，用于控制BswM如何初始化其管理的资源和模块。|
|描述|注意：在配置BswMInitMode时，需要确保它与系统的启动策略和依赖模块的初始化顺序相匹配；此外，BswMInitMode的配置应该遵循AUTOSAR CP 4.4标准中对于模块初始化模式的规定；在多模式系统中，还需要考虑模式切换对初始化模式的影响。|
|多实例个数|1 - 1|
|IMPLEMENTATION-CONFIG-CLASSES|   |
|目标引用项的路径|/AUTOSAR/EcucDefs/BswM/BswMConfig/BswMRteModeDclGroup/BswMRteMode|

#### 1.1.1. BswMRteMode

|容器属性|值（容器）|
|---|---|
|名称|BswMRteMode|
|描述|This container describes a Mode of a ModeDeclarationGroup.|
|描述|概述：BswMRteMode配置项定义了基本软件模块（BswM）与运行时环境（RTE）之间的模式切换逻辑，用于控制和管理软件组件的行为模式。|
|描述|注意：在配置BswMRteMode时，需要确保模式之间的转换逻辑清晰且无歧义；模式切换应考虑系统的实时性和安全性要求；AUTOSAR CP 4.4标准中对模式管理有详细规范，需遵循相关规则以保证兼容性。|
|说明|The name of the container represents the name of the corresponding Mode.|
|多实例个数|1 - inf|
|POST-BUILD-CHANGEABLE|false|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|BswMModePhysicalValue|
|描述|Describes the physical value of the Mode. Value is used in the CompuMehod of the ImplemenationType.|
|描述|概述：BswMModePhysicalValue 用于定义基础软件模块管理（BswM）中的模式控制值，这些值与物理设备状态或操作模式直接相关。|
|描述|注意：确保BswMModePhysicalValue与实际物理设备或操作模式的状态匹配；在配置时考虑系统的安全和性能需求；在AUTOSAR CP 4.4中，应确保这些值的更新和管理遵循标准的模式管理策略。|
|多实例个数|1 - 1|
|IMPLEMENTATION-CONFIG-CLASSES| |
|取值范围|0 - 255|

### 1.2. BswMArbitration

|容器属性|值（容器）|
|---|---|
|名称|BswMArbitration|
|描述|This container includes all configuration sub-containers and parameters related to the mode arbitration functionality of the BswM.|
|描述|概述：BswMArbitration配置项用于定义基本软件模块（BswM）的仲裁逻辑，这涉及到模块间的优先级和控制决策，以确保系统中不同模块的协调运行。|
|描述|注意：在配置BswMArbitration时，必须确保所有参与仲裁的模块的优先级和决策逻辑正确定义，以避免潜在的资源冲突或死锁；此外，仲裁逻辑应当与系统的实时性和安全性要求相匹配；在AUTOSAR CP 4.4标准中，应当遵循相关规范来配置仲裁逻辑，以确保与标准的兼容性。|
|多实例个数|1 - 1|

#### 1.2.1. BswMEventRequestPort

|容器属性|值（容器）|
|---|---|
|名称|BswMEventRequestPort|
|描述|Each instance of this container defines an event which can be sent to the BswM. Basic Software Modules may send these events to the BswM by calling the corresponding BswM C-API (for example: BswM_ComM_InitiateReset()).|
|描述|概述：BswMEventRequestPort 配置项用于定义基础软件模块管理（BswM）组件中的事件请求端口，这些端口用于接收来自其他软件组件的事件通知。|
|描述|注意：在配置BswMEventRequestPort时，需要确保端口的标识符与系统中其他端口的标识符不冲突；端口的类型和数据元素需要与发送事件的组件匹配；在AUTOSAR CP 4.4标准中，BswM的配置应遵循模块的定义和规范，确保端口配置的正确性和一致性。|
|多实例个数|0 - inf|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|BswMEventRequestProcessing|
|描述|This parameter defines if the processing of the mode arbitration shall be done immediately when an event request is received or if it shall be deferred to the processing of the main function of BswM.|
|描述|概述：BswMEventRequestProcessing配置项用于定义基本软件模块管理（BswM）如何处理来自各种软件组件的事件请求，包括事件的触发方式和处理优先级。|
|描述|注意：在配置BswMEventRequestProcessing时，需要确保事件处理策略与系统的实时性和安全性要求相符；此外，应注意不同事件可能需要不同的处理策略，例如立即处理或延迟处理；最后，配置时应遵循AUTOSAR CP 4.4标准中对事件请求处理的相关规定，以保证配置的一致性和系统的可靠性。|
|多实例个数|1 - 1|
|默认值|BSWM_DEFERRED|

##### 1.2.1.1. BswMEventRequestSource

|容器属性|值（容器）|
|---|---|
|名称|BswMEventRequestSource|
|描述|This choice container specifies the source of the event request. The sender of the event can be another BSW Module, such as ComM.|
|描述|概述：BswMEventRequestSource配置项用于定义基础软件模块管理（BswM）中的事件请求源，这些请求源触发BswM对特定模式的切换或行为的执行。|
|描述|注意：在配置BswMEventRequestSource时，必须确保每个事件请求源的标识符在整个系统中是唯一的；配置的事件请求源应与实际系统中的事件产生机制相匹配，以确保正确的模式切换；在AUTOSAR CP 4.4标准中，对事件请求源的处理和配置方法可能有特定的要求和限制，需要仔细遵守相关规范。|
|多实例个数|1 - 1|

###### 1.2.1.1.1. BswMComMInitiateReset

|容器属性|值（容器）|
|---|---|
|名称|BswMComMInitiateReset|
|描述|This is an indication from the ComM to signal a shutdown.|
|描述|概述：BswMComMInitiateReset配置项用于定义基础软件模块管理（BswM）如何处理来自通信管理模块（ComM）的重置请求，确保系统能够根据需要安全地重启或进入特定的重置状态。|
|描述|注意：在配置BswMComMInitiateReset时，需要确保重置策略与系统的安全需求相匹配；此配置项在AUTOSAR CP 4.4中可能需要与ECU的重置管理功能紧密集成，确保兼容性；设计时应考虑重置请求的来源和条件，以避免意外触发重置。|
|多实例个数|0 - 1|

###### 1.2.1.1.2. BswMDcmApplicationUpdatedIndication

|容器属性|值（容器）|
|---|---|
|名称|BswMDcmApplicationUpdatedIndication|
|描述|This is a request to update application data from the DCM. This container does not contain any parameters since there are no further configuration needed for this type of request.|
|描述|概述：BswMDcmApplicationUpdatedIndication是一个配置项，用于指示基础软件模块（BswM）当诊断通信管理器（Dcm）完成了ECU固件更新后，应当执行的动作或状态变更。|
|描述|注意：在配置此项时，需要确保Dcm模块与BswM模块之间的接口和数据交互正确定义，以便在固件更新后能够正确地通知BswM；此配置项通常与ECU固件更新流程紧密相关，因此需要根据具体的应用场景和项目需求进行配置；在AUTOSAR CP 4.4标准中，应当遵循相应的模块交互规范和数据定义，以确保系统的兼容性和稳定性。|
|多实例个数|0 - 1|

###### 1.2.1.1.3. BswMModeSwitchErrorEvent

|容器属性|值（容器）|
|---|---|
|名称|BswMModeSwitchErrorEvent|
|描述|This is a notification that an error occurred because the partition containing mode users of the referenced PPort was restarted by the RTE. Because the Mode Machine Instance holding the current mode can reside on that terminated partition, the Mode Manager has to be informed about|
|描述|概述：BswMModeSwitchErrorEvent 用于定义基础软件模块管理（BswM）中的模式切换错误事件，这些事件通常用于处理模式切换过程中发生的错误或异常。|
|描述|注意：确保正确配置错误处理逻辑以增强系统的健壮性；在设计模式切换策略时，应详细定义可能的错误类型和相应的恢复策略；此配置项应与系统的诊断策略紧密结合，以便于错误追踪和系统恢复。|
|说明|the loss of this partition.|
|多实例个数|0 - 1|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|BswMRteSwitchPortRef|
|描述|This is a reference to the BswMSwitchPort.|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/BswM/BswMConfig/BswMModeControl/BswMSwitchPort|

###### 1.2.1.1.4. BswMNmCarWakeUpIndication

|容器属性|值（容器）|
|---|---|
|名称|BswMNmCarWakeUpIndication|
|描述|This is an indication of a CarWakeup from the Nm.|
|描述|概述：BswMNmCarWakeUpIndication是一个配置项，用于指示网络管理（Nm）模块接收到车辆唤醒指示时应采取的行动，这通常涉及到网络的状态转换或特定动作的执行。|
|描述|注意：在配置时需确保与车辆的唤醒逻辑兼容；该配置项的行为应与系统的低功耗和唤醒策略紧密结合；AUTOSAR CP 4.4标准中未明确定义此配置项，具体实现可能依赖于供应商或项目具体要求。|
|多实例个数|0 - 1|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|BswMNmChannelRef|
|描述|This is a reference to the channel handle that the indication corresponds to.|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/ComM/ComMConfigSet/ComMChannel|

###### 1.2.1.1.5. BswMPartitionRestarted

|容器属性|值（容器）|
|---|---|
|名称|BswMPartitionRestarted|
|描述|This is a notification that an error occured because the partition containing the BswM was restarted by the RTE. The Mode Users may lie in another (still running) partition. So the BswM has to be informed that the start of its partition is no normal startup but a restart of a single partition. This information can be used inside the Rules. This notification has to be used by the Restart Task of the particular partition.|
|描述|概述：BswMPartitionRestarted 配置项用于指示基础软件模块分区（BswM Partition）在系统复位后是否被重新启动。|
|描述|注意：在AUTOSAR CP 4.4标准中，需要确保系统设计能够适应分区重启的情况；此配置项的使用应与系统复位策略和安全要求相一致；在配置时，应考虑分区重启对系统状态和通信的影响。|
|多实例个数|0 - 1|

###### 1.2.1.1.6. BswMWdgMRequestPartitionReset

|容器属性|值（容器）|
|---|---|
|名称|BswMWdgMRequestPartitionReset|
|描述|This is a Partition Reset request from from the WdgM. This port|
|描述|概述：BswMWdgMRequestPartitionReset 配置项用于定义基础软件模块监控看门狗（WdgM）请求分区重置的属性，这是为了确保系统在检测到严重错误时能够安全地恢复。|
|描述|注意：在AUTOSAR CP 4.4标准中，确保分区重置请求与系统分区管理策略一致；分区重置请求应当仅在检测到无法恢复的错误时发起；配置时需考虑与其他安全机制的协同，如Error Handling和Supervision。|
|说明|corresponds to a call of the BswM_WdgM_RequestPartitionReset API.|
|多实例个数|0 - 1|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|BswMWdgMRequestPartitionResetRef|
|描述|This is a reference to the partition that shall be reset.|
|描述|概述：BswMWdgMRequestPartitionResetRef 配置项用于定义基本软件模块监控看门狗管理器（WdgM）请求分区重置的引用，这允许WdgM在检测到错误时重置特定的软件分区。|
|描述|注意：在配置时需确保引用的分区是可重置的，并且分区重置的策略与系统的安全要求相符；此配置项应与系统分区管理策略和错误处理策略紧密结合；在AUTOSAR CP 4.4标准中，确保该配置项的使用与标准规定的模块间接口和行为一致。|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/EcuC/EcucPartitionCollection/EcucPartition|

#### 1.2.2. BswMLogicalExpression

|容器属性|值（容器）|
|---|---|
|名称|BswMLogicalExpression|
|描述|This container describes the logical expressions that can be used for the mode arbitration. The logical expressions are built of a set of arguments and a logical operator.|
|描述|概述：BswMLogicalExpression是AUTOSAR BSW模块管理（BswM）的一部分，用于定义布尔逻辑表达式，这些表达式基于不同的输入来控制BSW模块的行为。|
|描述|注意：在配置BswMLogicalExpression时，必须确保所使用的表达式符合AUTOSAR的逻辑运算规则；表达式中引用的每个元素都必须在系统中有定义且可达；逻辑表达式的复杂度应当考虑到系统资源和性能的限制。|
|说明|Each argument can either be a mode condition or a sub-expression to allow definition of more complex logical expressions. There may be an unlimited number of arguments in each logical expression. Note that the order of evaluation of the expressions is not defined.|
|多实例个数|0 - 4294967295|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|BswMLogicalOperator|
|描述|This parameter specifies the logical operator to be used in the logical expression. If the logical operator is set to something other than BSWM_NOT, and the expression only consists of a single condition, then this parameter will have no effect.|
|描述|概述：BswMLogicalOperator 是 AUTOSAR BSW Module Management (BswM) 的一个配置参数，用于定义逻辑表达式中使用的逻辑运算符，如 AND、OR、NOT 等，以便在决定模块模式请求时进行条件判断。|
|描述|注意：在配置逻辑表达式时，需要确保使用的逻辑运算符与所需的逻辑行为相匹配；逻辑运算符的使用应遵循AUTOSAR规范中定义的语法和语义；在复杂的逻辑表达式中，应注意运算符的优先级和括号的使用，以避免逻辑错误。|
|多实例个数|0 - 1|
|默认值|BSWM_AND|

|配置项属性|值（选择引用配置项）|
|---|---|
|名称|BswMArgumentRef|
|描述|This is a choice reference either to a mode condition or a sub-expression.|
|说明|In case the BswMLogicalExpression.BswMLogicalOperator equals BSWM_NAND only two operands are supported. In case the BswMLogicalExpression.BswMLogicalOperator equals BSWM_NOT only one operand is supported.|
|多实例个数|1 - inf|
|目标引用|/AUTOSAR/EcucDefs/BswM/BswMConfig/BswMArbitration/BswMLogicalExpression/AUTOSAR/EcucDefs/BswM/BswMConfig/BswMArbitration/BswMModeCondition|

#### 1.2.3. BswMModeCondition

|容器属性|值（容器）|
|---|---|
|名称|BswMModeCondition|
|描述|This container describes the BswM mode conditions that can be used either by itself to form a rule or as a part of a logical expression.|
|描述|概述：BswMModeCondition配置项用于定义基本软件模块管理（BswM）中的模式条件，这些条件用于控制BswM逻辑的执行，例如根据ECU的不同模式来启动或停止特定的功能。|
|描述|注意：在配置BswMModeCondition时，需要确保所依赖的模式声明与实际系统模式一致；此外，对于每个模式条件的触发逻辑，应明确定义以避免逻辑冲突或不一致；AUTOSAR CP 4.4标准中对模式管理有详细规范，确保遵循这些规范以保证系统的可靠性和一致性。|
|多实例个数|0 - 4294967295|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|BswMConditionType|
|描述|This parameter specifies what kind of comparison that is made for the evaluation of the mode condition.|
|描述|概述：BswMConditionType是用于定义基本软件模块管理（BswM）中的条件类型，这些条件用于控制BswM逻辑的执行，例如模式切换或功能激活。|
|描述|注意：在定义BswMConditionType时，需要确保其与系统中的其他条件类型不冲突，并且与实际的系统需求相匹配；此外，应注意该配置项在AUTOSAR CP 4.4标准中的具体属性和限制，以确保兼容性和正确性。|
|说明|For BSWM_EQUALS and BSWM_EQUALS_NOT, the BswMModeRequestPort port referenced by BswMConditionMode is compared with the value configured in BswMConditionValue for equality or not-equality. For BSWM_EVENT_IS_SET and BSWM_EVENT_IS_CLEARED, the BswMEventRequestPort port referenced by BswMConditionMode is checked for being set or cleared (not-set).|
|多实例个数|1 - 1|
|默认值|BSWM_EQUALS|

|配置项属性|值（选择引用配置项）|
|---|---|
|名称|BswMConditionMode|
|描述|This parameter references either a mode request port or an event request port.|
|多实例个数|1 - 1|
|目标引用|/AUTOSAR/EcucDefs/BswM/BswMConfig/BswMArbitration/BswMEventRequestPort/AUTOSAR/EcucDefs/BswM/BswMConfig/BswMArbitration/BswMModeRequestPort|

##### 1.2.3.1. BswMConditionValue

|容器属性|值（容器）|
|---|---|
|名称|BswMConditionValue|
|描述|This container holds the parameters and references necessary to identify the mode type and the value that the mode request is compared to.|
|描述|概述：BswMConditionValue是AUTOSAR BSW模块管理（BswM）的配置参数，用于定义模块管理逻辑中的条件值，这些条件值用于控制BswM逻辑执行的分支。|
|描述|注意：在配置BswMConditionValue时，必须确保其值与BswM逻辑中预期的条件匹配；此外，每个条件值应该是唯一的，以避免在模块管理逻辑中的混淆；在配置过程中还应注意条件值的数据类型，确保它与BswM逻辑中使用的数据类型兼容。|
|多实例个数|0 - 1|

###### 1.2.3.1.1. BswMBswMode

|容器属性|值（容器）|
|---|---|
|名称|BswMBswMode|
|描述|This container defines the value and type of a mode in the BSW. The mode value is defined by configuring either BswMBswRequestedMode or BswMCompuScaleModeValue.|
|描述|概述：BswMBswMode配置项用于定义基础软件模块（BswM）的模式管理逻辑，包括模式切换的条件和行为，以及模式之间的转换规则。|
|描述|注意：在配置BswMBswMode时，需要确保模式之间的转换逻辑清晰且无歧义；模式切换条件应当明确，避免因条件模糊导致的不确定行为；此配置项在AUTOSAR CP 4.4中是标准的一部分，但实现细节可能因AUTOSAR版本或供应商实现而异。|
|多实例个数|0 - 1|

|配置项属性|值（字符串参数配置项）|
|---|---|
|名称|BswMBswRequestedMode|
|描述|This parameter contains the symbolic name (as a string) of a certain mode/state that can be requested/indicated by the BSW modules.|
|描述|概述：BswMBswRequestedMode配置项用于定义基础软件模块（BswM）请求的模式，它指定了BswM在特定条件下应当请求的软件模块的操作模式。|
|描述|注意：该配置项需要与系统中其他模块的模式管理机制紧密协作，确保模式切换的一致性和正确性；在配置时需考虑系统的实时性和安全性要求；配置错误可能导致系统行为不符合预期，特别是在涉及安全相关的模块时更需谨慎。|
|多实例个数|0 - 1|

####### 1.2.3.1.1.1. BswMCompuScaleModeValue

|容器属性|值（容器）|
|---|---|
|名称|BswMCompuScaleModeValue|
|描述|This container contains parameters used to define a mode value.|
|多实例个数|0 - 1|

|配置项属性|值（字符串参数配置项）|
|---|---|
|名称|BswMCompuConstText|
|描述|The value of this parameter shall match the VT member of a CompuConst defined within the referenced CompuMethod (BswMCompuMethodRef). The interval value of the corresponding CompuScale shall be used as the mode request value.|
|多实例个数|1 - 1|

|配置项属性|值（外部引用配置项）|
|---|---|
|名称|BswMCompuMethodRef|
|描述|This is a foreign reference to the CompuMethod used for mode requests.|
|多实例个数|1 - 1|
|目标类型|COMPU-METHOD|

###### 1.2.3.1.2. BswMModeDeclaration

|容器属性|值（容器）|
|---|---|
|名称|BswMModeDeclaration|
|描述|When the mode corresponds to a mode request or mode indication interface the mode is defined by a mode declaration. The mode declarations are defined in the SW-C Template and hence a foreign reference to the corresponding Mode Declaration is used.|
|描述|概述：BswMModeDeclaration 用于定义基本软件模块管理（BswM）的模式声明，这些模式用于控制和管理不同的软件模块之间的交互和行为。|
|描述|注意：确保模式声明与系统需求和功能安全要求相匹配；模式声明应由系统架构师或相应的软件架构师定义和维护；在实现时，应注意模式切换的时序和依赖关系，避免系统不稳定或功能异常。|
|多实例个数|0 - 1|

|配置项属性|值（外部引用配置项）|
|---|---|
|名称|BswMModeValueRef|
|描述|This is a foreign reference to the Mode Declaration used for the mode requests corresponding to this condition.|
|描述|概述：BswMModeValueRef用于引用特定的模块模式，它允许基础软件模块管理器(BswM)根据不同的模块模式来改变其行为或配置。|
|描述|注意：确保引用的模块模式已在系统中定义且有效；BswMModeValueRef的使用需要遵循AUTOSAR的模块间通信规则；在配置时，应注意模式切换的实时性和一致性要求。|
|多实例个数|1 - 1|
|目标类型|MODE-DECLARATION|

#### 1.2.4. BswMModeRequestPort

|容器属性|值（容器）|
|---|---|
|名称|BswMModeRequestPort|
|描述|Each instance of this container defines a mode request interface that is used to requests or indicate modes from/to the BswM. These interfaces are implemented as ports or as ordinary C-functions based upon if the request is made by an SW-C or a BSW module.|
|描述|概述：BswMModeRequestPort是AUTOSAR BSW模块管理（BswM）的配置参数，用于定义模式请求端口，这些端口允许BswM模块接收来自其他软件模块的模式切换请求。|
|描述|注意：在配置BswMModeRequestPort时，需要确保端口的定义与请求发送模块的模式声明一致；端口的模式请求类型应与BswM的逻辑执行路径相匹配；在配置过程中，应注意模式请求的优先级和处理策略，以避免模式切换冲突。|
|说明|There are different types of mode requests: 1. Mode requests from the SW-C:s 2. Mode Requests from other BSW modules such as the DCM. 3. State/mode indications from the RTE or other BSW modules such as the bus specific State Managers. Note that the BswM treats all request and indications in the exact same way.|
|多实例个数|0 - 4294967295|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|BswMRequestProcessing|
|描述|This parameter defines if the processing of the mode arbitration shall be done immediately when a mode request is received or if it shall be deferred to the processing of the main function of BswM.|
|多实例个数|1 - 1|
|默认值|BSWM_DEFERRED|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|BswMArbitrateOnInit|
|描述|This parameter defines immediately arbitrate will be act in Init.|
|描述|概述：BswMArbitrateOnInit 用于定义基础软件模块在初始化阶段的仲裁策略，确保模块按照特定的顺序和条件进行初始化。|
|描述|注意：该配置项需要根据系统的具体需求和依赖关系来设定；不正确的初始化顺序可能导致系统启动失败或运行不稳定；在多模块依赖的环境中，仲裁策略尤为重要以确保正确的初始化顺序。|
|说明|only available in immediately|
|多实例个数|1 - 1|
|默认值|true|

##### 1.2.4.1. BswMModeRequestSource

|容器属性|值（容器）|
|---|---|
|名称|BswMModeRequestSource|
|描述|This choice container specifies the source of the mode request or state/mode indication. The requester of a mode can be both SW-C:s and other BSW Modules, such as the bus specific State Managers.|
|描述|概述：BswMModeRequestSource配置项用于定义基础软件模块管理（BswM）中的模式请求源，它指定了哪些模块或实体可以向BswM发出模式切换的请求。|
|描述|注意：在配置BswMModeRequestSource时，需要确保每个请求源的标识符是唯一的；请求源应当明确对应到能够发出模式请求的实体；在AUTOSAR CP 4.4标准中，对于模式管理的配置要求严格，需要遵循标准文档中的规范进行配置。|
|多实例个数|1 - 1|

###### 1.2.4.1.1. BswMBswModeNotification

|容器属性|值（容器）|
|---|---|
|名称|BswMBswModeNotification|
|描述|This is a mode request source emanating from another BSW Module.|
|描述|概述：BswMBswModeNotification配置项用于定义基础软件模块（BswM）如何被通知关于模式变化的信息，这允许BswM根据不同的模式改变其行为。|
|描述|注意：在配置BswMBswModeNotification时，需要确保正确映射到相应的模块和模式，以便于BswM能够接收到正确的模式通知；此外，要注意模式通知的时序和条件，确保在系统的正确状态下通知BswM；根据AUTOSAR CP 4.4标准，还需确保配置项符合标准中定义的属性和参数。|
|多实例个数|0 - 1|

|配置项属性|值（外部引用配置项）|
|---|---|
|名称|BswMBswModeDeclarationGroupPrototypeRef|
|描述|This is a foreign reference to the Mode Declaration Group Prototype.|
|描述|概述：BswMBswModeDeclarationGroupPrototypeRef 是一个配置项，用于引用模式声明组原型，这通常用于定义基本软件模块的模式管理接口。|
|描述|注意：在配置时，确保引用的模式声明组原型在系统中是唯一的且已经定义；此配置项通常与BswM模块的模式管理功能紧密相关，因此需要与BswM模块的其他配置保持一致；在AUTOSAR CP 4.4标准中，应当遵循模式管理的规范来正确配置此项，以确保基本软件模块能够正确地进行模式切换。|
|多实例个数|1 - 1|
|目标类型|MODE-DECLARATION-GROUP-PROTOTYPE|

###### 1.2.4.1.2. BswMCanSMIcomIndication

|容器属性|值（容器）|
|---|---|
|名称|BswMCanSMIcomIndication|
|描述|This is an indication from CanSM of the configuration Id of the Icom configuration|
|描述|概述：BswMCanSMIcomIndication是一个配置项，用于定义BswM（Basic Software Module）如何处理来自CanSM（CAN State Manager）的Icom（Interruptible Communication）状态指示。|
|描述|注意：在配置BswMCanSMIcomIndication时，需要确保与CAN网络管理的需求相一致；此配置项应与具体的CAN网络和Icom配置相匹配；在AUTOSAR CP 4.4标准中，确保使用正确的数据类型和结构来定义此配置项，以避免兼容性问题。|
|多实例个数|0 - 1|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|BswMCanSMIcomIndicationSwitchError|
|描述|Identifies the type of indications (error or error-free) from the CanSM which this mode request corresponds to.|
|描述|概述：BswMCanSMIcomIndicationSwitchError 是一个配置项，用于定义当CAN通信状态管理（CanSM）的Icom（即隔离通信）指示发生切换错误时，BswM（基础软件模块管理器）应如何响应。|
|描述|注意：在配置此项时，需要确保BswM模块已经配置了相应的逻辑处理规则；此配置项的行为应与系统的故障管理策略一致；在配置过程中，应注意与其他通信管理模块的交互和依赖关系。|
|多实例个数|1 - 1|
|默认值|BSWM_ICOM_SWITCH_E_OK|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|BswMCanSMChannelRef|
|描述|This is a reference to the CAN channel handle that the mode request corresponds to.|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/ComM/ComMConfigSet/ComMChannel|

###### 1.2.4.1.3. BswMCanSMIndication

|容器属性|值（容器）|
|---|---|
|名称|BswMCanSMIndication|
|描述|This is an indication of the current state of the CAN State Manager.|
|描述|概述：BswMCanSMIndication配置项用于定义CAN状态管理（CanSM）模块向BSW Mode Manager（BswM）报告网络模式变化的指示，允许BswM根据CAN网络的状态改变来调整ECU的行为。|
|描述|注意：在配置BswMCanSMIndication时，需要确保正确映射CanSM网络和BswM模式之间的关系；此配置项应与系统中实际的CAN网络数量和状态一致；在AUTOSAR CP 4.4标准中，BswM模块的配置应遵循最新的模块架构和API规范。|
|多实例个数|0 - 1|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|BswMCanSMChannelRef|
|描述|This is a reference to the CAN channel handle that the mode request corresponds to.|
|描述|概述：BswMCanSMChannelRef配置项用于定义BswM模块与CanSM通道之间的关联，这样BswM可以根据CanSM通道的状态来管理BswM的逻辑视图和行为。|
|描述|注意：在配置时需确保CanSM通道与BswM逻辑视图的正确映射；CanSM通道的状态变化应当能够触发BswM的规则评估；在多通道CAN网络中，每个CanSM通道应有其对应的BswMCanSMChannelRef配置。|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/ComM/ComMConfigSet/ComMChannel|

###### 1.2.4.1.4. BswMNmStateChangeNotification

|容器属性|值（容器）|
|---|---|
|名称|BswMNmStateChangeNotification|
|描述|This is a notification from the Nm module that its state has changed.|
|描述|概述：BswMNmStateChangeNotification配置项用于定义网络管理状态机（Nm）在状态变化时，通知相应的Bsw模块（基础软件模块）的回调函数。|
|描述|注意：在配置时，需要确保回调函数与Nm状态机的状态变化正确对应；回调函数应当是可靠的，不会引起长时间的阻塞；在多个模块需要状态变化通知时，应考虑通知顺序和优先级。|
|多实例个数|0 - 1|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|BswMNmChannelRef|
|描述|This is a reference to the NM channel handle that the mode request corresponds to.|
|描述|概述：BswMNmChannelRef配置项用于指定网络管理通信通道的引用，它将基本软件模块与特定的网络管理通道相关联。|
|描述|注意：在配置BswMNmChannelRef时，需要确保引用的通道已在系统中定义并且与网络管理模块兼容；此配置项通常与网络管理模块的配置紧密相关，因此需要与网络配置保持一致；在多通道系统中，正确的通道引用对于网络管理功能的正确性至关重要。|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/ComM/ComMConfigSet/ComMChannel|

###### 1.2.4.1.5. BswMComMIndication

|容器属性|值（容器）|
|---|---|
|名称|BswMComMIndication|
|描述|This is an indication of the current communication mode of a channel in the Communication Manager.|
|描述|概述：BswMComMIndication配置项用于定义BswM（基础软件模块管理器）如何响应来自ComM（通信管理器）的用户模式指示，以便根据网络管理需求调整ECU（电子控制单元）的行为。|
|描述|注意：确保每个BswMComMIndication配置正确映射到��应的ComM用户以避免行为不一致；在配置时需注意系统的实时性和资源限制；该配置项在AUTOSAR CP 4.4中应与网络管理需求紧密结合，以确保网络的有效管理。|
|多实例个数|0 - 1|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|BswMComMChannelRef|
|描述|This is a reference to the Communication Manager channel handle that the indication corresponds to.|
|描述|概述：BswMComMChannelRef配置项用于定义BSW Mode Manager (BswM)与Communication Manager (ComM)之间的通道引用，确保BswM能够根据ComM的通道状态改变来执行相应的模式切换逻辑。|
|描述|注意：在配置BswMComMChannelRef时，需要确保引用的ComM通道��经在系统中定义并正确配置；BswM模块的模式管理逻辑应与ComM通道状态变化保持一致；在多通道系统中，每个BswMComMChannelRef应唯一对应一个ComM通道。|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/ComM/ComMConfigSet/ComMChannel|

###### 1.2.4.1.6. BswMComMPncRequest

|容器属性|值（容器）|
|---|---|
|名称|BswMComMPncRequest|
|描述|This is a request of the current communication mode of a Partial Network Cluster in the Communication Manager.|
|描述|概述：BswMComMPncRequest配置项用于定义BswM模块如何处理来自ComM模块的PNC（Partial Network Cluster）请求，以控制网络的部分唤醒和休眠。|
|描述|注意：确保正确配置PNC请求以满足网络管理需求；不正确的配置可能导致网络唤醒和休眠行为异常；AUTOSAR CP 4.4标准中对BswM和ComM的交互提供了详细规范，需要遵循这些规范以保证系统的正确行为。|
|多实例个数|0 - 1|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|BswMComMPncRef|
|描述|This is a reference to the Communication Manager PNC handle of the Partial Network Cluster that the request corresponds to.|
|描述|概述：BswMComMPncRef配置项用于定义BswM模块（基础软件模块管理器）与ComM（通信管理器）之间的PNC（部分网络群组）引用关系，以便管理PNC状态变化时的行为。|
|描述|注意：确保PNC引用正确对应于ComM配置中的PNC定义；在配置时考虑PNC状态变化对系统行为的影响；AUTOSAR CP 4.4标准中，对BswM与ComM之间的交互有明确规范，需遵循这些规范以保证系统的正确性和稳定性。|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/ComM/ComMConfigSet/ComMPnc|

###### 1.2.4.1.7. BswMDcmComModeRequest

|容器属性|值（容器）|
|---|---|
|名称|BswMDcmComModeRequest|
|描述|The source of the mode request is the Diagnostic Communication Manager.|
|描述|概述：BswMDcmComModeRequest配置项用于定义诊断通信管理（Dcm）模块请求改变ECU通信模式的行为，以支持不同的诊断会话或操作需要。|
|描述|注意：确保该配置与ECU支持的通信模式和诊断会话类型相匹配；在配置时需考虑ECU的通信能力和限制；AUTOSAR CP 4.4标准中，该配置项的属性和使用方法应严格遵循规范文档，以保证诊断功能的正确实现和通信的稳定性。|
|多实例个数|0 - 1|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|BswMDcmComMChannelRef|
|描述|This is a reference from DcmModeRequest to the ComM channel that the indication corresponds to.|
|描述|概述：BswMDcmComMChannelRef是一个配置项，用于指定诊断通信管理模块（Dcm）与通信管理模块（ComM）之间的通道引用，确保Dcm能够管理和控制与车辆通信网络的连接状态。|
|描述|注意：在配置时需确保引用的ComM通道与Dcm模块的需��相匹配；若项目中使用了多个通信通道，每个Dcm通道应正确映射到相应的ComM通道；AUTOSAR CP 4.4标准要求明确指定通信管理的依赖关系，以保证诊断通信的正确性和可靠性。|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/ComM/ComMConfigSet/ComMChannel|

###### 1.2.4.1.8. BswMEcuMIndication

|容器属性|值（容器）|
|---|---|
|名称|BswMEcuMIndication|
|描述|This is a notification of the current operation mode of the ECU State Manager. This container does not contain any parameters since there are no further configuration needed for this type of request.|
|描述|概述：BswMEcuMIndication配置项用于定义ECU管理模块（EcuM）状态变化时的通知机制，允许软件组件根据ECU状态变化做出响应。|
|描述|注意：确保正确配置通知机制以避免在ECU状态变化时错过重要事件；在设计系统时考虑ECU状态变化对系���行为的影响；该配置项在AUTOSAR CP 4.4中应与EcuM模块的状态管理功能紧密集成。|
|多实例个数|0 - 1|

###### 1.2.4.1.9. BswMEcuMRUNRequestIndication

|容器属性|值（容器）|
|---|---|
|名称|BswMEcuMRUNRequestIndication|
|描述|This is an indication of the current State of the RUN Request Protocol.|
|描述|概述：BswMEcuMRUNRequestIndication配置项用于定义ECU管理模块接收到远程唤醒请求时的指示，它是BswM模块与ECU管理需求之间的接口配置。|
|描述|注意：该配置项需要与ECU的低功耗模式和唤醒源配置相匹配，确保系统能够正确响应外部唤醒请求；在配置时需考虑ECU支持的唤醒源类型，以及与其他唤醒源的优先级关系；AUTOSAR CP 4.4标准中，确保该配置项的使用与ECU支持的功能和唤醒机制一致。|
|多实例个数|0 - 1|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|BswMEcuMRUNRequestProtocolPort|
|描述|Identifies the EcuM State which is related to the mode request.|
|描述|概述：BswMEcuMRUNRequestProtocolPort是用于定义基础软件模块（BswM）与ECU管理运行控制（EcuM）之间的请求协议端口，用于处理运行管理请求。|
|描述|注意：该配置项需要确保与ECU的运行管理策略相匹配；在配置时需注意与其他BswM配置项的兼容性；AUTOSAR CP 4.4标准中未明确定义此配置项，需参考具体实现或供应商文档。|
|多实例个数|1 - 1|
|默认值|BSWM_ECUM_STATE_APP_RUN|

###### 1.2.4.1.10. BswMEcuMWakeupSource

|容器属性|值（容器）|
|---|---|
|名称|BswMEcuMWakeupSource|
|描述|This is a notification of the current state of an ECU State Manager wakeup source.|
|描述|概述：BswMEcuMWakeupSource 配置项用于定义车辆中用于唤醒电子控制单元（ECU）的唤醒源。|
|描述|注意：确保唤醒源的配置与实际硬件和外部事件匹配；在系统休眠或低功耗模式下，正确管理唤醒源以避免不必要的功耗；AUTOSAR CP 4.4标准中对唤醒源的管理和配置有详细规定，需要严格遵守。|
|多实例个数|0 - 1|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|BswMEcuMWakeupSrcRef|
|描述|This is a reference to the ECU State Manager Wakeup Source that the indication corresponds to.|
|描述|概述：BswMEcuMWakeupSrcRef配置项用于定义基础软件模块（BswM）中，ECU唤醒源的引用，这有助于BswM管理和响应不同的唤醒源事件。|
|描述|注意：在配置时需确保唤醒源与ECU支持的唤醒源相匹配；此配置项对于实现低功耗模式和唤醒策略至关重要；AUTOSAR CP 4.4标准中，对唤醒源的管理和配置有详细规定，需要遵循相关规范以保证系统的兼容性和可靠性。|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/EcuM/EcuMConfiguration/EcuMCommonConfiguration/EcuMWakeupSource|

###### 1.2.4.1.11. BswMEthIfPortGroupLinkStateChg

|容器属性|值（容器）|
|---|---|
|名称|BswMEthIfPortGroupLinkStateChg|
|描述|This is an indication from the EthIf if the link state of a Ethernet interface switch port group has changed.|
|描述|概述：BswMEthIfPortGroupLinkStateChg配置项用于定义基础软件模块（BswM）中以太网接口端口组（EthIfPortGroup）的链路状态变化时的行为。|
|描述|注意：在AUTOSAR CP 4.4标准中，必须确保该配置项正确映射到相应的以太网接口端口组状态变化通知机制；此配置项通常与网络管理和诊断功能紧密相关，因此需要确保与这些功能的集成是正确的；在配置时，应注意与EthIf模块的配置一致性，避免配置不一致导致的功能异常。|
|多实例个数|0 - 1|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|BswMEthIfSwitchPortGroupRef|
|描述|This is a reference to the Ethernet Interface Switch Port Group that the indication corresponds to.|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/EthIf/EthIfConfigSet/EthIfSwitchPortGroup|

###### 1.2.4.1.12. BswMEthSMIndication

|容器属性|值（容器）|
|---|---|
|名称|BswMEthSMIndication|
|描述|This is an indication of the current state of the Ethernet State Manager.|
|描述|概述：BswMEthSMIndication配置项用于定义以太网状态管理指示，它指定了当以太网通信控制器状态发生变化时，应当通知哪个BswM模块的函数。|
|描述|注意：确保正确配置以太网控制器与BswM模块之间的映射关系，以便于正确处理网络状态变化；在配置时需注意AUTOSAR版本兼容性，确保配置项属性与AUTOSAR CP 4.4标准一致；此配置对于网络管理功能至关重要，错误的配置可能导致网络状态管理失效。|
|多实例个数|0 - 1|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|BswMEthSMChannelRef|
|描述|This is a reference to the Ethernet channel handle that the mode request corresponds to.|
|描述|概述：BswMEthSMChannelRef 配置项用于定义基础软件模块（BswM）与以太网状态管理（EthSM）之间的通道引用，确保网络管理功能的正确实现。|
|描述|注意：该配置项必须确保引用的通道与实际的以太网通道配置相匹配；在配置过程中应避免重复或错误的通道引用；在AUTOSAR CP 4.4中，确保该配置项的正确性对网络管理的稳定性和可靠性至关重要。|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/ComM/ComMConfigSet/ComMChannel|

###### 1.2.4.1.13. BswMFrSMIndication

|容器属性|值（容器）|
|---|---|
|名称|BswMFrSMIndication|
|描述|This is an indication of the current state of the FlexRay State Manager.|
|描述|概述：BswMFrSMIndication配置项用于定义BswM模块如何响应来自FlexRay通信堆栈管理（FrSM）模块的状态指示，以便根据FlexRay网络的当前状态调整BswM的内部管理逻辑。|
|描述|注意：确保正确映射FlexRay通信状态到BswM的管理决策中，以避免网络状态误判；在配置时需考虑系统的实时性和网络的稳定性；AUTOSAR CP 4.4标准中，对于BswM模块与其他通信堆栈模块的交互提供了详细的指导，应遵循这些指导以确保兼容性和性能。|
|多实例个数|0 - 1|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|BswMFrSMChannelRef|
|描述|This is a reference to the FlexRay Cluster handle that the mode request corresponds to.|
|描述|概述：BswMFrSMChannelRef配置项用于定义BswM模块与FlexRay通信状态管理模块（FrSM）之间的关联，指定BswM模块应当监控的FlexRay通道。|
|描述|注意：在配置时需要确保引用的FlexRay通道与实际的FrSM通道一致；BswM模块的策略决策可能依赖于FrSM通道的状态，因此正确的关联至关重要；在多通道FlexRay系统中，每个通道都应有一个对应的BswMFrSMChannelRef配置。|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/ComM/ComMConfigSet/ComMChannel|

###### 1.2.4.1.14. BswMGenericRequest

|容器属性|值（容器）|
|---|---|
|名称|BswMGenericRequest|
|描述|This mode request originates from a requester that is not among the list of standardized mode requesters (i.e. the different resource managers).|
|描述|概述：BswMGenericRequest是一个配置项，用于定义基本软件模块管理（BswM）对于特定请求的处理，这些请求可能来自于应用层或其他基础软件模块。|
|描述|注意：在配置BswMGenericRequest时，需要确保请求ID的唯一性，避免处理冲突；此配置项应与系统中的其他管理需求一起考虑，以确保整体的一致性和优先级管理；在AUTOSAR CP 4.4中，对于请求的处理可能涉及到复杂的逻辑，因此需要仔细设计以满足系统的实时性和可靠性要求。|
|多实例个数|0 - 1|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|BswMModeRequesterId|
|描述|This parameters identifies the different users of the generic mode request interface.|
|描述|概述：BswMModeRequesterId用于唯一标识请求模式切换的软件模块，它是BswM（基础软件模块管理器）配置中的一个关键元素，用于管理和映射不同软件模块的模式请求。|
|描述|注意：确保每个BswMModeRequesterId在系统中是唯一的，以避���模式管理的冲突；在配置时需考虑模式请求的优先级，以确保系统的稳定性和预期行为；BswM配置应与系统中所有模式请求者的实际需求相匹配，以确保正确的模式切换逻辑。|
|多实例个数|1 - 1|
|取值范围|0 - 65535|

###### 1.2.4.1.15. BswMJ1939DcmBroadcastStatus

|容器属性|值（容器）|
|---|---|
|名称|BswMJ1939DcmBroadcastStatus|
|描述|This is a notification of the desired broadcast status per network, triggered via DM13.|
|描述|概述：BswMJ1939DcmBroadcastStatus配置项用于定义诊断通信管理器（DCM）在J1939网络上广播状态信息的行为和条件，确保符合J1939协议的要求。|
|描述|注意：该配置项需要根据J1939网络的具体要求进行详细配置，包括但不限于广播的周期、条件和优先级；在AUTOSAR CP 4.4标准中，确保配置与网络管理和诊断需求一致；特别注意广播消息的安全性和隐私保护措施，避免敏感信息泄露。|
|多实例个数|0 - 1|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|BswMJ1939DcmChannelRef|
|描述|Reference to the communication channel which is affected by this mode request.|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/ComM/ComMConfigSet/ComMChannel|

###### 1.2.4.1.16. BswMJ1939NmIndication

|容器属性|值（容器）|
|---|---|
|名称|BswMJ1939NmIndication|
|描述|This is an indication of the current state of the J1939 network management module.|
|描述|概述：BswMJ1939NmIndication是一个配置项，用于定义基础软件模块J1939网络管理（Nm）的指示回调函数，该函数在网络管理状态发生变化时被调用。|
|描述|注意：在配置BswMJ1939NmIndication时，需要确保回调函数符合AUTOSAR标准中定义的接口规范；此配置项通常由网络管理模块的开发者提供，应确保其与系统中其他网络管理功能的兼容性；在实际应用中，需要注意该指示的执行时间和资源消耗，以免影响系统性能。|
|多实例个数|0 - 1|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|BswMJ1939NmChannelRef|
|描述|This is a reference to the J1939Nm channel handle that the mode request corresponds to.|
|描述|概述：BswMJ1939NmChannelRef 配置项用于指定某个J1939网络管理模块（Nm）所使用的CAN通道引用，确保网络管理功能能够正确地与特定的通信通道关联。|
|描述|注意：在配置时需确保引用的CAN通道已经在系统中定义并正确初始化；J1939网络管理模块与CAN通道的关联必须一一对应，不能出现多个Nm模块引用同一CAN通道的情况；在多通道系统中，正确的通道引用对于网络管理的分区和隔离至关重要。|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/ComM/ComMConfigSet/ComMChannel|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|BswMJ1939NmNodeRef|
|描述|This is a reference to the node that the mode request corresponds to.|
|描述|概述：BswMJ1939NmNodeRef 是一个配置参数，用于将基本软件模块中的J1939网络管理节点引用到具体的网络管理配置。|
|描述|注意：在配置BswMJ1939NmNodeRef时，需要确保引用的节点与实际的网络拓扑和节点地址设置相匹配；此配置项应与J1939堆栈的其他部分协同工作，以确保网络管理功能的正确实现；在AUTOSAR CP 4.4标准中，应当遵循相关的网络管理规范来配置此项，以保证与标准的兼容性。|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/J1939Nm/J1939NmConfigSet/J1939NmNode|

###### 1.2.4.1.17. BswMLinSMIndication

|容器属性|值（容器）|
|---|---|
|名称|BswMLinSMIndication|
|描述|This is an indication of the current state of the LIN State Manager.|
|描述|概述：BswMLinSMIndication配置项用于定义LIN通信状态机（LinSM）的指示函数，该函数由LIN状态管理模块调用，以通知BswM模块有关LIN通道状态的变化。|
|描述|注意：在配置BswMLinSMIndication时，需要确保指示函数与BswM模块的逻辑正确对应；此外，该配置项应与LIN通道的实际硬件和软件资源相匹配；在多通道LIN系统中，每个通道的状态指示应独立配置以避免状态信息的混淆。|
|多实例个数|0 - 1|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|BswMLinSMChannelRef|
|描述|This is a reference to the LIN channel handle that the mode request corresponds to.|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/ComM/ComMConfigSet/ComMChannel|

###### 1.2.4.1.18. BswMLinScheduleIndication

|容器属性|值（容器）|
|---|---|
|名称|BswMLinScheduleIndication|
|描述|This is an indication of the currently active LIN Schedule Table for a specific LIN Interface.|
|描述|概述：BswMLinScheduleIndication配置项用于定义LIN Schedule表的状态变化时，需要调用的BswM模块中的指示函数，以便BswM可以根据LIN Schedule的变化来管理和调整BSW模式。|
|描述|注意：在配置BswMLinScheduleIndication时，需要确保所引用的BswM模块和LIN Schedule表已经定义且匹配；此配置项对于实现LIN通信管理的逻辑至关重要，因此必须准确配置；AUTOSAR CP 4.4标准要求LIN通信管理逻辑与BswM模块的集成，所以该配置项应与整体系统设计紧密结合。|
|多实例个数|0 - 1|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|BswMLinScheduleRef|
|描述|This is a reference to the LIN Schedule Table handle that the mode request corresponds to.|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/LinSM/LinSMConfigSet/LinSMChannel/LinSMSchedule|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|BswMLinSMChannelRef|
|描述|This is a reference to the LIN channel handle that the mode request corresponds to.|
|描述|概述：BswMLinSMChannelRef配置项用于指定LIN通信堆栈中LIN状态管理模块（LinSM）所管理的LIN通道的引用。|
|描述|注意：在配置BswMLinSMChannelRef时，必须确保引用的LIN通道已在系统中定义并正确配置；此配置项应与LIN通信控制器和相应的LIN网络管理配置保持一致；在多通道LIN系统中，每个LinSM实例应该引用不同的通道以避免通道冲突。|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/ComM/ComMConfigSet/ComMChannel|

###### 1.2.4.1.19. BswMLinTpModeRequest

|容器属性|值（容器）|
|---|---|
|名称|BswMLinTpModeRequest|
|描述|This is a LinTp mode request from the LinIf. This port corresponds to a call of the BswM_LinTp_RequestMode API.|
|描述|概述：BswMLinTpModeRequest 配置项用于定义LIN传输协议模块的操作模式请求，确保LIN网络通信符合预期的数据传输模式。|
|描述|注意：在配置BswMLinTpModeRequest时，必须确保与LIN通信需求和系统的实际工作模式相匹配；此配置项应与其他LIN配置参数协同工作，以保证整体的通信效率和稳定性；在AUTOSAR CP 4.4标准中，对于LIN TP模式的具体配置细节应详细参考相关通信管理模块的规范。|
|多实例个数|0 - 1|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|BswMLinTpChannelRef|
|描述|This is a reference to the LIN Interface Channel that the mode|
|描述|概述：BswMLinTpChannelRef 是一个配置参数，用于将 LIN Transport Protocol 模块（LinTp）与特定的 LIN 通道相关联。|
|描述|注意：在配置时，必须确保引用的 LIN 通道已经在系统中定义并正确配置；LinTp模块与LIN通道的关联必须符合系统的通信需求；在AUTOSAR CP 4.4标准中，应当遵循模块间通信接口的规范来确保模块间的兼容性。|
|说明|request corresponds to.|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/ComM/ComMConfigSet/ComMChannel|

###### 1.2.4.1.20. BswMNvMJobModeIndication

|容器属性|值（容器）|
|---|---|
|名称|BswMNvMJobModeIndication|
|描述|Indicates the current status of the multiblock job. The job is identified via BswMNvmService. Possible values for this indication are the possible values of NvM_RequestResultType.|
|描述|概述：BswMNvMJobModeIndication配置项用于指定NvM（非易失性内存管理模块）作业的模式指示，它允许基础软件模块（BswM）根据NvM作业的结果来更新其内部管理逻辑。|
|描述|注意：在使用此配置项时，需要确保NvM和BswM之间的接口和数据交互正确配置，以便BswM可以准确地根据NvM作业的状态改变其行为；此配置项的使用应与系统的诊断和监控需求相一致；在配置过程中，应注意避免与其他模块的作业指示配置冲突。|
|多实例个数|0 - 1|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|BswMNvmService|
|描述|Identifies the Nvm job which is related to the mode request.|
|描述|概述：BswMNvmService 配置项定义了基本软件模块（BswM）与非易失性存储管理（NvM）服务之间的交互，用于控制和监视NvM请求的处理。|
|描述|注意：在AUTOSAR CP 4.4标准中，确保BswMNvmService配置正确反映了BswM模块与NvM服务之间的依赖关系；配置时需注意BswM模块的版本与NvM服务的版本兼容性；在配置BswMNvmService时，应遵循项目特定的需求和指导，以确保系统的正确性和稳定性。|
|多实例个数|1 - 1|
|默认值|NvmReadAll|

###### 1.2.4.1.21. BswMNvMRequest

|容器属性|值（容器）|
|---|---|
|名称|BswMNvMRequest|
|描述|Via this Mode Request Source the NvM indicates the current status of the specified block. Possible Values are:|
|描述|概述：BswMNvMRequest配置项用于定义基本软件模块（BswM）与非易失性内存管理模块（NvM）之间的请求关系，包括请求的类型和目标，以便于控制和管理非易失性数据的读写操作。|
|描述|注意：在配置BswMNvMRequest时，需要确保请求类型与目标NvM块的兼容性；对于每个请求，必须明确指定请求的触发条件和执行动作；在AUTOSAR CP 4.4标准中，对于NvM请求的处理流程和状态管理有明确规定，需要遵守这些规定以保证系统的稳定性和数据的一致性。|
|说明|NvM_RequestResultType NVM_REQ_OK NVM_REQ_NOT_OK NVM_REQ_PENDING NVM_REQ_INTEGRITY_FAILED NVM_REQ_BLOCK_SKIPPED NVM_REQ_NV_INVALIDATED NVM_REQ_CANCELED NVM_REQ_REDUNDANCY_FAILED NVM_REQ_RESTORED_FROM_ROM|
|多实例个数|0 - 1|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|BswMNvMBlockRef|
|描述|This is a reference to the NvM Block Descriptor that the request corresponds to.|
|描述|概述：BswMNvMBlockRef配置项用于定义基本软件模块（BswM）与非易失性存储管理模块（NvM）之间的关联，指定BswM应当如何参考NvM中的数据块。|
|描述|注意：在配置BswMNvMBlockRef时，需要确保引用的NvM块ID是存在且有效的；此外，应当注意BswM和NvM之间的数据一致性和同步机制；在AUTOSAR CP 4.4标准中，该配置项的属性应与标准定义的数据类型和结构相匹配。|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/NvM/NvMBlockDescriptor|

###### 1.2.4.1.22. BswMSdClientServiceCurrentState

|容器属性|值（容器）|
|---|---|
|名称|BswMSdClientServiceCurrentState|
|描述|Used by Service Discovery module to indicate current state of the Client Service (available/down).|
|描述|概述：BswMSdClientServiceCurrentState配置项用于定义基于服务发现的客户端服务的当前状态，包括服务是否可用以及其它相关状态信息。|
|描述|注意：在使用此配置项时，需要确保服务发现机制已正确配置并且处于激活状态；状态更新应及时反映服务的实际可用性；此配置项在AUTOSAR CP 4.4中未明确定义，因此具体实现可能依赖于供应商的实现细节。|
|多实例个数|0 - 1|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|BswMSdClientMethodsRef|
|描述|This is a reference to a client service in the Sd module.|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Sd/SdConfig/SdInstance/SdClientService|

###### 1.2.4.1.23. BswMSdConsumedEventGroupCurrentState

|容器属性|值（容器）|
|---|---|
|名称|BswMSdConsumedEventGroupCurrentState|
|描述|Used by Service Discovery to indicate current status of the EventHandler (requested/released).|
|描述|概述：BswMSdConsumedEventGroupCurrentState配置项用于定义软件组件消费的事件组的当前状态，这有助于管理和跟踪事件的处理状态。|
|描述|注意：在AUTOSAR CP 4.4标准中，对于BswMSdConsumedEventGroupCurrentState的具体定义和使用可能有所不同，需要参考最新的AUTOSAR文档以确保正确实现；此配置项的正确设置对于事件驱动的通信机制至关重要，需要仔细管理以避免状态不一致；在设计系统时，应考虑状态管理的复杂性和对系统性能的影响。|
|多实例个数|0 - 1|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|BswMSdConsumedEventGroupRef|
|描述|This is a reference to an eventGroup that is defined within a client service in the Sd module.|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Sd/SdConfig/SdInstance/SdClientService/SdConsumedEventGroup|

###### 1.2.4.1.24. BswMSdEventHandlerCurrentState

|容器属性|值（容器）|
|---|---|
|名称|BswMSdEventHandlerCurrentState|
|描述|Used by Service Discovery to indicate current status of the EventHandler (requested/released).|
|描述|概述：BswMSdEventHandlerCurrentState 配置项用于定义基本软件模块调度管理器（BswMScheduler）中事件处理程序的当前状态，这有助于调度管理器控制和管理基本软件组件的执行流程。|
|描述|注意：在AUTOSAR CP 4.4标准中，确保状态的定义与BswM模块的规范一致；状态的变更应由BswM逻辑决定，不应随意修改；在配置时，应注意与其他BswM配置项的一致性和依赖关系。|
|多实例个数|0 - 1|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|BswMSdEventHandlerRef|
|描述|This is a reference to an event handler that is defined within a server service in the Sd module.|
|描述|概述：BswMSdEventHandlerRef 是一个配置参数，用于将基本软件模块的服务依赖事件处理器（Service Dependency Event Handler）与特定的事件处理函数关联起来。|
|描述|注意：在配置时，确保引用的事件处理函数与服务依赖事件处理器兼容；此配置项通常由工具自动生成，应避免手动修改以防止不一致；在多服务依赖场景中，正确管理事件处理器的引用关系以确保系统的稳定性和预期行为。|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Sd/SdConfig/SdInstance/SdServerService/SdEventHandler|

###### 1.2.4.1.25. BswMSwcModeNotification

|容器属性|值（容器）|
|---|---|
|名称|BswMSwcModeNotification|
|描述|This is a mode switch notification associated with a RTE switch interface.|
|描述|概述：BswMSwcModeNotification配置项用于定义基本软件模块（BswM）与应用软件组件（Swc）之间的模式切换通知机制，确保系统在不同模式下能够正确响应和执行相应的行为。|
|描述|注意：在配置时需确保模式切换的通知路径和条件清晰定义，避免因配置不当导致系统响应不及时或错误；此配置项对系统的实时性和可靠性有较大影响，需谨慎处理；AUTOSAR CP 4.4标准中对模式管理和通知机制有详细规定，需确保配置符合标准要求。|
|多实例个数|0 - 1|

|配置项属性|值（外部引用配置项）|
|---|---|
|名称|BswMSwcModeNotificationModeDeclarationGroupPrototypeRef|
|描述|This is a foreign reference to the ModeDeclarationGroupPrototype.|
|描述|概述：BswMSwcModeNotificationModeDeclarationGroupPrototypeRef 配置项用于指定基本软件模块（BswM）通知软件组件（Swc）关于模式声明组的引用，这样软件组件可以根据模式变化做出响应。|
|描述|注意：在配置时，确保引用的模式声明组在系统中是存在且有效的；此配置项通常与BswM模式管理逻辑紧密相关，需要与系统设计师协作以确保正确性；在AUTOSAR CP 4.4标准中，应遵循模式管理的规范来配置此项，以保证模式通知机制的正确实现。|
|多实例个数|1 - 1|
|目标类型|MODE-DECLARATION-GROUP-PROTOTYPE|

###### 1.2.4.1.26. BswMSwcModeRequest

|容器属性|值（容器）|
|---|---|
|名称|BswMSwcModeRequest|
|描述|The source of the mode request is a SW Component.|
|描述|概述：BswMSwcModeRequest配置项用于定义基础软件模块（BswM）与软件组件（Swc）之间的模式请求关系，确保系统中不同软件组件的模式切换请求能够被基础软件模块正确处理和响应。|
|描述|注意：在配置时需确保模式请求的唯一性和一���性，避免不同软件组件对同一模式的重复请求；此配置项对于系统的模式管理和控制至关重要，需谨慎定义；AUTOSAR CP 4.4标准中对于模式管理的机制和接口有明确规定，需确保配置项符合这些规定。|
|多实例个数|0 - 1|

|配置项属性|值（外部引用配置项）|
|---|---|
|名称|BswMSwcModeRequestVariableDataPrototypeRef|
|描述|This is a reference to the VariableDataPrototype.|
|描述|概述：BswMSwcModeRequestVariableDataPrototypeRef 配置项用于指定基本软件模块（BswM）中用于请求模式变更的软件组件（Swc）的变量原型引用。|
|描述|注意：在AUTOSAR CP 4.4标准中，确保引用的变量原型与请求的模式声明一致；变量原型应当是定义在相应软件组件中的模式请求接口的一部分；正确配置此项对于模式管理逻辑的正确实现至关重要。|
|多实例个数|1 - 1|
|目标类型|VARIABLE-DATA-PROTOTYPE|

###### 1.2.4.1.27. BswMTimer

|容器属性|值（容器）|
|---|---|
|名称|BswMTimer|
|描述|This is a timer which can be used for time dependent rules. This mode request port can be in one of three modes (depending on the state of the timer):|
|描述|概述：BswMTimer是一个配置项，用于定义基本软件模块（BswM）中的定时器，它控制BswM逻辑的执行频率和定时行为。|
|描述|注意：在配置BswMTimer时，需要确保定时器的时间参数与系统的时钟和调度策略相匹配；定时器的精度和分辨率应满足应用需求；在多核或分布式系统中，还需考虑定时器同步和一致性问题。|
|说明|\* BSWM_TIMER_STOPPED (intial) (The timer has been stopped by an action) \* BSWM_TIMER_STARTED (The timer has been started by an action) \* BSWM_TIMER_EXPIRED (The timer has expired)|
|多实例个数|0 - 1|

###### 1.2.4.1.28. BswMUserConditionRequest

|容器属性|值（容器）|
|---|---|
|名称|BswMUserConditionRequest|
|描述|This mode request originates from a user defined function.|
|描述|概述：BswMUserConditionRequest是一个配置项，用于定义基本软件模块管理（BswM）中用户条件的请求，这些请求会影响BswM的决策和行为。|
|描述|注意：在配置BswMUserConditionRequest时，需要确保其与BswM的逻辑表达式和规则相匹配；用户条件请求的标识符必须在整个系统中唯一；在实际应用中，应当注意这些用户条件请求可能会受到外部因素的影响，因此需要仔细管理和测试以确保系统的稳定性。|
|多实例个数|0 - 1|

|配置项属性|值（函数名配置项）|
|---|---|
|名称|User Condition|
|描述|This parameters identifies the different functions defined by users.|
|描述|概述：User Condition是一个配置项，用于定义AUTOSAR软件组件（SW-C）或交互层（Service Layer）中的条件表达式，这些条件表达式通常用于决定某个功能是否执行。|
|描述|注意：在配置User Condition时，需要确保表达式的逻辑正确性和一致性；应当遵循AUTOSAR的数据类型和操作符规范；在多条件表达式中，注意优先级和括号的使用，以避免逻辑错误。|
|多实例个数|1 - 1|

##### 1.2.4.2. BswMModeInitValue

|容器属性|值（容器）|
|---|---|
|名称|BswMModeInitValue|
|描述|This container defines the initial mode value that is used by BswM for the corresponding mode request after initialization. The initial mode value is defined by configuring either BswMBswModeInitValue or BswMCompuScaleModeValue. This container is optional.|
|描述|概述：BswMModeInitValue配置项用于定义BSW Mode Manager（BswM）模块在系统启动时的初始模式值，这个值将作为系统启动后模块的默认行为状态。|
|描述|注意：在配置BswMModeInitValue时，需要确保初始模式值与系统设计和需求相匹配；初始模式值应该与BswM的模式声明一致，避免配置了一个未声明的模式；在系统复位或启动时，BswM将使用这个初始值来初始化模式管理逻辑，因此需要谨慎配置以避免系统启动时的行为异常。|
|多实例个数|0 - 1|

|配置项属性|值（字符串参数配置项）|
|---|---|
|名称|BswMBswModeInitValue|
|描述|This parameter defines the initial mode value that is used by BswM for the corresponding mode request after initialization.|
|描述|概述：BswMBswModeInitValue配置项用于定义基础软件模块（BswM）在系统启动时的初始模式。这个配置确保了在系统启动时，各个模块能够以一种预定义的模式开始运行。|
|描述|注意：在配置BswMBswModeInitValue时，需要确保初始模式与模块的设计和依赖关系相匹配；此外，应当注意该初始模式值是否符合AUTOSAR标准中对于模式管理的规定；在多模式系统中，还需考虑模式切换的一致性和依赖关系。|
|多实例个数|0 - 1|

###### 1.2.4.2.1. BswMCompuScaleModeValue

|容器属性|值（容器）|
|---|---|
|名称|BswMCompuScaleModeValue|
|描述|This container contains parameters used to define a mode value.|
|描述|概述：BswMCompuScaleModeValue是AUTOSAR BSW模块配置中的一个参数，用于定义基础软件模块管理（BswM）中的计算尺度模式值，这通常与诊断、网络管理等功能相关联，用于控制或调整模块的行为。|
|描述|注意：在配置BswMCompuScaleModeValue时，需要确保其值与相关模块的期望行为相匹配；此外，该值通常应与系统中其他模块或组件的配置保持一致，以确保整个系统的协同工作；在AUTOSAR CP 4.4标准中，如果该属性的使用或取值范围有所变化，需要参考最新的标准文档进行配置。|
|多实例个数|0 - 1|

|配置项属性|值（字符串参数配置项）|
|---|---|
|名称|BswMCompuConstText|
|描述|The value of this parameter shall match the VT member of a CompuConst defined within the referenced CompuMethod (BswMCompuMethodRef). The interval value of the corresponding CompuScale shall be used as the mode request value.|
|描述|概述：BswMCompuConstText是一个配置参数，用于定义基本软件模块管理（BswM）中的计算方法常量文本，这些文本常用于与人机界面（HMI）之间的数据交换。|
|描述|注意：在AUTOSAR CP 4.4标准中，所有的配置参数都应当遵循标准的数据定义和格式；BswMCompuConstText的值应当与系统中使用的语言和编码标准一致；在配置时，应确保文本字符串与预期的计算方法常量匹配，避免因为文本错误导致的功能异常。|
|多实例个数|1 - 1|

|配置项属性|值（外部引用配置项）|
|---|---|
|名称|BswMCompuMethodRef|
|描述|This is a foreign reference to the CompuMethod used for mode requests.|
|描述|概述：BswMCompuMethodRef是一个配置项，用于引用一个CompuMethod，该CompuMethod定义了基础软件模块管理（BswM）模块中使用的数据转换方法。|
|描述|注意：在AUTOSAR CP 4.4标准中，确保引用的CompuMethod与BswM模块的数据处理需求相匹配；CompuMethod应已在系统中定义且有效；在BswM模块配置中正确设置BswMCompuMethodRef以确保数据转换的正确性。|
|多实例个数|1 - 1|
|目标类型|COMPU-METHOD|

#### 1.2.5. BswMRule

|容器属性|值（容器）|
|---|---|
|名称|BswMRule|
|描述|Each instance of this container describes a BswM arbitration rule. The rule either consists of a simple mode condition or a more complex logical expression. This container also references the action lists that shall be invoked when the rule is evaluated to True or False.|
|描述|概述：BswMRule是用于定义基本软件模块管理（BswM）的逻辑规则，这些规则根据输入的模式请求来控制BswM的行为，从而管理ECU内部的软件模块和通信。|
|描述|注意：在配置BswMRule时，需要确保规则的唯一性和一致性，避免相互冲突；规则的设计应考虑到系统的实时性和资源限制；AUTOSAR CP 4.4标准中对BswM的配置和实现提供了详细指导，确保遵循这些指导以保证系统的兼容性和性能。|
|多实例个数|0 - 65535|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|BswMNestedExecutionOnly|
|描述|This parameter defines for its related Rule if the Rule is an Independent rule or a Subordinate rule;|
|描述|概述：BswMNestedExecutionOnly 配置项用于指定基础软件模块（BswM）是否仅在嵌套执行上下文中被调用。|
|描述|注意：此配置项确保BswM的调用模式与系统设计的预期一致；不正确的配置可能导致系统行为不符合预期；在AUTOSAR CP 4.4中，此配置项应仔细管理以避免执行时的冲突或错误。|
|说明|false: an Independent rule, i.e. to be evaluated each time applicable (both as standalone Rule driven by its own BswMModeRequestSource and when referenced by another Rule). true: a Subordinated rule, to be evaluated ONLY as a result of being referenced in one or more Action Lists.|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|BswMRuleInitState|
|描述|This parameter is a part of the reset/initialization behavior of BswM.|
|描述|概述：BswMRuleInitState 配置项定义了基本软件模块管理（BswM）规则的初始状态，这是BswM启动时评估规则所依据的状态。|
|描述|注意：在配置BswMRuleInitState时，需要确保初始状态与系统的启动行为一致；不正确的初始状态可能导致系统在启动时采取错误的行为；此配置项应与BswM的逻辑和依赖关系紧密结合，以确保系统的正确初始化。|
|说明|Action lists are executed when the result of a rule evaluation have changed since the last evaluation. This parameter defines the "previous evaluation result" of a rule to be used after initialization of the BswM. If this parameter is set to BSWM_UNDEFINED, the evaluation result is always treated as changed at the first evaluation of the rule after initialization. If this parameter is set to BSWM_TRUE, the evaluation result is treated as changed if the rule is evaluated to false. If this parameter is set to BSWM_FALSE, the evaluation result is treated as changed if the rule is evaluated to true.|
|多实例个数|1 - 1|
|默认值|BSWM_FALSE|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|BswMRuleExpressionRef|
|描述|This is a reference to the logical expression that is evaluated for each rule.|
|描述|概述：BswMRuleExpressionRef 是一个配置参数，用于引用一个特定的BswM规则表达式，该表达式定义了基本软件模块管理逻辑中的条件判断。|
|描述|注意：在配置BswMRuleExpressionRef时，必须确保引用的规则表达式在系统中是存在且有效的；规则表达式应当被定义在BswM模块的上下文中，以保证模块管理逻辑的正确性；在AUTOSAR CP 4.4标准中，应当遵循定义规则表达式的语法和语义约定，以确保其兼容性和正确性。|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/BswM/BswMConfig/BswMArbitration/BswMLogicalExpression|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|BswMRuleFalseActionList|
|描述|This is a reference to the action list that shall be executed when the rule is evaluated to False|
|描述|概述：BswMRuleFalseActionList配置项定义了在基本软件模块管理（BswM）中，当规则评估结果为假（FALSE）时应执行的一系列动作。|
|描述|注意：在配置BswMRuleFalseActionList时，需要确保列出的动作与系统设计和需求相符；动作列表中的每个动作都必须是系统中定义的有效动作；在配置动作时，应注意动作的执行顺序可能会影响系统行为和性能。|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/BswM/BswMConfig/BswMModeControl/BswMActionList|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|BswMRuleTrueActionList|
|描述|This is a reference to the action list that shall be executed when the rule is evaluated to True|
|描述|概述：BswMRuleTrueActionList配置项定义了在基本软件模块管理（BswM）中，当规则评估结果为真时应执行的动作列表。|
|描述|注意：在配置BswMRuleTrueActionList时，需要确保列出的动作与系统设计和需求相符；动作列表中的每个动作都必须在BswM配置中定义；在实现时要注意动作执行的顺序和依赖关系，以避免潜在的执行冲突或优先级问题。|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/BswM/BswMConfig/BswMModeControl/BswMActionList|

### 1.3. BswMDataTypeMappingSets

|容器属性|值（容器）|
|---|---|
|名称|BswMDataTypeMappingSets|
|描述|Collection of references to DataTypeMappingSet.|
|描述|概述：BswMDataTypeMappingSets配置项用于定义基本软件模块（BswM）中使用的数据类型与AUTOSAR标准数据类型之间的映射关系，确保数据类型的一致性和兼容性。|
|描述|注意：在配置BswMDataTypeMappingSets时，必须确保映射关系符合AUTOSAR标准中定义的数据类型；不正确的数据类型映射可能导致运行时类型不匹配错误；在多个软件组件或模块之间共享数据时，统一的数据类型映射尤为重要。|
|多实例个数|0 - 1|

|配置项属性|值（外部引用配置项）|
|---|---|
|名称|BswMDataTypeMappingSetRef|
|描述|Reference to DataTypeMappingSet.|
|描述|概述：BswMDataTypeMappingSetRef 配置项用于引用基本软件模块（BswM）中使用的数据类型映射集，确保BswM模块能够正确理解和处理来自其他模块的数据。|
|描述|注意：在配置BswMDataTypeMappingSetRef时，必须确保引用的数据类型映射集与BswM模块所需的数据类型兼容；如果存在多个数据类型映射集，需要选择与BswM模块交互的正确映射集；在AUTOSAR CP 4.4标准中，数据类型映射集的定义应遵循标准的数据类型定义和映射规则。|
|多实例个数|0 - inf|
|目标类型|DATA-TYPE-MAPPING-SET|

### 1.4. BswMModeControl

|容器属性|值（容器）|
|---|---|
|名称|BswMModeControl|
|描述|This container includes all configuration sub-containers and parameters related to the mode control functionality of the BswM.|
|描述|概述：BswMModeControl是AUTOSAR BSW模块管理（BswM）的配置参数，用于定义模式控制接口，这些接口允许BswM模块根据系统或网络的不同模式来控制BSW模块的行为。|
|描述|注意：在配置BswMModeControl时，需要确保其模式请求和模式切换逻辑与系统设计和需求相匹配；此外，应注意模式控制接口的实现必须满足实时性要求；在多模式系统中，还需考虑模式之间的依赖关系和切换策略。|
|多实例个数|1 - 1|

#### 1.4.1. BswMAction

|容器属性|值（容器）|
|---|---|
|名称|BswMAction|
|描述|Each container of this type defines an action. These actions can be part of one or several action lists.|
|描述|概述：BswMAction配置项定义了基本软件模块管理（BswM）中的动作，这些动作是在满足特定条件时由BswM触发的，用于控制和管理基础软件模块及其通信。|
|描述|注意：在配置BswMAction时，需要确保动作的定义与系统需求相匹配，避免配置错误导致系统行为不符预期；BswMAction的触发条件需明确，以确保系统的可靠性和稳定性；AUTOSAR CP 4.4标准中对BswMAction的属性和行为有详细规定，需遵循这些规定以保证兼容性。|
|多实例个数|0 - 4294967295|

##### 1.4.1.1. BswMAvailableActions

|容器属性|值（容器）|
|---|---|
|名称|BswMAvailableActions|
|描述|Choice container including the available actions to be used in the action lists.|
|描述|概述：BswMAvailableActions配置项定义了基本软件模块（BswM）可以执行的动作列表，这些动作根据系统状态或事件进行触发，以实现系统的模式管理和控制逻辑。|
|描述|注意：动作类型必须与BswM的模式管理逻辑一致，确保配置的动作可由BswM管理；动作定义需遵循AUTOSAR CP 4.4标准中对BswMAvailableActions的规范；在定义动作时，考虑系统的实时性和资源限制，避免配置过于复杂的动作导致系统性能下降。|
|多实例个数|1 - 1|

###### 1.4.1.1.1. BswMClearEventRequest

|容器属性|值（容器）|
|---|---|
|名称|BswMClearEventRequest|
|描述|This container contains a reference to a BswMEventRequestPort which will be cleared (i.e. set to CLEAR state) when this action is executed.|
|描述|概述：BswMClearEventRequest 用于清除在基本软件模块中设置的事件，这有助于管理事件触发的任务和中断。|
|描述|注意：在配置时需确保正确的事件标识符与对应的模块关联，避免错误清除可能导致系统行为不可预测；此配置项应与BswMEvent配置保持一致，确保系统的稳定性和可靠性。|
|多实例个数|0 - 1|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|BswMClearEventRequestPortRef|
|描述|This parameter references the BswMEventRequestPort which will be cleared.|
|描述|概述：BswMClearEventRequestPortRef配置项用于指定基础软件模块（BswM）清除特定事件请求的端口引用，以便于BswM管理和控制事件状态。|
|描述|注意：确保引用的端口正确对应于需要清除事件请求的事件；在配置时需注意与BswM的其他配置项的一致性和兼容性；此配置项在AUTOSAR CP 4.4标准中应确保与BswM的事件管理机制兼容。|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/BswM/BswMConfig/BswMArbitration/BswMEventRequestPort|

###### 1.4.1.1.2. BswMComMAllowCom

|容器属性|值（容器）|
|---|---|
|名称|BswMComMAllowCom|
|描述|This container includes all parameters for the action to allow or to block communication for a ComM Channel. ComM_CommunicationAllowed is called when this action is configured.|
|描述|概述：BswMComMAllowCom 配置项用于管理通信管理器（ComM）的通信授权，允许或禁止网络通信。|
|描述|注意：确保该配置与车辆的网络管理策略一致；在实施时应考虑系统的安全性和隐私要求；该配置项应与其他BswM模式管理配置项协同工作，以确保系统行为的一致性。|
|多实例个数|0 - 1|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|BswMComAllowed|
|描述|The parameter BswMComMAllowChannelRef refers to a channel which will allow or block communication using the function ComM_CommunicationAllowed().|
|描述|概述：BswMComAllowed 是一个配置参数，用于控制基本软件模块管理（BswM）对通信管理模块（ComM）的控制权限，允许或禁止通信。|
|描述|注意：在配置BswMComAllowed时，需要确保它与系统的通信需求相匹配；此配置项对系统的通信管理有直接影响，因此应谨慎处理；在AUTOSAR CP 4.4标准中，应检查此配置项的属性是否与标准定义的数据类型和使用约束一致。|
|说明|This parameter corresponds to the parameter "Allowed" of the function ComM_CommunicationAllowed().|
|多实例个数|1 - 1|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|BswMComMAllowChannelRef|
|描述|This is a reference to the ComM Channel for which communication shall be allowed or blocked.|
|描述|概述：BswMComMAllowChannelRef是一个配置参数，用于将BswM模块中的通信管理逻辑与特定的ComM通道相关联，从而允许BswM根据ComM通道的状态改变来执行相应的管理逻辑。|
|描述|注意：在配置BswMComMAllowChannelRef时，必须确保引用的ComM��道已经在系统中定义并且有效；此配置项的正确性对于BswM模块能否正确响应ComM通道状态变化至关重要；在AUTOSAR CP 4.4标准中，应当遵循模块间的接口和数据交换规范来配置此参数。|
|说明|This reference corresponds to the parameter "Channel" of the function ComM_CommunicationAllowed().|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/ComM/ComMConfigSet/ComMChannel|

###### 1.4.1.1.3. BswMComMModeLimitation

|容器属性|值（容器）|
|---|---|
|名称|BswMComMModeLimitation|
|描述|This container includes all parameters related to a limitation of communication mode for a ComM Channel. ComM_LimitChannelToNoComMode is called when this action is configured.|
|描述|概述：BswMComMModeLimitation配置项用于定义车辆通信管理器（ComM）的模式限制，这些限制由基础软件模块管理器（BswM）根据车辆的不同状态来控制。|
|描述|注意：在配置BswMComMModeLimitation时，需要确保它与系统中其他BswM配置项的依赖关系和优先级设置相协调；此外，应当考虑到不同ECU上的ComM模式限制可能会有所不同，因此需要根据具体的应用场景进行配置；最后，要确保配置的模式限制符合AUTOSAR CP 4.4标准中对于BswM模块的要求和规范。|
|多实例个数|0 - 1|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|BswMComMLimitMode|
|描述|The function ComM_LimitChannelToNoComMode() takes in this boolean parameter to limit the channel's com mode to no-com mode.|
|描述|概述：BswMComMLimitMode配置项用于定义通信管理模块（ComM）在网络管理策略中的限制模式，控制网络通信资源的使用，以满足不同的网络带宽和能耗要求。|
|描述|注意：在配置BswMComMLimitMode时，需要确保其设置与系统的网络管理策略一致；此配置项对系统的通信效率和资源使用有直接影响，需谨慎设置；AUTOSAR CP 4.4标准中对于网络管理的配置和策略提供了详细的指导，建议仔细阅读相关章节以确保配置的正确性。|
|说明|This parameter corresponds to the parameter "Status" of the function ComM_LimitChannelToNoComMode.|
|多实例个数|1 - 1|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|BswMComMLimitChannelRef|
|描述|This is a reference to the ComM channel for which the communication mode should be limited.|
|描述|概述：BswMComMLimitChannelRef 配置项用于引用通信管理器（ComM）中定义的通道限制，这样BSW管理器（BswM）可以根据这些限制来管理BSW模块的行为。|
|描述|注意：在配置BswMComMLimitChannelRef时，需要确保引用的ComM通道确实存在且已被定义；此外，BswM模块的配置应与ComM模块的配置保持一致，以确保通信管理的正确性；在AUTOSAR CP 4.4标准中，任何对BswMComMLimitChannelRef的修改都应当通过标准的配置工具来进行，以避免手动错误。|
|说明|This reference corresponds to the parameter "Channel" of the function ComM_LimitChannelToNoComMode.|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/ComM/ComMConfigSet/ComMChannel|

###### 1.4.1.1.4. BswMComMModeSwitch

|容器属性|值（容器）|
|---|---|
|名称|BswMComMModeSwitch|
|描述|This container includes all parameters related to a switch of communication mode for a ComM User. ComM_RequestComMode is called when this action is configured.|
|描述|概述：BswMComMModeSwitch 配置项用于定义基本软件模块管理器（BswM）如何根据通信管理器（ComM）的模式变化来切换其管理的不同模式。这允许BswM根据网络管理需求来控制ECU内部的行为。|
|描述|注意：在配置时，需要确保BswM模块能够正确识别和响应ComM模式变化的通知；BswM的模式切换逻辑应与系统的通信需求和依赖关系相匹配；在AUTOSAR CP 4.4标准中，应当遵循相关的模式管理接口和通信协议规范来实现此配置项。|
|多实例个数|0 - 1|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|BswMComMRequestedMode|
|描述|This parameter specifies if the requested communication mode.|
|描述|概述：BswMComMRequestedMode 是一个配置参数，用于定义基本软件模块管理（BswM）如何根据通信管理器（ComM）的状态请求来控制网络管理器（Nm）的状态。|
|描述|注意：在配置BswMComMRequestedMode时，需要确保其值与ComM和Nm模块的状态机和模式切换逻辑相匹配；此配置项的设置应考虑系统的通信需求和节能策略；在AUTOSAR CP 4.4标准中，应当遵循模块间接口定义和模式管理规范，以确保正确的模式转换和系统行为。|
|说明|This parameter corresponds to the parameter "ComMode" of the function ComM_RequestComMode.|
|多实例个数|1 - 1|
|默认值|BSWM_COMM_FULL_COMMUNICATION|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|BswMComMUserRef|
|描述|This is a reference to the ComM User that is associated to the Communication channel for which the communication mode should be requested.|
|描述|概述：BswMComMUserRef 是一个配置项，用于在BswM（基础软件模块管理器）中引用ComM（通信管理器）用户，以便BswM可以根据ComM用户的状态来管理和调整基础软件模块的行为。|
|描述|注意：在配置BswMComMUserRef时，需要确保引用的ComM用户已经在系统中定义；BswM模块需要正确处理ComM用户状态的变化，以便实现预期的管理逻辑；在AUTOSAR CP 4.4标准中，确保使用正确的引用机制和数据类型，以符合标准规范。|
|说明|This reference corresponds to the parameter "User" of the function ComM_RequestComMode.|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/ComM/ComMConfigSet/ComMUser|

###### 1.4.1.1.5. BswMCoreHaltMode

|容器属性|值（容器）|
|---|---|
|名称|BswMCoreHaltMode|
|描述|This container includes all parameters related to a switch of the activation state of core Halt.|
|描述|概述：BswMCoreHaltMode 配置项用于定义基本软件模块（BswM）在系统核心（Core）发生故障时的行为模式，通常涉及到系统的安全停机策略。|
|描述|注意：在配置BswMCoreHaltMode时，需要确保该行为与系统的安全需求和故障管理策略相符合；此配置项的设置必须考虑到所有相关核心的故障处理机制；在多核系统中，还需注意核间的故障传播和处理一致性。|
|多实例个数|0 - 1|

|配置项属性|值（字符串参数配置项）|
|---|---|
|名称|BswMCoreHaltActivationState|
|描述|Different possibilities are offered depending on the OS implementation and the CPU HW. The HALT modes addressed by this parameter are defined as names (strings) in the OS implementation. Different implementation may implement different HALT modes and subsequently different names.|
|描述|概述：BswMCoreHaltActivationState配置项用于定义基本软件模块管理（BswM）在系统核心（Core）停止或挂起时的激活状态，控制系统在特定条件下的行为。|
|描述|注意：在配置时需确保该状态与系统的安全需求相匹配；不同的硬件平台可能会对此配置项的支持有所不同，需仔细检查硬件兼容性；在多核系统中，每个核心的配置可能需要独立设置，以确保系统的稳定性和安全性。|
|多实例个数|1 - 1|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|BswMTargetCoreRef|
|描述|This is a reference to the core on which the Core Halt process must be influenced.|
|描述|概述：BswMTargetCoreRef 配置项用于指定基本软件模块（BswM）应当运行在哪一个处理器核心上，这有助于实现多核处理器上的软件分配和优化。|
|描述|注意：在多核系统设计中，必须确保BswMTargetCoreRef正确指向期望的核心，以避免资源竞争和性能问题；AUTOSAR CP 4.4标准要求对多核支持进行明确的配置，因此该属性应与系统设计和分区策略相一致；在配置时还需考虑与其他模块的依赖关系和核心间通信机制。|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/EcuC/EcucHardware/EcucCoreDefinition|

###### 1.4.1.1.6. BswMDeadlineMonitoringControl

|容器属性|值（容器）|
|---|---|
|名称|BswMDeadlineMonitoringControl|
|描述|This container includes all parameters related to enabling and disabling of deadline monitoring for one or several PDUs in COM.|
|描述|概述：BswMDeadlineMonitoringControl配置项用于控制基本软件模块（BswM）中的截止时间监控功能，允许开启或关闭特定模块或组件的截止时间监控。|
|描述|注意：在AUTOSAR CP 4.4标准中，确保在系统设计阶段明确哪些组件需要截止时间监控，以避免不必要的性能开销；配置时需考虑系统的实时性要求和资源限制；不正确的配置可能导致系统运行不稳定或不满足实时性要求。|
|多实例个数|0 - 1|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|BswMDisabledDMPduGroupRef|
|描述|This is a reference to a PDU Group for which the Deadline Monitoring should be disabled.|
|描述|概述：BswMDisabledDMPduGroupRef 配置项用于引用在BswM模块中被禁用的诊断消息PDU组。|
|描述|注意：在配置BswMDisabledDMPduGroupRef时，必须确保引用的PDU组在系统中存在且有效；此配置项通常与诊断通信管理相关，确保正确配置以避免诊断通信问题；在AUTOSAR CP 4.4标准中，应当遵循模块间的依赖关系和初始化顺序，以保证系统的稳定性。|
|说明|This reference corresponds to the parameter "IpduGroupId" of the function Com_DisableReceptionDM.|
|多实例个数|0 - 4294967295|
|目标引用项的路径|/AUTOSAR/EcucDefs/Com/ComConfig/ComIPduGroup|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|BswMEnabledDMPduGroupRef|
|描述|This is a reference to a PDU Group for which the Deadline Monitoring should be enabled.|
|描述|概述：BswMEnabledDMPduGroupRef是一个配置项，用于引用使能诊断通信的PDU组，这样BswM（Basis Software Module）可以管理这些PDU组的使能状态。|
|描述|注意：在配置BswMEnabledDMPduGroupRef时，需要确保引用的PDU组在系统中已定义且有效；此配置项通常与诊断通信管理相关，因此需要与DiagComM或相应的诊断管理模块协调；在AUTOSAR CP 4.4标准中，确保该配置项的使用符合BswM模块的规范要求。|
|说明|This reference corresponds to the parameter "IpduGroupId" of the function Com_EnableReceptionDM.|
|多实例个数|0 - 4294967295|
|目标引用项的路径|/AUTOSAR/EcucDefs/Com/ComConfig/ComIPduGroup|

###### 1.4.1.1.7. BswMEcuMDriverInitListBswM

|容器属性|值（容器）|
|---|---|
|名称|BswMEcuMDriverInitListBswM|
|描述|This container defines the action to trigger an EcuM driver initialization list.|
|描述|概述：BswMEcuMDriverInitListBswM 配置项用于定义ECU管理模块（BswM）在系统启动时初始化驱动程序的顺序和列表。|
|描述|注意：确保初始化顺序符合系统依赖性和启动策略要求；不正确的驱动初始化顺序可能导致系统启动失败或运行不稳定；该配置应与硬件抽象层和其他底层管理模块的配置保持一致。|
|多实例个数|0 - 1|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|BswMEcuMDriverInitListBswMRef|
|描述|This is a reference to the EcuM EcuMDriverInitListBswM container which represents the driver init list to be triggered.|
|描述|概述：BswMEcuMDriverInitListBswMRef 配置项用于指定在ECU管理模块初始化期间需要调用的BswM模块的驱动初始化列表。|
|描述|注意：在配置时，需要确保引用的BswM驱动初始化列表与实际的BswM配置相匹配；此配置项通常由工具自动生成，手动修改时应谨慎以避免初始化顺序错误；在多驱动系统中，正确的初始化顺序对系统稳定性和启动时间至关重要。|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/EcuM/EcuMConfiguration/EcuMFlexConfiguration/EcuMDriverInitListBswM|

###### 1.4.1.1.8. BswMEcuMGoDownHaltPoll

|容器属性|值（容器）|
|---|---|
|名称|BswMEcuMGoDownHaltPoll|
|描述|This container defines the action to trigger the EcuM_GoDownHaltPoll from BswM.|
|描述|概述：BswMEcuMGoDownHaltPoll是一个配置项，用于定义基础软件模块（BswM）在ECU管理器（EcuM）状态机中GoDown状态的轮询行为，以便在系统需要关闭时进行必要的轮询检查。|
|描述|注意：在AUTOSAR CP 4.4标准中，确保此配置项与ECU的低功耗管理策略相匹配；正确配置此项以避免在系统关闭过程中的不必要延迟；此配置项的使用应结合具体的硬件和系统需求来考虑，以确保系统的快速且安全的关闭。|
|多实例个数|0 - 1|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|BswMEcuMUserIdRef|
|描述|This is a reference to a EcuM UserId.|
|描述|概述：BswMEcuMUserIdRef是一个配置项，用于将基本软件模块（BswM）的用户定义的标识符与ECU管理模块（EcuM）中定义的用户标识符进行关联，以便在系统启动或运行时进行相应的模式管理和控制。|
|描述|注意：确保BswMEcuMUserIdRef正确映射到EcuM定义的用户标识符，避免配置错误导致系统行为不符合预期；该配置项的使用需要根据实际的系统需求和设计来决定，不是所有系统都需要配置此项；在AUTOSAR CP 4.4中，对于用户标识符的定义和使用有明确的规范，需要仔细遵守以保证系统的兼容性和可维护性。|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/EcuM/EcuMConfiguration/EcuMFlexConfiguration/EcuMFlexUserConfig|

###### 1.4.1.1.9. BswMEcuMSelectShutdownTarget

|容器属性|值（容器）|
|---|---|
|名称|BswMEcuMSelectShutdownTarget|
|描述|This container defines the shutdown target.|
|描述|概述：BswMEcuMSelectShutdownTarget配置项用于定义ECU管理模块（EcuM）在系统请求关闭时选择的关机目标状态，这决定了系统在关闭过程中将要进入的具体低功耗或关机状态。|
|描述|注意：在配置时需确保所选的关机目标状态与系统的低功耗需求和硬件支持相匹配；不同的关机目标可能需要不同的唤醒源配置；AUTOSAR CP 4.4标准中，确保该配置与EcuM的状态管理和唤醒逻辑兼容。|
|多实例个数|0 - 1|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|BswMEcuMShutdownTarget|
|描述|This parameter contains the shutdown target that the BswM selects at the EcuM.|
|描述|概述：BswMEcuMShutdownTarget配置项定义了ECU管理模块（EcuM）在系统关闭过程中应达到的目标状态，这有助于确保系统按照预定的顺序安全地关闭。|
|描述|注意：在配置BswMEcuMShutdownTarget时，必须确保所选目标状态与系统的安全需求和功耗需求相匹配；此配置项在系统设计阶段需要特别注意，以避免在实际操作中引发系统不稳定；AUTOSAR CP 4.4标准中对于关闭目标的定义可能与早期版本有所不同，需要根据最新标准进行配置。|
|多实例个数|1 - 1|
|默认值|BSWM_ECUM_SHUTDOWN_TARGET_OFF|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|BswMEcuMResetModeRef|
|描述|This is a reference to a reset mode.|
|描述|概述：BswMEcuMResetModeRef配置项用于指定基本软件模块（BswM）中ECU管理模块（EcuM）定义的重置模式引用，以便在特定条件下控制ECU的重置行为。|
|描述|注意：确保引用的EcuM重置模式与实际的系统重置策略相匹配；在配置时需注意与其他模块的依赖关系和交互；该配置项在AUTOSAR CP 4.4中应与EcuM模块的定义严格一致，避免不一致导致的系统行为异常。|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/EcuM/EcuMConfiguration/EcuMFlexConfiguration/EcuMResetMode|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|BswMEcuMSleepModeRef|
|描述|This is a reference to a sleep mode.|
|描述|概述：BswMEcuMSleepModeRef 配置项用于引用ECU管理模块中定义的睡眠模式，这样基础软件模块可以知道何时以及如何进入低功耗状态。|
|描述|注意：确保引用的睡眠模式与ECU支持的低功耗状态相匹配；在配置时应考虑ECU的硬件能力和所需的唤醒事件；AUTOSAR CP 4.4标准中，BswMEcuMSleepModeRef应正确指向EcuM配置中定义的SleepMode。|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/EcuM/EcuMConfiguration/EcuMCommonConfiguration/EcuMSleepMode|

###### 1.4.1.1.10. BswMEcuMStateSwitch

|容器属性|值（容器）|
|---|---|
|名称|BswMEcuMStateSwitch|
|描述|This container defines the action to switch a State of the ECU State Manager.|
|描述|概述：BswMEcuMStateSwitch配置项用于定义基本软件模块（BswM）与ECU管理模块（EcuM）之间的状态转换逻辑，确保系统在不同操作模式下正确切换状态。|
|描述|注意：在配置BswMEcuMStateSwitch时，需要确保所有的状态转换逻辑与系统的实际需求相匹配；对于不同的ECU状态，如睡眠、唤醒等，需要明确指定相应的BswM行为；AUTOSAR CP 4.4标准中对状态管理有详细规定，确保配置符合标准要求。|
|多实例个数|0 - 1|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|BswMEcuMState|
|描述|This parameter corresponds to the parameter "State" of the function EcuM_ SetState ().|
|描述|概述：BswMEcuMState 配置项定义了基本软件模块EcuM（ECU管理模块）的状态管理，它规定了ECU在启动、运行和关机等不同阶段的状态。|
|描述|注意：在配置BswMEcuMState时，需要确保状态转换的逻辑与AUTOSAR CP 4.4标准中定义的EcuM状态机一致；状态转换条件需要明确，避免歧义或不确定性；此外，应当注意与其他BswM模块的交互，确保状态管理的一致性和正确性。|
|多实例个数|1 - 1|
|默认值|BSWM_ECUM_STATE_APP_RUN|

###### 1.4.1.1.11. BswMEthIfSwitchPortGroupRequestMode

|容器属性|值（容器）|
|---|---|
|名称|BswMEthIfSwitchPortGroupRequestMode|
|描述|This container includes all parameters related to requesting a mode for the EthIfSwtPortGroup.|
|描述|概述：BswMEthIfSwitchPortGroupRequestMode配置项用于定义以太网交换机端口组的请求模式，这涉及到网络管理和端口组状态的控制。|
|描述|注意：在AUTOSAR CP 4.4标准中，网络管理配置需要符合通信堆栈的要求；确保端口组请求模式与实际硬件和网络管理策略相匹配；在配置时应参考相关的以太网驱动模块和网络管理模块的规范。|
|说明|The EthIf_SwitchPortGroupRequestMode API is called when this action is executed.|
|多实例个数|0 - 1|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|BswMEthTrcvMode|
|描述|This parameter contains the mode which will be requested.|
|描述|概述：BswMEthTrcvMode配置项定义了基本软件模块（BswM）中以太网收发器（EthTrcv）的模式管理，用于控制以太网收发器的不同操作模式。|
|描述|注意：在配置BswMEthTrcvMode时，需要确保模式与以太网收发器支持的实际模式相匹配；此外，应当注意BswM模块与EthTrcv模块之间的接口匹配和通信协议一致性；在AUTOSAR CP 4.4标准中，应遵循相关规范来配置模式管理，以确保系统的稳定性和可靠性。|
|多实例个数|1 - 1|
|默认值|BSWM_ETHTRCV_MODE_ACTIVE|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|BswMEthIfSwitchPortGroupRef|
|描述|This is a reference to the Ethernet Interface Switch Port Group which will receive the request.|
|描述|概述：BswMEthIfSwitchPortGroupRef 配置项用于引用以太网交换机端口组，它定义了基本软件模块以太网接口（BswMEthIf）与特定交换机端口组之间的关联。|
|描述|注意：在配置时需确保引用的交换机端口组在系统中存在且有效；此配置项对于实现网络管理和以太网交换功能至关重要；在AUTOSAR CP 4.4标准中，应当遵循相关网络配置规范，确保配置的一致性和正确性。|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/EthIf/EthIfConfigSet/EthIfSwitchPortGroup|

###### 1.4.1.1.12. BswMFrSMAllSlots

|容器属性|值（容器）|
|---|---|
|名称|BswMFrSMAllSlots|
|描述|This container includes all parameter(s) for the action to request an exit from Flexray KeySlotOnlyMode. FrSM_AllSlots is called when this action is executed.|
|描述|概述：BswMFrSMAllSlots配置项用于定义BswM模块如何管理FlexRay通信控制器的状态机，特别是在所有槽位（Slots）中的行为。|
|描述|注意：在配置BswMFrSMAllSlots时，需要确保与FlexRay网络的实际配置和需求相匹配；此配置项对于确保网络的稳定性和性能至关重要；在AUTOSAR CP 4.4标准中，对于FlexRay通信的管理有详细规范，需要遵循这些规范以保证兼容性。|
|多实例个数|0 - 1|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|BswMFrSMAllSlotsNetworkHandleRef|
|描述|This references the FlexRay cluster. The reference corresponds to the parameter "NetworkHandle" of the function FrSM_AllSlots.|
|描述|概述：BswMFrSMAllSlotsNetworkHandleRef配置项用于指定某个FlexRay网络通信控制器的网络句柄引用，以便BswM（基础软件模块管理器）可以管理和监视所有FlexRay通信槽的状态。|
|描述|注意：该配置项需要确保正确引用FlexRay网络控制器的唯一标识符；在配置时需注意与实际硬件和网络拓扑的一致性；AUTOSAR CP 4.4标准中，对于FlexRay网络管理的配置要求严格，确保配置的准确性对系统的稳定性和性能至关重要。|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/ComM/ComMConfigSet/ComMChannel|

###### 1.4.1.1.13. BswMJ1939DcmStateSwitch

|容器属性|值（容器）|
|---|---|
|名称|BswMJ1939DcmStateSwitch|
|描述|This container includes all parameters related to a switch of the J1939 Diagnostic Communication Managers network state for a J1939 node. J1939Dcm_SetState is called when this action is configured.|
|描述|概述：BswMJ1939DcmStateSwitch 配置项用于定义基于J1939协议的诊断控制模块（DCM）在不同状态下的行为和状态转换。|
|描述|注意：此配置项必须确保与车辆的J1939协议和诊断需求相匹配；状态转换逻辑应清晰，避免在实际应用中造成状态机错误；在配置时应考虑系统的安全和诊断策略。|
|多实例个数|0 - 1|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|BswMJ1939DcmRequestedState|
|描述|This parameter describes the communication state of the J1939 Diagnostic Communication Manager and corresponds to the parameter "newState" of the function J1939Dcm_SetState.|
|描述|概述：BswMJ1939DcmRequestedState 配置项用于定义诊断通信管理器（DCM）在J1939网络上请求的状态，这通常涉及到控制单元之间的诊断会话控制。|
|描述|注意：在配置BswMJ1939DcmRequestedState时，需要确保它与所使用的J1939诊断协议栈兼容，并且符合AUTOSAR CP 4.4标准中对于诊断会话控制的规定；此外，应当注意该配置项对于网络管理和诊断服务的影响，确保它不会与其他网络参与者的状态请求发生冲突；最后，由于J1939是基于CAN总线的协议，还应考虑到网络带宽和优先级分配等因素。|
|多实例个数|1 - 1|
|默认值|BSWM_J1939DCM_STATE_OFFLINE|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|BswMJ1939DcmChannelRef|
|描述|This reference points to the unique channel defined by the ComMChannel and provides access to the unique channel index value in ComMChannelId.|
|描述|概述：BswMJ1939DcmChannelRef配置项用于指定诊断通信管理器（DCM）模块中J1939通道的引用，确保DCM能够正确地与J1939网络上的节点进行通信。|
|描述|注意：在配置BswMJ1939DcmChannelRef时，需要确保引用的J1939通道已在系统中定义并正确配置；此配置项必须与系统中实际的J1939网络结构相匹配；在AUTOSAR CP 4.4标准中，确保该配置项的使用与标准规定的通信管理器的接口和行为一致。|
|说明|This reference corresponds to the parameter "channel" of the function J1939Dcm_SetState.|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/ComM/ComMConfigSet/ComMChannel|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|BswMJ1939DcmNodeRef|
|描述|This reference points to a J1939NmNode and provides access to the unique J1939NmNodeId.This reference corresponds to the parameter "node" of the function J1939Dcm_SetState.|
|描述|概述：BswMJ1939DcmNodeRef 配置项用于定义诊断通信管理器（DCM）在J1939网络中的节点引用，确保DCM能够正确地与其他节点进行通信。|
|描述|注意：在配置BswMJ1939DcmNodeRef时，需要确保引用的节点已在系统中定义且与实际的网络拓扑相匹配；此配置项应与网络管理和地址分配机制兼容；在AUTOSAR CP 4.4标准中，确保该配置项的使用与标准定义的网络层配置参数一致。|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/J1939Nm/J1939NmConfigSet/J1939NmNode|

###### 1.4.1.1.14. BswMJ1939RmStateSwitch

|容器属性|值（容器）|
|---|---|
|名称|BswMJ1939RmStateSwitch|
|描述|This container includes all parameters related to a switch of the J1939 Request Managers network state for a J1939 node. J1939Rm_SetState is called when this action is configured.|
|描述|概述：BswMJ1939RmStateSwitch 配置项用于定义基本软件模块J1939路由管理器（J1939Rm）的状态切换逻辑，控制J1939网络管理通信和节点状态。|
|描述|注意：在配置时需确保状态切换逻辑与系统需求和J1939协议标准一致；AUTOSAR CP 4.4标准中可能对J1939Rm的实现和配置有具体要求，需要遵循这些要求；在多节点系统中，应考虑节点间的交互和状态同步，以保证网络管理的正确性。|
|多实例个数|0 - 1|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|BswMJ1939RmRequestedState|
|描述|This parameter describes the communication state of the J1939 Request Manager and corresponds to the parameter "new state" of the function J1939Rm_SetState.|
|描述|概述：BswMJ1939RmRequestedState 配置项用于定义BSW模块J1939 Request Manager的请求状态，这通常涉及到网络管理和诊断请求的处理。|
|描述|注意：在配置时需确保该状态与系统中其他网络管理配置一致；根据AUTOSAR CP 4.4标准，应检查该配置项是否支持所需的网络管理策略；在多网络环境中，应注意不同网络间状态管理的一致性和冲突避免。|
|多实例个数|1 - 1|
|默认值|BSWM_J1939RM_STATE_OFFLINE|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|BswMJ1939RmChannelRef|
|描述|This reference points to the unique channel defined by the ComMChannel and provides access to the unique channel index value in ComMChannelId.|
|描述|概述：BswMJ1939RmChannelRef 配置项用于指定J1939通信管理模块（J1939Rm）与特定的CAN通道之间的关联。|
|描述|注意：在配置时，必须确保引用的CAN通道已经定义且与J1939Rm模块兼容；如果项目中使用了多个CAN通道，需要为每个使用J1939协议的通道配置相应的BswMJ1939RmChannelRef；AUTOSAR CP 4.4标准中对于J1939通信的配置可能有特定的参数要求，需要根据标准文档进行准确配置。|
|说明|This reference corresponds to the parameter "channel" of the function J1939Rm_SetState.|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/ComM/ComMConfigSet/ComMChannel|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|BswMJ1939RmNodeRef|
|描述|This reference points to a J1939NmNode and provides access to the unique J1939NmNodeId.|
|描述|概述：BswMJ1939RmNodeRef 配置项是用于定义基于J1939网络管理的软件模块（BswM）中节点的引用，确保网络管理策略能够正确地与特定的节点关联。|
|描述|注意：在配置BswMJ1939RmNodeRef时，需要确保引用的节点已经在系统中定义，并且与网络管理策略相匹配；此配置项应与J1939网络管理的其他配置保持一致性；在AUTOSAR CP 4.4标准中，确保使用正确的数据类型和结构来定义节点引用。|
|说明|This reference corresponds to the parameter "node" of the function J1939Rm_SetState.|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/J1939Nm/J1939NmConfigSet/J1939NmNode|

###### 1.4.1.1.15. BswMLinScheduleSwitch

|容器属性|值（容器）|
|---|---|
|名称|BswMLinScheduleSwitch|
|描述|This container includes all parameters related to a switch of LIN schedule table. LinSM_ScheduleRequest is called when this action is configured.|
|描述|概述：BswMLinScheduleSwitch 配置项用于管理LIN通信调度表的切换，允许基于不同的运行时条件动态选择合适的调度表。|
|描述|注意：确保在使用BswMLinScheduleSwitch时，系统中已定义了多个LIN调度表以支持动态切换；此配置项应与LIN驱动的运行状态和事件触发机制紧密协调；在AUTOSAR CP 4.4标准中，此配置项的使用应遵循LIN通信管理模块的规范。|
|说明|The configuration for the "network" parameter can be accessed via the reference LinSMComMNetworkHandleRef contained in the parent container LinSMChannel of the container referenced by BswMLinScheduleRef.|
|多实例个数|0 - 1|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|BswMLinScheduleRef|
|描述|This is a reference to the LIN schedule table that the LIN SM shall change to.|
|描述|概述：BswMLinScheduleRef 是一个配置项，用于指定基本软件模块（BswM）中LIN通信调度表的引用，确保LIN通信调度能够按照预定的策略进行。|
|描述|注意：在配置BswMLinScheduleRef时，需要确保引用的LIN调度表在系统中是存在且有效的；此配置项通常与LIN通信管理和调度策略紧密相关；在多个调度表之间切换时，应考虑切换的时机和条件，以保证通信的连续性和正确性。|
|说明|This reference corresponds to the parameter "schedule" of the function LinSM_ScheduleRequest.|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/LinSM/LinSMConfigSet/LinSMChannel/LinSMSchedule|

###### 1.4.1.1.16. BswMNMControl

|容器属性|值（容器）|
|---|---|
|名称|BswMNMControl|
|描述|This container includes all parameters related to enabling and disabling of Network Management communication. Disabling of NM communication can be requested by DCM.|
|描述|概述：BswMNMControl配置项用于定义网络管理通信控制的行为，它指定了基本软件模块（BswM）如何控制网络管理（NM）模块的状态和行为。|
|描述|注意：在配置BswMNMControl时，需要确保与网络管理策略和需求相匹配；此配置项在AUTOSAR CP 4.4中可能需要与其他网络管理配置项协同工作，以确保网络的正确管理和控制；配置时应注意不同网络通道的特定需求和特性。|
|说明|Nm_EnableCommunication or Nm_DisableCommunication is called when this action is configured.|
|多实例个数|0 - 1|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|BswMNMAction|
|描述|This parameter specifies if the communication of the corresponding NM channel should be enabled or disabled.|
|描述|概述：BswMNMAction配置项用于定义网络管理通信状态机中的动作，这些动作是由网络管理模块在特定条件下执行的，以管理ECU的网络状态。|
|描述|注意：在配置BswMNMAction时，需要确保动作与网络管理状态机的状态和转换逻辑相匹配；此外，应当遵循AUTOSAR CP 4.4标准中对于网络管理动作的定义和约束；在实现时，还需注意不同网络管理硬件和协议的特定要求，以确保动作的正确执行。|
|多实例个数|1 - 1|
|默认值|BSWM_NM_DISABLE|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|BswMComMNetworkHandleRef|
|描述|This reference points to the unique channel defined by the ComMChannel and provides access to the unique channel index value in ComMChannelId.|
|描述|概述：BswMComMNetworkHandleRef配置项用于定义BswM模块与ComM模块之间的网络通道引用，确保BswM可以根据网络状态改变来执行相应的模式切换逻辑。|
|描述|注意：确保每个BswMComMNetworkHandleRef正确映射到一个存在的ComM网络通道；在配置时需考虑网络通道的实际使用情况，避免错误引用；该配置项在AUTOSAR CP 4.4标准中应与网络管理需求紧密相关，确保配置的一致性和准确性。|
|说明|This reference corresponds to the parameter "NetworkHandle" of the function Nm_EnableCommunication and Nm_DisableCommunication.|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/ComM/ComMConfigSet/ComMChannel|

###### 1.4.1.1.17. BswMPduGroupSwitch

|容器属性|值（容器）|
|---|---|
|名称|BswMPduGroupSwitch|
|描述|This container includes references to the PDU groups that shall be enabled and disabled.|
|描述|概述：BswMPduGroupSwitch配置项用于定义基本软件模块PDU组的开关状态，允许控制PDU组的传输或接收功能的启用或禁用。|
|描述|注意：在配置BswMPduGroupSwitch时，需要确保PDU组的定义与系统中的通信需求相匹配；此外，切换PDU组状态时应注意对系统的影响，特别是在动态切换时对通信一致性和实时性的影响；在AUTOSAR CP 4.4标准中，应遵循相关的通信管理规范，确保配置的正确性和兼容性。|
|多实例个数|0 - 1|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|BswMPduGroupSwitchReinit|
|描述|This parameter defines if the data of the I-PDU, the shadow buffers of included signal groups, etc. are reinitialized when a PDU Group is started.|
|描述|概述：BswMPduGroupSwitchReinit配置项用于定义在通信堆栈中，基础软件模块PDU组切换后是否需要重新初始化的行为，确保数据传输的连续性和正确性。|
|描述|注意：在AUTOSAR CP 4.4中，确保在使用此配置项时考虑系统的实时性和安全要求；不恰当的使用可能导致数据一致性问题；此配置项的使用应与系统的通信需求和模块的初始化时间紧密相关。|
|说明|This parameter corresponds to the parameter "initialize" of the function Com_IpduGroupStart.|
|多实例个数|0 - 1|
|默认值|false|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|BswMDisabledPduGroupRef|
|描述|This is a reference to a PDU Group that should be disabled.|
|描述|概述：BswMDisabledPduGroupRef配置项用于引用在BswM模块中被禁用的PDU组，这允许基础软件模块管理器（BswM）控制PDU组的启用或禁用状态。|
|描述|注意：在配置时需要确保引用的PDU组在系统中是存在的；BswM配置必须与PDU组配置保持一致，以避免运行时错误；在AUTOSAR CP 4.4标准中，对PDU组的管理应遵循最新的规范和方法。|
|说明|This reference corresponds to the parameter "IpduGroupId" of the function Com_IpduGroupStop.|
|多实例个数|0 - 4294967295|
|目标引用项的路径|/AUTOSAR/EcucDefs/Com/ComConfig/ComIPduGroup|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|BswMEnabledPduGroupRef|
|描述|This is a reference to a PDU Group that should be enabled.|
|描述|概述：BswMEnabledPduGroupRef 是一个配置参数，用于引用使能的PDU组，这些PDU组由BswM模块管理，用于控制PDU的传输状态。|
|描述|注意：在配置BswMEnabledPduGroupRef时，需要确保引用的PDU组已在PDU路由表中定义；此配置项必须与系统中的通信堆栈配置保持一致；在AUTOSAR CP 4.4标准中，确保BswM模块的配置与通信管理模块的配置相匹配。|
|说明|This reference corresponds to the parameter "IpduGroupId" of the function Com_IpduGroupStart.|
|多实例个数|0 - 4294967295|
|目标引用项的路径|/AUTOSAR/EcucDefs/Com/ComConfig/ComIPduGroup|

###### 1.4.1.1.18. BswMPduRouterControl

|容器属性|值（容器）|
|---|---|
|名称|BswMPduRouterControl|
|描述|This container includes all parameters related to enabling and disabling of routing of Routing Path Groups in the PDU Router. PduR_EnableRouting or PduR_DisableRouting is called when this action is configured.|
|描述|概述：BswMPduRouterControl配置项用于控制基础软件模块（BswM）中PDU路由器的行为，包括启用或禁用特定的PDU通道。|
|描述|注意：在配置BswMPduRouterControl时，确保已定义所有需要路由的PDU通道；不正确的配置可能导致数据传输中断；此配置项在AUTOSAR CP 4.4中应与通信堆栈的其他部分紧密协调，以保证数据的正确路由。|
|多实例个数|0 - 1|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|BswMPduRouterDisableInitBuffer|
|描述|When BswPduRouterAction is set to BSWM_PDUR_DISABLE and this parameter is set to true, then the call to PduR_DisableRouting will be invoked with parameter "initialize" set to true, otherwise false.|
|描述|概述：BswMPduRouterDisableInitBuffer 是一个配置项，用于指定是否在初始化时禁用PDU路由器的缓冲区初始化。|
|描述|注意：在AUTOSAR CP 4.4标准中，通常PDU路由器的缓冲区在初始化时会被清零或设置为默认值，以确保数据的一致性和系统的可靠性；如果选择禁用缓冲区初始化，开发者需要确保这一决策不会导致系统中的数据不一致或其他潜在问题；此配置项的使用应当谨慎，并且在系统设计时充分评估其对系统行为的影响。|
|多实例个数|0 - 1|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|BswMPduRouterAction|
|描述|This parameter specifies if the routing of the corresponding PDU should be enabled or disabled.|
|描述|概述：BswMPduRouterAction配置项定义了基本软件模块之间的PDU路由动作，包括PDU的源和目的模块，以及路由时可能执行的转换或过滤操作。|
|描述|注意：在配置BswMPduRouterAction时，必须确保源和目的模块的兼容性和正确的数据流向；对于可能的转换或过滤操作，需要明确指定操作的类型和条件，确保数据的正确处理；此配置项在AUTOSAR CP 4.4标准中应当遵循PDU路由的相关规范和约束。|
|多实例个数|1 - 1|
|默认值|BSWM_PDUR_DISABLE|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|BswMPduRoutingPathGroupRef|
|描述|This is a reference to the PDU Routing Path Group for which the routing in the PDU Router should be enabled or disabled.|
|描述|概述：BswMPduRoutingPathGroupRef 是一个配置项，用于引用一组PDU路由路径，这些路径定义了基本软件模块如何处理和转发网络上的消息数据单元（PDU）。|
|描述|注意：在配置BswMPduRoutingPathGroupRef时，必须确保引用的PDU路由路径组在系统中是存在且有效的；此配置项通常与网络管理和通信堆栈的配置紧密相关，因此需要与相关网络配置保持一致；在AUTOSAR CP 4.4标准中，确保该配置项的使用符合PDU路由的模块规范和约束。|
|说明|This reference corresponds to the parameter "id" of the function PduR_EnableRouting and PduR_DisableRouting.|
|多实例个数|1 - inf|
|目标引用项的路径|/AUTOSAR/EcucDefs/PduR/PduRRoutingPaths/PduRRoutingPathGroup|

###### 1.4.1.1.19. BswMRteModeRequest

|容器属性|值（容器）|
|---|---|
|名称|BswMRteModeRequest|
|描述|This container defines a mode request that the BswM may send to a SW-C which is acting as a mode-manager. RTE_Write is called when this action is configured.|
|描述|概述：BswMRteModeRequest配置项用于定义基本软件模块（BswM）如何请求运行时环境（RTE）改变模式。这通常涉及到BswM通知RTE切换到不同的功能模式，以便控制软件组件的行为。|
|描述|注意：在配置BswMRteModeRequest时，必须确保所请求的模式与RTE中定义的模式一致；此外，BswM和RTE之间的接口必须正确配置以支持模式请求；最后，考虑到模式管理的实时性要求，应当合理安排模式请求的触发时机。|
|多实例个数|0 - 1|

|配置项属性|值（外部引用配置项）|
|---|---|
|名称|BswMRequestedModeRef|
|描述|This is a foreign reference to the Mode Declaration used for the mode request|
|描述|概述：BswMRequestedModeRef用于引用BSW模块请求的特定模式，允许BSW Mode Manager（BswM）根据这些请求来控制和管理不同BSW模块间的模式切换。|
|描述|注意：确保引用的模式与BSW模块的实际可用模式一致；在配置时考虑模式切换的依赖关系和优先级，以避免死锁或优先级反转问题；该配置项在AUTOSAR CP 4.4中是标准的，但实现方式可能因供应商而异，需参考具体的供应商文档。|
|多实例个数|1 - 1|
|目标类型|MODE-DECLARATION|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|BswMRteModeRequestPortRef|
|描述|This is a reference to a BswMRteModeRequestPort.|
|描述|概述：BswMRteModeRequestPortRef 配置项用于指定基础软件模块（BswM）中的模式请求端口引用，这是BswM与RTE之间交互模式请求的接口。|
|描述|注意：在配置BswMRteModeRequestPortRef时，必须确保引用的端口是存在的且正确配置了模式声明组；此配置项的正确性对于模式管理逻辑至关重要，错误的配置可能导致模式切换失败；在AUTOSAR CP 4.4标准中，应遵循模式管理的规范来配置此项，以保证系统的模式管理功能正常工作。|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/BswM/BswMConfig/BswMModeControl/BswMRteModeRequestPort|

###### 1.4.1.1.20. BswMRteStart

|容器属性|值（容器）|
|---|---|
|名称|BswMRteStart|
|描述|This container defines the action to start the Rte from BswM.|
|描述|概述：BswMRteStart 是一个配置参数，用于指定基本软件模块（BswM）在初始化时调用RTE（Runtime Environment）启动函数的行为。|
|描述|注意：在AUTOSAR CP 4.4标准中，确保BswMRteStart配置与系统启动流程一致；通常此参数由系统生成工具配置，不建议手动修改；配置错误可能导致系统启动时序问题，影响整个软件的初始化和运行。|
|多实例个数|0 - 1|

###### 1.4.1.1.21. BswMRteStop

|容器属性|值（容器）|
|---|---|
|名称|BswMRteStop|
|描述|This container defines the action to stop the Rte from BswM|
|描述|概述：BswMRteStop 是一个配置参数，用于指定基本软件模块（BswM）在系统停止时是否应该通知运行时环境（RTE）。|
|描述|注意：在AUTOSAR CP 4.4标准中，需要确保系统停止过程中的所有通知都能正确配置以保证系统的安全停止；如果系统设计不需要BswM在停止时通知RTE，该配置应设置为不启用；在配置时应考虑系统的安全需求和停止策略。|
|多实例个数|0 - 1|

###### 1.4.1.1.22. BswMRteSwitch

|容器属性|值（容器）|
|---|---|
|名称|BswMRteSwitch|
|描述|This container defines a mode switch indication that the BswM provides to the SW-C that need to be notified about the mode switch. RTE_Switch is called when this action is configured.|
|描述|概述：BswMRteSwitch 是一个配置参数，用于启用或禁用基本软件模块（BswM）与运行时环境（RTE）之间的接口，这影响BswM模块是否可以调用RTE提供的服务。|
|描述|注意：在AUTOSAR CP 4.4标准中，确保在启用BswMRteSwitch时，BswM模块与RTE之间的接口是正确配置的；如果不需要BswM模块与RTE之间的交互，则可以禁用此选项以节省资源；在配置此参数时，应考虑系统的整体架构和模块间的依赖关系。|
|多实例个数|0 - 1|

|配置项属性|值（外部引用配置项）|
|---|---|
|名称|BswMSwitchedMode|
|描述|This parameter contains the integer value that corresponds to a certain mode in a Mode Declaration Group.|
|描述|概述：BswMSwitchedMode配置项用于定义基本软件模块（BswM）在不同模式下的行为，允许基于系统或网络状态的变化动态调整模块的行为。|
|描述|注意：确保每个模式的定义清晰且互斥，避免模式间的冲突；在设计模式切换逻辑时，考虑系统的实时性和稳定性；该配置项在AUTOSAR CP 4.4中是标准的一部分，但实现细节可能因AUTOSAR版本和供应商实现而异。|
|多实例个数|1 - 1|
|目标类型|MODE-DECLARATION|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|BswMRteSwitchPortRef|
|描述|This is a reference to the BswMSwitchPort.|
|描述|概述：BswMRteSwitchPortRef配置项用于指定基础软件模块（BswM）与运行时环境（RTE）之间的交互接口，确保BswM可以通过特定的端口引用与RTE进行通信。|
|描述|注意：该配置项确保了BswM模块与RTE之间的数据交换和控制流的正确性；在配置时需确保引用的端口存在且可用；此配置项对于实现BswM模块的逻辑控制至关重要，需谨慎处理。|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/BswM/BswMConfig/BswMModeControl/BswMSwitchPort|

###### 1.4.1.1.23. BswMSchMSwitch

|容器属性|值（容器）|
|---|---|
|名称|BswMSchMSwitch|
|描述|This container defines a mode switch indication that the BswM provides to the SW-C that need to be notified about the mode switch. SchM_Switch is called when this action is configured.|
|描述|概述：BswMSchMSwitch 是一个配置参数，用于启用或禁用基本软件模块调度管理器（BswMSchM）的功能开关。|
|描述|注意：在配置BswMSchMSwitch时，需要确保它与系统的需求和其他模块的配置相兼容；如果禁用了BswMSchM，那么依赖于调度管理器的功能将无法工作；在修改此配置项之前，应仔细评估对系统行为的影响。|
|多实例个数|0 - 1|

|配置项属性|值（外部引用配置项）|
|---|---|
|名称|BswMSchMModeDeclarationGroupRef|
|描述|This is the reference to a ModeDeclarationGroup to define a ModeDeclarationGroupPrototype in the role BswModuleDescription.providedModeGroup.|
|描述|概述：BswMSchMModeDeclarationGroupRef是一个配置项，用于引用模式声明组，该组定义了基本软件模块（BswM）可以管理的不同模式。|
|描述|注意：确保引用的模式声明组在系统中是唯一定义的；该配置项对于实现模式管理逻辑至关重要，需要仔细配置以避免运行时错误；在AUTOSAR CP 4.4标准中，模式管理的配置和实现应遵循标准的模式声明和管理机制。|
|多实例个数|0 - 1|
|目标类型|MODE-DECLARATION-GROUP|

|配置项属性|值（外部引用配置项）|
|---|---|
|名称|BswMSchMSwitchedMode|
|描述|This parameter contains the integer value that corresponds to a certain mode in a Mode Declaration Group.|
|描述|概述：BswMSchMSwitchedMode配置项用于定义基本软件模块调度管理器（BswMScheduler）中的模式切换逻辑，它指定了在不同模式下，哪些BswMSchedulableEntities应当被激活或停用。|
|描述|注意：在配置BswMSchMSwitchedMode时，必须确保所有参与���式切换的BswMSchedulableEntities已经被正确定义；模式切换逻辑应与系统的功能安全要求相符合；在实现模式切换时，需要考虑切换的原子性和一致性，避免出现中间状态导致的系统不稳定。|
|多实例个数|1 - 1|
|目标类型|MODE-DECLARATION|

###### 1.4.1.1.24. BswMSdClientServiceModeRequest

|容器属性|值（容器）|
|---|---|
|名称|BswMSdClientServiceModeRequest|
|描述|This container includes all parameters related to the selection of an client service of Sd. Sd_ClientServiceSetState is called when this action is configured.|
|描述|概述：BswMSdClientServiceModeRequest配置项用于定义基础软件模块服务（BswM）客户端请求的模式，这些模式请求可以触发BswM来改变内部管理的模式，从而影响系统行为。|
|描述|注意：在配置时需要确保请求的模式与BswM模块定义的模式一致；应当注意模式请求的优先级，以避免不必要的模式冲突；在多客户端环境中，需要协调不同客户端对同一模式的请求。|
|多实例个数|0 - 1|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|BswMSdClientServiceState|
|描述|This parameter specifies if the corresponding client service shall be released or requested.|
|描述|概述：BswMSdClientServiceState 配置项用于定义基本软件模块服务发现客户端的状态，这些状态通常包括请求服务、服务就绪和服务不可用等。|
|描述|注意：在配置BswMSdClientServiceState时，需要确保状态的定义与AUTOSAR CP 4.4标准中的服务发现状态机模型保持一致；状态转换应当遵循标准定义的逻辑和条件；在实现时，应当考虑服务状态变化对系统其他部分的影响，确保系统的稳定性和可靠性。|
|多实例个数|1 - 1|
|默认值|BSWM_SD_CLIENT_SERVICE_RELEASED|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|BswMSdClientMethodsRef|
|描述|This is a reference to a client service in the Sd module.|
|描述|(6, TypeError("'AssertionError' object is not subscriptable"))|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Sd/SdConfig/SdInstance/SdClientService|

###### 1.4.1.1.25. BswMSdConsumedEventGroupModeRequest

|容器属性|值（容器）|
|---|---|
|名称|BswMSdConsumedEventGroupModeRequest|
|描述|This container includes all parameters related to the selection of a consumed EventGroup of Sd. Sd_ConsumedEventGroupSetState is called when this action is configured.|
|描述|概述：BswMSdConsumedEventGroupModeRequest配置项用于定义基础软件模块请求改变某个消费事件组的模式的能力，这通常涉及到服务发现机制中的动态事件组管理。|
|描述|注意：在配置时需确保事件组的模式请求与服务提供者的模式能力相匹配；此配置项在设计服务发现和事件管理策略时尤为重要，需要仔细规划；AUTOSAR CP 4.4中对服务发现和事件组模式管理提供了详细的规范，确保遵循这些规范以保证系统的兼容性和稳定性。|
|多实例个数|0 - 1|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|BswMSdConsumedEventGroupState|
|描述|This parameter specifies if the corresponding consumed event group shall be released or requested.|
|描述|概述：BswMSdConsumedEventGroupState配置项用于定义基本软件模块（BswM）中消费的事件组的状态，这些状态通常用于BswM逻辑中以决定不同的行为。|
|描述|注意：在配置时需确保事件组的状态与实际的系统状态机制相匹配；BswM配置应与通信管理和网络管理模块紧密协调，以确保状态的正确传递和处理；在AUTOSAR CP 4.4标准中，应遵循相关的模块间接口规范和数据类型定义。|
|多实例个数|1 - 1|
|默认值|BSWM_SD_CONSUMED_EVENTGROUP_RELEASED|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|BswMSdConsumedEventGroupRef|
|描述|This is a reference to an eventGroup that is defined within a client service in the Sd module.|
|描述|概述：BswMSdConsumedEventGroupRef 配置项用于指定基本软件模块（BswM）中的一个消费事件组引用，这通常与网络管理或通信管理相关联，用于处理来自其他ECUs的事件通知。|
|描述|注意：在配置时，需要确保引用的事件组与BswM模块的期望行为相匹配；此配置项应与网络配置和通信矩阵保持一致；在AUTOSAR CP 4.4中，确保使用正确的引用格式和数据类型，以避免集成时的兼容性问题。|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Sd/SdConfig/SdInstance/SdClientService/SdConsumedEventGroup|

###### 1.4.1.1.26. BswMSdServerServiceModeRequest

|容器属性|值（容器）|
|---|---|
|名称|BswMSdServerServiceModeRequest|
|描述|This container includes all parameters related to the selection of a server service of Sd. Sd_ServerServiceSetState is called when this action is configured.|
|描述|概述：BswMSdServerServiceModeRequest配置项用于定义基础软件模块服务（BswM）在服务发现（Sd）服务器请求特定服务模式时的行为，确保系统能够根据服务请求调整其运行模式。|
|描述|注意：在配置时需确保服务模式请求与系统中定义的服务模式匹配；此配置项对系统的服务管理策略有直接影响，需谨慎配置；AUTOSAR CP 4.4标准中对服务发现的管理和配置有详细规定，需遵守相关规范。|
|多实例个数|0 - 1|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|BswMSdServerServiceState|
|描述|This parameter specifies if the corresponding server service shall be down or available.|
|描述|概述：BswMSdServerServiceState 配置项用于定义基本软件模块服务发现（Service Discovery）服务器的服务状态，这通常涉及服务的可用性和服务注册的状态。|
|描述|注意：在配置BswMSdServerServiceState时，需要确保状态的定义与系统中服务发现的实际需求相匹配；此配置项应与服务发现策略和服务注册机制紧密结合；在AUTOSAR CP 4.4标准中，务必遵循相关的服务发现规范和约定，以保证服务状态的正确性和一致性。|
|多实例个数|1 - 1|
|默认值|BSWM_SD_SERVER_SERVICE_AVAILABLE|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|BswMSdServerMethodsRef|
|描述|This is a reference to a server service in the Sd module.|
|描述|概述：BswMSdServerMethodsRef配置项用于引用基本软件模块（BswM）中定义的服务发现（Service Discovery）服务器方法，它关联了BswM模块与服务发现的服务器方法实现。|
|描述|注意：在配置BswMSdServerMethodsRef时，需要确保引用的服务器方法与实际实现的服务发现逻辑相匹配；此配置项通常由系统设计者根据系统架构和通信需求进行设置；在多服务环境中，正确的服务方法引用对于服务发现的准确性和效率至关重要。|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Sd/SdConfig/SdInstance/SdServerService|

###### 1.4.1.1.27. BswMSwitchIPduMode

|容器属性|值（容器）|
|---|---|
|名称|BswMSwitchIPduMode|
|描述|This container includes all parameters related to the selection of the transmission mode an I-PDU to be sent by COM. Com_SwitchIpduTxMode is called when this action is configured.|
|描述|概述：BswMSwitchIPduMode配置项用于定义基础软件模块（BswM）如何根据不同的网络管理状态切换IPDU（Protocol Data Unit）的发送或接收模式，以优化网络通信效率和满足不同操作模式下的网络需求。|
|描述|注意：在配置BswMSwitchIPduMode时，需要确保每个IPDU的模式切换逻辑与实际网络管理需求相匹配；此配置项对于网络带宽优化和减少不必要的网络通信非常关键；AUTOSAR CP 4.4标准中，对于IPDU模式切换的具体实现细节有明确规范，需要仔细遵守以保证兼容性和系统的可靠性。|
|多实例个数|0 - 1|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|BswMSwitchIPduModeValue|
|描述|This parameter defines which transmission mode shall be selected during this call.|
|描述|概述：BswMSwitchIPduModeValue 配置项用于定义基本软件模块（BswM）中，IPDU（PDU路由器）模式切换的值，这个值决定了IPDU的传输模式。|
|描述|注意：在配置BswMSwitchIPduModeValue时，需要确保其值与PduR模块中定义的IPDU模式一致；此外，该值通常与ECU状态或网络管理事件相关联，因此需要确保与这些条件的映射正确无误；在AUTOSAR CP 4.4标准中，应当遵循模块间接口定义和数据类型约定，以保证模块间的兼容性和正确的行为。|
|说明|This parameter corresponds to the parameter "Mode" of the function Com_SwitchIpduTxMode.|
|多实例个数|1 - 1|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|BswMSwitchIPduModeRef|
|描述|This is a reference to an I-PDU for which the transmission mode shall be set.|
|描述|概述：BswMSwitchIPduModeRef 配置项用于引用一个或多个IPDU模式，这些模式定义了BswM模块在特定模式下如何管理IPDU（网络数据单元）的发送和接收。|
|描述|注意：在配置BswMSwitchIPduModeRef时，需要确保引用的IPDU模式与BswM模块的模式管理策略相匹配；引用的IPDU模式必须在系统中定义且有效；在AUTOSAR CP 4.4标准中，确保使用正确的数据类型和结构来引用IPDU模式。|
|说明|This reference corresponds to the parameter "PduId" of the function Com_SwitchIpduTxMode.|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Com/ComConfig/ComIPdu|

###### 1.4.1.1.28. BswMTimerControl

|容器属性|值（容器）|
|---|---|
|名称|BswMTimerControl|
|描述|This container includes all parameters for the action to start or to stop a timer.|
|描述|概述：BswMTimerControl配置项用于定义基本软件模块（BswM）中定时器的控制逻辑，包括定时器的启动、停止以及超时时间的设置，以支持基于时间的服务和管理功能。|
|描述|注意：在配置BswMTimerControl时，需要确保定时器的超时时间与系统的实时性要求相匹配；定时器的控制逻辑应避免引入不必要的系统开销；此配置项在AUTOSAR CP 4.4标准中可能未明确定义，需参考具体的BswM模块实现和供应商文档。|
|多实例个数|0 - 1|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|BswMTimerAction|
|描述|Specify the action for the timer. The timer can be started or stopped.|
|描述|概述：BswMTimerAction配置项用于定义基本软件模块中的定时器动作，它指定了当定时器到期时应该执行的回调函数。|
|描述|注意：在配置BswMTimerAction时，需要确保回调函数符合AUTOSAR标准中对定时器到期回调的要求；定时器的精度和分辨率应满足系统的实时性要求；在多任务环境中，应考虑定时器回调的执行上下文和优先级。|
|多实例个数|1 - 1|
|默认值|BSWM_TIMER_START|

|配置项属性|值（浮点型参数配置项）|
|---|---|
|名称|BswMTimerValue|
|描述|Specify the timer value (in seconds) that is used when the timer is started.|
|描述|概述：BswMTimerValue配置项用于定义基础软件模块计时器的时间值，这是一个用于控制或监测时间相关行为的参数。|
|描述|注意：配置成0代表停止timer，该配置项的值需根据实际的时间需求和系统的时钟精度来设定；过小的值可能导致计时器过快溢出，而过大的值可能影响计时精度；在配置时需考虑目标硬件的时钟频率和可用的计时器资源。|
|多实例个数|1 - 1|
|取值范围|0 - Inf|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|BswMTimerRef|
|描述|Specify the Timer for which the timer action shall be executed.|
|描述|概述：BswMTimerRef是一个配置项，用于引用操作系统中定义的定时器，它允许基础软件模块（BswM）使用这些定时器来管理和监控时间相关的行为。|
|描述|注意：在配置BswMTimerRef时，需要确保引用的定时器在操作系统中已经定义并正确配置；此外，定时器的分辨率和范围应满足BswM模块的时间管理需求；在多任务环境中，还需考虑定时器的访问冲突和同步问题。|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/BswM/BswMConfig/BswMArbitration/BswMModeRequestPort/BswMModeRequestSource/BswMTimer|

###### 1.4.1.1.29. BswMTriggerIPduSend

|容器属性|值（容器）|
|---|---|
|名称|BswMTriggerIPduSend|
|描述|This container includes all parameters related to the triggering of an I-PDU to be sent by COM. Com_TriggerIPDUSend is called when this action is configured.|
|描述|概述：BswMTriggerIPduSend配置项用于定义BswM模块何时触发IPDU（即网络数据单元）的发送，这通常与CAN、LIN或其他通信堆栈的交互有关。|
|描述|注意：在配置BswMTriggerIPduSend时，需要确保与通信堆栈的配置相匹配，以避免发送触发不一致的问题；此配置项应与BswM的模式管理和规则检查机制紧密集成，以确保在正确的模式下触发IPDU发送；在AUTOSAR CP 4.4标准中，应当遵循模块间通信接口的定义和规范，以保证系统的可靠性和一致性。|
|多实例个数|0 - 1|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|BswMTriggeredIPduRef|
|描述|This is a reference to an I-PDU that should be triggered for transmission.|
|描述|概述：BswMTriggeredIPduRef是一个配置项，用于在BswM模块中引用一个触发式的IPDU，这样BswM可以根据IPDU的发送或接收来决定执行特定的模式切换逻辑。|
|描述|注意：在配置BswMTriggeredIPduRef时，需要确保所引用的IPDU确实是触发式的，并且与BswM模块的模式切换逻辑相匹配；此外，引用的IPDU必须在系统中存在且正确配置，以保证BswM的正确运行；在AUTOSAR CP 4.4标准中，应当遵循相关的模块间通信和数据交换原则，确保数据的一致性和模块的协同工作。|
|说明|This reference corresponds to the parameter "PduId" of the function Com_TriggerIPDUSend.|
|多实例个数|1 - inf|
|目标引用项的路径|/AUTOSAR/EcucDefs/Com/ComConfig/ComIPdu|

###### 1.4.1.1.30. BswMUserCallout

|容器属性|值（容器）|
|---|---|
|名称|BswMUserCallout|
|描述|This container includes all details needed for a user defined function call.|
|描述|概述：BswMUserCallout配置项用于定义BswM模块中用户自定义的回调函数，这些回调函数可以在BswM的不同决策点被调用，以执行特定的用户定义行为。|
|描述|注意：用户定义的回调函数需要遵循AUTOSAR标准中定义的特定原型；确保回调函数的执行时间尽可能短，避免影响系统的实时性；在配置BswMUserCallout时，应确保回调函数与BswM模块的交互不会引入任何不确定性或安全风险。|
|多实例个数|0 - 1|

|配置项属性|值（字符串参数配置项）|
|---|---|
|名称|BswMUserCalloutFunction|
|描述|This parameter specifies the complete function call including all parameters. The parameters are specified during configuration time, and cannot be changed during run time. Any return values passed by the callout will be ignored.|
|描述|概述：BswMUserCalloutFunction配置项用于定义BswM（Basis Software Module Management）模块在执行模式切换前后调用的用户自定义函数，允许在模式切换的过程中加入特定的用户逻辑。|
|描述|注意：用户定义的回调函数需要遵循AUTOSAR规范中定义的函数原型和调用约定；确保回调函数的执行时间尽可能短，避免影响系统的实时性；在配置时需确保函数的可靠性和安全性，避免引入系统不稳定因素。|
|说明|Example usage can be: Actions to initialize other BSW modules Action to call NvM_ReadAll() Action to call NvM_WriteAll()|
|多实例个数|1 - 1|

#### 1.4.2. BswMActionList

|容器属性|值（容器）|
|---|---|
|名称|BswMActionList|
|描述|Each instance of this container defines an action list that is invoked based on the BswM Rules. An action list contains a list of numbered action items to be processed. An action list can also include other action lists.|
|描述|概述：BswMActionList是AUTOSAR BSW模块管理器（BswM）的配置参数，用于定义一系列的动作（Actions），这些动作在满足特定的逻辑表达式后将被执行。|
|描述|注意：在配置BswMActionList时，需要确保动作列表中的动作与对应的模式请求和决策逻辑相匹配；动作列表中的每个动作都应该有明确的执行条件和顺序；在配置动作时，应注意不同动作之间的依赖关系和潜在的资源冲突。|
|多实例个数|0 - 4294967295|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|BswMActionListExecution|
|描述|This parameter controls if the corresponding action list shall be executed every time the rule is evaluated or only when the result of the evaluation changes. This parameter does not have an effect when this action list is executed within another action list.|
|描述|概述：BswMActionListExecution配置项用于定义基本软件模块管理（BswM）中的动作列表执行属性，这些属性决定了动作列表在特定条件下的执行时机和行为。|
|描述|注意：在配置BswMActionListExecution时，需要确保动作列表与触发它们的模式请求之间的关系正确无误；此外，应当注意动作列表的执行优先级，以避免执行顺序上的冲突；根据AUTOSAR CP 4.4标准，还需要确保动作列表的执行不会违反系统的实时性要求或造成资源竞争。|
|多实例个数|1 - 1|
|默认值|BSWM_TRIGGER|

##### 1.4.2.1. BswMActionListItem

|容器属性|值（容器）|
|---|---|
|名称|BswMActionListItem|
|描述|This container defines an item in an action list.|
|描述|概述：BswMActionListItem配置项用于定义基本软件模块管理（BswM）的行为列表项，它指定了在特定条件下应当执行的动作序列。|
|描述|注意：在配置BswMActionListItem时，需要确保动作的顺序和条件与系统需求相匹配；此外，每个行为列表项应当与相应的BswMModeRequestTrigger或BswMRule关联；在配置过程中，还需注意不同动作之间的依赖关系和潜在的资源冲突。|
|多实例个数|1 - inf|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|BswMAbortOnFail|
|描述|This parameter defines if the execution of the action list shall be aborted if this specific action returns E_NOT_OK. Note that this is only applicable for actions that have E_NOT_OK as a possible return value.|
|描述|概述：BswMAbortOnFail配置项用于指定当BswM模块中的某个模式请求失败时，是否应中止当前操作或继续执行后续操作。|
|描述|注意：在配置此项时，需考虑系统的容错需求和安全要求；错误处理策略应与系统的整体异常管理策略保持一致；此配置项在AUTOSAR CP 4.4标准中未明确定义，需根据具体实现和版本要求进行考虑。|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|BswMActionListItemIndex|
|描述|This parameter defines the index of the action in the action list. It is used define in which order the actions shall be performed.|
|描述|(1, TypeError("'AssertionError' object is not subscriptable"))|
|多实例个数|1 - 1|
|取值范围|0 - 255|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|BswMReportFailRuntimeErrorId|
|描述|If this parameter is configured, and this specific action returns E_NOT_OK, the BswM will report a Det Runtime Error. The ErrorId reported in the Runtime Error is given by the value configured in this parameter.|
|描述|概述：BswMReportFailRuntimeErrorId用于定义在基础软件模块管理（BswM）中报告运行时错误的唯一标识符，该标识符用于识别和处理特定的运行时错误。|
|描述|注意：该标识符必须在系统中唯一，以避免错误处理的混淆；在配置时应确保与系统中其他错误报告机制的标识符不冲突；AUTOSAR CP 4.4标准要求错误处理机制能够准确地识别和响应各种运行时错误，因此正确配置此项至关重要。|
|多实例个数|0 - 1|
|默认值|128|
|取值范围|128 - 255|

|配置项属性|值（选择引用配置项）|
|---|---|
|名称|BswMActionListItemRef|
|描述|The action item can either be an atomic action or a reference to another action list or rule.|
|多实例个数|1 - 1|
|目标引用|/AUTOSAR/EcucDefs/BswM/BswMConfig/BswMModeControl/BswMAction/AUTOSAR/EcucDefs/BswM/BswMConfig/BswMModeControl/BswMActionList/AUTOSAR/EcucDefs/BswM/BswMConfig/BswMArbitration/BswMRule|

#### 1.4.3. BswMRteModeRequestPort

|容器属性|值（容器）|
|---|---|
|名称|BswMRteModeRequestPort|
|描述|This container defines a mode request port which the BswM may utilize to send a mode request to a SW-C which is acting as a mode-manager. If this container is referenced by a BswMRteModeRequest, the BswM shall create a corresponding PPort in its service description.|
|描述|概述：BswMRteModeRequestPort配置项用于定义基础软件模块（BswM）与运行时环境（RTE）之间的模式请求端口，允许BswM请求RTE切换特定模式。|
|描述|注意：在配置时需确保端口的唯一性和正确性，以保证模式请求能够正确传递；此配���项在AUTOSAR CP 4.4中应与BswM模块的模式管理功能紧密集成，确保模式切换请求的一致性和实时性；配置时应注意与相关的RTE模式声明保持一致，避免模式匹配错误。|
|多实例个数|0 - inf|

|配置项属性|值（外部引用配置项）|
|---|---|
|名称|BswMRteModeRequestVariableDataPrototypeSRRef|
|描述|This is a foreign reference to a VariableDataPrototype used for the mode request.|
|描述|概述：BswMRteModeRequestVariableDataPrototypeSRRef 是一个配置项，用于指定基本软件模块（BswM）中的模式请求变量与软件组件（Swc）提供的模式声明组（ModeDeclarationGroup）之间的关联。|
|描述|注意：在配置时，必须确保模式请求变量与正确的模式声明组相对应；模式声明组需要在系统描述中预先定义；此配置项对于实现BswM逻辑和Swc之间的模式管理交互至关重要。|
|多实例个数|0 - 1|
|目标类型|VARIABLE-DATA-PROTOTYPE|

|配置项属性|值（实例引用配置项）|
|---|---|
|名称|BswMRteModeRequestPortInterfaceRef|
|描述|This is an instance reference to the variable data prototype used for the mode request.|
|描述|概述：BswMRteModeRequestPortInterfaceRef 配置项用于指定基本软件模块（BswM）中用于请求模式切换的RTE端口接口的引用。|
|描述|注意：在配置BswMRteModeRequestPortInterfaceRef时，必须确保引用的RTE端口接口与BswM模块的模式管理需求相匹配；引用的接口应已在系统中定义且符合AUTOSAR标准的接口规范；在配置过程中，应注意接口的一致性和正确性，避免引用错误或不存在的接口。|
|多实例个数|0 - 1|
|目标上下文|SW-COMPONENT-PROTOTYPE\*PORT-PROTOTYPE|
|目标类型|VARIABLE-DATA-PROTOTYPE|

#### 1.4.4. BswMSwitchPort

|容器属性|值（容器）|
|---|---|
|名称|BswMSwitchPort|
|描述|This container includes a reference to mode switch interface which the BswM must instantiate for the creation of a PPortPrototype in its SWCD.|
|描述|概述：BswMSwitchPort配置项用于定义基本软件模块（BswM）中的端口开关，它控制不同软件模块间的通信路径，以及模块内部功能的启用或禁用。|
|描述|注意：在配置BswMSwitchPort时，必须确保端口的状态转换逻辑与系统需求相匹配，避免因错误配置导致通信故障；此外，AUTOSAR CP 4.4标准中对于端口开关的配置和管理提供了详细的规范，需要仔细遵守以保证兼容性和系统的稳定性。|
|多实例个数|0 - inf|

|配置项属性|值（外部引用配置项）|
|---|---|
|名称|BswMModeSwitchInterfaceRef|
|描述|Reference to the ModeSwitchInterface of this BswMModeSwitchPort.|
|描述|概述：BswMModeSwitchInterfaceRef 配置项用于引用模式切换接口，它指定了基础软件模块（BswM）与其他模块间的模式切换通信接口。|
|描述|注意：在配置时需确保引用的模式切换接口与实际的模块定义一致；AUTOSAR CP 4.4标准中可能对模式切换接口的实现和使用有特定的要求，需要遵守这些要求；在多模块协作环境中，要注意模式切换的同步和一致性问题。|
|多实例个数|1 - 1|
|目标类型|MODE-SWITCH-INTERFACE|

## 2. BswMGeneral

|容器属性|值（容器）|
|---|---|
|名称|BswMGeneral|
|描述|General configuration parameters of the Basic SW Mode Manager.|
|描述|概述：BswMGeneral 是 AUTOSAR BSW Module Management的一个配置容器，它包含了基本的模块管理配置参数，如模块的开启或关闭状态、开发错误检测等。|
|描述|注意：在配置BswMGeneral时，需要确保配置参数与系统需求相匹配；开发错误检测（Development Error Detection）应根据项目的调试和发布需求来启用或禁用；如果配置了模块为关闭状态，则相关的BswM功能将不会被编译或执行。|
|多实例个数|1 - 1|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|BswMCanSMEnabled|
|描述|enable/disable CanSM module related BswM API:|
|描述|概述：BswMCanSMEnabled 是一个配置项，用于启用或禁用CAN状态管理器（CanSM）模块在BswM（基础软件模块管理器）中的功能。|
|描述|注意：在配置BswMCanSMEnabled时，需要确保CAN网络管理需求与BswM模块的策略一致；如果项目不使用BswM对CanSM的管理，则该配置项应设置为禁用；在配置时应参照具体项目的网络管理需求和架构设计来决定该配置项的启用状态。|
|说明|true: Enabled false: Disabled|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|BswMCanSMIcomEnabled|
|描述|enable/disable CanSM Icom related BswM API:|
|描述|概述：BswMCanSMIcomEnabled 是一个布尔型配置参数，用于启用或禁用CAN网络管理接口(CanSM)的Icom(Integration Communication)支持，这是为了优化网络管理策略和降低网络带宽消耗。|
|描述|注意：在使用此配置项时，需要确保硬件和底层CAN驱动支持Icom功能；如果项目不使用Icom或硬件不支持，应将此配置项设置为false；在配置时应参照具体的AUTOSAR CAN网络管理模块规范，确保与AUTOSAR CP 4.4标准的要求一致。|
|说明|true: Enabled false: Disabled|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|BswMComMEnabled|
|描述|enable/disable ComM module related BswM API:|
|描述|概述：BswMComMEnabled配置项用于启用或禁用BswM（基础软件模块管理器）对ComM（通信管理器）模块的管理功能，允许BswM根据系统状态控制ComM的行为。|
|描述|注意：在使用此配置项时，需确保项目中已集成了ComM模块；若项目不需要BswM对ComM的管理，则应将此配置项禁用以节省资源；在配置时应注意与其他BswM管理的模块配置的兼容性和依赖关系。|
|说明|true: Enabled false: Disabled|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|BswMDcmEnabled|
|描述|enable/disable Dcm module related BswM API:|
|描述|概述：BswMDcmEnabled 用于启用或禁用车载诊断通信管理模块（Dcm）中的基础软件模块（BswM）逻辑。|
|描述|注意：在配置时需确保BswMDcmEnabled与系统中实际使用的诊断需求一致；如果禁用，可能会影响诊断服务的可用性和响应；此配置项应与其他诊断相关配置项协同考虑。|
|说明|true: Enabled false: Disabled|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|BswMDevErrorDetect|
|描述|Switches the development error detection and notification on or off.|
|描述|概述：BswMDevErrorDetect是一个配置参数，用于启用或禁用基本软件模块管理（BswM）的开发错误检测功能，以便在开发阶段识别配置或运行时错误。|
|描述|注意：在生产代码中通常禁用此功能以优化性能；确保在开发和测试阶段启用以捕获潜在错误；与AUTOSAR 4.4标准一致，无特殊不一致事项。|
|说明|\* true: detection and notification is enabled. \* false: detection and notification is disabled.|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|BswMEcuMEnabled|
|描述|enable/disable EcuM module related BswM API:|
|描述|概述：BswMEcuMEnabled 配置项用于启用或禁用ECU管理模块（EcuM）中的基本软件模块（BswM）的功能，这决定了BswM是否参与ECU的管理过程。|
|描述|注意：在AUTOSAR CP 4.4标准中，确保在使用BswM时，ECU配置正确地反映了BswM的启用状态；如果BswM未被使用，应确保该配置项被设置为禁用以避免不必要的资源消耗；在配置过程中，需要注意BswM与其他模块的依赖关系和交互。|
|说明|true: Enabled false: Disabled|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|BswMEthIfEnabled|
|描述|enable/disable EthIf module related BswM API:|
|描述|概述：BswMEthIfEnabled 配置项用于启用或禁用基本软件模块（BswM）中以太网接口（EthIf）的管理功能，这决定了BswM是否会对以太网接口的状态变化做出响应。|
|描述|注意：在配置BswMEthIfEnabled时，需要确保与系统中以太网接口的实际使用情况相匹配；如果系统不使用以太网接口，则应禁用此功能以节省资源；在启用时，还需要配置相应的BswM规则和逻辑，以确保以太网接口的正确管理。|
|说明|true: Enabled false: Disabled|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|BswMEthSMEnabled|
|描述|enable/disable EthSM module related BswM API:|
|描述|概述：BswMEthSMEnabled 配置项用于启用或禁用基础软件模块以太网状态管理（BswM Ethernet State Management）的功能。|
|描述|注意：在使用此配置项时，确保已经评估了以太网通信对系统的影响和需求；此配置项必须与网络管理需求相协调；在不同的项目或平台中，此配置的默认值可能不同，需仔细检查。|
|说明|true: Enabled false: Disabled|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|BswMFrSMEnabled|
|描述|enable/disable FrSM module related BswM API:|
|描述|概述：BswMFrSMEnabled 是一个配置参数，用于启用或禁用BswM模块对FlexRay状态管理（FrSM）的监控功能。|
|描述|注意：在使用此配置项时，需要确保FlexRay通信控制器已经集成到系统中，并且FrSM模块已经配置；如果不使用FlexRay通信或者不需要BswM模块监控FrSM状态，则应将此配置项禁用；在配置此项时，应参照AUTOSAR CP 4.4标准中BswM模块的相关规范，确保配置的正确性和一致性。|
|说明|true: Enabled false: Disabled|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|BswMGenericRequestEnabled|
|描述|enable/disable Generic Request related BswM API:|
|描述|概述：BswMGenericRequestEnabled 是一个配置参数，用于启用或禁用基本软件模块管理（BswM）中的通用请求功能，允许模块管理器根据来自其他模块的请求来改变其内部管理决策。|
|描述|注意：在使用此配置项时，需要确保BswM模块已经配置了相应的逻辑来处理通用请求；如果不需要此功能，应将其禁用以节省系统资源；在AUTOSAR CP 4.4标准中，此配置项应与其他BswM配置一致，以保证模块间的正确交互。|
|说明|true: Enabled false: Disabled|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|BswMJ1939DcmEnabled|
|描述|Enable/disable J1939Dcm module related BswM API:|
|描述|(3, TypeError("'AssertionError' object is not subscriptable"))|
|说明|true: Enabled false: Disabled|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|BswMJ1939NmEnabled|
|描述|Enable/disable J1939Nm module related BswM API.|
|描述|概述：BswMJ1939NmEnabled配置项用于启用或禁用基于J1939网络管理的基本软件模块功能，这是针对特定于汽车行业的网络协议J1939的网络管理需求。|
|描述|注意：在使用此配置项时，必须确保整个系统中的网络配置支持J1939协议；如果项目不涉及J1939网络，该配置应设置为禁用以避免不必要的资源消耗；AUTOSAR CP 4.4标准中并未明确定义名为BswMJ1939NmEnabled的配置项，因此实际使用时应参考具体的AUTOSAR BSW模块文档或供应商实现。|
|说明|true: Enabled false: Disabled|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|BswMLinSMEnabled|
|描述|enable/disable LinSM module related BswM API:|
|描述|概述：BswMLinSMEnabled 是一个配置项，用于启用或禁用LIN通信堆栈中的LIN状态管理模块（LinSM）。|
|描述|注意：在配置LIN通信堆栈时，必须根据系统是否需要LIN状态管理来设置此属性；如果系统不使用LIN通信或不需要状态管理，则不应启用此模块；在AUTOSAR CP 4.4标准中，确保与其他BswM模块的依赖和交互被正确配置。|
|说明|true: Enabled false: Disabled|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|BswMLinTPEnabled|
|描述|enable/disable LinTP module related BswM API:|
|描述|概述：BswMLinTPEnabled 是一个配置项，用于启用或禁用基本软件模块（BswM）中LIN传输协议（LinTP）的支持，以便控制LIN网络上的数据传输。|
|描述|注意：在配置BswMLinTPEnabled时，需要确保LIN通信堆栈已经包含了LinTP模块；此配置项的启用与否应与系统的实际需求和设计相匹配；如果系统不使用LIN网络或不需要LinTP功能，则不应启用此配置项以节省资源。|
|说明|true: Enabled false: Disabled|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|BswMNmEnabled|
|描述|enable/disable Nm module related BswM API:|
|描述|概述：BswMNmEnabled是一个配置项，用于启用或禁用基本软件模块（BswM）中网络管理（Nm）的功能，控制网络管理功能的激活状态。|
|描述|注意：在不需要网络管理功能时应将此配置项禁用以节省资源；确保在启用此功能前已正确配置网络管理相关的参数和依赖项；此配置项的启用与否可能会影响系统的通信行为和性能。|
|说明|true: Enabled false: Disabled|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|BswMNvMEnabled|
|描述|enable/disable NvM module related BswM API:|
|描述|概述：BswMNvMEnabled配置项用于启用或禁用非易失性内存管理（NvM）模块下的基本软件模块（BswM）逻辑，控制BswM模块是否参与NvM的操作流程。|
|描述|注意：在不需要BswM参与NvM操作的场景下，应将此配置项禁用以节省系统资源；确保在启用此配置项时，系统中已正确配置和初始化了NvM和BswM模块；此配置项在AUTOSAR CP 4.4标准中未明确提及，具体实现可能依赖于供应商的AUTOSAR实现。|
|说明|true: Enabled false: Disabled|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|BswMSchMEnabled|
|描述|enable/disable SchM module related BswM API:|
|描述|概述：BswMSchMEnabled 是一个配置项，用于启用或禁用BswM模块的调度管理功能，这决定了BswM模块是否会被编译和链接到最终的软件中。|
|描述|注意：在不需要BswM模块提供调度管理功能的情况下，可以将此配置项设置为禁用以节省资源；如果BswM模块是系统设计的一部分，确保此配置项被正确设置为启用；在配置过程中，需要考虑与其他模块的依赖关系和交互。|
|说明|true: Enabled false: Disabled|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|BswMSdEnabled|
|描述|enable/disable Sd module related BswM API.|
|描述|概述：BswMSdEnabled配置项用于启用或禁用基本软件模块监控守护（BswM）的诊断状态管理功能，允许系统根据需要开启或关闭对特定基本软件模块的诊断监控。|
|描述|注意：在AUTOSAR CP 4.4标准中，对于BswMSdEnabled的具体属性或使用方式没有直接的描述，因此在实际应用中需要参考具体的BswM模块实现文档或供应商指南；确保在系统设计阶段明确是否需要启用该功能，以避免不必要的资源消耗；在配置时需注意与其他诊断功能的兼容性和依赖关系。|
|说明|true: Enabled false: Disabled|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|BswMVersionInfoApi|
|描述|Switches the possibility to read the version information with the service BswM_GetVersionInfo().|
|描述|概述：BswMVersionInfoApi 是一个配置参数，用于启用或禁用基础软件模块管理（BswM）的版本信息API功能，允许软件组件获取当前BswM模块的版本信息。|
|描述|注意：在AUTOSAR CP 4.4标准中，如果启用了该功能，必须确保BswM模块提供了一个标准的API来返回版本信息；如果不需要模块版本信息，可以禁用以节省资源；在设计系统时应考虑是否其他模块或诊断功能依赖于此API。|
|说明|true: Enabled false: Disabled|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|BswMWdgMEnabled|
|描述|enable/disable WdgM module related BswM API:|
|描述|概述：BswMWdgMEnabled 是一个配置项，用于启用或禁用基本软件模块中的看门狗管理器（WdgM）功能，这是AUTOSAR中负责监控系统运行状态并在检测到错误时执行恢复措施的组件。|
|描述|注意：在配置BswMWdgMEnabled时，需要确保系统的安全需求是否需要看门狗管理器的功能；如果启用，还需要配置相关的看门狗监控策略和动作；在不同的ECU上，根据硬件能力和安全需求，该配置项的设置可能会有所不同。|
|说明|true: Enabled false: Disabled|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（浮点型参数配置项）|
|---|---|
|名称|BswMMainFunctionPeriod|
|描述|The cycle time of the periodic main function of BswM. Defined in seconds .|
|描述|概述：BswMMainFunctionPeriod配置项定义了基础软件模块管理器（BswM）主函数的调用周期，即BswM主函数多久被调度执行一次。|
|描述|注意：该周期值必须与实际系统定时器配置相匹配，以确保系统的定时精度；不正确的配置可能导致系统响应时间不符合预期；在AUTOSAR CP 4.4标准中，确保该值符合ECU的实时性要求和性能限制。|
|多实例个数|0 - 1|
|取值范围|0 - Inf|

### 2.1. BswMUserIncludeFiles

|容器属性|值（容器）|
|---|---|
|名称|BswMUserIncludeFiles|
|描述|Collection of header file names which shall be included by the BswM.|
|描述|概述：BswMUserIncludeFiles配置项用于指定基本软件模块管理器(BswM)在生成代码时需要包含的用户头文件，这些头文件通常包含用户定义的数据类型、宏定义或者函数声明。|
|描述|注意：在指定用户头文件时，需要确保文件路径的正确性和文件的可访问性；避免包含不必要的或者与AUTOSAR标准冲突的头文件；在多模块协作的环境中，注意头文件的包含顺序和依赖关系，以防止编译错误。|
|多实例个数|0 - 1|

|配置项属性|值（字符串参数配置项）|
|---|---|
|名称|BswMUserIncludeFile|
|描述|Header file name which shall be included by the BswM.|
|描述|概述：BswMUserIncludeFile配置项用于指定基本软件模块（BswM）在生成代码时需要包含的用户头文件，这样可以在BswM模块中直接使用用户定义的数据类型、宏定义或者函数原型。|
|描述|注意：在配置BswMUserIncludeFile时，需要确保指定的头文件路径正确且文件可访问；头文件中的内容应与AUTOSAR标准兼容，避免引入非标准的数据类型或宏定义；如果项目中有多个BswMUserIncludeFile配置，需要确保它们之间不会产生包含冲突或重复定义的问题。|
|说明|The value of this parameter shall be used as h-char-sequence or q-char-sequence according to ISO C90 section 6.10.2 "source file inclusion". The parameter value MUST NOT represent a path, since ISO C90 does not specify how such a path is treated (i.e., this is implementation defined (and additionally depends on the operating system and the underlying file system)).|
|多实例个数|1 - inf|
