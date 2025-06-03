# time_user_api 配置项参考文档

|容器属性|值（容器）|
|---|---|
|名称|StbM|
|描述|Configuration of the Synchronized Time-base Manager (StbM) module.|
|描述|概述：StbM (Synchronized Time-base Manager) 是用于管理系统时间同步和时间戳服务的模块，确保系统中各组件的时间一致性。|
|描述|注意：在配置StbM时，需要确保与网络管理和通信堆栈的时间同步需求相匹配；StbM配置应支持高精度时间同步协议，如IEEE 1588；在分布式系统中，特别注意跨节点的时间同步精度和稳定性。|
|多实例个数|0 - 1|

## 1. StbMGeneral

|容器属性|值（容器）|
|---|---|
|名称|StbMGeneral|
|描述|This container holds the general parameters of the Synchronized Time-base Manager|
|描述|概述：StbMGeneral是同步时间基管理模块（Synchronized Time-base Manager）的一般配置参数，用于定义全局属性，如模块的开启或关闭，时间源的选择等。|
|描述|注意：在配置StbMGeneral时，需要确保选择的时间源与系统中其他模块的时间需求一致；如果系统不需要精确的时间同步，可以关闭StbM模块以节省资源。|
|多实例个数|1 - 1|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|StbMDevErrorDetect|
|描述|Switches the development error detection and notification on or off.|
|描述|概述：StbMDevErrorDetect配置项用于开启或关闭同步时间基管理（StbM）模块的开发错误检测功能，以便在开发阶段识别和报告模块内部的错误。|
|描述|注意：在生产代码中通常禁用此功能以优化性能；确保在开发和测试阶段启用以捕获潜在错误。|
|说明|\* true: detection and notification is enabled. \* false: detection and notification is disabled.|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（浮点型参数配置项）|
|---|---|
|名称|StbMMainFunctionPeriod|
|描述|Schedule period of the main function tm_mainfunction. Unit: [s].|
|描述|概述：StbMMainFunctionPeriod配置项定义了同步时间基管理模块（StbM）主函数的调用周期，即StbM主函数多久被调度执行一次。|
|描述|注意：该配置项的值应当与系统的时间同步需求相匹配，确保时间管理的精确性；配置的周期值必须是实际ECU调度器可以支持的周期；在配置时需要考虑ECU的性能，以避免因为过高的调用频率导致系统资源过载。|
|多实例个数|1 - 1|
|取值范围|0 - Inf|

## 2. StbMSynchronizedTimeBase

