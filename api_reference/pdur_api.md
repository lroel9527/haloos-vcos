# pdur 接口参考文档

> 提示：本API参考文档仅代表功能栈的接口描述和功能说明，帮助开发者快速了解接口作用。应用开发者应通过服务映射调用对应的RTE接口，而非直接调用本文接口

## `pdur_init`

|属性|描述|
|---|---|
|函数定义|`void pdur_init(const pdur_pb_config_type *config_ptr)`|
|简要描述|初始化pdur模块 |
|详细说明|初始化pdur模块 |
|参数[输入]|`config_ptr` pdur配置指针 |
|同步/异步|同步|
|可重入性|不支持重入|

## `pdur_get_configuration_id`

|属性|描述|
|---|---|
|函数定义|`pdur_pb_config_id_type pdur_get_configuration_id(void)`|
|简要描述|pdur获取配置信息 |
|详细说明|pdur获取配置信息 |
|返回值|config_id 配置id|
|同步/异步|同步|
|可重入性|支持重入|

## `pdur_enable_routing`

|属性|描述|
|---|---|
|函数定义|`void pdur_enable_routing(pdur_routing_path_group_id_type id)`|
|简要描述|pdur使能路由 |
|详细说明|pdur使能路由|
|参数[输入]|`id` 路由路径组id |
|同步/异步|同步|
|可重入性|不支持重入|

## `pdur_disable_routing`

|属性|描述|
|---|---|
|函数定义|`void pdur_disable_routing(pdur_routing_path_group_id_type id, boolean initialize)`|
|简要描述|pdur去使能路由 |
|详细说明|pdur去使能路由|
|参数[输入]|`id` 路由路径组id |
|参数[输入]|`initialize` 初始值 |
|同步/异步|同步|
|可重入性|不支持重入|

## `pdur_up_cancel_transmit`

|属性|描述|
|---|---|
|函数定义|`void pdur_up_cancel_transmit(PduIdType pdu_id, uint8 service_id)`|
|简要描述|pdur上层模块取消发送 |
|详细说明|pdur上层模块取消发送|
|参数[输入]|`id` 报文id |
|参数[输入]|`service_id` 服务id |
|同步/异步|同步|
|可重入性|不支持重入|

## `pdur_up_change_parameter`

|属性|描述|
|---|---|
|函数定义|`void pdur_up_change_parameter(PduIdType pdu_id, TPParameterType parameter, uint16 value, uint8 service_id)`|
|简要描述|pdur上层模块改变参数 |
|详细说明|pdur上层模块改变参数|
|参数[输入]|`id` 报文id |
|参数[输入]|`parameter` 要改变的参数 |
|参数[输入]|`value` 要改变的值 |
|参数[输入]|`service_id` 服务id |
|同步/异步|同步|
|可重入性|不支持重入|

## `pdur_up_cancel_receive`

|属性|描述|
|---|---|
|函数定义|`Std_ReturnType pdur_up_cancel_receive(PduIdType pdu_id, uint8 service_id)`|
|简要描述|pdur上层模块取消接收 |
|详细说明|pdur上层模块取消接收|
|参数[输入]|`pdu_id` 报文id |
|参数[输入]|`service_id` 服务id |
|返回值|E_OK pdur上层模块取消接收成功|
|返回值|E_NOT_OK pdur上层模块取消接收失败|
|同步/异步|同步|
|可重入性|不支持重入|

## `pdur_lo_tp_copy_rx_data`

|属性|描述|
|---|---|
|函数定义|`BufReq_ReturnType pdur_lo_tp_copy_rx_data(PduIdType pdu_id, const PduInfoType *info, PduLengthType *buffer_size_ptr, uint8 service_id)`|
|简要描述|pdur下层tp模块拷贝接收数据 |
|详细说明|pdur下层tp模块拷贝接收数据|
|参数[输入]|`pdu_id` 报文id |
|参数[输入]|`info` 信息指针 |
|参数[输入]|`buffer_size_ptr` 缓存大小指针 |
|参数[输入]|`service_id` 服务id |
|返回值|BUFREQ_OK pdur下层tp模块拷贝接收数据成功|
|返回值|BUFREQ_E_NOT_OK pdur下层tp模块拷贝接收数据失败|
|返回值|BUFREQ_E_BUSY pdur下层tp模块拷贝接收数据忙碌|
|返回值|BUFREQ_E_OVFL pdur下层tp模块拷贝接收数据溢出|
|同步/异步|同步|
|可重入性|不支持重入|

## `pdur_lo_tp_rx_indication`

|属性|描述|
|---|---|
|函数定义|`void pdur_lo_tp_rx_indication(PduIdType pdu_id, NotifResultType result, uint8 service_id)`|
|简要描述|pdur下层tp模块接收指示 |
|详细说明|pdur下层tp模块接收指示|
|参数[输入]|`pdu_id` 报文id |
|参数[输入]|`result` 通知结果 |
|参数[输入]|`service_id` 服务id |
|同步/异步|同步|
|可重入性|不支持重入|

## `pdur_lo_tp_start_of_reception`

