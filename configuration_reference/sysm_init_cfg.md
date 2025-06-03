# EcuM 配置项参考文档

|容器属性|值（容器）|
|---|---|
|名称|EcuM|
|描述|Configuration of the EcuM (ECU State Manager) module.|
|描述|概述：EcuM配置项代表电子控制单元管理模块（ECU Manager），它负责ECU的启动、关机逻辑以及与底层MCU驱动的交互，确保系统的正确初始化和电源管理。|
|描述|注意：在配置EcuM时，需要确保与具体的硬件平台和MCU驱动兼容；EcuM的配置参数必须符合AUTOSAR CP 4.4标准中定义的模块和参数规范；在多ECU系统中，还需要考虑ECU间的通信和同步机制。|
|多实例个数|0 - 1|

## 1. EcuMConfiguration

|容器属性|值（容器）|
|---|---|
|名称|EcuMConfiguration|
|描述|This container contains the configuration (parameters) of the ECU State Manager.|
|描述|概述：EcuMConfiguration 是用于定义电子控制单元管理（EcuM）模块的配置参数，包括启动配置、休眠模式、唤醒源等，以支持ECU的启动、管理和休眠策略。|
|描述|注意：在配置EcuMConfiguration时，需要确保唤醒源与硬件能力相匹配；正确配置休眠模式以优化能耗；在多ECU系统中，需考虑ECU间的通信和同步。|
|多实例个数|1 - 1|

### 1.1. EcuMCommonConfiguration

|容器属性|值（容器）|
|---|---|
|名称|EcuMCommonConfiguration|
|描述|This container contains the common configuration (parameters) of the ECU State Manager.|
|描述|概述：EcuMCommonConfiguration 是用于定义ECU管理模块中所有基本配置的参数，这些配置涵盖了系统启动、电源管理和诊断等方面。|
|描述|注意：确保所有的配置参数符合ECU的硬件和软件需求；在多核或多ECU系统中，需要特别注意配置的一致性和兼容性；配置参数应当通过专业的配置工具进行设置和验证，以防止错误配置导致系统不稳定。|
|多实例个数|1 - 1|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|EcuMConfigConsistencyHash|
|描述|In the pre-compile and link-time configuration phase a hash value is generated across all pre-compile and link-time parameters of all BSW modules.|
|描述|概述：EcuMConfigConsistencyHash 是一个用于验证ECU配置一致性的哈希值，确保在软件开发和部署过程中，ECU的配置数据保持一致。|
|描述|注意：在软件开发的不同阶段，如编译、链接和加载到ECU上时，都需要验证EcuMConfigConsistencyHash以确保配置的一致性；如果在这些阶段中发现哈希值不匹配，可能意味着配置数据已被更改，需要重新生成和验证；AUTOSAR CP 4.4标准中对于生成和比较该哈希值的具体算法和方法有明确规定，需要遵循这些规定以确保兼容性。|
|说明|In the post-build phase a hash value is generated across all pre-compile and link-time parameters, except for parameters located in EcucParamConfContainerDef instances or subContainers which have been introduced at post-build configuration time. This hash value is compared against each other and allows checking the consistency of the entire configuration.|
|多实例个数|1 - 1|
|取值范围|0 - 18446744073709551615|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|EcuMDefaultAppMode|
|描述|The default application mode loaded when the ECU comes out of reset.|
|描述|概述：EcuMDefaultAppMode配置项用于定义系统启动后的默认应用模式，这决定了系统在启动后将进入哪种操作模式。|
|描述|注意：该配置项的设置必须与系统设计的应用模式一致，以确保系统能按预期工作；在多应用系统中，正确的默认应用模式选择对系统行为有重要影响；该配置项在AUTOSAR CP 4.4标准中是必需的，缺失可能导致系统启动异常。|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Os/OsAppMode|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|EcuMOSResource|
|描述|This parameter is a reference to a OS resource which is used to bring the ECU into sleep mode.|
|描述|概述：EcuMOSResource配置项用于定义ECU管理模块（EcuM）所需的操作系统资源，如任务、事件、资源等，以确保EcuM模块能够正确管理ECU的启动、关闭和模式切换。|
|描述|注意：在AUTOSAR CP 4.4中，确保为EcuM模块配置的操作系统资源满足其实时性和优先级要求；操作系统资源的配置应遵循AUTOSAR OS模块的规范；不正确的资源配置可能导致系统启动或模式切换时的性能问题。|
|说明|In case of multi core each core shall have an own OsResource.|
|多实例个数|0 - 255|
|目标引用项的路径|/AUTOSAR/EcucDefs/Os/OsResource|

#### 1.1.1. EcuMDefaultShutdownTarget

|容器属性|值（容器）|
|---|---|
|名称|EcuMDefaultShutdownTarget|
|描述|This container describes the default shutdown target to be selected by EcuM. The actual shutdown target may be overridden by the EcuM_SelectShutdownTarget service.|
|多实例个数|1 - 1|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|EcuMDefaultShutdownTarget|
|描述|This parameter describes the state part of the default shutdown target selected when the ECU comes out of reset. If EcuMShutdownTargetSleep is selected, the parameter EcuMDefaultSleepModeRef selects the specific sleep mode.|
|描述|概述：EcuMDefaultShutdownTarget配置项定义了ECU管理器（EcuM）在没有接收到任何明确的关机目标时应采取的默认关机行为，例如选择默认的睡眠模式或是重启。|
|描述|注意：在配置EcuMDefaultShutdownTarget时，需要确保所选的默认关机目标与系统的功耗和安全要求相符；此配置项对系统的启动和关机策略有直接影响，因此需要仔细规划；在AUTOSAR CP 4.4标准中，应确保该配置项的属性与标准定义的参数一致，以免出现不兼容的情况。|
|多实例个数|1 - 1|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|EcuMDefaultResetModeRef|
|描述|If EcuMDefaultShutdownTarget is EcuMShutdownTargetReset, this parameter selects the default reset mode. Otherwise this parameter may be ignored.|
|描述|概述：EcuMDefaultResetModeRef 配置项用于指定ECU管理模块在系统复位时默认采用的复位模式。|
|描述|注意：确保该配置项引用的复位模式在EcuM模块中已定义且有效；复位模式的选择应符合系统的安全和恢复需求；在多模式系统中，正确管理不同模式下的转换和行为。|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/EcuM/EcuMConfiguration/EcuMFlexConfiguration/EcuMResetMode|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|EcuMDefaultSleepModeRef|
|描述|If EcuMDefaultShutdownTarget is EcuMShutdownTargetSleep, this parameter selects the default sleep mode. Otherwise this parameter may be ignored.|
|描述|概述：EcuMDefaultSleepModeRef配置项用于指定ECU管理模块（EcuM）默认的睡眠模式，这是系统在没有活动或操作时应进入的低功耗状态。|
|描述|注意：确保选择的默认睡眠模式与系统的能耗要求和唤醒源兼容；在系统设计阶段就确定并配置好此项，以避免运行时能耗过高；AUTOSAR CP 4.4标准中，对睡眠模式的定义和管理有明确规范，需要遵循这些规范以确保系统的可靠性和效率。|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/EcuM/EcuMConfiguration/EcuMCommonConfiguration/EcuMSleepMode|

