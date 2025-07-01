# Os API参考文档

> 提示：本API参考文档仅代表功能栈的接口描述和功能说明，帮助开发者快速了解接口作用。应用开发者应通过服务映射调用对应的RTE接口，而非直接调用本文接口

## `ActivateTask`

| 属性         | 描述                |
|--------------|---------------------|
| 函数定义      | `StatusType ActivateTask(TaskType TaskID)`        |
| 简要描述      | 激活指定任务             |
| 详细说明      | 将任务从挂起态转为就绪态，确保从任务入口函数开始执行    |
| 参数[输入] | `TaskType TaskID` 任务标识符  |
| 返回值 | StatusType E_OK 操作成功 |
| 返回值 | StatusType E_OS_LIMIT 激活次数超过阈值 |
| 返回值 | StatusType E_OS_ID 无效的任务ID |
| 同步/异步     | 同步调用 |
| 可重入性     | 可重入 |

## `ActivateTaskAsyn`

| 属性         | 描述                |
|--------------|---------------------|
| 函数定义      | `void ActivateTaskAsyn(TaskType TaskID)`        |
| 简要描述      | 异步任务激活             |
| 详细说明      | 非阻塞式激活任务，立即返回不等待任务执行    |
| 参数[输入] | `TaskType TaskID` 任务标识符  |
| 同步/异步     | 异步调用 |
| 可重入性     | 可重入 |

## `TerminateTask`

| 属性         | 描述                |
|--------------|---------------------|
| 函数定义      | `StatusType TerminateTask(void)`        |
| 简要描述      | 终止当前任务             |
| 详细说明      | 将调用任务从运行态转为挂起态，释放所有占用的资源 注意：在终止前需释放持有的自旋锁    |
| 返回值 | StatusType E_OK 操作成功 |
| 返回值 | StatusType E_NOT_OK 终止失败（如处于中断上下文） |
| 同步/异步     | 同步调用 |
| 可重入性     | 可重入 |

## `task_tickdelay`

| 属性         | 描述                |
|--------------|---------------------|
| 函数定义      | `StatusType task_tickdelay(TickType ticks_to_delay)`        |
| 简要描述      | 任务延时函数             |
| 详细说明      | 使当前任务阻塞等待一段时间    |
| 参数[输入] | `TickType ticks_to_delay` 阻塞等待Tick  |
| 返回值 | StatusType E_OK 无错误 |
| 返回值 | StatusType E_OS_CALLEVEL 在ISR上下文中调用 |
| 返回值 | StatusType E_OS_RESOURCE 资源被占用 |
| 返回值 | StatusType E_OS_VALUE 参数小于0 |
| 同步/异步     | 同步调用 |
| 可重入性     | 可重入 |

## `StartScheduleTableRel`

| 属性         | 描述                |
|--------------|---------------------|
| 函数定义      | `StatusType StartScheduleTableRel(ScheduleTableType SchedTableID, TickType Offset)`        |
| 简要描述      | 相对时间启动调度表             |
| 详细说明      | 基于当前计数器值偏移启动    |
| 参数[输入] | `ScheduleTableType SchedTableID` 调度表ID  |
| 参数[输入] | `TickType Offset` 启动偏移量  |
| 返回值 | StatusType E_OK 启动成功 |
| 返回值 | StatusType E_OS_ID 无效调度表ID |
| 返回值 | StatusType E_OS_VALUE 偏移量超过(OsCounterMaxValue - InitialOffset)或为0 |
| 返回值 | StatusType E_OS_STATE 调度表已运行 |
| 同步/异步     | 同步调用 |
| 可重入性     | 可重入 |

## `StartScheduleTableAbs`

| 属性         | 描述                |
|--------------|---------------------|
| 函数定义      | `StatusType StartScheduleTableAbs(ScheduleTableType SchedTableID, TickType Start)`        |
| 简要描述      | 绝对时间启动调度表             |
| 详细说明      | 在指定计数器绝对数值点启动调度表，适用于时间精准触发的场景    |
| 参数[输入] | `ScheduleTableType SchedTableID` 调度表ID（范围：1~OS_SCHTBL_NUM，参见Os_Cfg.h）  |
| 参数[输入] | `TickType Start` 启动的绝对计数值（需满足：Start % OsCounterCycle = 0）  |
| 返回值 | StatusType E_OK 启动成功，调度表进入RUNNING状态 |
| 返回值 | StatusType E_OS_ID 无效调度表ID（建议使用GetActiveScheduleTable进行诊断） |
| 返回值 | StatusType E_OS_VALUE Start值超过OsCounterMaxAllowedValue（最大值：OS_COUNTER_MAX_VALUE） |
| 返回值 | StatusType E_OS_STATE 调度表已处于STARTED/RUNNING状态（需先调用StopScheduleTable） |
| 同步/异步     | 同步调用（阻塞直到调度表加入就绪队列） |
| 可重入性     | 可重入（采用自旋锁保护调度表状态机） |

## `StopScheduleTable`

