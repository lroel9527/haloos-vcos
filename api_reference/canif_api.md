# canif 接口参考文档

> 提示：本API参考文档仅代表功能栈的接口描述和功能说明，帮助开发者快速了解接口作用。应用开发者应通过服务映射调用对应的RTE接口，而非
直接调用本文接口

## `canif_init`

|属性|描述|
|---|---|
|函数定义|`FUNC(void, CANIF_CODE) canif_init(const canif_config_type *config_ptr)`|
|简要描述|初始化canif模块 |
|详细说明|该服务初始化can接口的内部和外部接口以供进一步处理 |
|参数[输入]|`config_ptr` 指向配置参数集的指针，例如使用为了后期构建参数 |
|同步/异步|同步|
|可重入性|相同控制器不可重入，不同控制器可重入|

## `canif_set_controller_mode`

|属性|描述|
|---|---|
|函数定义|`canif_set_controller_mode(uint8 controller_id, Can_ControllerStateType controller_mode)`|
|简要描述|更改控制器模式 |
|详细说明|该服务调用相应的can driver服务来更改can控制器模式 |
|参数[输入]|`controller_id` 分配给can控制器的抽象canif controller_id,请求用于模式转换。 |
|参数[输入]|`controller_mode` 请求的模式转换 |
|返回值|E_OK 控制器模式请求已被接受|
|返回值|E_NOT_OK 控制器模式请求未被接受|
|同步/异步|同步|
|可重入性|不支持重入|

## `canif_get_controller_mode`

|属性|描述|
|---|---|
|函数定义|`canif_get_controller_mode(uint8 controller_id, canif_controller_mode_type *controller_mode_ptr)`|
|简要描述|获取控制器模式 |
|详细说明|该服务调用对应的can driver服务来获取can控制器的当前状态|
|参数[输入]|`controller_id` 抽象的canif controller_id，分配给can控制器，当前操作模式需要此控制器。 |
|参数[输出]|`controller_mode_ptr` 指向存储位置的指针，CAN 控制器的当前模式将存储在该位置。 |
|返回值|E_OK 控制器模式请求已被接受|
|返回值|E_NOT_OK 控制器模式请求未被接受|
|同步/异步|同步|
|可重入性|相同控制器不可重入，不同控制器可重入|

## `canif_transmit`

|属性|描述|
|---|---|
|函数定义|`canif_transmit(PduIdType can_tx_pdu_id, const PduInfoType *pdu_info_ptr)`|
|简要描述|发送pdu |
|详细说明|请求pdu发送|
|参数[输入]|`can_tx_pdu_id` 要传输的pdu的id |
|参数[输入]|`pdu_info_ptr` PDU 数据的长度和指针以及指向元数据的指针。 |
|返回值|CANIF_TRANSMIT_OK 发送请求已被can驱动接受 or 发送请求未被can驱动接受，但成功入队canif tx_buffer，报文未丢弃|
|返回值|CANIF_TRANSMIT_NOT_OK 发送请求未被can驱动接受，报文丢弃|
|返回值|CANIF_TRANSMIT_BUSY_TXBUFFER_NOT_INSERTED 发送请求未被can驱动接受，并且canif tx_buffer入队没成功，报文丢弃|
|返回值|CANIF_TRANSMIT_BUSY_NO_TXBUFFER_CONFIG 发送请求未被can驱动接受，并且没有配置canif tx_buffer，报文丢弃|
|同步/异步|同步|
|可重入性|支持重入不同的pdu_ids。不支持相同的pdu_id重入。|

## `canif_set_pdu_mode`

|属性|描述|
|---|---|
|函数定义|`canif_set_pdu_mode(uint8 channel_id, canif_pdu_mode_type pdu_mode_request)`|
|简要描述|设置pdu模式 |
|详细说明|该服务在预定义的逻辑pdu通道的l-pdu处设置请求的模式。|
|参数[输入]|`channel_id` 连接到对应的canif controller_id的自己的ecu的所有pdu被分配给物理can控制器。 |
|参数[输入]|`pdu_mode_request` 请求pdu模式转换 |
|返回值|E_OK 模式转换请求已被接受|
|返回值|E_NOT_OK 模式转换请求未被接受|
|同步/异步|同步|
|可重入性|相同控制器不可重入，不同控制器可重入|

## `canif_get_pdu_mode`

|属性|描述|
|---|---|
|函数定义|`canif_get_pdu_mode(uint8 channel_id, canif_pdu_mode_type *pdu_mode_ptr)`|
|简要描述|获取pdu模式 |
|详细说明|该服务在预定义的逻辑pdu通道的l-pdu处获取当前模式。|
|参数[输入]|`channel_id` 连接到对应的canif controller_id的自己的ecu的所有pdu被分配给物理can控制器。 |
|参数[输出]|`pdu_mode_ptr` 指向内存位置的指针，将存储逻辑 PDU 通道的当前模式。 |
|返回值|E_OK pdu模式转换请求已被接受|
|返回值|E_NOT_OK pdu模式转换请求未被接受|
|同步/异步|同步|
|可重入性|相同控制器不可重入，不同控制器可重入|

