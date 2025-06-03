# comm 接口参考文档

> 提示：本API参考文档仅代表功能栈的接口描述和功能说明，帮助开发者快速了解接口作用。应用开发者应通过服务映射调用对应的RTE接口，而非直接调用本文接口

## `comm_init`

|属性|描述|
|---|---|
|函数定义|`void comm_init(const comm_config_type *config)`|
|简要描述|comm 初始化 |
|详细说明|初始化配置 |
|参数[输入]|`config` 配置项指针 |
|同步/异步|同步|
|可重入性|不可重入|

## `comm_deinit`

|属性|描述|
|---|---|
|函数定义|`void comm_deinit(void)`|
|简要描述|comm 反初始化 |
|详细说明|comm 反初始化 |
|同步/异步|同步|
|可重入性|不可重入|

## `comm_bus_sm_mode_indication`

|属性|描述|
|---|---|
|函数定义|`void comm_bus_sm_mode_indication(NetworkHandleType channel, const comm_mode_type *com_mode)`|
|简要描述|通信方式指示 |
|详细说明|通知通信管理器（comm）有关网络频道的当前通信模式 |
|参数[输入]|`channel` 用于标识网络频道的网络句柄 |
|参数[输入]|`com_mode` 指向当前通信模式的指针 |
|同步/异步|同步|
|可重入性|不可重入|

## `comm_get_state`

|属性|描述|
|---|---|
|函数定义|`Std_ReturnType comm_get_state(NetworkHandleType channel, comm_state_type *state)`|
|简要描述|获取comm子状态 |
|详细说明|查询指定网络频道的当前通信管理器（comm）状态 |
|参数[输入]|`channel` 用于标识网络频道的网络句柄 |
|参数[输入]|`state` 指向用于接收当前comm状态的变量的指针 |
|返回值|E_OK 执行成功|
|返回值|E_NOT_OK 执行失败|
|同步/异步|同步|
|可重入性|不可重入|

## `comm_get_status`

|属性|描述|
|---|---|
|函数定义|`Std_ReturnType comm_get_status(NetworkHandleType channel, comm_state_type *state)`|
|简要描述|获取comm子状态 |
|详细说明|查询指定网络频道的当前通信管理器（comm）状态 |
|参数[输入]|`channel` 用于标识网络频道的网络句柄 |
|参数[输入]|`state` 指向用于接收当前comm状态的变量的指针 |
|返回值|E_OK 执行成功|
|返回值|E_NOT_OK 执行失败|
|同步/异步|同步|
|可重入性|不可重入|

## `comm_request_com_mode`

|属性|描述|
|---|---|
|函数定义|`Std_ReturnType comm_request_com_mode(comm_user_handle_type user, comm_mode_type com_mode)`|
|简要描述|用户请求通信模式 |
|详细说明|由用户请求一个特定的通信模式 |
|参数[输入]|`user` 用户句柄，用于标识发出通信模式请求的用户 |
|参数[输入]|`com_mode` 请求的通信模式，如comm_mode_type所定义的通信模式 |
|返回值|E_OK 执行成功|
|返回值|E_NOT_OK 执行失败|
|同步/异步|同步|
|可重入性|不可重入|

## `comm_communication_allowed`

|属性|描述|
|---|---|
|函数定义|`void comm_communication_allowed(NetworkHandleType channel, boolean allowed)`|
|简要描述|设置通信允许状态 |
|详细说明|当允许通信时，ecum 或 bswm 应向 comm 指示 |
|参数[输入]|`channel` 网络通道的句柄，指定将受到控制的通信通道 |
|参数[输入]|`allowed` 布尔值，表示通信是否被允许。true表示允许通道上的通信，false表示禁止通道上的通信 |
|同步/异步|同步|
|可重入性|不可重入|

## `comm_main_function`

|属性|描述|
|---|---|
|函数定义|`void comm_main_function(NetworkHandleType channel)`|
|简要描述|comm 主函数 |
|详细说明|comm 主函数 |
|参数[输入]|`channel` 网络通道的句柄，指定将受到控制的通信通道 |
|同步/异步|同步|
|可重入性|不可重入|