#### 1.1.2. EcuMDriverInitListOne

|容器属性|值（容器）|
|---|---|
|名称|EcuMDriverInitListOne|
|描述|Container for Init Block I.|
|描述|概述：EcuMDriverInitListOne 是用于定义在ECU管理模块初始化阶段一中需要调用的驱动初始化列表。|
|描述|注意：确保所有列出的驱动与硬件和系统需求兼容；初始化顺序应根据系统依赖性和优先级合理安排；遵循AUTOSAR CP 4.4标准，确保驱动初始化的正确性和顺序。|
|说明|This container holds a list of modules to be initialized. Each module in the list will be called for initialization in the list order. All modules in this list are initialized before the OS is started and so these modules require no OS support.|
|多实例个数|0 - 1|

##### 1.1.2.1. EcuMDriverInitItem

|容器属性|值（容器）|
|---|---|
|名称|EcuMDriverInitItem|
|描述|These containers describe the entries in a driver init list.|
|多实例个数|1 - 255|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|EcuMModuleParameter|
|描述|Definition of the function prototype and the parameter passed to the function.|
|多实例个数|1 - 1|
|默认值|NULL_PTR|

|配置项属性|值（字符串参数配置项）|
|---|---|
|名称|EcuMAdditionalInitCode|
|描述|Additional Init Code.|
|多实例个数|0 - 1|

|配置项属性|值（字符串参数配置项）|
|---|---|
|名称|EcuMMoudleHeader|
|描述|Moudle Header.|
|多实例个数|0 - 1|

|配置项属性|值（字符串参数配置项）|
|---|---|
|名称|EcuMModuleService|
|描述|The service to be called to initialize that module, e.g. Init, PreInit, Start etc. If nothing is defined "Init" is taken by default.|
|多实例个数|0 - 1|

|配置项属性|值（外部引用配置项）|
|---|---|
|名称|EcuMModuleRef|
|描述|Foreign reference to the configuration of a module instance which shall be initialized by EcuM|
|多实例个数|0 - 1|
|目标类型|ECUC-MODULE-CONFIGURATION-VALUES|

#### 1.1.3. EcuMDriverInitListZero

|容器属性|值（容器）|
|---|---|
|名称|EcuMDriverInitListZero|
|描述|Container for Init Block 0.|
|描述|概述：EcuMDriverInitListZero 是一个配置项，用于定义在操作系统启动阶段，即启动列表0（Start List Zero）中，需要初始化的驱动模块的顺序。|
|描述|注意：在配置EcuMDriverInitListZero时，需要确保列出的驱动初始化顺序与硬件和系统启动要求相匹配；此外，应注意不要在此列表中重复初始化同一驱动，以避免潜在的初始化冲突；根据AUTOSAR CP 4.4标准，确保所有必要的驱动在系统启动时得到正确的初始化。|
|说明|This container holds a list of modules to be initialized. Each module in the list will be called for initialization in the list order. All modules in this list are initialized before the post-build configuration has been loaded and the OS is initialized. Therefore, these modules may not use post-build configuration.|
|多实例个数|0 - 1|

##### 1.1.3.1. EcuMDriverInitItem

|容器属性|值（容器）|
|---|---|
|名称|EcuMDriverInitItem|
|描述|These containers describe the entries in a driver init list.|
|多实例个数|1 - 255|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|EcuMModuleParameter|
|描述|Definition of the function prototype and the parameter passed to the function.|
|多实例个数|1 - 1|
|默认值|NULL_PTR|

|配置项属性|值（字符串参数配置项）|
|---|---|
|名称|EcuMAdditionalInitCode|
|描述|Additional Init Code.|
|多实例个数|0 - 1|

|配置项属性|值（字符串参数配置项）|
|---|---|
|名称|EcuMMoudleHeader|
|描述|Moudle Header.|
|多实例个数|0 - 1|

|配置项属性|值（字符串参数配置项）|
|---|---|
|名称|EcuMModuleService|
|描述|The service to be called to initialize that module, e.g. Init, PreInit, Start etc. If nothing is defined "Init" is taken by default.|
|多实例个数|0 - 1|

|配置项属性|值（外部引用配置项）|
|---|---|
|名称|EcuMModuleRef|
|描述|Foreign reference to the configuration of a module instance which shall be initialized by EcuM|
|多实例个数|0 - 1|
|目标类型|ECUC-MODULE-CONFIGURATION-VALUES|

#### 1.1.4. EcuMDriverRestartList

|容器属性|值（容器）|
|---|---|
|名称|EcuMDriverRestartList|
|描述|List of modules to be initialized.|
|描述|概述：EcuMDriverRestartList 配置项定义了在ECU管理器（EcuM）重启过程中需要重新初始化的驱动程序列表，确保在系统复位或重启时，相关驱动能够正确地恢复到初始状态。|
|描述|注意：在配置EcuMDriverRestartList时，需要确保所有需要在EcuM启动过程中重新初始化的驱动都被包含在列表中；此外，驱动的初始化顺序可能会影响系统的启动时间和稳定性，因此需要仔细规划；根据AUTOSAR CP 4.4标准，应当遵循EcuM模块的定义和依赖关系来配置此列表。|
|多实例个数|0 - 1|

