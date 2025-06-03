# NvM API参考文档

> 提示：本API参考文档仅代表功能栈的接口描述和功能说明，帮助开发者快速了解接口作用。应用开发者应通过服务映射调用对应的RTE接口，而非直接调用本文接口

## `nvm_init`

| 属性         | 描述                |
|--------------|---------------------|
| 函数定义      | `void nvm_init(void)`        |
| 简要描述      | NvM 初始化             |
| 详细说明      | 初始化 NvM 内部变量和设置为其默认状态，配置模块所需的资源，为后续操作提供一致的起始状态。    |
| 同步/异步     | 同步 |
| 可重入性     | 非可重入 |

## `nvm_deinit`

| 属性         | 描述                |
|--------------|---------------------|
| 函数定义      | `void nvm_deinit(void)`        |
| 简要描述      | NvM 反初始化             |
| 详细说明      | 反初始化 NvM 内部变量和设置为未初始化状态，使其回到未初始化的状态，为关闭或重启系统做准备。    |
| 同步/异步     | 同步 |
| 可重入性     | 非可重入 |

## `nvm_read_all`

| 属性         | 描述                |
|--------------|---------------------|
| 函数定义      | `void nvm_read_all(void)`        |
| 简要描述      | 创建ReadAll Job             |
| 详细说明      | 请求读取所有配置块（Block），将数据从非易失性存储读取到 RAM，通常在系统启动时调用。    |
| 同步/异步     | 异步 |
| 可重入性     | 非可重入 |

## `nvm_write_all`

| 属性         | 描述                |
|--------------|---------------------|
| 函数定义      | `void nvm_write_all(void)`        |
| 简要描述      | 创建WriteAll Job             |
| 详细说明      | 请求将所有RAM块（Block）写入到相应的非易失性存储（NV Block）中，通常用于系统休眠时保存当前运行时的数据。    |
| 同步/异步     | 异步 |
| 可重入性     | 非可重入 |

## `nvm_cancel_write_all`

| 属性         | 描述                |
|--------------|---------------------|
| 函数定义      | `void nvm_cancel_write_all(void)`        |
| 简要描述      | 取消WriteAll job             |
| 详细说明      | 取消当前进行的WriteAll操作，如果可能的话，以避免不必要的数据写入操作。    |
| 同步/异步     | 异步 |
| 可重入性     | 非可重入 |

## `nvm_set_data_index`

| 属性         | 描述                |
|--------------|---------------------|
| 函数定义      | `Std_ReturnType nvm_set_data_index(nvm_block_id_t block_id, uint8 data_index)`        |
| 简要描述      | 设置 NvM block dataindex             |
| 详细说明      | 该请求将设置 dataset 类型的 NVRAM block 的 dataindex，用于选择性地访问或修改相关数据集。    |
| 参数[输入] | `nvm_block_id_t block_id` 存储块的标识符。  |
| 参数[输入] | `uint8 data_index` 要设置的数据索引值。  |
| 返回值 | Std_ReturnType E_OK dataindex 成功设置。 |
| 返回值 | Std_ReturnType E_NOT_OK 设置失败。 |
| 同步/异步     | 同步 |
| 可重入性     | 可重入 |

## `nvm_get_data_index`

| 属性         | 描述                |
|--------------|---------------------|
| 函数定义      | `Std_ReturnType nvm_get_data_index(nvm_block_id_t block_id, uint8 *data_index_ptr)`        |
| 简要描述      | 获取 NvM block dataindex             |
| 详细说明      | 该请求将获取 dataset 类型的 NVRAM block 的 dataindex，帮助上层应用程序确定被操作的数据集。    |
| 参数[输入] | `nvm_block_id_t block_id` 存储块的标识符。  |
| 参数[输入输出] | `uint8 * data_index_ptr` 指向变量的指针，该变量将更新为获取到的数据索引值。  |
| 返回值 | Std_ReturnType E_OK dataindex 成功获取。 |
| 返回值 | Std_ReturnType E_NOT_OK 获取失败。 |
| 同步/异步     | 同步 |
| 可重入性     | 可重入 |

## `nvm_set_block_lock_status`

| 属性         | 描述                |
|--------------|---------------------|
| 函数定义      | `void nvm_set_block_lock_status(nvm_block_id_t block_id, boolean block_locked)`        |
| 简要描述      | 设置 NvM block 锁定状态             |
| 详细说明      | 更改 NV 块的锁定状态，可以防止对关键数据的意外修改，确保数据保密性和安全性。    |
| 参数[输入] | `nvm_block_id_t block_id` 存储块的标识符。  |
| 参数[输入] | `boolean block_locked` 锁定状态，true为锁定，false为解锁。  |
| 同步/异步     | 同步 |
| 可重入性     | 可重入 |

## `nvm_control_main_function`