| 属性         | 描述                |
|--------------|---------------------|
| 函数定义      | `StatusType StopScheduleTable(ScheduleTableType SchedTableID)`        |
| 简要描述      | 立即停止调度表             |
| 详细说明      | 强制终止指定调度表的运行，将其状态置为STOPPED    |
| 参数[输入] | `ScheduleTableType SchedTableID` 调度表ID  |
| 返回值 | StatusType E_OK 停止成功，调度表进入STOPPED状态 |
| 返回值 | StatusType E_OS_ID 无效调度表ID |
| 返回值 | StatusType E_OS_NOFUNC 调度表已处于STOPPED状态 |
| 同步/异步     | 同步调用 |
| 可重入性     | 可重入 |

## `GetScheduleTableStatus`

| 属性         | 描述                |
|--------------|---------------------|
| 函数定义      | `StatusType GetScheduleTableStatus(ScheduleTableType SchedTableID, ScheduleTableStatusRefType StatusRef)`        |
| 简要描述      | 获取调度表状态信息             |
| 详细说明      | 查询指定调度表的完整运行状态    |
| 参数[输入] | `ScheduleTableType SchedTableID` 调度表ID（范围：1~OS_SCHTBL_NUM，参考Os_SchedTbl_CfgType配置）  |
| 参数[输出] | `ScheduleTableStatusRefType StatusRef` 状态信息结构体指针（内存需由调用方分配）  |
| 返回值 | StatusType E_OK 查询成功，StatusRef字段已更新 |
| 返回值 | StatusType E_OS_ID 无效调度表ID（建议结合ListActiveSchedTables接口验证） |
| 同步/异步     | 同步调用（执行时间<500ns，无上下文切换） |
| 可重入性     | 可重入（采用RCU机制保障多核读取一致性） |

## `NextScheduleTable`

| 属性         | 描述                |
|--------------|---------------------|
| 函数定义      | `StatusType NextScheduleTable(ScheduleTableType CurrSchedTableID, ScheduleTableType NextSchedTableID)`        |
| 简要描述      | 动态切换调度表             |
| 详细说明      | 实现运行中调度表的热切换，保持时序连续性：    |
| 参数[输入] | `ScheduleTableType CurrSchedTableID` 当前活跃调度表ID  |
| 参数[输入] | `ScheduleTableType NextSchedTableID` 目标调度表ID  |
| 返回值 | StatusType E_OK 切换成功，NextSchedTableID进入RUNNING状态 |
| 返回值 | StatusType E_OS_ID 无效调度表ID |
| 返回值 | StatusType E_OS_NOFUNC 当前调度表未启动 |
| 返回值 | StatusType E_OS_STATE 目标调度表处于非法状态（STARTED/RUNNING/NEXT） |
| 同步/异步     | 同步调用（最大阻塞时间50us，符合ASIL-D时序约束） |
| 可重入性     | 可重入（采用双锁机制保护状态迁移） |

## `NextScheduleTableFromStop`

| 属性         | 描述                |
|--------------|---------------------|
| 函数定义      | `StatusType NextScheduleTableFromStop(ScheduleTableType CurrSchedTableID, ScheduleTableType NextSchedTableID)`        |
| 简要描述      | 停止态调度表链式切换             |
| 详细说明      | 在当前调度表处于STOPPED状态时建立调度表执行链，实现调度策略的预配置切换：    |
| 参数[输入] | `ScheduleTableType CurrSchedTableID` 已停止的调度表ID（范围：1~OS_SCHTBL_NUM）  |
| 参数[输入] | `ScheduleTableType NextSchedTableID` 后续调度表ID（需配置相同counter基准）  |
| 返回值 | StatusType E_OK 链式关系建立成功 |
| 返回值 | StatusType E_OS_ID 无效调度表ID（建议使用VerifySchedTableChain接口预校验） |
| 返回值 | StatusType E_OS_NOFUNC 当前调度表未停止（需先执行StopScheduleTable） |
| 返回值 | StatusType E_OS_STATE 目标调度表处于非法状态（STARTED/RUNNING/NEXT） |
| 同步/异步     | 同步调用（执行时间确定，最大延迟15us） |
| 可重入性     | 可重入（基于每调度表的链式锁实现） |

## `StartScheduleTableSynchron`

| 属性         | 描述                |
|--------------|---------------------|
| 函数定义      | `StatusType StartScheduleTableSynchron(ScheduleTableType SchedTableID)`        |
| 简要描述      | 显式同步启动调度表             |
| 详细说明      | 启动配置为显式同步(EXPLICIT)模式的调度表    |
| 参数[输入] | `ScheduleTableType SchedTableID` 调度表ID  |
| 返回值 | StatusType E_OK 成功进入WAIT_SYNC状态 |
| 返回值 | StatusType E_OS_ID 无效调度表ID或非显式同步表 |
| 返回值 | StatusType E_OS_STATE 调度表已处于非STOPPED状态 |
| 同步/异步     | 同步调用 |
| 可重入性     | 可重入 |