## `canif_set_trcv_mode`

|属性|描述|
|---|---|
|函数定义|`canif_set_trcv_mode(uint8 transceiver_id, CanTrcv_TrcvModeType transceiver_mode)`|
|简要描述|设置收发器模式 |
|详细说明|该服务通过调用相应的can 收发器驱动服务来改变tansceiver transceiver_id的操作模式。|
|参数[输入]|`transceiver_id` 抽象的 canif transceiver_id，分配给一个 can收发器，请求用于模式转换 |
|参数[输入]|`transceiver_mode` 请求模式转换 |
|返回值|E_OK 收发器模式请求已被接受|
|返回值|E_NOT_OK 收发器模式请求未被接受|
|同步/异步|异步|
|可重入性|不可重入|

## `canif_get_trcv_mode`

|属性|描述|
|---|---|
|函数定义|`canif_get_trcv_mode(CanTrcv_TrcvModeType *transceiver_mode_ptr, uint8 transceiver_id)`|
|简要描述|获取收发器模式 |
|详细说明|此函数调用cantrcv_get_op_mode并使用cantrcv提供的值op_mode更新参数transceiver_mode_ptr。|
|参数[输入]|`transceiver_id` 抽象的 canif transceiver_id，分配给 CAN 收发器，为当前操作模式请求。。 |
|参数[输出]|`transceiver_mode_ptr` 收发器连接到的请求网络的请求模式。 |
|返回值|E_OK 收发器模式请求已被接受|
|返回值|E_NOT_OK 收发器模式请求未被接受|
|同步/异步|同步|
|可重入性|不可重入|

## `canif_get_trcv_wakeup_reason`

|属性|描述|
|---|---|
|函数定义|`canif_get_trcv_wakeup_reason(uint8 transceiver_id, CanTrcv_TrcvWakeupReasonType *trcv_wu_reason_ptr)`|
|简要描述|获取收发器唤醒原因 |
|详细说明|该服务通过调用相应的can收发器驱动服务返回唤醒收发器transceiver_id的原因。|
|参数[输入]|`transceiver_id` 抽象的 canif transceiver_id，分配给 CAN 收发器，出于唤醒原因请求。 |
|参数[输出]|`trcv_wu_reason_ptr` 提供指向所请求的收发器唤醒原因应返回的位置的指针 |
|返回值|E_OK 收发器唤醒原因请求已被接受。|
|返回值|E_NOT_OK 收发器唤醒原因请求未被接受。|
|同步/异步|同步|
|可重入性|不支持重入|

## `canif_set_trcv_wakeup_mode`

|属性|描述|
|---|---|
|函数定义|`canif_set_trcv_wakeup_mode(uint8 transceiver_id, CanTrcv_TrcvWakeupModeType trcv_wakeup_mode)`|
|简要描述|设置收发唤醒模式 |
|详细说明|该函数应调用cantrcv_set_trcv_wakeup_mode。|
|参数[输入]|`transceiver_id` 抽象的 canif transceiver_id，分配给一个 CAN 收发器，请求用于模式转换 |
|参数[输入]|`trcv_wakeup_mode` 请求模式转换 |
|返回值|E_OK 如果唤醒通知状态已更改为请求模式，将返回e_ok。|
|返回值|E_NOT_OK 如果唤醒通知状态更改失败或参数超出允许范围，将返回e_not_ok。|
|同步/异步|同步|
|可重入性|不支持重入|

## `canif_check_wakeup`

|属性|描述|
|---|---|
|函数定义|`canif_check_wakeup(ecum_wakeup_source_t wakeup_source)`|
|简要描述|检测唤醒源 |
|详细说明|此服务检查底层can驱动程序或can收发器驱动程序是否已发出唤醒事件信号。|
|参数[输入]|`wakeup_source` 发起唤醒事件的源设备：CAN 控制器或 can收发器 |
|返回值|E_OK 如果检测唤醒请求已被接收，将返回e_ok|
|返回值|E_NOT_OK 如果检测唤醒请求未被接收，将返回e_not_ok|
|同步/异步|异步|
|可重入性|不支持重入|

## `canif_check_validation`

|属性|描述|
|---|---|
|函数定义|`canif_check_validation(ecum_wakeup_source_t wakeup_source)`|
|简要描述|验证被动唤醒 |
|详细说明|执行此服务以验证先前的唤醒事件。|
|参数[输入]|`wakeup_source` 启动唤醒事件且必须验证的源设备：can控制器或can收发器 |
|返回值|E_OK 如果检测验证请求已被接收，将返回e_ok|
|返回值|E_NOT_OK 如果检测验证请求未被接收，将返回e_not_ok|
|同步/异步|同步|
|可重入性|不支持重入|

