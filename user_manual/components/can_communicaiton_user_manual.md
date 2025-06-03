# CAN通信开发者手册

## 1. 简介

CAN总线具备实时性、高可靠性的特性，成为了现代车载网络架构的关键组成之一。CAN通信栈支持业务报文收发、报文路由、报文和信号管理等功能；支持CAN多核部署，用户可按照实际需求，将CAN通道部署在不同的核上。

## 2. 代码目录

```plaintext
communication
├── CMakeLists.txt          # communication仓库的编译脚本，用于控制编译相关资源
├── DISCLAIMER.md           # 免责声明文档
├── Kconfig                 # communication模块的Kconfig文件
├── LICENSE                 # 项目许可证文件
├── README.md               # communication仓库的readme，用于介绍该代码仓库(即本文)
├── net_manager             # 网络总线管理面相关实现
│   └── comm                # 通信管理
├── net_dev                 # 驱动抽象层，对驱动资源及功能进行抽象封装，供上层模块使用
│   ├── CMakeLists.txt      # 驱动抽象层的编译脚本，用于控制编译相关资源
│   └── canif               # CAN驱动抽象层
├── pdu_router              # pdu路由层
└── rt_com                  # 实时通信层
```

## 3. 主要功能描述

### 3.1. 功能讲解

![Can Communication Architecture Diagram](../../_static/image/can/arch.png)

* 设备抽象层封装硬件驱动细节，为协议层提供硬件操作接口
* 路由层提供报文路由功能
* com通信模块提供报文和信号转换的功能

## 4. 功能配置方法

Com是Can通信栈的关键组件，为应用层与底层之间的通信提供服务。它负责数据的“翻译”与传输，实现了对底层通信的抽象，使上层应用可以进行信号级的通信。

### 4.1. Com配置项介绍

#### 4.1.1. ComIPdu

![ComIPdu Diagram](../../_static/image/can/com/comipdu.png)

* 描述IPdu相关配置信息

#### 4.1.2. ComIPduGroup

![ComIPduGroup Diagram](../../_static/image/can/com/comipdugroup.png)

* 一路CAN会默认生成TX RX两个Group

#### 4.1.3. ComMainFunctionGw

![MainFunction Gw Configurations](../../_static/image/can/com/commainfunction.png)

* 信号路由处理主函数

#### 4.1.4. ComMainFunctionRx

![MainFunction Rx Configurations](../../_static/image/can/com/commainfunction.png)

* 接收报文处理主函数，支持多实例

#### 4.1.5. ComMainFunctionTx

![MainFunction Tx Configurations](../../_static/image/can/com/commainfunction.png)

* 发送报文处理主函数，支持多实例

#### 4.1.6. ComSignal

![Com Signal Configurations Diagram](../../_static/image/can/com/comsignal.png)

* 描述Signal相关配置信息

### 4.2. PduR模块配置项介绍

#### 4.2.1. PduRBswModules

![PduRBswModules Diagram](../../_static/image/can/pdur/pdurbswmodules.png)

* PduR上下层模块描述

#### 4.2.2. PduRInterruptServiceRoutine

![PduRInterruptServiceRoutine Configuration](../../_static/image/can/pdur/pdurinterruptserviceroutine.png)

* 用于实现PduR跨核路由的软中断配置

#### 4.2.3. PduRRoutingPaths

![PduRRoutingPaths Configuration](../../_static/image/can/pdur/pdurroutingpaths.png)

* PduR路由路径配置

### 4.3. CanIf模块配置项介绍

#### 4.3.1. CanIfCtrlDrvCfg

![CanIfCtrlDrvCfg Diagram](../../_static/image/can/canif/canifctrldrvcfg.png)

* CanIf层CAN控制器配置
* 该配置会和CAN驱动的控制器进行映射

#### 4.3.2. CanIfTrcvDrvCfg

![CanIfTrcvDrvCfg Configuration](../../_static/image/can/canif/caniftrcvdrvcfg.png)

* CanIf层CAN收发器配置
* 该配置会和CAN驱动的收发器进行映射

#### 4.3.3. CanIfBufferCfg

![CanIfBufferCfg Configuration](../../_static/image/can/canif/canifbuffercfg.png)

