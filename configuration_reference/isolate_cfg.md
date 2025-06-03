# Isolate 配置项参考文档

| 容器属性 | 值（容器） |
|-|-|
|名称|Isolate|
|描述|Configuration of Isolate Module.|
|描述|Isolate 模块的配置.|
|多实例个数|0 - 1|

## 1. Module

| 容器属性 | 值（容器） |
|-|-|
|名称|Module|
|描述|This container consists of isolate modules' configuration and subcontainer.|
|描述|这个容器包含软软解耦模块软件组件的配置参数和子容器.|
|描述|概述：Module配置项在AUTOSAR中用于定义软件模块的属性，包括模块的名称、供应商信息、版本号等，是软件组件描述文件中的一个基本构成部分。|
|描述|注意：在配置Module时，确保模块名称的唯一性和标识性，以避免在软件架构中产生混淆；遵循AUTOSAR规定的版本号格式，以确保兼容性和追溯性；供应商信息应准确无误，以便于模块的管理和维护。|
|多实例个数|0 - inf|

| 配置项属性 | 值（关联引用配置项） |
|-|-|
|名称|OsApplicationRef|
|描述|The owner application of the current isolate module.|
|描述|当前软件组件所部署的OsApplication的引用.|
|描述|概述：OsApplicationRef 是一个配置项，用于指定一个OS应用程序对象的引用，该对象通常用于定义软件组件或模块与操作系统应用程序之间的关联。|
|描述|注意：在配置OsApplicationRef时，需要确保引用的OS应用程序已经在系统中定义；此外，该引用必须符合操作系统的隔离和保护级别要求；在多核系统中，还需考虑应用程序与特定核心的绑定关系。|
|多实例个数|1 - 31|
|目标引用项的路径|/AUTOSAR/EcucDefs/Os/OsApplication|

### 1.1. PPCFunction

| 容器属性 | 值（容器） |
|-|-|
|名称|PPCFunction|
|描述|The PPCFunction configuration of the current software module|
|描述|当前软件组件的PPCFunction配置|
|多实例个数|0 - inf|

| 配置项属性 | 值（函数名配置项） |
|-|-|
|名称|PPCFunctionName|
|描述|PPCFunction name.|
|描述|PPCFunction 名称.|
|多实例个数|1 - 1|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|IsolateCallRetRequired|
|描述|whether there is a return value.|
|描述|是否有返回值.|
|描述|概述：VariadicArguments 配置项用于定义一个接口或操作可以接受可变数量的参数，这通常用于那些需要处理不定数量参数的函数。|
|描述|注意：在AUTOSAR中，接口通常具有固定数量的参数，因此VariadicArguments的使用并不符合AUTOSAR CP 4.4的标准接口定义；如果需要使用可变参数功能，应当通过其他机制如数组或列表来实现；在设计接口时应避免使用可变参数，以保持与AUTOSAR标准的兼容性。|
|多实例个数|1 - 1|
|默认值|false|

| 配置项属性 | 值（字符串参数配置项） |
|-|-|
|名称|IsolateCallRetType|
|描述|PPC call return type.|
|描述|PPC 返回类型.|
|描述|概述：IsolateCallRetType用于声明PPC函数返回类型名称。|
|描述|注意：此配置项只能在IsolateCallRetRequired打开时配置；当IsolateCallRetRequired打开，但此配置项为空时，生成代码会默认地使用int类型为IsolateCallRetType；配置正确的返回类型可避免类型转换带来的编译器警告。|
|多实例个数|0 - 1|
|默认值|NULL|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|IsolateCallParamNumber|
|描述|The number of parameters of this function.|
|描述|函数调用的参数数量.|
|描述|概述：IsolateCallParamNumber 用于定义在AUTOSAR环境中，某个隔离函数调用时传递的参数数量。|
|描述|注意：此配置项必须与实际在代码中实现的隔离函数的参数数量一致，以避免运行时错误；在AUTOSAR CP 4.4标准中，确保参数数量的正确性是关键，以保证系统的稳定性和安全性；参数数量的配置错误可能导致系统崩溃或不可预测的行为。|
|多实例个数|1 - 1|
|默认值|0|
|取值范围|0 - 255|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|VariadicArguments|
|描述|Configuration of whether this API has variadic function arguments.|
|描述|当前接口是否含有可变参数|
|多实例个数|1 - 1|
|默认值|false|