##### 1.1.4.1. EcuMDriverInitItem

|容器属性|值（容器）|
|---|---|
|名称|EcuMDriverInitItem|
|描述|These containers describe the entries in a driver init list.|
|多实例个数|1 - 255|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|EcuMModuleParameter|
|描述|Definition of the function prototype and the parameter passed to the function.|
|多实例个数|1 - 1|
|默认值|NULL_PTR|

|配置项属性|值（字符串参数配置项）|
|---|---|
|名称|EcuMAdditionalInitCode|
|描述|Additional Init Code.|
|多实例个数|0 - 1|

|配置项属性|值（字符串参数配置项）|
|---|---|
|名称|EcuMMoudleHeader|
|描述|Moudle Header.|
|多实例个数|0 - 1|

|配置项属性|值（字符串参数配置项）|
|---|---|
|名称|EcuMModuleService|
|描述|The service to be called to initialize that module, e.g. Init, PreInit, Start etc. If nothing is defined "Init" is taken by default.|
|多实例个数|0 - 1|

|配置项属性|值（外部引用配置项）|
|---|---|
|名称|EcuMModuleRef|
|描述|Foreign reference to the configuration of a module instance which shall be initialized by EcuM|
|多实例个数|0 - 1|
|目标类型|ECUC-MODULE-CONFIGURATION-VALUES|

#### 1.1.5. EcuMSleepMode

|容器属性|值（容器）|
|---|---|
|名称|EcuMSleepMode|
|描述|These containers describe the configured sleep modes.|
|描述|概述：EcuMSleepMode 配置项定义了电子控制单元（ECU）的睡眠模式，包括睡眠模式的类型和相关属性，用于管理ECU的低功耗状态。|
|描述|注意：在配置EcuMSleepMode时，需要确保所选的睡眠模式与ECU硬件和所需的功耗要求相匹配；必须考虑唤醒事件和唤醒源，确保系统能够从睡眠模式中正确唤醒；AUTOSAR CP 4.4标准可能对睡眠模式的配置参数有特定的要求或限制，需要遵守这些规范以确保兼容性。|
|说明|The names of these containers specify the symbolic names of the different sleep modes.|
|多实例个数|1 - 256|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|EcuMSleepModeSuspend|
|描述|Flag, which is set true, if the CPU is suspended, halted, or powered off in the sleep mode. If the CPU keeps running in this sleep mode, then this flag must be set to false.|
|描述|概述：EcuMSleepModeSuspend配置项定义了ECU管理器（EcuM）在进入睡眠模式前需要挂起的各种ECU内部组件和通信服务。|
|描述|注意：在配置EcuMSleepModeSuspend时，需要确保所有需要在睡眠模式下被挂起的组件都被正确地列出；此外，挂起操作应与硬件能力和系统需求相匹配；最后，确保在唤醒时能够正确地恢复这些组件的状态。|
|多实例个数|1 - 1|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|EcuMSleepModeId|
|描述|This ID identifies this sleep mode in services like EcuM_SelectShutdownTarget.|
|描述|概述：EcuMSleepModeId用于标识ECU管理模块中定义的不同睡眠模式，每种模式下ECU的功耗和功能可有不同的配置，以适应不同的能耗要求和唤醒条件。|
|描述|注意：确保每个EcuMSleepModeId在系统中是唯一的，以避免配置混淆；在设计睡眠模式时考虑系统的唤醒源和功耗要求；AUTOSAR CP 4.4标准中，对睡眠模式的管理和配置有详细规定，需要遵循标准以确保兼容性。|
|多实例个数|1 - 1|
|取值范围|0 - 255|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|EcuMSleepModeMcuModeRef|
|描述|This parameter is a reference to the corresponding MCU mode for this sleep mode.|
|描述|概述：EcuMSleepModeMcuModeRef 配置项用于将ECU管理模块中定义的睡眠模式与微控制器的低功耗模式相关联，确保在ECU进入睡眠模式时，微控制器也相应地进入预定义的低功耗状态。|
|描述|注意：在配置EcuMSleepModeMcuModeRef时，必须确保引用的微控制器模式与ECU的睡眠模式兼容；此外，该配置项通常在EcuM配置中进行设置，需要与MCU驱动模块的配置保持一致；在多核或多微控制器系统中，还需要考虑不同核心或微控制器之间的睡眠模式协调。|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Mcu/McuModuleConfiguration/McuModeSettingConf|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|EcuMWakeupSourceMask|
|描述|These parameters are references to the wakeup sources that shall be enabled for this sleep mode.|
|描述|概述：EcuMWakeupSourceMask 是一个配置项，用于定义唤醒源的掩码，该掩码指定了哪些唤醒源可以触发ECU从低功耗模式唤醒。|
|描述|注意：在配置EcuMWakeupSourceMask时，需要确保掩码正确地映射到实际的硬件唤醒源；掩码值应与ECU支持的唤醒源能力相匹配；在多唤醒源系统中，需要注意唤醒源掩码之间的优先级和互斥关系。|
|多实例个数|1 - inf|
|目标引用项的路径|/AUTOSAR/EcucDefs/EcuM/EcuMConfiguration/EcuMCommonConfiguration/EcuMWakeupSource|

#### 1.1.6. EcuMWakeupSource

|容器属性|值（容器）|
|---|---|
|名称|EcuMWakeupSource|
|描述|These containers describe the configured wakeup sources.|
|描述|概述：EcuMWakeupSource 配置项用于定义ECU的唤醒源，它指定了可以唤醒ECU的硬件或软件元素，如CAN网络消息或定时器事件。|
|描述|注意：在配置EcuMWakeupSource时，需要确保唤醒源与ECU支持的唤醒机制相匹配；唤醒源的配置应与整车网络管理需求一致；在多唤醒源系统中，应考虑唤醒源之间的优先级和冲突管理。|
|多实例个数|1 - 32|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|EcuMWakeupSourcePolling|
|描述|This parameter describes if the wakeup source needs polling.|
|描述|概述：EcuMWakeupSourcePolling配置项用于定义ECU管理模块如何轮询唤醒源，以检测是否有外部事件或条件触发了ECU的唤醒。|
|描述|注意：在配置EcuMWakeupSourcePolling时，需要确保已经定义了所有需要轮询的唤醒源；此配置项对于实现低功耗模式和快速唤醒特别重要；AUTOSAR CP 4.4标准要求精确配置唤醒源，以优化轮询机制和减少功耗。|
|多实例个数|1 - 1|