## `SyncScheduleTable`

| 属性         | 描述                |
|--------------|---------------------|
| 函数定义      | `StatusType SyncScheduleTable(ScheduleTableType SchedTableID, TickType TickValue)`        |
| 简要描述      | 调度表同步信号注入             |
| 详细说明      | 向显式同步调度表注入时间基准信号，实现多ECU时间精准对齐。    |
| 参数[输入] | `ScheduleTableType SchedTableID` 调度表ID  |
| 参数[输入] | `TickType TickValue` 主计数器当前值（需通过安全时钟源获取）  |
| 返回值 | StatusType E_OK 同步成功 |
| 返回值 | StatusType E_OS_ID 无效ID或策略非显式同步 |
| 返回值 | StatusType E_OS_VALUE 数值越界（TickValue > OsCounterMaxValue） |
| 返回值 | StatusType E_OS_STATE 调度表未处于WAIT_SYNC状态 |
| 同步/异步     | 同步 |
| 可重入性     | 可重入 |

## `SetScheduleTableAsync`

| 属性         | 描述                |
|--------------|---------------------|
| 函数定义      | `StatusType SetScheduleTableAsync(ScheduleTableType SchedTableID)`        |
| 简要描述      | 调度表异步模式切换             |
| 详细说明      | 将显式同步调度表转为异步自由运行模式，解除与主计数器的时间耦合。切换后调度表周期由本地时钟驱动。    |
| 参数[输入] | `ScheduleTableType SchedTableID` 调度表ID  |
| 返回值 | StatusType E_OK 模式切换成功 |
| 返回值 | StatusType E_OS_ID 无效调度表ID |
| 同步/异步     | 同步 |
| 可重入性     | 可重入 |

## `DeviateScheduleTable`

| 属性         | 描述                |
|--------------|---------------------|
| 函数定义      | `StatusType DeviateScheduleTable(ScheduleTableType schedtable_id, DeviateType deviate_value)`        |
| 简要描述      | 调度表偏差值注入             |
| 详细说明      | 向显式同步调度表注入指定的偏差值，用于补偿调度表与同步计数器之间的时间漂移    |
| 参数[输入] | `ScheduleTableType schedtable_id` 调度表ID  |
| 参数[输入] | `DeviateType deviate_value` 偏差值（正值=加速调度表，负值=减速调度表，绝对值不得超过调度表duration ） |
| 返回值 | StatusType E_OK 偏差注入成功，调度表将在后续执行中逐步消除偏差 |
| 返回值 | StatusType E_OS_ID 无效ID或策略非显式同步 |
| 返回值 | StatusType E_OS_VALUE 偏差值超出允许范围 |
| 返回值 | StatusType E_OS_STATE 调度表未处于运行状态 |
| 同步/异步     | 同步 |
| 可重入性     | 可重入 |

## `EnableAllInterrupts`

| 属性         | 描述                |
|--------------|---------------------|
| 函数定义      | `void EnableAllInterrupts(void)`        |
| 简要描述      | 恢复由DisableAllInterrupts保存的状态             |
| 详细说明      | 该服务可从1类中断2类中断以及任务级别调用，但不能从hook调用。 本服务是DisableAllInterrupts服务的对应操作（必须先调用DisableAllInterrupts）， 其目的是结束临界区。离开临界区时不应调用任何API服务。 实现应根据目标硬件适配本服务以提供最小开销。 通常，该服务会启用CPU对中断的识别。    |
| 同步/异步     | 同步 |
| 可重入性     | 可重入 |

## `DisableAllInterrupts`

| 属性         | 描述                |
|--------------|---------------------|
| 函数定义      | `void DisableAllInterrupts(void)`        |
| 简要描述      | 禁用所有硬件支持屏蔽的中断。在调用EnableAllInterrupts前保存状态             |
| 详细说明      | 该服务可从1类中断2类中断以及任务级别调用，但不能从hook调用。 本服务用于启动临界区。该临界区必须通过调用EnableAllInterrupts服务来结束。 在此临界区内不允许调用任何API服务。实现应根据目标硬件适配本服务以提供最小开销。 通常，该服务会禁用CPU对中断的识别。 注意：本服务不支持嵌套。如需临界区嵌套（如库函数场景）， 应使用SuspendOSInterrupts/ResumeOSInterrupts或SuspendAllInterrupt/ResumeAllInterrupts服务。    |
| 同步/异步     | 同步 |
| 可重入性     | 可重入 |

## `ResumeAllInterrupts`

