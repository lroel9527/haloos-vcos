# time_user_api 接口参考文档

> 提示：本API参考文档仅代表功能栈的接口描述和功能说明，帮助开发者快速了解接口作用。应用开发者应通过服务映射调用对应的RTE接口，而非直接调用本文接口

## `tm_get_current_time`

|属性|描述|
|---|---|
|函数定义|`Std_ReturnType tm_get_current_time(tm_synchronized_time_base_type time_base_id, tm_timestamp_type *timestamp_ptr, tm_user_data_type *user_data_ptr)`|
|简要描述|获取当前时间 |
|详细说明|获取指定时间基上的当前时间和用户定义的数据|
|参数[输入]|`tm_synchronized_time_base_type time_base_id` 时间基的唯一标识 |
|参数[输出]|`tm_timestamp_type timestamp_ptr` 指向时间戳结构体的指针 |
|参数[输出]|`tm_user_data_type user_data_ptr` 指向用户数据结构体的指针 |
|同步/异步|同步|
|可重入性|可重入|

## `tm_init`

|属性|描述|
|---|---|
|函数定义|`void tm_init(const tm_config_type *config_ptr)`|
|简要描述|初始化user_api |
|详细说明|初始化user_api模块|
|参数[输入]|`const tm_config_type *config_ptr` 指向配置参数结构体的指针 |
|同步/异步|同步|
|可重入性|不可重入|

## `tm_get_current_time_raw`

|属性|描述|
|---|---|
|函数定义|`Std_ReturnType tm_get_current_time_raw(tm_synchronized_time_base_type time_base_id, tm_timestamp_raw_type *timestamp_ptr)`|
|简要描述|获取当前时间（纳秒部分） |
|详细说明|获取指定时间基上的当前时间（纳秒部分）|
|参数[输入]|`tm_synchronized_time_base_type time_base_id` 时间基的唯一标识 |
|参数[输出]|`tm_timestamp_raw_type timestamp_ptr` 指向时间戳结构体的指针 |
|同步/异步|同步|
|可重入性|不可重入|

## `tm_get_current_virtual_local_time`

|属性|描述|
|---|---|
|函数定义|`Std_ReturnType tm_get_current_virtual_local_time(tm_synchronized_time_base_type time_base_id, tm_virtual_local_time_type *local_time_ptr)`|
|简要描述|获取当前虚拟本地时间 |
|详细说明|获取指定时间基上当前的虚拟本地时间|
|参数[输入]|`tm_synchronized_time_base_type time_base_id` 时间基的唯一标识 |
|参数[输出]|`tm_virtual_local_time_type local_time_ptr` 指向虚拟本地时间结构体的指针 |
|同步/异步|同步|
|可重入性|不可重入|

## `tm_bus_set_global_time`

|属性|描述|
|---|---|
|函数定义|`Std_ReturnType tm_bus_set_global_time(tm_synchronized_time_base_type time_base_id, const tm_timestamp_type *global_time_ptr, const tm_user_data_type *user_data_ptr, const tm_measurement_type *measure_data_ptr, const tm_virtual_local_time_type *local_time_ptr)`|
|简要描述|设置全局时间 |
|详细说明|允许时间基提供模块设置全局时间|
|参数[输入]|`tm_synchronized_time_base_type time_base_id` 时间基的唯一标识 |
|参数[输入]|`tm_timestamp_type global_time_ptr` 指向全局时间结构体的指针 |
|参数[输入]|`tm_user_data_type user_data_ptr` 指向用户数据结构体的指针 |
|参数[输入]|`tm_measurement_type measure_data_ptr` 指向测量数据结构体的指针 |
|参数[输入]|`tm_virtual_local_time_type local_time_ptr` 指向虚拟本地时间结构体的指针 |
|同步/异步|同步|
|可重入性|不可重入|

## `tm_set_global_time`