|配置项属性|值（浮点型参数配置项）|
|---|---|
|名称|EcuMCheckWakeupTimeout|
|描述|This Parameter is the initial Value for the Time of the EcuM to delay shut down of the ECU if the check of the Wakeup Source is done asynchronously (CheckWakeupTimer).|
|描述|概述：EcuMCheckWakeupTimeout 用于定义ECU管理模块检查唤醒源是否超时的时间阈值，确保系统能够及时响应或者处理不同的唤醒源。|
|描述|注意：该时间阈值应根据具体硬件和系统需求进行配置；配置值过低可能导致频繁的误判，而配置值过高可能导致响应延迟；在AUTOSAR CP 4.4标准中，该配置项的具体数值需要与系统的实时性和唤醒源特性相匹配。|
|说明|The unit is in seconds.|
|多实例个数|0 - 1|
|默认值|0|
|取值范围|0 - 10|

|配置项属性|值（浮点型参数配置项）|
|---|---|
|名称|EcuMValidationTimeout|
|描述|The validation timeout (period for which the ECU State Manager will wait for the validation of a wakeup event) can be defined for each wakeup source independently. The timeout is specified in seconds.|
|描述|概述：EcuMValidationTimeout 配置项用于定义ECU管理模块（EcuM）在执行唤醒源验证时所允许的最大时间，超过这个时间后，系统将认为唤醒源验证失败。|
|描述|注意：该值需要根据实际硬件和系统需求仔细配置，以避免过早超时导致系统错误地判断唤醒源无效；同时，设置过长的超时时间可能会导致系统响应延迟；在配置时，应确保与AUTOSAR CP 4.4标准中关于唤醒源验证的规定一致。|
|说明|When the timeout is not instantiated, there is no validation routine and the ECU Manager shall not validate the wakeup source.|
|多实例个数|0 - 1|
|取值范围|0 - Inf|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|EcuMWakeupSourceId|
|描述|This parameter defines the identifier of this wakeup source.|
|描述|概述：EcuMWakeupSourceId 是用于唯一标识ECU唤醒源的配置项，它关联到具体的唤醒事件，以便系统能够识别和处理不同的唤醒源。|
|描述|注意：唤醒源ID必须在整个系统中是唯一的，以避免唤醒源之间的冲突；在配置时需要确保唤醒源ID与实际硬件和外部唤醒事件相匹配；在多ECU系统中，需要协调不同ECU间的唤醒源ID，以保证系统级的一致性。|
|多实例个数|1 - 1|
|取值范围|0 - 31|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|EcuMComMChannelRef|
|描述|This parameter is a reference to a Network (channel) defined in the Communication Manager. No reference indicates that the wakeup source is not a communication channel.|
|描述|概述：EcuMComMChannelRef是一个配置参数，用于将ECU管理模块（EcuM）与通信管理模块（ComM）中定义的通信通道相关联，确保ECU的管理策略与通信通道的状态管理保持一致。|
|描述|注意：在配置EcuMComMChannelRef时，必须确保引用的ComM通道已经在ComM模块中定义；此外，每个EcuM配置应只引用一个唯一的ComM通道，以避免状态管理混乱；如果系统中有多个通信通道，需要为每个通道分别配置EcuMComMChannelRef。|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/ComM/ComMConfigSet/ComMChannel|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|EcuMComMPNCRef|
|描述|This is a reference to a one or more PNC's defined in the Communication Manager.|
|描述|概述：EcuMComMPNCRef是一个配置项，用于指定ECU管理模块（EcuM）与通信管理器（ComM）之间的部分网络集群（PNC）引用，以便于管理ECU的网络请求和状态。|
|描述|注意：在配置EcuMComMPNCRef时，必须确保引用的PNC与ECU支持的网络能力相匹配；此配置项对于实现网络管理策略至关重要，应仔细配置以避免网络通信问题；AUTOSAR CP 4.4标准中，对PNC的管理和引用机制有明确规定，需要确保配置符合标准要求。|
|说明|No reference indicates that the wakeup source is not assigned to a partial network.|
|多实例个数|0 - inf|
|目标引用项的路径|/AUTOSAR/EcucDefs/ComM/ComMConfigSet/ComMPnc|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|EcuMResetReasonRef|
|描述|This parameter describes the mapping of reset reasons detected by the MCU driver into wakeup sources.|
|描述|概述：EcuMResetReasonRef 配置项用于引用系统复位原因，它关联了EcuM模块与复位原因之间的映射，以便于系统在复位后能够识别和处理不同的复位原因。|
|描述|注意：在配置EcuMResetReasonRef时，需要确保引用的复位原因与实际硬件和系统支持的复位原因相匹配；此外，应当注意与诊断事件管理器（DEM）的配置一致性，以便正确记录和报告复位原因；在多核或多ECU系统中，还需考虑复位原因在不同核心或ECU间的一致性和传递机制。|
|多实例个数|0 - inf|
|目标引用项的路径|/AUTOSAR/EcucDefs/Mcu/McuPublishedInformation/McuResetReasonConf|

### 1.2. EcuMFlexConfiguration