| 属性         | 描述                |
|--------------|---------------------|
| 函数定义      | `void ResumeAllInterrupts(void)`        |
| 简要描述      | 恢复由SuspendAllInterrupts服务保存的所有中断识别状态             |
| 详细说明      | 该服务可从1类中断2类中断以及任务级别调用， 但不能从所有钩子例程调用。本服务是SuspendAllInterrupts服务的对应操作 （必须先调用SuspendAllInterrupts），其目的是结束临界区。 在此临界区内，除SuspendAllInterrupts/ResumeAllInterrupts对和 SuspendOSInterrupts/ResumeOSInterrupts对外，不允许调用其他API服务。 实现应根据目标硬件适配本服务以提供最小开销。 SuspendAllInterrupts/ResumeAllInterrupts可嵌套调用。 当嵌套调用SuspendAllInterrupts和ResumeAllInterrupts时， 首次SuspendAllInterrupts调用保存的中断识别状态将由最后一次 ResumeAllInterrupts服务调用恢复。    |
| 同步/异步     | 同步 |
| 可重入性     | 可重入 |

## `SuspendAllInterrupts`

| 属性         | 描述                |
|--------------|---------------------|
| 函数定义      | `void SuspendAllInterrupts(void)`        |
| 简要描述      | 保存所有中断的识别状态并禁用硬件支持屏蔽的所有中断             |
| 详细说明      | 该服务可从1类中断2类中断、警报回调例程以及任务级别调用， 但不能从所有钩子例程调用。本服务用于保护代码临界区免受任何中断干扰。 该临界区必须通过调用ResumeAllInterrupts服务来结束。 在此临界区内，除SuspendAllInterrupts/ResumeAllInterrupts对和 SuspendOSInterrupts/ResumeOSInterrupts对外，不允许调用其他API服务。 实现应根据目标硬件适配本服务以提供最小开销。    |
| 同步/异步     | 同步 |
| 可重入性     | 可重入 |

## `ResumeOSInterrupts`

| 属性         | 描述                |
|--------------|---------------------|
| 函数定义      | `void ResumeOSInterrupts(void)`        |
| 简要描述      | 恢复由SuspendOSInterrupts服务保存的中断识别状态             |
| 详细说明      | 该服务可从ISR类别1和类别2以及任务级别调用，但不能从钩子例程调用。 本服务是SuspendOSInterrupts服务的对应操作（必须先调用SuspendOSInterrupts）， 其目的是结束临界区。在此临界区内，除SuspendAllInterrupts/ResumeAllInterrupts对和 SuspendOSInterrupts/ResumeOSInterrupts对外，不允许调用其他API服务。 实现应根据目标硬件适配本服务以提供最小开销。 SuspendOSInterrupts/ResumeOSInterrupts支持嵌套调用。当嵌套调用 SuspendOSInterrupts和ResumeOSInterrupts时，首次SuspendOSInterrupts调用 保存的中断识别状态将由最后一次ResumeOSInterrupts服务调用恢复。    |
| 同步/异步     | 同步 |
| 可重入性     | 可重入 |

## `SuspendOSInterrupts`

| 属性         | 描述                |
|--------------|---------------------|
| 函数定义      | `void SuspendOSInterrupts(void)`        |
| 简要描述      | 保存2类中断的识别状态并禁用其中断识别             |
| 详细说明      | 该服务可从ISR和任务级别调用，但不能从钩子例程调用。 本服务用于保护代码临界区，该临界区必须通过调用ResumeOSInterrupts服务来结束。 在此临界区内，除SuspendAllInterrupts/ResumeAllInterrupts对和 SuspendOSInterrupts/ResumeOSInterrupts对外，不允许调用其他API服务。 实现应根据目标硬件适配本服务以提供最小开销。本服务仅禁用类别2中断的识别， 但如果无法高效实现，则可能会禁用更多中断。    |
| 同步/异步     | 同步 |
| 可重入性     | 可重入 |

## `SetEvent`

| 属性         | 描述                |
|--------------|---------------------|
| 函数定义      | `StatusType SetEvent(TaskType TaskID, EventMaskType Mask)`        |
| 简要描述      | 向任务发送事件             |
| 详细说明      | 该接口将Mask指定的事件发送至目标任务。若目标任务正在等待Mask中指定的 一个或多个事件，则目标任务将转为就绪状态。    |
| 参数[输入] | `TaskType TaskID` 目标任务ID  |
| 参数[输入] | `EventMaskType Mask` 待发送的事件掩码  |
| 返回值 | StatusType E_OK 事件发送成功 |
| 返回值 | StatusType E_OS_ID 目标任务ID无效 |
| 返回值 | StatusType E_OS_ACCESS 目标任务不是扩展任务 |
| 返回值 | StatusType E_OS_STATE 目标任务处于挂起状态 |
| 同步/异步     | 同步 |
| 可重入性     | 可重入 |

## `SetEventAsyn`

| 属性         | 描述                |
|--------------|---------------------|
| 函数定义      | `void SetEventAsyn(TaskType TaskID, EventMaskType Mask)`        |
| 简要描述      | 异步向任务发送事件             |
| 详细说明      | 该接口将Mask指定的事件发送至目标任务。若目标任务正在等待Mask中指定的一个或多个事件， 则目标任务将转为就绪状态。    |
| 参数[输入] | `TaskType TaskID` 目标任务ID  |
| 参数[输入] | `EventMaskType Mask` 待发送的事件掩码  |
| 同步/异步     | 同步 |
| 可重入性     | 可重入 |

