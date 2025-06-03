# cansm 接口参考文档

> 提示：本API参考文档仅代表功能栈的接口描述和功能说明，帮助开发者快速了解接口作用。应用开发者应通过服务映射调用对应的RTE接口，而非直接调用本文接口

## `cansm_init`

|属性|描述|
|---|---|
|函数定义|`cansm_init(const cansm_config_type *config_ptr)`|
|简要描述|CanSM module initialization |
|详细说明|Notify the CanSM module that the transceiver is operating in PN communication |
|参数[输入]|`未知类型 config_ptr` Pointer to the initialization structure of CanSM built parameters |
|同步/异步|Synchronous|
|可重入性|Reentrant|

## `cansm_request_com_mode`

|属性|描述|
|---|---|
|函数定义|`cansm_request_com_mode(network_handle_type network_handle`|
|简要描述|Request CanSM module to switch communication mode |
|详细说明|CanNm has detected a tx timeout exception in some affected CAN networks |
|参数[输入]|`未知类型 network_handle` network handle |
|参数[输入]|`未知类型 comm_mode` Request to switch network mode Request acceptance @ret_val E_NOT_OK Request Rejection |
|同步/异步|Synchronous|
|可重入性|Reentrant|

## `cansm_get_bus_off_status`

|属性|描述|
|---|---|
|函数定义|`cansm_get_bus_off_status(network_handle_type network_handle)`|
|简要描述|CanSM obtains the bus_off_status of the network corresponding to this core based on the NetworkId |
|详细说明|When NetworkId is valid, return the bus_off_status of the corresponding network; otherwise, return False |
|参数[输入]|`未知类型 network_handle` network handle @ret_val bus_off_status |
|同步/异步|Synchronous|
|可重入性|Reentrant|

## `cansm_get_bus_off_counter`

|属性|描述|
|---|---|
|函数定义|`cansm_get_bus_off_counter(network_handle_type network_handle)`|
|简要描述|CanSM obtains the bus_off_counter corresponding to the network of this core based on the NetworkId |
|详细说明|When NetworkId is valid, return bus_off_status of corresponding network; otherwise, return 0xFFFF|
|参数[输入]|`未知类型 network_handle` network handle @ret_val bus_off_counter |
|同步/异步|Synchronous|
|可重入性|Reentrant|

## `cansm_controller_bus_off`

|属性|描述|
|---|---|
|函数定义|`cansm_controller_bus_off(uint8 controller_id)`|
|简要描述|Notify the CanSM module that a CAN controller has a BusOff |
|详细说明|Notify the CanSM module that the transceiver is operating in PN communication |
|参数[输入]|`未知类型 controller_id` CAN Controller Id |
|同步/异步|Synchronous|
|可重入性|Reentrant|