|容器属性|值（容器）|
|---|---|
|名称|EcuMFlexConfiguration|
|描述|This container contains the configuration (parameters) of the EcuMFlex.|
|描述|概述：EcuMFlexConfiguration 是一个配置项，用于定义ECU管理模块（EcuM）在AUTOSAR系统中的灵活配置参数，这些参数涉及启动、关闭和运行时行为。|
|描述|注意：在配置EcuMFlexConfiguration时，需要确保所有参数与ECU硬件和系统需求相匹配；AUTOSAR CP 4.4标准可能对某些参数的取值范围或者可配置性有特定要求，需要仔细参照标准文档；在多ECU系统中，还需考虑不同ECU间的配置一致性和兼容性。|
|说明|Only applicable if EcuMFlex is implemented.|
|多实例个数|0 - 1|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|EcuMNormalMcuModeRef|
|描述|This parameter is a reference to the normal MCU mode to be restored after a sleep.|
|描述|概述：EcuMNormalMcuModeRef是一个配置项，用于指定ECU管理模块（EcuM）在正常运行模式下应当使用的微控制器（MCU）模式。|
|描述|注意：该配置项确保了系统在正常运行时，微控制器处于正确的能耗和性能状态；在配置时需确保所���用的MCU模式已在MCU驱动模块中定义；不正确的配置可能导致系统性能不佳或能耗过高。|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Mcu/McuModuleConfiguration/McuModeSettingConf|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|EcuMPartitionRef|
|描述|Reference denotes the partition a EcuM shall run inside.|
|描述|概述：EcuMPartitionRef 是一个配置项，用于引用ECU管理模块中定义的特定分区，这有助于实现软件组件的隔离和资源管理。|
|描述|注意：确保引用的分区已在ECU管理模块中定义；分区配置应符合AUTOSAR CP 4.4的安全和隔离要求；正确的分区引用对系统的稳定性和安全性至关重要。|
|说明|Please note that in case of a multicore ECU this reference is mandatory.|
|多实例个数|0 - inf|
|目标引用项的路径|/AUTOSAR/EcucDefs/EcuC/EcucPartitionCollection/EcucPartition|

#### 1.2.1. EcuMAlarmClock

|容器属性|值（容器）|
|---|---|
|名称|EcuMAlarmClock|
|描述|These containers describe the configured alarm clocks.|
|描述|概述：EcuMAlarmClock配置项用于定义ECU唤醒的闹钟机制，它允许系统在预定的时间点自动唤醒，以执行必要的任务或者转换到运行状态。|
|描述|注意：在配置EcuMAlarmClock时，需要确保闹钟时间的准确性和唤醒源的可靠性；此外，应当考虑到与低功耗模式的兼容性，确保在ECU处于低功耗状态时也能够被正确唤醒；根据AUTOSAR CP 4.4标准，还需确保闹钟配置与ECU支持的硬件和操作系统定时器功能相匹配。|
|说明|The name of these conatiners allows giving a symbolic name to one alarm clock.|
|多实例个数|0 - inf|

|配置项属性|值（浮点型参数配置项）|
|---|---|
|名称|EcuMAlarmClockTimeOut|
|描述|This parameter allows to define a timeout for this alarm clock.|
|描述|概述：EcuMAlarmClockTimeOut配置项用于定义ECU管理模块中，闹钟（Alarm Clock）功能的超时时间，这是一个用于唤醒ECU的定时器设置。|
|描述|注意：该配置项的值应根据系统的实际需求和硬件能力进行设置，以确保ECU能够在预定时间内被正确唤醒；超时时间设置过短可能导致ECU未能及时唤醒，过长则可能影响系统的能效表现；在AUTOSAR CP 4.4标准中，对于EcuMAlarmClockTimeOut的具体数值范围没有严格限制，但建议详细参考硬件手册和系统需求。|
|多实例个数|1 - 1|
|取值范围|0 - Inf|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|EcuMAlarmClockId|
|描述|This ID identifies this alarmclock.|
|描述|概述：EcuMAlarmClockId用于标识ECU管理模块中的闹钟实例，这些闹钟用于唤醒系统或者触发特定的时间事件。|
|描述|注意：在配置EcuMAlarmClockId时，需要确保每个闹钟ID在系统中是唯一的；此外，闹钟的配置和使用应符合ECU休眠和唤醒策略；AUTOSAR CP 4.4标准中对闹钟的管理和使用有详细规定，需要仔细遵守。|
|多实例个数|1 - 1|
|取值范围|0 - 255|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|EcuMAlarmClockUser|
|描述|This parameter allows an alarm to be assigned to a user.|
|描述|概述：EcuMAlarmClockUser配置项用于定义ECU管理模块中的闹钟用户，这些用户可以是ECU内部的软件组件或者外部的系统，它们依赖于闹钟机制来唤醒ECU。|
|描述|注意：在配置EcuMAlarmClockUser时，需要确保闹钟用户与实际的唤醒源相匹配；用户应当遵循AUTOSAR CP 4.4标准中对于闹钟用户的定义和使用限制；在设计系统唤醒策略时，应考虑所有闹钟用户的需求以确保系统能够按预期被唤醒。|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/EcuM/EcuMConfiguration/EcuMFlexConfiguration/EcuMFlexUserConfig|

#### 1.2.2. EcuMDriverInitListBswM

|容器属性|值（容器）|
|---|---|
|名称|EcuMDriverInitListBswM|
|描述|This container holds a list of modules to be initialized by the BswM.|
|描述|概述：EcuMDriverInitListBswM 是一个配置项，用于定义在ECU管理模块初始化期间由BswM管理的驱动程序的初始化列表。|
|描述|注意：确保所有列出的驱动程序与BswM模块的依赖关系正确配置；初始化顺序应根据系统需求和依赖关系合理安排；在多ECU系统中，考虑跨ECU的依赖和初始化顺序。|
|多实例个数|0 - inf|

##### 1.2.2.1. EcuMDriverInitItem

|容器属性|值（容器）|
|---|---|
|名称|EcuMDriverInitItem|
|描述|These containers describe the entries in a driver init list.|
|描述|概述：EcuMDriverInitItem配置项用于定义ECU管理模块（EcuM）初始化过程中，特定驱动的初始化顺序和属性。|
|描述|注意：确保每个EcuMDriverInitItem的配置与实际硬件和软件初始化需求相匹配；初始化顺序对系统启动时间和资源使用有重要影响，需谨慎设计；该配置项在AUTOSAR CP 4.4中应与EcuM模块的其他配置项协同工作，以确保系统的正确初始化。|
|多实例个数|1 - 255|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|EcuMModuleParameter|
|描述|Definition of the function prototype and the parameter passed to the function.|
|描述|概述：EcuMModuleParameter配置项用于定义ECU管理模块（EcuM）的参数，这些参数控制ECU的启动、关闭和运行行为，以及与其他BswM模块的交互。|
|描述|注意：在配置EcuMModuleParameter时，必须确保参数与ECU硬件和系统需求相匹配；参数的配置应遵循AUTOSAR CP 4.4标准中对EcuM的规定；不正确的参数配置可能会导致ECU行为异常或系统启动失败。|
|多实例个数|1 - 1|
|默认值|NULL_PTR|