## `canif_get_tx_confirmation_state`

|属性|描述|
|---|---|
|函数定义|`canif_get_tx_confirmation_state(uint8 controller_id)`|
|简要描述|获取发送状态 |
|详细说明|此服务报告自上次can控制器启动以来是否已为整个can控制器完成任何tx确认。|
|参数[输入]|`controller_id` 分配给can控制器的抽象canif controller_id |
|返回值|canif_notif_status_type can控制器的所有tx pdu的组合tx确认状态|
|同步/异步|同步|
|可重入性|相同控制器不可重入，不同控制器可重入|

## `canif_clear_trcv_wuf_flag`

|属性|描述|
|---|---|
|函数定义|`canif_clear_trcv_wuf_flag(uint8 transceiver_id)`|
|简要描述|清除收发唤醒标志 |
|详细说明|请求canif模块清除指定can收发器的wuf标志。|
|参数[输入]|`transceiver_id` 抽象canif transceiver_id，分配给指定的can收发器。 |
|返回值|E_OK 请求已被接受|
|返回值|E_NOT_OK 请求未被接受|
|同步/异步|异步|
|可重入性|不可重入|

## `canif_check_trcv_wake_flag`

|属性|描述|
|---|---|
|函数定义|`canif_check_trcv_wake_flag(uint8 transceiver_id)`|
|简要描述|清除校验唤醒源 |
|详细说明|请求canif模块检查指定can收发器的唤醒标志。|
|参数[输入]|`transceiver_id` 抽象canif transceiver_id，分配给指定的can收发器。 |
|返回值|E_OK 请求已被接受|
|返回值|E_NOT_OK 请求未被接受|
|同步/异步|异步|
|可重入性|不可重入|

## `canif_rx_indication`

|属性|描述|
|---|---|
|函数定义|`canif_rx_indication(Can_HwHandleType hrh, Can_IdType can_id, uint8 can_dlc, const uint8 *can_sdu_ptr)`|
|简要描述|接收回调函数 |
|详细说明|canif接收回调函数|
|参数[输入]|`Can_HwHandleType hrh` 接收表 |
|参数[输入]|`Can_IdType can_id` 标识 |
|参数[输入]|`uint8 can_dlc` 长度 |
|参数[输入]|`const uint8 * can_sdu_ptr` sdu指针 |
|同步/异步|同步|
|可重入性|相同pdu_id不可重入，不同pdu_id可重入|

## `canif_clear_trcv_wuf_flag_indication`

|属性|描述|
|---|---|
|函数定义|`canif_clear_trcv_wuf_flag_indication(uint8 transceiver_id)`|
|简要描述|清除收发唤醒标志位 |
|详细说明|该服务表明收发器已经清除了引用相应can收发器的wuf_flag，该can收发器具有抽象的canif transceiver_id。|
|参数[输入]|`transceiver_id` 收发器ID |
|同步/异步|同步|
|可重入性|对于不同的收发器可重入，相同收发器不可重入|

## `canif_check_trcv_wake_flag_indication`

|属性|描述|
|---|---|
|函数定义|`canif_check_trcv_wake_flag_indication(uint8 transceiver_id)`|
|简要描述|清除收发唤醒标志位 |
|详细说明|该服务表明收发器唤醒标志的检查已由相应的can收发器完成，带有抽象的id。 该指示用于处理异步收发器通信。|
|参数[输入]|`transceiver_id` 抽象canif transceiver_id，分配给指定的can收发器，检查pn可用性。 |
|同步/异步|同步|
|可重入性|对于不同的收发器可重入，相同收发器不可重入|

## `canif_trcv_mode_indication`

|属性|描述|
|---|---|
|函数定义|`canif_trcv_mode_indication(uint8 transceiver_id, CanTrcv_TrcvModeType transceiver_mode)`|
|简要描述|收发器模式指示 |
|详细说明|该服务指示一个收发器状态转换，它引用具有抽象canif transceiver_id的相应can收发器。|
|参数[输入]|`transceiver_id` 抽象canif transceiver_id，分配给指定的can收发器，检查pn可用性。 |
|参数[输入]|`transceiver_mode` 收发器模式 |
|同步/异步|同步|
|可重入性|对于不同的收发器可重入，相同收发器不可重入|

## `canif_controller_mode_indication`

|属性|描述|
|---|---|
|函数定义|`canif_controller_mode_indication(uint8 controller_id, canif_controller_mode_type controller_mode)`|
|简要描述|控制器模式指示 |
|详细说明|该服务指示一个控制器状态转换，它引用具有抽象canif controller_id的相应can控制器。|
|参数[输入]|`controller_id` 抽象 canif controller_id，分配给一个can控制器，其状态已转换。 |
|参数[输入]|`controller_mode` can控制器转换到的模式 |
|同步/异步|同步|
|可重入性|对于不同的控制器可重入，相同控制器不可重入|