## `ClearEvent`

| 属性         | 描述                |
|--------------|---------------------|
| 函数定义      | `StatusType ClearEvent(EventMaskType Mask)`        |
| 简要描述      | 清除事件值             |
| 详细说明      | 该接口从当前任务的事件值中清除由Mask指定的事件。    |
| 参数[输入] | `EventMaskType Mask` 待清除的事件掩码  |
| 返回值 | StatusType E_OK 事件清除成功 |
| 返回值 | StatusType E_OS_ACCESS 调用任务不是扩展任务 |
| 返回值 | StatusType E_OS_CALLEVEL 在中断上下文中调用 |
| 同步/异步     | 同步 |
| 可重入性     | 可重入 |

## `GetEvent`

| 属性         | 描述                |
|--------------|---------------------|
| 函数定义      | `StatusType GetEvent(TaskType TaskID, EventMaskRefType Mask)`        |
| 简要描述      | 获取事件值             |
| 详细说明      | 该接口用于获取目标任务当前的事件值    |
| 参数[输入] | `TaskType TaskID` 目标任务ID  |
| 参数[输出] | `EventMaskRefType Mask` 用于存储获取到的事件值的指针  |
| 返回值 | StatusType E_OK 事件获取成功 |
| 返回值 | StatusType E_OS_ID 目标任务ID无效 |
| 返回值 | StatusType E_OS_ACCESS 目标任务不是扩展任务 |
| 返回值 | StatusType E_OS_STATE 目标任务处于挂起状态 |
| 同步/异步     | 同步 |
| 可重入性     | 可重入 |

## `WaitEvent`

| 属性         | 描述                |
|--------------|---------------------|
| 函数定义      | `StatusType WaitEvent(EventMaskType Mask)`        |
| 简要描述      | 等待事件             |
| 详细说明      | 当未发生任何事件时，调用任务将进入等待状态。当等待的一个或多个事件发生时， 任务将转为就绪状态。此调用可能触发任务重新调度。当任务处于等待状态时， 其内部资源将被释放。该接口只能由拥有事件对象的扩展任务调用。    |
| 参数[输入] | `EventMaskType Mask` 等待的事件掩码  |
| 返回值 | StatusType E_OK 等待事件成功 |
| 返回值 | StatusType E_OS_ACCESS 调用任务不是扩展任务 |
| 返回值 | StatusType E_OS_RESOURCE 调用任务占用资源 |
| 返回值 | StatusType E_OS_CALLEVEL 在中断上下文中调用 |
| 同步/异步     | 同步 |
| 可重入性     | 可重入 |

## `event_tickwait`

| 属性         | 描述                |
|--------------|---------------------|
| 函数定义      | `StatusType event_tickwait(EventMaskType mask, TickType ticks_to_wait)`        |
| 简要描述      | 带超时的等待事件             |
| 详细说明      | 当未发生任何事件时，调用任务将进入等待状态。当等待的一个或多个事件发生时，任务将转为就绪状态。如果在指定的超时时间内没有事件发生，任务也会转为就绪状态。此调用可能触发任务重新调度当任务处于等待状态时，其内部资源将被释放。该接口只能由拥有事件对象的扩展任务调用    |
| 参数[输入] | `EventMaskType mask` 等待的事件掩码  |
| 参数[输入] | `TickType ticks_to_wait` 等待的超时时间(系统节拍数)  |
| 返回值 | StatusType E_OK 等待事件成功 |
| 返回值 | StatusType E_OS_ACCESS 调用任务不是扩展任务 |
| 返回值 | StatusType E_OS_RESOURCE 调用任务占用资源 |
| 返回值 | StatusType E_OS_CALLEVEL 在中断上下文中调用 |
| 返回值 | StatusType E_OS_TIMEOUT 等待超时 |
| 同步/异步     | 同步 |
| 可重入性     | 可重入 |

## `GetResource`

| 属性         | 描述                |
|--------------|---------------------|
| 函数定义      | `StatusType GetResource( ResourceType ResourceID )`        |
| 简要描述      | 进入代码中由 ResID 引用的资源分配的关键区域。关键区域应始终使用 ReleaseResource 离开。             |
| 详细说明      | 仅当内层关键区域完全在外围关键区域内执行时，才允许嵌套资源占用。同一资源的嵌套占用也是禁止的！建议在同一函数内出现对应的 GetResource 和 ReleaseResource 调用。在关键区域内不允许使用对不可抢占任务进行重新调度的服务。此外，必须在中断服务例程完成之前离开关键区域。一般来说，关键区域应尽量简短。本服务可从 ISR 和任务级别调用。    |
| 参数[输入] | `ResourceType ResourceID` 资源引用实例标识符  |
| 返回值 | StatusType E_OK 无错误 |
| 返回值 | StatusType E_OS_ID 资源 ResID 无效 |
| 返回值 | StatusType E_OS_ACCESS 尝试获取已被任何任务或 ISR 占用的资源，或调用任务或中断例程的静态分配优先级高于计算的顶级优先级 |
| 同步/异步     | 同步 |
| 可重入性     | 可重入 |