|配置项属性|值（字符串参数配置项）|
|---|---|
|名称|EcuMAdditionalInitCode|
|描述|Additional Init Code.|
|描述|概述：EcuMAdditionalInitCode 是一个配置参数，用于指定在 ECU 管理模块的初始化过程中是否需要执行额外的用户定义代码。|
|描述|注意：在使用此配置时，需要确保用户定义的初始化代码与 AUTOSAR ECU 管理框架的初始化流程兼容；用户定义的代码不应该违反 AUTOSAR 的启动和关闭规范；此外，应当注意代码的执行时间，以免影响系统的启动性能。|
|多实例个数|0 - 1|

|配置项属性|值（字符串参数配置项）|
|---|---|
|名称|EcuMMoudleHeader|
|描述|Moudle Header.|
|描述|概述：EcuMModuleHeader 用于定义ECU管理模块的版本信息和供应商标识，确保模块的兼容性和识别。|
|描述|注意：确保EcuMModuleHeader中的版本信息与实际软件版本一致；供应商标识应符合AUTOSAR规范要求；在模块交互时，正确的头信息是确保模块间正确通信的关键。|
|多实例个数|0 - 1|

|配置项属性|值（字符串参数配置项）|
|---|---|
|名称|EcuMModuleService|
|描述|The service to be called to initialize that module, e.g. Init, PreInit, Start etc. If nothing is defined "Init" is taken by default.|
|描述|概述：EcuMModuleService 是用于管理ECU（电子控制单元）的启动和关闭序列，确保系统在启动和关闭过程中的正确性和顺序性。|
|描述|注意：在配置EcuMModuleService时，必须确保所有依赖的模块按照正确的顺序进行初始化和关闭；此配置项应与系统的实际硬件和软件资源相匹配，避免配置错误导致系统启动失败；在多ECU系统中，还需考虑ECU间的通信和同步。|
|多实例个数|0 - 1|

|配置项属性|值（外部引用配置项）|
|---|---|
|名称|EcuMModuleRef|
|描述|Foreign reference to the configuration of a module instance which shall be initialized by EcuM|
|描述|概述：EcuMModuleRef 配置项用于指定ECU管理模块（EcuM）所引用的其他BswM模块，确保正确的模块间通信和依赖关系。|
|描述|注意：确保所有引用的模块在系统中已定义且可用；引用关系必须符合系统的依赖和启动顺序要求；在配置时应避免循环依赖以保证系统启动的顺利进行。|
|多实例个数|0 - 1|
|目标类型|ECUC-MODULE-CONFIGURATION-VALUES|

#### 1.2.3. EcuMFlexUserConfig

|容器属性|值（容器）|
|---|---|
|名称|EcuMFlexUserConfig|
|描述|These containers describe the identifiers that are needed to refer to a software component or another appropriate entity in the system which uses the EcuMFlex Interfaces.|
|描述|概述：EcuMFlexUserConfig 是一个配置参数，用于定义ECU管理模块（EcuM）中用户可定制的行为和属性，以适应不同的硬件和软件需求。|
|描述|注意：在配置EcuMFlexUserConfig时，必须确保所有的用户定义设置与AUTOSAR CP 4.4标准中规定的EcuM模块的参数兼容；用户需要根据具体的ECU硬件特性和软件架构来定制这些参数；不当的配置可能会影响系统的启动流程和运行效率。|
|多实例个数|1 - 256|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|EcuMFlexUser|
|描述|Parameter used to identify one user.|
|描述|概述：EcuMFlexUser配置项用于定义ECU管理模块中的用户自定义功能，允许开发者在ECU管理框架内实现特定的业务逻辑。|
|描述|注意：该配置项在AUTOSAR CP 4.4标准中未明确定义，因此在使用时需要特别注意与标准的兼容性和集成方式；开发者应确保自定义功能不会干扰ECU管理框架的核心功能；在实现自定义功能时，应遵循AUTOSAR的基本设计原则，确保系统的稳定性和可维护性。|
|多实例个数|1 - 1|
|取值范围|0 - 255|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|EcuMFlexEcucPartitionRef|
|描述|Denotes in which "EcucPartition" the user of the EcuM is executed.|
|描述|概述：EcuMFlexEcucPartitionRef 是一个配置参数，用于引用ECU管理模块中的特定ECUC分区，这有助于在ECU中管理不同的软件组件和应用。|
|描述|注意：确保引用的ECUC分区在系统中是存在的；正确的分区引用对于系统资源的分配和管理至关重要；在多核ECU配置中，分区的分配应考虑核间的负载平衡和通信需求。|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/EcuC/EcucPartitionCollection/EcucPartition|

#### 1.2.4. EcuMGoDownAllowedUsers

|容器属性|值（容器）|
|---|---|
|名称|EcuMGoDownAllowedUsers|
|描述|This container describes the collection of allowed users which are allowed to call the EcuM_GoDownHaltPoll API (only applies in the case that the previously set shutdown target is TARGET_RESET or TARGET_OFF).|
|描述|概述：EcuMGoDownAllowedUsers配置项定义了在执行ECU关机过程中允许参与的用户列表，这些用户可以是软件组件或者系统服务，它们有权限请求或者阻止ECU进入关机状态。|
|描述|注意：确保所有需要在ECU关机过程中执行特定操作的用户都被正确列出；未在此列表中的用户将无法阻止ECU关机；在配置此项时，需要考虑系统的安全和实时性要求，避免不必要的关机延迟。|
|多实例个数|0 - 1|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|EcuMGoDownAllowedUserRef|
|描述|This references an allowed user.|
|描述|概述：EcuMGoDownAllowedUserRef 用于引用允许发起ECU关机过程的用户定义实体，确保只有授权的用户或实体可以触发ECU的关机。|
|描述|注意：确保所有引用的用户或实体都是经过验证的，以防止未授权的关机操作；在多用户系统中，应详细管理和审查每个用户的权限设置；此配置项应与系统的安全需求严格对应，避免安全漏洞。|
|多实例个数|1 - inf|
|目标引用项的路径|/AUTOSAR/EcucDefs/EcuM/EcuMConfiguration/EcuMFlexConfiguration/EcuMFlexUserConfig|

