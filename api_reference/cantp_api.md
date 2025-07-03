# cantp 接口参考文档

> 提示：本API参考文档仅代表功能栈的接口描述和功能说明，帮助开发者快速了解接口作用。应用开发者应通过服务映射调用对应的RTE接口，而非直接调用本文接口

## `cantp_init`

|属性|描述|
|---|---|
|函数定义|`FUNC(void, CANTP_CODE) cantp_init(const cantp_config_type *cfg_ptr)`|
|简要描述|cantp模块初始化|
|详细说明|cantp模块初始化|
|参数[输入]|`cfg_ptr` 配置数据指针|
|同步/异步|同步|
|可重入性|不可重入|

## `cantp_shutdown`

|属性|描述|
|---|---|
|函数定义|`FUNC(void, CANTP_CODE) cantp_shutdown(void)`|
|简要描述|cantp模块关闭|
|详细说明|cantp模块关闭|
|参数[输入]|void|
|同步/异步|同步|
|可重入性|不可重入|

## `cantp_transmit`

|属性|描述|
|---|---|
|函数定义|`FUNC(Std_ReturnType, CANTP_CODE) cantp_transmit(PduIdType cantp_tx_pdu_id, const PduInfoType *cantp_tx_info_ptr)`|
|简要描述|请求传输 PDU|
|详细说明|请求传输 PDU|
|参数[输入]|`cantp_tx_pdu_id` 要传输的pdu的标识符|
|参数[输入]|`cantp_tx_info_ptr` pdu数据的长度和指针|
|同步/异步|同步|
|可重入性|相同pdu_id不可重入，不同pdu_id可重入|

## `cantp_cancel_transmit`

|属性|描述|
|---|---|
|函数定义|`FUNC(Std_ReturnType, CANTP_CODE) cantp_cancel_transmit(PduIdType tx_pdu_id)`|
|简要描述|取消发送请求|
|详细说明|取消发送请求|
|参数[输入]|`tx_pdu_id` 取消传输的pdu的标识符|
|同步/异步|同步|
|可重入性|相同pdu_id不可重入，不同pdu_id可重入|

## `cantp_cancel_receive`

|属性|描述|
|---|---|
|函数定义|`FUNC(Std_ReturnType, CANTP_CODE) cantp_cancel_receive(PduIdType rx_pdu_id)`|
|简要描述|取消接收请求|
|详细说明|取消接收请求|
|参数[输入]|`rx_pdu_id` 取消接收的pdu的标识符|
|同步/异步|同步|
|可重入性|不可重入|

## `cantp_change_parameter`

|属性|描述|
|---|---|
|函数定义|`FUNC(Std_ReturnType, CANTP_CODE) cantp_change_parameter(PduIdType id, tp_parameter_type parameter, uint16 value)`|
|简要描述|修改传输层参数|
|详细说明|修改传输层参数|
|参数[输入]|`id` pdu的标识符|
|参数[输入]|`parameter` 要修改的参数|
|参数[输入]|`value` 要修改的值|
|同步/异步|同步|
|可重入性|不可重入|

## `cantp_read_parameter`

|属性|描述|
|---|---|
|函数定义|`FUNC(Std_ReturnType, CANTP_CODE) cantp_read_parameter(PduIdType id, tp_parameter_type parameter, uint16 *value)`|
|简要描述|读取传输层参数|
|详细说明|读取传输层参数|
|参数[输入]|`id` pdu的标识符|
|参数[输入]|`parameter` 要读取的参数|
|参数[输入]|`value` 读取的值|
|同步/异步|同步|
|可重入性|不可重入|

## `cantp_rx_indication`

|属性|描述|
|---|---|
|函数定义|`FUNC(void, CANTP_CODE) cantp_rx_indication(PduIdType cantp_rx_pdu_id, const PduInfoType *cantp_rx_pdu_ptr)`|
|简要描述|cantp接收回调函数|
|详细说明|cantp接收回调函数|
|参数[输入]|`cantp_rx_pdu_id` 接收pdu id|
|参数[输入]|`cantp_rx_pdu_ptr` 接收pdu头指针|
|同步/异步|同步|
|可重入性|相同pdu id不可重入，不同pdu id可重入|

## `cantp_tx_confirmation`

|属性|描述|
|---|---|
|函数定义|`FUNC(void, CANTP_CODE) cantp_tx_confirmation(PduIdType cantp_tx_pdu_id, Std_ReturnType result)`|
|简要描述|cantp发送确认接口|
|详细说明|cantp发送确认接口|
|参数[输入]|`cantp_tx_pdu_id` 发送pdu id|
|参数[输入]|`result` 发送确认结果|
|同步/异步|同步|
|可重入性|相同pdu id不可重入，不同pdu id可重入|