## `ReleaseResource`

| 属性         | 描述                |
|--------------|---------------------|
| 函数定义      | `ReleaseResource( ResourceType ResourceID )`        |
| 简要描述      | ReleaseResource 是 GetResource 的对应操作，用于离开代码中由 ResID 引用的资源分配的关键区域。             |
| 详细说明      | 有关嵌套条件的信息，请参阅 GetResource 的详细说明。本服务可从 ISR 和任务级别调用。    |
| 参数[输入] | `ResourceType ResourceID` 资源引用实例标识符  |
| 返回值 | StatusType E_OK 无错误 |
| 返回值 | StatusType E_OS_ID 资源 ResID 无效 |
| 返回值 | StatusType E_OS_NOFUNC 尝试释放未被任何任务或 ISR 占用的资源，或应先释放另一个资源 |
| 返回值 | StatusType E_OS_ACCESS 尝试获取已被任何任务或 ISR 占用的资源，或调用任务或中断例程的静态分配优先级高于计算的顶级优先级 |
| 同步/异步     | 同步 |
| 可重入性     | 可重入 |

## `GetSpinlock`

| 属性         | 描述                |
|--------------|---------------------|
| 函数定义      | `StatusType GetSpinlock(SpinlockIdType SpinlockID)`        |
| 简要描述      | 尝试占用自旋锁变量。函数返回时，表示锁已成功占用或发生错误。 自旋锁机制采用主动轮询方式，本函数不会触发任务重新调度。             |
| 详细说明      | 若函数返回，表示锁已成功占用或发生错误。自旋锁机制采用主动轮询方式， 本函数不会触发任务重新调度。    |
| 参数[输入] | `未知类型 SpinlockId` 要锁定的自旋锁实例标识符  |
| 返回值 | StatusType E_OK [标准:] 无错误 |
| 返回值 | StatusType E_OS_ID [扩展:] 自旋锁ID无效 |
| 返回值 | StatusType E_OS_ACCESS [扩展:] 无法访问自旋锁 |
| 返回值 | StatusType E_OS_INTERFERENCE_DEADLOCK [扩展:] 任务尝试占用已被同核任务占用的自旋锁， 可能导致死锁 |
| 返回值 | StatusType E_OS_NESTING_DEADLOCK [扩展:] 任务尝试占用自旋锁，但同核任务以可能 导致死锁的方式持有其他自旋锁 |
| 同步/异步     | 同步 |
| 可重入性     | 可重入 |

## `ReleaseSpinlock`

| 属性         | 描述                |
|--------------|---------------------|
| 函数定义      | `StatusType ReleaseSpinlock(SpinlockIdType SpinlockID)`        |
| 简要描述      | 释放先前占用的自旋锁变量             |
| 详细说明      | 在终止任务前，应释放所有通过GetSpinlock()占用的自旋锁变量。 在调用WaitEVENT前，必须释放所有自旋锁。    |
| 参数[输入] | `未知类型 SpinlockId` 要释放的自旋锁实例标识符  |
| 返回值 | StatusType 执行结果状态 |
| 返回值 | StatusType E_OK [标准:] 无错误 |
| 返回值 | StatusType E_OS_ID [扩展:] 自旋锁ID无效 |
| 返回值 | StatusType E_OS_ACCESS [扩展:] 无法访问自旋锁 |
| 返回值 | StatusType E_OS_STATE [扩展:] 自旋锁未被当前任务占用 |
| 返回值 | StatusType E_OS_NOFUNC [扩展:] 在释放本自旋锁前尝试释放其他自旋锁(或资源) |
| 同步/异步     | 同步 |
| 可重入性     | 可重入 |

## `TryToGetSpinlock`

| 属性         | 描述                |
|--------------|---------------------|
| 函数定义      | `StatusType TryToGetSpinlock(SpinlockIdType SpinlockID, TryToGetSpinlockType *Success)`        |
| 简要描述      | 尝试获取自旋锁并立即返回状态             |
| 详细说明      | TryToGetSpinlock与GetSpinlock功能相同，区别在于：如果自旋锁已被不同核的任务占用， 本函数将设置OUT参数"Success"并返回E_OK。    |
| 参数[输入] | `未知类型 SpinlockId` 要锁定的自旋锁实例标识符  |
| 参数[输出] | `TryToGetSpinlockType * Success` 返回是否成功占用锁的布尔值  |
| 返回值 | StatusType 执行结果状态 |
| 返回值 | StatusType E_OK [标准:] 无错误 |
| 返回值 | StatusType E_OS_ID [扩展:] 自旋锁ID无效 |
| 返回值 | StatusType E_OS_ACCESS [扩展:] 无法访问自旋锁 |
| 返回值 | StatusType E_OS_INTERFERENCE_DEADLOCK [扩展:] 任务尝试占用已被同核任务占用的自旋锁， 可能导致死锁 |
| 返回值 | StatusType E_OS_NESTING_DEADLOCK [扩展:] 任务尝试占用自旋锁，但同核任务以可能 导致死锁的方式持有其他自旋锁 |
| 同步/异步     | 同步 |
| 可重入性     | 可重入 |

