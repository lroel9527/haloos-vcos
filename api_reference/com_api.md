# com 接口参考文档

> 提示：本API参考文档仅代表功能栈的接口描述和功能说明，帮助开发者快速了解接口作用。应用开发者应通过服务映射调用对应的RTE接口，而非
直接调用本文接口

## `com_send_signal`

|属性|描述|
|---|---|
|函数定义|`uint8 com_send_signal(com_signal_id_type signal_id, const void *signal_data_ptr)`|
|简要描述|发送信号 |
|详细说明|发送信号|
|参数[输入]|`signal_id` 信号ID |
|参数[输入]|`signal_data_ptr` 信号数据指针 |
|返回值|E_OK 消息发送成功|
|返回值|COM_SERVICE_NOT_AVAILABLE 消息发送失败, Com 服务不可用|
|返回值|COM_BUSY 消息发送失败, Com 繁忙|
|同步/异步|同步|
|可重入性|FALSE|

## `com_receive_signal`

|属性|描述|
|---|---|
|函数定义|`uint8 com_receive_signal(com_signal_id_type signal_id, void *signal_data_ptr)`|
|简要描述|接收信号 |
|详细说明|接收信号|
|参数[输入]|`signal_id` 信号ID |
|参数[输入]|`signal_data_ptr` 信号数据指针 |
|返回值|E_OK 消息接收成功|
|返回值|COM_SERVICE_NOT_AVAILABLE 消息接收失败, Com 服务不可用|
|返回值|COM_BUSY 消息接收失败, Com 繁忙|
|同步/异步|同步|
|可重入性|FALSE|

## `com_invalidate_signal`

|属性|描述|
|---|---|
|函数定义|`uint8 com_invalidate_signal(com_signal_id_type signal_id)`|
|简要描述|无效信号 |
|详细说明|无效信号|
|参数[输入]|`signal_id` 信号ID |
|返回值|E_OK 消息发送成功|
|返回值|COM_SERVICE_NOT_AVAILABLE 消息发送失败, Com 服务不可用|
|返回值|COM_BUSY 消息发送失败, Com 繁忙|
|同步/异步|同步|
|可重入性|FALSE|

## `com_trigger_transmit`

|属性|描述|
|---|---|
|函数定义|`Std_ReturnType com_trigger_transmit(PduIdType tx_pdu_id, PduInfoType *pdu_info_ptr)`|
|简要描述|触发发送 PDU数据 |
|详细说明|触发发送 PDU数据|
|参数[输入]|`tx_pdu_id` pdu id |
|参数[输入]|`pdu_info_ptr` pdu info指针 |
|返回值|E_OK 触发PDU发送成功|
|返回值|E_NOT_OK 触发PDU发送失败|
|同步/异步|同步|
|可重入性|TRUE|

## `com_trigger_ipdu_send`

|属性|描述|
|---|---|
|函数定义|`uint8 com_trigger_ipdu_send(PduIdType pdu_id, com_self_tx_ipdu_type *self_ipdu, const com_tx_ipdu_type *ipdu)`|
|简要描述|触发PDU发送功能 |
|详细说明|触发PDU发送功能|
|参数[输入]|`pdu_id` pdu id |
|参数[输入]|`self_ipdu` ipdu管理面变量 |
|参数[输入]|`ipdu` ipdu配置变量指针 |
|返回值|E_OK 发送成功|
|返回值|E_NOT_OK 发送失败|
|同步/异步|同步|
|可重入性|TRUE|

## `com_rx_indication`

|属性|描述|
|---|---|
|函数定义|`com_rx_indication(PduIdType rx_pdu_id, const PduInfoType *pdu_info_ptr)`|
|简要描述|com报文接收中断处理函数|
|详细说明|com报文接收中断处理函数|
|参数[输入]|`rx_pdu_id` pdu id |
|参数[输入]|`pdu_info_ptr` pdu info指针 |
|同步/异步|同步|
|可重入性|FALSE|