* CanIf层缓存配置
* 可以缓存Tx报文，防止丢包

#### 4.3.4. CanIfInitHohCfg

![CanIfInitHohCfg Configuration](../../_static/image/can/canif/canifinithohcfg.png)

* CanIf Hoh配置
* 会和驱动HardwareObject进行映射

#### 4.3.5. CanIfRxPduCfg

![CanIfRxPduCfg Configuration](../../_static/image/can/canif/canifrxpducfg.png)

* CanIf Rx Pdu配置

#### 4.3.6. CanIfTxPduCfg

![CanIfTxPduCfg Configuration](../../_static/image/can/canif/caniftxpducfg.png)

* CanIf Tx Pdu配置

### 4.4. ComM模块配置项介绍

#### 4.4.1. ComMChannel

![ComMChannel Diagram](../../_static/image/can/comm/commchannel.png)

* 通信通道配置

#### 4.4.2. ComMUser

![4.4.2 ComMUser Configuration](../../_static/image/can/comm/commuser.png)

* 通信管理User配置

## 5. 使用示例

### 5.1. 使用EB配置CAN驱动MCAL

* CAN驱动通过EB软件配置好驱动
* 将EB配置好的驱动导出arxml

### 5.2. 使用VCOS配置CAN协议栈

#### 5.2.1. 准备一个做好基础配置的工程，配置了OS、EcuC模块

![Base Project Diagram](../../_static/image/can/import/baseproject.png)

#### 5.2.2. 点击Import ARXML导入MCAL arxml文件

![Base Project Diagram](../../_static/image/can/import/importmcal.png)

#### 5.2.3. 选择CAN模块（即CAN驱动模块）

![Base Project Diagram](../../_static/image/can/import/can.png)

#### 5.2.4. 选择ResourceManager模块（定义了CAN部署的Core信息）

![Base Project Diagram](../../_static/image/can/import/resourcem.png)

#### 5.2.5. VCOS工具会自动生成CAN、CanIf、ResourceManager模块

![Base Project Diagram](../../_static/image/can/import/module.png)

#### 5.2.6. 点击Input files

![Base Project Diagram](../../_static/image/can/import/inputfile.png)

#### 5.2.7. 选择DBC（CAN矩阵文件）PduRCfg.xlsx（描述报文路由信息）

![Base Project Diagram](../../_static/image/can/import/dbc.png)

#### 5.2.8. 点击OK  自动生成CAN协议栈模块

![Base Project Diagram](../../_static/image/can/import/canstack.png)

#### 5.2.9. 通过导入DBC和MCAL，自动生成CAN多核部署配置

#### 5.2.10. Com会自动按照多核部署来生成每个Core的MainFunction

![Com Main Diagram](../../_static/image/can/import/commainfunciton.png)

#### 5.2.11. CanNm会自动按照多核部署来生成每个Core的MainFunction

![CanNm Main Diagram](../../_static/image/can/import/cannmmainfunction.png)

#### 5.2.12. CanSM会自动按照多核部署来生成每个Core的MainFunction

![CanSM Main Diagram](../../_static/image/can/import/cansmmainfunction.png)

#### 5.2.13. CanIf模块会自动和Can驱动自动mapping，并自动填充Can通道和Core的映射关系

![CanIf Core Diagram](../../_static/image/can/import/canif_core.png)

![CanIf Ref Diagram](../../_static/image/can/import/canif_ref.png)

#### 5.2.14. EcuC自动填充IPDU和Core的ref信息

![EcuC Main Diagram](../../_static/image/can/import/ecucref.png)

#### 5.2.15. 手动task mapping

![Task Mapping Diagram](../../_static/image/can/import/taskmapping.png)

### 5.3. 测试CAN通信收发验证

#### 5.3.1. 接线图

![Board Link](../../_static/image/can/import/boardlink.png)

![Host](../../_static/image/can/import/host.png)

#### 5.3.2. 报文基础通信

![Test CAN TRX](../../_static/image/can/import/testcom.png)

#### 5.3.3. 报文跨核路由

![Test Pdu Rout](../../_static/image/can/import/pducorerout.png)