|容器属性|值（容器）|
|---|---|
|名称|StbMSynchronizedTimeBase|
|描述|Synchronized time.base collects the information about a specific time-base provider within the system.|
|描述|概述：StbMSynchronizedTimeBase配置项用于定义系统时间基准的同步策略，确保系统中的各个组件能够基于一个统一的时间参考进行操作和通信。|
|描述|注意：在配置StbMSynchronizedTimeBase时，需要确保所选同步策略与系统的实时性要求和通信策略相匹配；此外，对于分布式系统，还需考虑网络延迟和时钟偏差的补偿机制。|
|多实例个数|1 - inf|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|StbMAllowSystemWideGlobalTimeMaster|
|描述|For postbuild variant of the StbM this parameter has to be set to true for a Global Time Master that may act as a system-wide source of time. Otherwise no corresponding service ports/interfaces is provided.|
|描述|概述：StbMAllowSystemWideGlobalTimeMaster配置项用于指定系统是否允许存在一个全局的时间主控（Global Time Master），这个主控负责维护系统范围内的时间同步。|
|描述|注意：在设计系统时，需要考虑是否有必要启用全局时间主控，以及如何选举或指定该主控；此配置项对于实现跨ECU的时间同步非常关键。|
|说明|The Global Time Master functionality behind the service ports/interfaces has to be enabled/disabled separately via parameter StbMIsSystemWideGlobalTimeMaster.|
|多实例个数|0 - 1|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|StbMIsSystemWideGlobalTimeMaster|
|描述|This parameter shall be set to true for a Global Time Master that acts as a system-wide source of time information with respect to Global Time.|
|描述|概述：StbMIsSystemWideGlobalTimeMaster 配置项用于指定是否将当前模块配置为系统范围的全局时间主控（Global Time Master），这决定了模块是否负责提供和维护系统时间。|
|描述|注意：在一个系统中只能有一个全局时间主控，以确保时间同步的一致性；如果多个模块被错误地配置为全局时间主控，可能会导致系统时间同步冲突；正确配置此项对于实现基于时间的通信和同步操作至关重要。|
|说明|It is possible that several Global Time Masters exist that have set this parameter set to true because the Global Time Masters exist once per Global Time Domain and one ECU may own several Global Time Domains on different buses it is connected to.|
|多实例个数|1 - 1|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|StbMSynchronizedTimeBaseIdentifier|
|描述|Identification of a Synchronized TimeBase via a unique identifier.|
|描述|概述：StbMSynchronizedTimeBaseIdentifier 用于标识同步时间基，这是一个用于时间同步和时间戳服务的关键配置项。|
|描述|注意：确保每个StbMSynchronizedTimeBaseIdentifier在系统中是唯一的，以避免时间同步冲突；正确配置时间基以确保系统中的时间敏感操作的准确性；在分布式系统中特别注意时间同步的精度和一致性。|
|说明|Range: \* 0 .. 15: Synchronized Time Bases \* 16 .. 31: Offset Time Bases \* 32 .. 127: Pure Local Time Bases \* 128 .. 65535: Reserved|
|多实例个数|1 - 1|
|取值范围|0 - 15|

### 2.1. StbMLocalTimeClock

|容器属性|值（容器）|
|---|---|
|名称|StbMLocalTimeClock|
|描述|References the hardware reference clock of this Synchronized Time Base.|
|描述|概述：StbMLocalTimeClock 是一个配置项，用于定义系统时间基准管理（StbM）模块中的本地时钟属性，这些属性包括时钟源、时钟有效性和时间同步等信息。|
|描述|注意：在配置StbMLocalTimeClock时，需要确保选择的时钟源与系统中实际可用的时钟源相匹配；此外，应当注意时钟同步策略的配置，以保证系统时间的准确性和一致性。|
|多实例个数|0 - 1|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|StbMClockFrequency|
|描述|Represents the frequency [Hz] of the HW reference clock used by the StbM.|
|描述|概述：StbMClockFrequency 用于定义系统时钟的频率，这是控制和管理硬件时钟速度的关键参数。|
|描述|注意：必须确保StbMClockFrequency的设置与硬件规格相匹配，避免时钟频率过高导致硬件损坏；在配置时应考虑系统的实时性需求和功耗优化；该参数的设置应由系统架构师或硬件工程师确定，以保证系统的稳定运行。|
|多实例个数|0 - 1|
|取值范围|0 - 4294967295|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|StbMClockPrescaler|
|描述|Represents the prescaler to calculate the resulting frequency of the HW reference clock used by the StbM.|
|描述|概述：StbMClockPrescaler 是一个配置项，用于设置系统定时器模块（StbM）的时钟预分频值，这个值决定了系统时间基准的精度和分辨率。|
|描述|注意：在配置StbMClockPrescaler时，需要确保预分频值与系统时钟和所需的时间精度相匹配；不正确的预分频设置可能会导致时间管理不准确；此外，预分频值应该符合ECU硬件能力和性能要求。|
|多实例个数|0 - 1|
|取值范围|0 - 4294967295|

|配置项属性|值（选择引用配置项）|
|---|---|
|名称|StbMLocalTimeHardware|
|描述|Reference to the local time hardware.|
|多实例个数|1 - 1|