## `com_tx_confirmation`

|属性|描述|
|---|---|
|函数定义|`com_tx_confirmation(PduIdType tx_pdu_id, Std_ReturnType result)`|
|简要描述|com报文发送确认|
|详细说明|com报文发送确认|
|参数[输入]|`tx_pdu_id` pdu id |
|参数[输入]|`result` 发送确认结果 |
|同步/异步|同步|
|可重入性|FALSE|

## `com_send_signal_group`

|属性|描述|
|---|---|
|函数定义|`uint8 com_send_signal_group(com_signal_group_id_type signal_group_id)`|
|简要描述|发送信号组|
|详细说明|发送信号组|
|参数[输入]|`signal_group_id` 信号组ID |
|返回值|E_OK 消息发送成功|
|返回值|COM_SERVICE_NOT_AVAILABLE 消息发送失败, Com 服务不可用|
|返回值|COM_BUSY 消息发送失败, Com 繁忙|
|同步/异步|同步|
|可重入性|FALSE|

## `com_receive_signal_group`

|属性|描述|
|---|---|
|函数定义|`uint8 com_receive_signal_group(com_signal_group_id_type signal_group_id)`|
|简要描述|接收信号组|
|详细说明|接收信号组|
|参数[输入]|`signal_group_id` 信号组ID |
|返回值|E_OK 消息接收成功|
|返回值|COM_SERVICE_NOT_AVAILABLE 消息接收失败, Com 服务不可用|
|返回值|COM_BUSY 消息接收失败, Com 繁忙|
|同步/异步|同步|
|可重入性|FALSE|

## `com_init`

|属性|描述|
|---|---|
|函数定义|`void com_init(const com_config_type *config)`|
|简要描述|com初始化|
|详细说明|com初始化|
|参数[输入]|`config` com配置指针 |
|同步/异步|同步|
|可重入性|FALSE|

## `com_de_init`

|属性|描述|
|---|---|
|函数定义|`void com_de_init(void)`|
|简要描述|com反初始化|
|详细说明|com反初始化|
|同步/异步|同步|
|可重入性|FALSE|

## `com_ipdu_group_control`

|属性|描述|
|---|---|
|函数定义|`void com_ipdu_group_control(const com_ipg_vec ipg_vec, boolean initialize)`|
|简要描述|ipdu 组控制|
|详细说明|ipdu 组控制|
|参数[输入]|`ipg_vec` ipdu组状态变量 |
|参数[输入]|`initialize` 初始化状态 |
|同步/异步|同步|
|可重入性|TRUE|

## `com_clear_ipdu_group_vector`

|属性|描述|
|---|---|
|函数定义|`void com_clear_ipdu_group_vector(com_ipg_vec ipg_vec)`|
|简要描述|清除ipdu组|
|详细说明|清除ipdu组|
|参数[输入]|`ipg_vec` ipdu组状态变量 |
|同步/异步|同步|
|可重入性|TRUE|

## `com_set_ipdu_group`

|属性|描述|
|---|---|
|函数定义|`void com_set_ipdu_group(com_ipg_vec ipg_vec, com_ipdu_group_id_type ipdu_group_id, boolean bitval)`|
|简要描述|设置ipdu组|
|详细说明|设置ipdu组|
|参数[输入]|`ipg_vec` ipdu组状态变量 |
|参数[输入]|`ipdu_group_id` ipdu组id |
|参数[输入]|`bitval` 控制位 |
|同步/异步|同步|
|可重入性|TRUE|

## `com_reception_dm_control`

|属性|描述|
|---|---|
|函数定义|`void com_reception_dm_control(const com_ipg_vec ipg_vec)`|
|简要描述|接收超时控制|
|详细说明|接收超时控制|
|参数[输入]|`ipg_vec` ipdu组状态变量 |
|同步/异步|同步|
|可重入性|TRUE|