#### 5.3.4. CAN2转CAN1

![Test CAN2 CAN1](../../_static/image/can/import/can2tocan1.png)

#### 5.3.5. CAN1转CAN2

![Test CAN1 CAN2](../../_static/image/can/import/can1tocan2.png)

### 5.4. 关键代码

* 打开通信，在启动流程中，上层请求CAN1、CAN2通道为FULL通信：

```C
comm_request_com_mode(ComMConf_ComMUser_ComMUser_EcuDemo_CAN1_Ctrl, COMM_FULL_COMMUNICATION);
comm_communication_allowed((NetworkHandleType)ComMConf_ComMUser_ComMUser_EcuDemo_CAN1_Ctrl, (boolean)TRUE);
comm_request_com_mode(ComMConf_ComMUser_ComMUser_EcuDemo_CAN2_Ctrl, COMM_FULL_COMMUNICATION);
comm_communication_allowed((NetworkHandleType)ComMConf_ComMUser_ComMUser_EcuDemo_CAN2_Ctrl, (boolean)TRUE);
```

* Com发送主函数

```C

FUNC(void, COM_CODE) com_main_function_tx_run(uint8 main_function_id)
{
#if (COM_SUPPORT_MUTICORE == STD_ON)
    com_core_id_type core_id = (com_core_id_type)GetCoreID();
    uint8 com_init_status_temp = com_init_status[core_id];
#else
    uint8 com_init_status_temp = com_init_status;
#endif
    if (COM_INIT != com_init_status_temp) {
        COM_DET_REPORT(COM_COM_MAINFUNCTIONTX_ID_COM_E_UNINIT);
        return;
    }
    if (main_function_id >= COM_MAINFUNCTION_TX_NUM) {
        COM_DET_REPORT(COM_COM_MAINFUNCTIONTX_ID_COM_E_PARAM);
        return;
    }
    ...............
 }
```

* Com接收主函数

```C
FUNC(void, COM_CODE) com_main_function_rx_run(uint8 main_function_id)
{
#if (COM_SUPPORT_MUTICORE == STD_ON)
    com_core_id_type core_id = (com_core_id_type)GetCoreID();
    uint8 com_init_status_temp = com_init_status[core_id];
#else
    uint8 com_init_status_temp = com_init_status;
#endif
    if (COM_INIT != com_init_status_temp) {
        COM_DET_REPORT(COM_COM_MAINFUNCTIONRX_ID_COM_E_UNINIT);
        return;
    }
    if (main_function_id >= COM_MAINFUNCTION_RX_NUM) {
        COM_DET_REPORT(COM_COM_MAINFUNCTIONRX_ID_COM_E_PARAM);
        return;
    }
#if ((COM_RXTOU_ENABLE == STD_ON) && (COM_RXIPDU_SAME_TIMEOUT_ENABLE == STD_OFF))
    if (com_main_function_rx_struct[main_function_id].rx_timeout_info == TRUE) {
        com_tout_mon_rx(main_function_id);
    }
#endif

#if ((COM_RXTOU_ENABLE == STD_ON) && (COM_RXIPDU_SAME_TIMEOUT_ENABLE == STD_ON))
    if (com_main_function_rx_struct[main_function_id].rx_timeout_info == TRUE) {
        com_tout_mon_rx_signal(main_function_id);
    }
#endif

    com_process_deffered_rxpdu(main_function_id);
    return;
}
```

* 路由实现