## `GetSpinlockRead`

| 属性         | 描述                |
|--------------|---------------------|
| 函数定义      | `StatusType GetSpinlockRead(SpinlockIdType SpinlockID)`        |
| 简要描述      | 尝试占用读写锁中的读锁。函数返回时，表示锁已成功占用或发生错误。 读写锁机制采用主动轮询方式，本函数不会触发任务重新调度。             |
| 详细说明      | 若函数返回，表示锁已成功占用或发生错误。读写锁机制采用主动轮询方式， 本函数不会触发任务重新调度。    |
| 参数[输入] | `未知类型 SpinlockId` 要锁定的读写锁实例标识符  |
| 返回值 | StatusType E_OK [标准:] 无错误 |
| 返回值 | StatusType E_OS_ID [扩展:] 读写锁ID无效 |
| 返回值 | StatusType E_OS_ACCESS [扩展:] 无法访问读写锁 |
| 返回值 | StatusType E_OS_INTERFERENCE_DEADLOCK [扩展:] 任务尝试占用读锁，但该任务已持有 同一读写锁（读/写模式），可能导致死锁 |
| 同步/异步     | 同步 |
| 可重入性     | 可重入 |

## `GetSpinlockWrite`

| 属性         | 描述                |
|--------------|---------------------|
| 函数定义      | `StatusType GetSpinlockWrite(SpinlockIdType SpinlockID)`        |
| 简要描述      | 尝试占用读写锁中的写锁。函数返回时，表示锁已成功占用或发生错误。 读写锁机制采用主动轮询方式，本函数不会触发任务重新调度。             |
| 详细说明      | 若函数返回，表示锁已成功占用或发生错误。读写锁机制采用主动轮询方式， 本函数不会触发任务重新调度。    |
| 参数[输入] | `未知类型 SpinlockId` 要锁定的读写锁实例标识符  |
| 返回值 | StatusType E_OK [标准:] 无错误 |
| 返回值 | StatusType E_OS_ID [扩展:] 读写锁ID无效 |
| 返回值 | StatusType E_OS_ACCESS [扩展:] 无法访问读写锁 |
| 返回值 | StatusType E_OS_INTERFERENCE_DEADLOCK [扩展:] 任务尝试占用写锁，但该任务已持有 同一读写锁（读/写模式），可能导致死锁 |
| 同步/异步     | 同步 |
| 可重入性     | 可重入 |

## `ReleaseSpinlockRead`

| 属性         | 描述                |
|--------------|---------------------|
| 函数定义      | `StatusType ReleaseSpinlockRead(SpinlockIdType SpinlockID)`        |
| 简要描述      | 释放先前占用的读锁，减少读锁计数器             |
| 详细说明      | 在终止任务前，应释放所有通过GetSpinlockRead()占用的读写锁变量。 在调用WaitEVENT前，必须释放所有读写锁。    |
| 参数[输入] | `未知类型 SpinlockId` 要释放的读写锁实例标识符  |
| 返回值 | StatusType 执行结果状态 |
| 返回值 | StatusType E_OK [标准:] 无错误 |
| 返回值 | StatusType E_OS_ID [扩展:] 读写锁ID无效 |
| 返回值 | StatusType E_OS_ACCESS [扩展:] 无法访问读写锁 |
| 返回值 | StatusType E_OS_STATE [扩展:] 读写锁未被当前任务占用 |
| 同步/异步     | 同步 |
| 可重入性     | 可重入 |

## `ReleaseSpinlockWrite`

| 属性         | 描述                |
|--------------|---------------------|
| 函数定义      | `StatusType ReleaseSpinlockWrite(SpinlockIdType SpinlockID)`        |
| 简要描述      | 释放先前占用的写锁，并将写锁计数器清零             |
| 详细说明      | 在终止任务前，应释放所有通过GetSpinlockWrite()占用的读写锁变量。 在调用WaitEVENT前，必须释放所有读写锁。    |
| 参数[输入] | `未知类型 SpinlockId` 要释放的读写锁实例标识符  |
| 返回值 | StatusType 执行结果状态 |
| 返回值 | StatusType E_OK [标准:] 无错误 |
| 返回值 | StatusType E_OS_ID [扩展:] 读写锁ID无效 |
| 返回值 | StatusType E_OS_ACCESS [扩展:] 无法访问读写锁 |
| 返回值 | StatusType E_OS_STATE [扩展:] 读写锁未被当前任务占用 |
| 返回值 | StatusType E_OS_NOFUNC [扩展:] 在释放本读写锁前尝试释放其他读写锁(或资源) |
| 同步/异步     | 同步 |
| 可重入性     | 可重入 |

## `TryToGetSpinlockRead`