#### 1.2.5. EcuMResetMode

|容器属性|值（容器）|
|---|---|
|名称|EcuMResetMode|
|描述|These containers describe the configured reset modes.|
|描述|概述：EcuMResetMode配置项用于定义电子控制单元(ECU)的复位模式，这包括了软件复位、硬件复位等不同类型的复位方式，以确保系统能够按照预期的方式重新启动或恢复。|
|描述|注意：在配置EcuMResetMode时，需要确保所选复位模式与硬件支持和系统需求相匹配；复位模式的选择会影响系统的恢复时间和稳定性；AUTOSAR CP 4.4标准中，对复位模式的定义和管理提供了详细的规范，需要遵循这些规范以确保兼容性。|
|说明|The name of these containers allows one of the following symbolic names to be given to the different reset modes: - ECUM_RESET_MCU - ECUM_RESET_WDG - ECUM_RESET_IO.|
|多实例个数|1 - 256|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|EcuMResetModeId|
|描述|This ID identifies this reset mode in services like EcuM_SelectShutdownTarget.|
|描述|概述：EcuMResetModeId 是一个配置项，用于定义电子控制单元管理（EcuM）模块中的复位模式标识符，这些标识符用于区分不同的复位原因和类型。|
|描述|注意：在配置EcuMResetModeId时，需要确保每个复位模式具有唯一的标识符；此外，应当与系统设计文档中定义的复位策略保持一致；在实现时，还需注意与实际硬件复位信号和诊断工具的交互是否匹配。|
|多实例个数|1 - 1|
|取值范围|0 - 255|

#### 1.2.6. EcuMSetClockAllowedUsers

|容器属性|值（容器）|
|---|---|
|名称|EcuMSetClockAllowedUsers|
|描述|This container describes the collection of allowed users which are allowed to call the EcuM_SetClock API.|
|描述|概述：EcuMSetClockAllowedUsers配置项定义了允许设置ECU时钟的用户列表，确保只有授权的软件组件可以修改ECU的系统时钟。|
|描述|注意：在配置时需确保列表中的用户或组件确实需要时钟设置权限，以避免安全风险；该配置项在AUTOSAR CP 4.4中可能不直接显式存在，需要根据具体的ECU管理需求进行合理解释和应用；不当的时钟设置权限分配可能会影响系统的稳定性和安全性。|
|多实例个数|0 - 1|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|EcuMSetClockAllowedUserRef|
|描述|These parameters describe the references to the users which are allowed to call the EcuM_SetClock API.|
|描述|概述：EcuMSetClockAllowedUserRef用于定义哪些用户（模块或组件）被允许设置ECU的系统时钟。|
|描述|注意：在配置时，确保只有信任的模块或组件被授权，以防止系统时钟被恶意或错误地修改；此配置项在AUTOSAR CP 4.4中应与系统的安全需求相一致；不当的配置可能会影响系统的时间敏感操作。|
|多实例个数|1 - inf|
|目标引用项的路径|/AUTOSAR/EcucDefs/EcuM/EcuMConfiguration/EcuMFlexConfiguration/EcuMFlexUserConfig|

#### 1.2.7. EcuMShutdownCause

|容器属性|值（容器）|
|---|---|
|名称|EcuMShutdownCause|
|描述|These containers describe the configured shut down or reset causes.|
|描述|概述：EcuMShutdownCause配置项用于定义系统关闭的原因，它允许系统根据不同的关闭原因执行相应的关闭策略或过程。|
|描述|注意：在配置EcuMShutdownCause时，需要确保每个定义的关闭原因都与系统设计和需求相匹配；此外，AUTOSAR CP 4.4标准可能对可用的关闭原因和它们的处理方式有特定的要求或限制，需要仔细遵守；在实现时，应考虑如何有效地记录和诊断不同的关闭原因，以便于系统维护和问题排查。|
|说明|The name of these containers allows to give one of the following symbolic names to the different shut down causes: - ECUM_CAUSE_ECU_STATE - ECU state machine entered a state for shutdown, - ECUM_CAUSE_WDGM - WdgM detected failure, - ECUM_CAUSE_DCM - Dcm requests shutdown (split into UDS services?), - and values from configuration.|
|多实例个数|1 - 256|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|EcuMShutdownCauseId|
|描述|This ID identifies this shut down cause.|
|描述|概述：EcuMShutdownCauseId用于唯一标识导致ECU关机的原因，这有助于系统在重新启动时进行故障诊断和恢复。|
|描述|注意：确保每个EcuMShutdownCauseId是唯一的，以避免诊断信息的混淆；在设计时应考虑所有可能的关机原因，包括软件和硬件故障；AUTOSAR CP 4.4标准中，关机原因的管理和识别应遵循EcuM模块的规范。|
|多实例个数|1 - 1|
|取值范围|0 - 255|

## 2. EcuMFlexGeneral