| 属性         | 描述                |
|--------------|---------------------|
| 函数定义      | `void nvm_control_main_function(boolean enable_execute)`        |
| 简要描述      | 控制 NvM 主功能的执行             |
| 详细说明      | 提供独立于全局状态的信息，返回指定块的错误或成功状态，以帮助诊断和处理块级操作问题。    |
| 参数[输入] | `boolean enable_execute` 启用或禁用执行的标志。  |
| 同步/异步     | 同步 |
| 可重入性     | 可重入 |

## `nvm_get_error_status`

| 属性         | 描述                |
|--------------|---------------------|
| 函数定义      | `Std_ReturnType nvm_get_error_status(nvm_block_id_t block_id, nvm_request_result_type *request_result)`        |
| 简要描述      | 获取 NvM block 结果状态             |
| 详细说明      | 该请求将获取每个 block 独立的 error/status 信息    |
| 参数[输入] | `nvm_block_id_t block_id` 存储块的标识符。  |
| 参数[输入输出] | `nvm_request_result_type * request_result` 指向请求结果的指针。  |
| 返回值 | Std_ReturnType E_OK 状态成功获取。 |
| 返回值 | Std_ReturnType E_NOT_OK 获取失败。 |
| 同步/异步     | 同步 |
| 可重入性     | 可重入 |

## `nvm_set_ram_block_status`

| 属性         | 描述                |
|--------------|---------------------|
| 函数定义      | `Std_ReturnType nvm_set_ram_block_status(nvm_block_id_t block_id, boolean block_changed)`        |
| 简要描述      | 设置 NvM block 中 RAM Block 状态             |
| 详细说明      | 该请求将设置 permanent RAM block 状态，包括 valid/invalid。    |
| 参数[输入] | `nvm_block_id_t block_id` 存储块的标识符。  |
| 参数[输入] | `boolean block_changed` RAM块状态改变标志。  |
| 返回值 | Std_ReturnType E_OK 成功设置 RAM block 状态。 |
| 返回值 | Std_ReturnType E_NOT_OK 未能成功设置 RAM block 状态。 |
| 同步/异步     | 同步 |
| 可重入性     | 可重入 |

## `nvm_read_block`

| 属性         | 描述                |
|--------------|---------------------|
| 函数定义      | `Std_ReturnType nvm_read_block(nvm_block_id_t block_id, void *dst_ptr)`        |
| 简要描述      | 读取指定的 NvM block             |
| 详细说明      | 请求将 NV block 中的数据读取到所对应的 RAM block 中。    |
| 参数[输入] | `nvm_block_id_t block_id` 存储块的标识符。  |
| 参数[输入] | `void * dst_ptr` 指向目标RAM块的指针。  |
| 返回值 | Std_ReturnType E_OK 成功创建请求。 |
| 返回值 | Std_ReturnType E_NOT_OK 未能成功创建请求。 |
| 同步/异步     | 异步 |
| 可重入性     | 可重入 |

## `nvm_write_block`

| 属性         | 描述                |
|--------------|---------------------|
| 函数定义      | `Std_ReturnType nvm_write_block(nvm_block_id_t block_id, const void *src_ptr)`        |
| 简要描述      | 将数据写入到 NvM block             |
| 详细说明      | 请求将 RAM block 中的数据写入到所对应的 NV block 中。    |
| 参数[输入] | `nvm_block_id_t block_id` 存储块的标识符。  |
| 参数[输入] | `const void * src_ptr` 指向源RAM块的指针。  |
| 返回值 | Std_ReturnType E_OK 成功创建请求。 |
| 返回值 | Std_ReturnType E_NOT_OK 未能成功创建请求。 |
| 同步/异步     | 异步 |
| 可重入性     | 可重入 |

## `nvm_restore_block_defaults`

| 属性         | 描述                |
|--------------|---------------------|
| 函数定义      | `Std_ReturnType nvm_restore_block_defaults(nvm_block_id_t block_id, void *dst_ptr)`        |
| 简要描述      | 将 NvM block 中的数据恢复为默认值             |
| 详细说明      | 使用 ROM block 中的数据拷贝到相对应的 RAM block 中。    |
| 参数[输入] | `nvm_block_id_t block_id` 存储块的标识符。  |
| 参数[输入] | `void * dst_ptr` 指向目标RAM块的指针。  |
| 返回值 | Std_ReturnType E_OK 成功创建请求。 |
| 返回值 | Std_ReturnType E_NOT_OK 未能成功创建请求。 |
| 同步/异步     | 异步 |
| 可重入性     | 非可重入 |

## `nvm_cancel_jobs`