| 属性         | 描述                |
|--------------|---------------------|
| 函数定义      | `StatusType TryToGetSpinlockRead(SpinlockIdType SpinlockID, TryToGetSpinlockType *Success)`        |
| 简要描述      | 尝试获取读锁并立即返回状态             |
| 详细说明      | TryToGetSpinlockRead与GetSpinlockRead功能相同，区别在于：如果读写锁已被不同核的任务占用， 本函数将设置OUT参数"Success"并返回E_OK。    |
| 参数[输入] | `未知类型 SpinlockId` 要锁定的读写锁实例标识符  |
| 参数[输出] | `TryToGetSpinlockType * Success` 返回是否成功占用读锁的布尔值  |
| 返回值 | StatusType 执行结果状态 |
| 返回值 | StatusType E_OK [标准:] 无错误 |
| 返回值 | StatusType E_OS_ID [扩展:] 读写锁ID无效 |
| 返回值 | StatusType E_OS_ACCESS [扩展:] 无法访问读写锁 |
| 返回值 | StatusType E_OS_INTERFERENCE_DEADLOCK [扩展:] 任务尝试占用读锁，但该锁已被同核任务占用， 可能导致死锁 |
| 同步/异步     | 同步 |
| 可重入性     | 可重入 |

## `TryToGetSpinlockWrite`

| 属性         | 描述                |
|--------------|---------------------|
| 函数定义      | `StatusType TryToGetSpinlockWrite(SpinlockIdType SpinlockID, TryToGetSpinlockType *Success)`        |
| 简要描述      | 尝试获取写锁并立即返回状态             |
| 详细说明      | TryToGetSpinlockWrite与GetSpinlockWrite功能相同，区别在于：如果读写锁已被不同核的任务占用， 本函数将设置OUT参数"Success"并返回E_OK。    |
| 参数[输入] | `未知类型 SpinlockId` 要锁定的读写锁实例标识符  |
| 参数[输出] | `TryToGetSpinlockType * Success` 返回是否成功占用写锁的布尔值  |
| 返回值 | StatusType 执行结果状态 |
| 返回值 | StatusType E_OK [标准:] 无错误 |
| 返回值 | StatusType E_OS_ID [扩展:] 读写锁ID无效 |
| 返回值 | StatusType E_OS_ACCESS [扩展:] 无法访问读写锁 |
| 返回值 | StatusType E_OS_INTERFERENCE_DEADLOCK [扩展:] 任务尝试占用写锁，但该锁已被同核任务占用， 可能导致死锁 |
| 同步/异步     | 同步 |
| 可重入性     | 可重入 |

## `GetCoreID`

| 属性         | 描述                |
|--------------|---------------------|
| 函数定义      | `CoreIdType GetCoreID(void)`        |
| 简要描述      | OS服务GetCoreID()             |
| 详细说明      | 返回调用核的唯一逻辑核标识符。从物理核到逻辑CoreID的映射由具体实现决定。 本API仅允许在AUTOSAR核上使用。如需在非AUTOSAR核上使用该API， 可将该核配置为AUTOSAR核，但使用StartNonAutosarCore() API以非AUTOSAR核方式启动。    |
| 返回值 | CoreIdType 调用核的唯一ID |
| 同步/异步     | 同步 |
| 可重入性     | 可重入 |

## `IncrementCounter`

| 属性         | 描述                |
|--------------|---------------------|
| 函数定义      | `StatusType IncrementCounter(CounterType CounterID)`        |
| 简要描述      | OS服务IncrementCounter()            |
| 详细说明      | 该服务增加一个软件计数器    |
| 参数[输入] | `CounterType CounterID` 计数器索引值  |
| 返回值 | StatusType E_OK 无错误 |
| 返回值 | StatusType E_OS_ID  CounterID不是有效的软件计数器ID。 |
| 返回值 | StatusType E_OS_CALLEVEL 从无效的上下文调用。 |
| 返回值 | StatusType E_OS_CORE 给定对象属于外部核心。 |
| 返回值 | StatusType E_OS_ACCESS 调用者可以使用。 |
| 返回值 | StatusType E_OS_DISABLEDINT 调用者在中断API序列中。 |
| 同步/异步     | 同步 |
| 可重入性     | 可重入 |

## `GetCounterValue`

| 属性         | 描述                |
|--------------|---------------------|
| 函数定义      | `StatusType GetCounterValue(CounterType CounterID,  TickRefType TickValue)`        |
| 简要描述      | 读取计数器的当前计数值            |
| 详细说明      | 读取计数器的当前计数值(如果计数器由硬件驱动，则返回硬件计时器的计数值，如果由用户驱动，则返回软件计时器的计数值)    |
| 参数[输入] | `CounterType CounterID` 计数器索引值  |
| 参数[输入] | `TickRefType TickValue` 计数器的当前计数值  |
| 返回值 | StatusType E_OK 无错误 |
| 返回值 | StatusType E_OS_ID CounterID不是有效的软件计数器ID |
| 同步/异步     | 同步 |
| 可重入性     | 可重入 |