|属性|描述|
|---|---|
|函数定义|`Std_ReturnType tm_set_global_time(tm_synchronized_time_base_type time_base_id, const tm_timestamp_type *timestamp_ptr, const tm_user_data_type *user_data_ptr)`|
|简要描述|设置全局时间 |
|详细说明|允许用户设置全局时间|
|参数[输入]|`tm_synchronized_time_base_type time_base_id` 时间基的唯一标识 |
|参数[输入]|`tm_timestamp_type timestamp_ptr` 指向时间戳结构体的指针 |
|参数[输入]|`tm_user_data_type user_data_ptr` 指向用户数据结构体的指针 |
|同步/异步|同步|
|可重入性|不可重入|

## `tm_update_global_time`

|属性|描述|
|---|---|
|函数定义|`Std_ReturnType tm_update_global_time(tm_synchronized_time_base_type time_base_id, const tm_timestamp_type *timestamp_ptr, const tm_user_data_type *user_data_ptr)`|
|简要描述|更新全局时间 |
|详细说明|允许用户更新全局时间，该时间不会立刻向总线传输|
|参数[输入]|`tm_synchronized_time_base_type time_base_id` 时间基的唯一标识 |
|参数[输入]|`tm_timestamp_type timestamp_ptr` 指向时间戳结构体的指针 |
|参数[输入]|`tm_user_data_type user_data_ptr` 指向用户数据结构体的指针 |
|同步/异步|同步|
|可重入性|不可重入|

## `tm_bus_get_current_time`

|属性|描述|
|---|---|
|函数定义|`Std_ReturnType tm_bus_get_current_time(tm_synchronized_time_base_type time_base_id, tm_timestamp_type *global_time_ptr, tm_virtual_local_time_type *local_time_ptr, tm_user_data_type *user_data_ptr)`|
|简要描述|获取总线当前时间 |
|详细说明|获取给定时间基上的全局时间、虚拟本地时间和用户数据|
|参数[输入]|`tm_synchronized_time_base_type time_base_id` 时间基的唯一标识 |
|参数[输出]|`tm_timestamp_type global_time_ptr` 指向全局时间戳结构体的指针 |
|参数[输出]|`tm_virtual_local_time_type local_time_ptr` 指向虚拟本地时间结构体的指针 |
|参数[输出]|`tm_user_data_type user_data_ptr` 指向用户数据结构体的指针 |
|同步/异步|同步|
|可重入性|不可重入|

## `tm_get_time_base_update_counter`

|属性|描述|
|---|---|
|函数定义|`uint8 tm_get_time_base_update_counter(tm_synchronized_time_base_type time_base_id)`|
|简要描述|获取时间基更新次数 |
|详细说明|返回指定时间基的更新计数器的当前值|
|参数[输入]|`tm_synchronized_time_base_type time_base_id` 时间基的唯一标识 |
|同步/异步|同步|
|可重入性|不可重入|

## `tm_get_time_base_status`

|属性|描述|
|---|---|
|函数定义|`Std_ReturnType tm_get_time_base_status(tm_synchronized_time_base_type time_base_id, tm_time_base_status_type *sync_time_base_status, tm_time_base_status_type *offset_time_base_status)`|
|简要描述|获取时间基状态 |
|详细说明|获取指定时间基的时间和偏移状态信息|
|参数[输入]|`tm_synchronized_time_base_type time_base_id` 时间基的唯一标识 |
|参数[输出]|`tm_time_base_status_type sync_time_base_status` 指向同步时间基状态结构体的指针 |
|参数[输出]|`tm_time_base_status_type offset_time_base_status` 指向偏移时间基状态结构体的指针 |
|同步/异步|同步|
|可重入性|可重入|

## `tm_init_status_check`

|属性|描述|
|---|---|
|函数定义|`tm_initialized_type tm_init_status_check(void)`|
|简要描述|检查user_api初始化状态 |
|详细说明|检查user_api模块是否已成功初始化|
|同步/异步|同步|
|可重入性|不可重入|
