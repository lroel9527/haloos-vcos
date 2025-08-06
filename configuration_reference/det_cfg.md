# Det 配置项参考文档

|容器属性|值（容器）|
|---|---|
|名称|Det|
|描述|Configuration of the Default Error Tracer (Det) module.|
|描述|概述：概述：Det（Default Error Tracer）模块用于提供开发时错误跟踪功能，它记录软件模块在运行时发生的开发错误，并提供错误报告机制。|
|描述|注意：Det模块的配置应确保与系统的错误处理策略一致；Det模块通常在开发和测试阶段使用，而在生产环境中可能被禁用或配置为最小化资源占用；配置Det时，应注意不同错误级别的区分和相应的错误处理动作。|
|多实例个数|0 - 1|

## 1. DetGeneral

|容器属性|值（容器）|
|---|---|
|名称|DetGeneral|
|描述|Generic configuration parameters of the Det module.|
|描述|概述：DetGeneral用于定义开发错误检测（Default Error Tracer, DET）模块的一般属性，如版本信息和错误记录机制。|
|描述|注意：错误记录机制的配置应考虑系统资源和性能要求；在配置错误记录级别时，需平衡开发调试的需求和系统的运行效率。|
|多实例个数|0 - 1|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|DetVersionInfoApi|
|描述|Pre-processor switch to enable / disable the API to read out the modules version information.|
|描述|概述：DetVersionInfoApi 是一个配置参数，用于启用或禁用开发错误跟踪器（Default Error Tracer, DET）模块中的版本信息API，该API允许获取模块的版本信息，如供应商ID、模块版本等。|
|描述|注意：如果启用了该配置项，则必须实现相应的版本信息接口函数；如果不需要模块版本信息，可以禁用以节省资源；确保与其他模块的版本信息获取方式保持一致性。|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|FlowControlEnable|
|描述|Is flow control enabled.|
|描述|FlowControlEnable 是一个配置参数，用于启用或禁用开发错误跟踪器（Default Error Tracer, DET）模块中的流量控制功能。|
|描述|注意：如果启用了该配置项，则可能因为流量控制，导致部分DET信息不上报。|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DetTokenNum|
|描述|The upper limit of the number of Det that a single module can print per unit time.|
|描述|概述：det默认的令牌桶数量。|
|描述|注意：需要配合令牌桶进行使用。|
|多实例个数|1 - 1|
|默认值|20|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|DetTokenPeriod|
|描述|The upper limit of the number of Det that a single module can print per unit time.|
|描述|概述：配置Det令牌桶的周期。|
|描述|注意：需要配合ModuleTokenNum配置项使用，ModuleTokenNum用于Det令牌桶的个数。|
|多实例个数|1 - 1|
|默认值|1024|

## 2. DetNotification

|容器属性|值（容器）|
|---|---|
|名称|DetNotification|
|描述|Configuration of the notification functions.|
|描述|概述：DetNotification用于定义诊断事件管理器（Diagnostic Event Manager, DEM）在检测到特定错误时，通知开发错误跟踪（Default Error Tracer, DET）的机制。|
|描述|注意：确保DetNotification配置与DEM和DET模块的交互逻辑一致；配置时需注意错误级别和通知策略，以避免过多的性能开销；此配置项对于错误诊断和系统稳定性至关重要，需谨慎处理。|
|多实例个数|0 - 1|

|配置项属性|值（字符串参数配置项）|
|---|---|
|名称|DetErrorHook|
|描述|Optional list of functions to be called by the Default Error Tracer in context of each call of Det_ReportError.|
|描述|概述：DetErrorHook是一个配置项，用于定义是否启用开发错误跟踪（Default Error Tracer, DET）的错误钩子函数，该函数在检测到开发时错误时被调用。|
|描述|注意：启用DetErrorHook可能会影响系统性能，因为每次错误检测都会调用该钩子函数；确保错误处理逻辑不会引入新的错误或异常；在资源受限的系统中谨慎使用，以避免过多消耗CPU时间和内存。|
|多实例个数|0 - 65535|

|配置项属性|值（字符串参数配置项）|
|---|---|
|名称|DetReportRuntimeErrorCallout|
|描述|This parameter defines the existence and the names of callout functions for the corresponding runtime error handler.|
|描述|概述：DetReportRuntimeErrorCallout 是一个配置项，用于定义在检测到运行时错误时调用的回调函数。|
|描述|注意：回调函数需要能够处理所有传入的错误参数；避免在回调函数中执行复杂或耗时的操作，以免影响系统性能。|
|多实例个数|0 - 65535|

|配置项属性|值（字符串参数配置项）|
|---|---|
|名称|DetReportTransientFaultCallout|
|描述|This parameter defines the existence and the names of callout functions for the corresponding transient fault handler.|
|描述|概述：DetReportTransientFaultCallout 是一个配置项，用于定义在检测到瞬态故障时调用的回调函数。|
|描述|注意：回调函数应具备高效处理故障的能力，避免影响系统性能；在多核或多任务环境中，确保回调函数的线程安全性。|
|多实例个数|0 - 65535|