|属性|描述|
|---|---|
|函数定义|`BufReq_ReturnType pdur_lo_tp_start_of_reception(PduIdType pdu_id, PduLengthType tp_sdu_length, PduLengthType *buffer_size_ptr, uint8 service_id)`|
|简要描述|pdur下层tp模块开始接收 |
|详细说明|pdur下层tp模块开始接收|
|参数[输入]|`pdu_id` 报文id |
|参数[输入]|`tp_sdu_length` tp报文长度 |
|参数[输入]|`buffer_size_ptr` 缓存大小指针 |
|参数[输入]|`service_id` 服务id |
|返回值|BUFREQ_OK pdur下层tp模块拷贝接收数据成功|
|返回值|BUFREQ_E_NOT_OK pdur下层tp模块拷贝接收数据失败|
|返回值|BUFREQ_E_BUSY pdur下层tp模块拷贝接收数据忙碌|
|返回值|BUFREQ_E_OVFL pdur下层tp模块拷贝接收数据溢出|
|同步/异步|同步|
|可重入性|不支持重入|

## `pdur_lo_tp_copy_tx_data`

|属性|描述|
|---|---|
|函数定义|`BufReq_ReturnType pdur_lo_tp_copy_tx_data(PduIdType dest_pdu_id, const PduInfoType *info, RetryInfoType *retry, PduLengthType *available_data_ptr, uint8 service_id)`|
|简要描述|pdur下层tp模块拷贝发送数据 |
|详细说明|pdur下层tp模块拷贝发送数据|
|参数[输入]|`dest_pdu_id` 报文id |
|参数[输入]|`info` 信息指针 |
|参数[输入]|`retry` 重试指针 |
|参数[输入]|`available_data_ptr` 可用数据指针 |
|参数[输入]|`service_id` 服务id |
|返回值|BUFREQ_OK pdur下层tp模块拷贝接收数据成功|
|返回值|BUFREQ_E_NOT_OK pdur下层tp模块拷贝接收数据失败|
|返回值|BUFREQ_E_BUSY pdur下层tp模块拷贝接收数据忙碌|
|返回值|BUFREQ_E_OVFL pdur下层tp模块拷贝接收数据溢出|
|同步/异步|同步|
|可重入性|不支持重入|

## `pdur_tp_tx_confirmation`

|属性|描述|
|---|---|
|函数定义|`void pdur_tp_tx_confirmation(PduIdType dest_pdu_id, NotifResultType result, uint8 service_id)`|
|简要描述|pdur路由tp发送确认接口 |
|详细说明|pdur路由tp发送确认接口|
|参数[输入]|`dest_pdu_id` 报文id |
|参数[输入]|`result` 结果 |
|参数[输入]|`service_id` 服务id |
|同步/异步|同步|
|可重入性|不支持重入|

## `pdur_transmit`

|属性|描述|
|---|---|
|函数定义|`void pdur_transmit(PduIdType pdu_id, const PduInfoType *pdu_info, uint8 service_id)`|
|简要描述|pdur发送接口 |
|详细说明|pdur发送接口|
|参数[输入]|`pdu_id` 报文id |
|参数[输入]|`pdu_info` 报文信息 |
|参数[输入]|`service_id` 服务id |
|返回值|E_OK pdur发送成功|
|返回值|E_NOT_OK pdur发送失败|
|同步/异步|同步|
|可重入性|不支持重入|

## `pdur_rx_indication`

|属性|描述|
|---|---|
|函数定义|`void pdur_rx_indication(PduIdType pdu_id, const PduInfoType *pdu_info, uint8 service_id)`|
|简要描述|pdur接收接口 |
|详细说明|pdur接收接口|
|参数[输入]|`pdu_id` 报文id |
|参数[输入]|`pdu_info` 报文信息 |
|参数[输入]|`service_id` 服务id |
|同步/异步|同步|
|可重入性|不支持重入|

## `pdur_tx_confirmation`

|属性|描述|
|---|---|
|函数定义|`void pdur_tx_confirmation(PduIdType pdu_id, uint8 result, uint8 service_id)`|
|简要描述|pdur发送确认接口 |
|详细说明|pdur发送确认接口|
|参数[输入]|`pdu_id` 报文id |
|参数[输入]|`result` 结果 |
|参数[输入]|`service_id` 服务id |
|同步/异步|同步|
|可重入性|不支持重入|

## `pdur_trigger_transmit`

|属性|描述|
|---|---|
|函数定义|`Std_ReturnType pdur_trigger_transmit(PduIdType pdu_id, PduInfoType *pdu_info, uint8 service_id)`|
|简要描述|pdur触发发送接口 |
|详细说明|pdur触发发送接口|
|参数[输入]|`pdu_id` 报文id |
|参数[输入]|`pdu_info` 结果 |
|参数[输入]|`service_id` 服务id |
|返回值|E_OK 执行成功|
|返回值|E_NOT_OK 执行失败|
|同步/异步|同步|
|可重入性|不支持重入|

## `pdur_internal_main_function`

|属性|描述|
|---|---|
|函数定义|`void pdur_internal_main_function(void)`|
|简要描述|pdur主函数 |
|详细说明|pdur主函数|
|同步/异步|同步|
|可重入性|不支持重入|

## `pdur_internal_interrupt_service_routine`

|属性|描述|
|---|---|
|函数定义|`void pdur_internal_interrupt_service_routine(void)`|
|简要描述|pdur中断处理函数 |
|详细说明|pdur中断处理函数|
|同步/异步|同步|
|可重入性|不支持重入|