|容器属性|值（容器）|
|---|---|
|名称|EcuMFlexGeneral|
|描述|This container holds the general, pre-compile configuration parameters for the EcuMFlex.|
|描述|概述：EcuMFlexGeneral配置项包含了用于ECU管理模块（EcuM）的一般性配置参数，这些参数控制ECU的启动行为、模式管理和诊断通信等。|
|描述|注意：在配置EcuMFlexGeneral时，需要确保参数设置符合项目的具体需求和硬件特性；此外，应当遵循AUTOSAR CP 4.4标准中对于EcuM模块的配置要求和限制；在多核或多ECU系统中，还需注意EcuM配置的一致性和互操作性。|
|说明|Only applicable if EcuMFlex is implemented.|
|多实例个数|0 - 1|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|EcuMAlarmClockPresent|
|描述|This flag indicates whether the optional AlarmClock feature is present.|
|描述|概述：EcuMAlarmClockPresent 配置项用于指示ECU管理模块（EcuM）是否支持闹钟功能，这是一种唤醒ECU的机制，可以在预定的时间点唤醒系统。|
|描述|注意：在AUTOSAR CP 4.4标准中，闹钟功能是可选的，因此只有在系统需要定时唤醒功能时才配置此项为真；如果硬件不支持此功能，该配置项应设置为假；确保与硬件抽象层（MCAL）的闹钟驱动配置保持一致。|
|多实例个数|1 - 1|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|EcuMModeHandling|
|描述|If false, Run Request Protocol is not performed.|
|描述|概述：EcuMModeHandling 配置项用于定义ECU管理模块（EcuM）如何处理不同的ECU模式，包括启动、运行、休眠等模式，并指定在这些模式下的行为和转换。|
|描述|注意：在配置EcuMModeHandling时，需要确保模式之间的转换逻辑符合系统的安全和性能要求；此外，应当遵循AUTOSAR CP 4.4标准中对于ECU模式管理的规范，包括模式定义和转换触发条件；最后，要注意与其他BswM（基础软件模块管理）和Rte（运行时环境）的交互，确保模式转换的一致性和正确性。|
|多实例个数|0 - 1|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|EcuMResetLoopDetection|
|描述|If false, no reset loop detection is performed. If this configuration parameter exists and is set to true, the callout "EcuM_LoopDetection" is called during startup of EcuM (during StartPreOS).|
|描述|概述：EcuMResetLoopDetection配置项用于启用或禁用ECU管理模块（EcuM）中的复位循环检测机制，该机制用于识别并处理系统可能进入的复位循环状态。|
|描述|注意：在配置EcuMResetLoopDetection时，需要确保其行为与系统的故障恢复策略相匹配；过于频繁的复位可能指示系统存在严重问题，应进行进一步的诊断；AUTOSAR CP 4.4标准中可能有具体的参数和阈值设定要求，需要根据标准进行配置。|
|多实例个数|0 - 1|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|EcuMSetProgrammableInterrupts|
|描述|If this configuration parameter exists and is to true, the callout "EcuM_AL_SetProgrammableInterrupts" is called during startup of EcuM (during StartPreOS).|
|描述|概述：EcuMSetProgrammableInterrupts配置项用于定义ECU管理模块（EcuM）初始化期间需要设置的可编程中断，这通常包括中断源和中断服务例程的配置。|
|描述|注意：在配置EcuMSetProgrammableInterrupts时，需要确保中断优先级符合系统要求，并且不会与其他中断源发生冲突；此配置项应与微控制器抽象层（MCAL）中断配置保持一致，以确保系统稳定性；在多核系统中，还需要注意中断分配策略，以避免跨核中断处理的复杂性。|
|多实例个数|0 - 1|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|EcuMAlarmWakeupSource|
|描述|This parameter describes the reference to the EcuMWakeupSource being used for the EcuM AlarmClock.|
|描述|概述：EcuMAlarmWakeupSource 配置项用于定义通过ECU管理模块的报警唤醒源，这些唤醒源可以是内部或外部的报警器。|
|描述|注意：确保唤醒源的标识符与系统中其他唤醒源不冲突；在配置时需考虑报警的优先级和响应时间；该配置项应与实际硬件和外部设备的支持能力相匹配。|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/EcuM/EcuMConfiguration/EcuMCommonConfiguration/EcuMWakeupSource|

## 3. EcuMGeneral

|容器属性|值（容器）|
|---|---|
|名称|EcuMGeneral|
|描述|This container holds the general, pre-compile configuration parameters.|
|描述|概述：EcuMGeneral是AUTOSAR ECU管理模块的一般配置容器，包含了启动、关闭和ECU管理模式切换等基本行为的配置参数。|
|描述|注意：在配置EcuMGeneral时，需要确保所选参数与ECU硬件和项目需求相匹配；对于多核系统，还需考虑核间通信和同步的配置；此外，AUTOSAR版本更新可能会引入新的配置参数或弃用旧参数，务必参考最新的AUTOSAR CP 4.4标准文档。|
|多实例个数|1 - 1|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|EcuMDevErrorDetect|
|描述|Switches the development error detection and notification on or off.|
|描述|概述：EcuMDevErrorDetect是一个配置参数，用于启用或禁用ECU管理模块（EcuM）的开发错误检测功能，以便在开发阶段识别和报告潜在的配置或运行时错误。|
|描述|注意：在生产代码中通常禁用此功能以优化性能；确保在开发和测试阶段启用以便及时发现问题；此配置项与AUTOSAR标准一致，但实际使用时需考虑对系统性能的影响。|
|说明|\* true: detection and notification is enabled. \* false: detection and notification is disabled.|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|EcuMIncludeDet|
|描述|If defined, the according BSW module will be initialized by the ECU State Manager|
|描述|概述：EcuMIncludeDet 配置项决定是否在ECU管理模块中包含开发错误检测（Development Error Tracer, DET）。|
|描述|注意：在AUTOSAR CP 4.4标准中，通常建议在开发和测试阶段包含DET以便于错误追踪和调试；在生产环境中，可能因性能考虑而禁用DET；确保配置正确反映项目的当前阶段需求。|
|多实例个数|1 - 1|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|EcuMVersionInfoApi|
|描述|Switches the version info API on or off|
|描述|概述：EcuMVersionInfoApi是一个配置项，用于启用或禁用ECU管理模块（EcuM）的版本信息API，允许软件组件获取当前EcuM模块的版本信息。|
|描述|注意：在AUTOSAR CP 4.4标准中，启用此API可能会增加额外的内存占用和执行时间；确保在需要进行诊断或监控时才启用此功能；在生产环境中，出于优化考虑，可能会选择禁用此API。|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（浮点型参数配置项）|
|---|---|
|名称|EcuMMainFunctionPeriod|
|描述|This parameter defines the schedule period of EcuM_MainFunction.|
|描述|概述：EcuMMainFunctionPeriod配置项定义了ECU管理模块（EcuM）主函数的调用周期，这是ECU状态管理和诊断通信等功能的基础时间单位。|
|描述|注意：该配置项的值必须与实际的操作系统调度周期相匹配，以确保EcuM主函数能够按照预期频率执行；过小的周期可能导致系统资源过度消耗，而过大的周期可能影响系统响应性；在AUTOSAR CP 4.4标准中，该值通常以毫秒为单位进行配置。|
|说明|Unit: [s]|
|多实例个数|1 - 1|
|取值范围|0 - Inf|