```C
for (uint8 dest_pdu_idx = 0u; dest_pdu_idx < routing_path_ptr->pdur_destinatn_num; dest_pdu_idx++) {
    const pdur_dest_pdu_type *destination = routing_path_ptr->pdur_dest_pdus[dest_pdu_idx];

    if (pdur_check_routing_path_enabled(destination) == (boolean)FALSE) {
        continue;
    }
    if (pdur_is_up_module(destination->dest_module)) {
        pdur_route_rx_indication(destination, pdu_info);
    } else if (pdur_is_lo_module(destination->dest_module)) {
#if (PDUR_MULTICORE_SUPPORT == STD_ON)
        if (destination->pdur_dest_pdu_core != (pdur_core_id_type)GetCoreID()) {
            if (pdur_buffer_manager_ptr == NULL) {
                PDUR_DET_REPORT(PDUR_PDUR_SERVICEID_RXINDICATION_IF_ROUTING_NO_BUFFER);
                continue;
            }
            Std_ReturnType trigger_ret_val = pdur_trigger_soft_interrupt(pdu_id, dest_pdu_idx);

            if (trigger_ret_val != E_OK) {
                PDUR_DET_REPORT(PDUR_PDUR_SERVICEID_RXINDICATION_RX_INTERRUPT_FAILED);
                continue;
            }
            if (destination->data_provision == PDUR_TRIGGERTRANSMIT) {
                pdur_buffer_manager_ptr->routing_state[dest_pdu_idx] =
                    PDUR_GATEWAY_IF_TT_TX_FIFO_APPEND;
            } else {
                pdur_buffer_manager_ptr->routing_state[dest_pdu_idx] =
                    PDUR_GATEWAY_IF_DIRECT_TX_FIFO_APPEND;
            }
        } else
#endif
        {
            pdur_dest_pdu_len_strategy_type handle_strategy =
                pdur_check_and_handle_dest_pdu_len_strategy(destination, pdu_info);
            Std_ReturnType ret_val = E_OK;

            if (handle_strategy == PDUR_STRATEGY_DISCARD) {
                PDUR_DET_REPORT(PDUR_PDUR_SERVICEID_RXINDICATION_STRATEGY_DISCARD);
                ret_val = E_NOT_OK;
            } else if (handle_strategy == PDUR_STRATEGY_SHORTEN) {
                PduInfoType pdu_info_temp;
                (void)memcpy(&pdu_info_temp, pdu_info, sizeof(PduInfoType));
                pdu_info_temp.SduLength = destination->pdu_len_in_ecuc;
                ret_val = pdur_route_transmit(destination, &pdu_info_temp);
            } else {
                ret_val = pdur_route_transmit(destination, pdu_info);
            }
            if (destination->data_provision == PDUR_TRIGGERTRANSMIT) {
                if (ret_val == E_OK) {
                    pdur_buffer_manager_ptr->routing_state[dest_pdu_idx] =
                        PDUR_GATEWAY_IF_TT_TX_FIFO_APPEND;
                }
            }
        }
    } else {
        /* do nothing */
    }
}
```

* 和驱动接口交互

```C
ret = canif_channel_mode_check_on_transmit(channel);
if (E_OK == ret) {
    ret = canif_pn_fliter_process(tx_pdu_ptr, channel);
    if (E_OK == ret) {
        if (CANIF_TX_OFFLINE_ACTIVE == canif_runtime_state.ctrl_runtime_state[channel].pdu_mode) {
            canif_usr_tx_confirmation_ptr =
                canif_user_tx_confirmations[tx_pdu_ptr->tx_pdu_ul_tx_confirmation];
            if ((CANIF_NO_FUNCTION_CALLOUT != tx_pdu_ptr->tx_pdu_ul_tx_confirmation) &&
                (canif_usr_tx_confirmation_ptr != NULL)) {
                canif_usr_tx_confirmation_ptr(tx_pdu_ptr->tx_pdu_id, E_OK);
            }
            transmit_status = E_OK;
        }
        if (transmit_status == E_NOT_OK)
            ret = canif_transmit_to_can_driver(channel, can_tx_pdu_id, tx_pdu_ptr, pdu_info_ptr);
        else
            ret = transmit_status;
    }
}
```

## 6. 配置项参考规范

[Com 配置项参考规范](../../configuration_reference/com_cfg.md)

[PduR 配置项参考规范](../../configuration_reference/pdur_cfg.md)

[ComM 配置项参考规范](../../configuration_reference/comm_cfg.md)

[CanIf 配置项参考规范](../../configuration_reference/canif_cfg.md)

## 7. 应用接口参考规范

[Com API 参考规范](../../api_reference/com_api.md)

[PduR API 参考规范](../../api_reference/pdur_api.md)

[ComM API 参考规范](../../api_reference/comm_api.md)

[CanIf API 参考规范](../../api_reference/canif_api.md)