| 属性         | 描述                |
|--------------|---------------------|
| 函数定义      | `Std_ReturnType nvm_cancel_jobs(nvm_block_id_t block_id)`        |
| 简要描述      | 取消处于等待状态下的任务             |
| 详细说明      | 将指定 Block 相关的所有任务都取消。    |
| 参数[输入] | `nvm_block_id_t block_id` 指定的非易失性内存（NvM）块的标识符。  |
| 返回值 | Std_ReturnType E_OK 成功取消。 |
| 返回值 | Std_ReturnType E_NOT_OK 操作失败。 |
| 同步/异步     | 异步 |
| 可重入性     | 可重入 |

## `nvm_read_pram_block`

| 属性         | 描述                |
|--------------|---------------------|
| 函数定义      | `Std_ReturnType nvm_read_pram_block(nvm_block_id_t block_id)`        |
| 简要描述      | 读取指定的 NvM block             |
| 详细说明      | 请求将 NV block 中的数据读取到所配置的 RAM block 中。    |
| 参数[输入] | `nvm_block_id_t block_id` 存储块的唯一标识符。  |
| 返回值 | Std_ReturnType E_OK 成功创建请求。 |
| 返回值 | Std_ReturnType E_NOT_OK 未能成功创建请求。 |
| 同步/异步     | 异步 |
| 可重入性     | 可重入 |

## `nvm_write_pram_block`

| 属性         | 描述                |
|--------------|---------------------|
| 函数定义      | `Std_ReturnType nvm_write_pram_block(nvm_block_id_t block_id)`        |
| 简要描述      | 将数据写入到 NvM block             |
| 详细说明      | 请求将配置的 RAM block 中的数据写入到所对应的 NV block 中。    |
| 参数[输入] | `nvm_block_id_t block_id` 存储块的唯一标识符。  |
| 返回值 | Std_ReturnType E_OK 成功创建请求。 |
| 返回值 | Std_ReturnType E_NOT_OK 未能成功创建请求。 |
| 同步/异步     | 异步 |
| 可重入性     | 可重入 |

## `nvm_restore_pram_block_defaults`

| 属性         | 描述                |
|--------------|---------------------|
| 函数定义      | `Std_ReturnType nvm_restore_pram_block_defaults(nvm_block_id_t block_id)`        |
| 简要描述      | 将 NvM block 中的数据恢复为默认值             |
| 详细说明      | 使用配置的 ROM block 中的数据拷贝到相对应的 RAM block 中。    |
| 参数[输入] | `nvm_block_id_t block_id` 存储块的唯一标识符。  |
| 返回值 | Std_ReturnType E_OK 成功创建请求。 |
| 返回值 | Std_ReturnType E_NOT_OK 未能成功创建请求。 |
| 同步/异步     | 异步 |
| 可重入性     | 不可重入 |

## `nvm_set_block_protection`

| 属性         | 描述                |
|--------------|---------------------|
| 函数定义      | `Std_ReturnType nvm_set_block_protection(nvm_block_id_t block_id, boolean protection_enabled)`        |
| 简要描述      | 设置 NvM Block 写保护             |
| 详细说明      | 设置 NvM Block 为写保护后将禁止该 Block 被写入和擦除。    |
| 参数[输入] | `nvm_block_id_t block_id` 存储块的唯一标识符。  |
| 参数[输入] | `boolean protection_enabled` 是否启用写保护。  |
| 返回值 | Std_ReturnType E_OK 写保护设置成功。 |
| 返回值 | Std_ReturnType E_NOT_OK 写保护设置失败。 |
| 同步/异步     | 同步 |
| 可重入性     | 可重入 |

## `nvm_erase_nv_block`

| 属性         | 描述                |
|--------------|---------------------|
| 函数定义      | `Std_ReturnType nvm_erase_nv_block(nvm_block_id_t block_id)`        |
| 简要描述      | 创建擦除指定 NV block 的任务             |
| 详细说明      | 发起请求以清除指定的 NV 存储块内容，但不影响其对应的 RAM 块数据。该步骤通常为Immediate Block写入的前置调用。    |
| 参数[输入] | `nvm_block_id_t block_id` 存储块的唯一标识符。  |
| 返回值 | Std_ReturnType E_OK 成功创建请求。 |
| 返回值 | Std_ReturnType E_NOT_OK 未能成功创建请求。 |
| 同步/异步     | 异步 |
| 可重入性     | 可重入 |

## `nvm_invalidate_nv_block`

| 属性         | 描述                |
|--------------|---------------------|
| 函数定义      | `Std_ReturnType nvm_invalidate_nv_block(nvm_block_id_t block_id)`        |
| 简要描述      | 创建将指定 NV block 标记为无效的任务             |
| 详细说明      | 此函数发起请求以将指定的存储块标记为无效，确保不再被访问或使用，以节省存储资源。    |
| 参数[输入] | `nvm_block_id_t block_id` 存储块的唯一标识符。  |
| 返回值 | Std_ReturnType E_OK 成功创建请求。 |
| 返回值 | Std_ReturnType E_NOT_OK 未能成功创建请求。 |
| 同步/异步     | 异步 |
| 可重入性     | 可重入 |
