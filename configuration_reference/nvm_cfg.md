#  NvM 配置项参考文档

| 容器属性 | 值（容器） |
|-|-|
|名称|NvM|
|描述|Configuration of the NvM (NvRam Manager) module.|
|描述|概述：NvM（Non-volatile Memory Manager），负责管理非易失性存储器的读写操作，确保数据的持久性和一致性。|
|描述|注意：在配置NvM时，需要确保正确设置存储块的大小和冗余策略，以防数据丢失；NvM配置应与ECU的硬件存储能力相匹配，避免性能瓶颈；|
|多实例个数|0 - 1|

## 1. NvMCommonVendorParams

| 容器属性 | 值（容器） |
|-|-|
|名称|NvMCommonVendorParams|
|描述|Container for a management structure to configure the composition of a given NVRAM Block Management Type. Its multiplicity describes the number of configured NVRAM blocks, one block is required to be configured. The NVRAM block descriptors are condensed in the NVRAM block descriptor table.|
|描述|概述：NvMCommonVendorParams 是一个配置容器，用于定义非易失性内存管理（NvM）模块的供应商特定参数，这些参数通常与硬件或底层存储设备的特性有关。|
|描述|注意：在配置NvMCommonVendorParams时，需要确保所选参数与底层存储硬件兼容；此外，在进行系统集成时，应当验证这些参数的设置是否对系统性能和可靠性产生了预期的影响。|
|多实例个数|1 - 1|

| 配置项属性 | 值（字符串参数配置项） |
|-|-|
|名称|NvMCfgCbkIncludeList|
|描述|This parameter describes the SectionInitializationPolicys for which a particular RTE initialization strategy applies.|
|描述|概述：NvMCfgCbkIncludeList配置项用于指定NvM模块在编译时需要包含的回调函数列表，确保在NvM操作过程中能够调用到用户定义的特定回调函数。|
|描述|注意：用户需要确保列表中的回调函数与实际实现相匹配，避免因找不到函数实现而导致编译错误；|
|说明|NvMCfgCbkIncludeList|
|多实例个数|0 - inf|

## 2. NvMBlockDescriptor

| 容器属性 | 值（容器） |
|-|-|
|名称|NvMBlockDescriptor|
|描述|Container for a management structure to configure the composition of a given NVRAM Block Management Type. Its multiplicity describes the number of configured NVRAM blocks, one block is required to be configured. The NVRAM block descriptors are condensed in the NVRAM block descriptor table.|
|描述|概述：NvMBlockDescriptor 是一个配置项，用于描述非易失性内存（NVM）模块中的一个数据块，包括其属性、管理策略和存储目标。|
|描述|注意：在配置NvMBlockDescriptor时，必须确保数据块的标识符（block_id）在整个系统中是唯一的；数据块的大小和存储结构应与实际的内存布局相匹配；对于需要冗余存储或ROM默认数据的数据块，还需配置相应的冗余策略和ROM数据属性。|
|多实例个数|1 - 65536|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|NvMBlockUseAutoValidation|
|描述|Defines whether the RAM Block shall be auto validated during shutdown phase.|
|描述|概述：NvMBlockUseAutoValidation配置项用于指定非易失性内存（NVM）块在读取操作后是否自动执行数据有效性验证，以确保数据的完整性和准确性。|
|描述|注意：此配置项对于确保数据一致性和错误处理机制至关重要；配置时需考虑系统的性能要求和错误恢复策略；不适当的使用可能导致性能下降或数据不一致问题。|
|说明|true: if auto validation mechanism is used, false: otherwise|
|多实例个数|1 - 1|
|默认值|false|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|NvMBlockUseCrc|
|描述|Defines CRC usage for the NVRAM block, i.e. memory space for CRC is reserved in RAM and NV memory.|
|描述|概述：NvMBlockUseCrc配置项用于指定是否对非易失性内存（NVM）块进行CRC（循环冗余校验）检查，以确保数据的完整性和正确性。|
|描述|注意：在启用CRC校验时，需要注意CRC计算和校验的性能开销，特别是在数据块较大时；选择合适的CRC算法以满足系统的可靠性要求；实现时需确保与底层存储介质的兼容性。|
|说明|true: CRC will be used for this NVRAM block. false: CRC will not be used for this NVRAM block.|
|多实例个数|1 - 1|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|NvMAutoBlockLength|
|描述|Defines the NvMBlocklength can be calculated by the generator automatically.|
|描述|概述：NvMAutoBlockLength配置项用于自动计算并设置非易失性内存（NVM）块的长度，简化了内存管理的配置过程。|
|描述|注意：在使用NvMAutoBlockLength时，必须确保所有相关的数据类型大小已正确定义，以便自动计算能准确进行；该特性可能不适用于所有项目，特别是那些对内存布局有特殊要求的项目；对NvMAutoBlockLength的支持可能因具体的NVM管理模块实现而异，需要参考具体供应商的实现文档。|
|说明|true: NvMBlocklength will not be considered during ECU Configuration but will be (re-)calculated by the code generator. false: NvMBlocklength will be considered during ECU Configuration.|
|多实例个数|1 - 1|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|NvMBlockUseCRCCompMechanism|
|描述|Defines whether the CRC of the RAM Block shall be compared during a write job with the CRC which was calculated during the last successful read or write job.|
|描述|概述：NvMBlockUseCRCCompMechanism配置项用于指定非易失性内存（NVM）块是否使用CRC（循环冗余校验）比较机制，以确保数据的完整性和一致性。|
|描述|注意：使用CRC机制可以提高数据可靠性，但可能会增加数据读写的时间开销；选择合适的CRC算法对性能和安全性有重要影响；在配置时需确保与系统的容错需求和性能预算相匹配。|
|说明|true: if compare mechanism is used, false: otherwise|
|多实例个数|1 - 1|
|默认值|false|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|NvMBlockUseSetRamBlockStatus|
|描述|Defines if NvMSetRamBlockStatusApi shall be used for this block or not.|
|描述|概述：NvMBlockUseSetRamBlockStatus配置项用于指定是否为非易失性内存（NVM）块启用SetRamBlockStatus API，该API允许动态更改NVM块的RAM块状态。|
|描述|注意：在使用此配置时，需要确保NVM管理器已正确配置以支持RAM块状态管理；此功能可能会增加RAM的使用量，因为每个启用了该功能的NVM块都需要额外的RAM空间来维护状态；此配置项的使用应与系统的内存管理策略和性能要求相匹配。|
|说明|Note: If NvMSetRamBlockStatusApi is disabled this configuration parameter shall be ignored. true: calling of NvMSetRamBlockStatus for this RAM block shall set the status of the RAM block. false: calling of NvMSetRamBlockStatus for this RAM block shall be ignored.|
|多实例个数|1 - 1|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|NvMBlockUseSyncMechanism|
|描述|Defines whether an explicit synchronization mechanism with a RAM mirror and callback routines for transferring data to and from NvM module's RAM mirror is used for NV block. true if synchronization mechanism is used, false otherwise.|
|描述|概述：NvMBlockUseSyncMechanism 是一个配置参数，用于指定非易失性内存（NVM）块的数据读取和写入操作是否应该同步执行，即在调用API返回之前完成。|
|描述|注意：在选择同步机制时，需要确保系统的实时性要求得以满足，因为同步操作可能会导致调用线程阻塞；此外，对于需要频繁访问的NVM块，过度使用同步机制可能会影响系统性能；此外，应当检查该配置项是否与系统设计和NVM驱动的实现相兼容。|
|多实例个数|1 - 1|
|默认值|false|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|NvMBlockWriteProt|
|描述|Defines an initial write protection of the NV block|
|描述|概述：NvMBlockWriteProt是一个配置参数，用于设置非易失性内存（NVM）块的写保护属性，以防止数据被意外或未授权地修改。|
|描述|注意：确保NvMBlockWriteProt的设置与系统安全需求相符合；写保护配置应在系统设计阶段确定，并在整个系统生命周期中保持一致；不正确的写保护设置可能导致数据完整性问题或阻止必要的数据更新。|
|说明|true: Initial block write protection is enabled. false: Initial block write protection is disabled.|
|多实例个数|1 - 1|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|NvMBswMBlockStatusInformation|
|描述|This parameter specifies whether BswM is informed about the current status of the specified block.|
|描述|概述：NvMBswMBlockStatusInformation配置项用于定义非易失性内存（NvM）块的状态信息，以便由BSW Mode Manager (BswM) 管理和监控，确保数据的一致性和完整性。|
|描述|注意：确保NvMBswMBlockStatusInformation的配置与BswM模块的要求相匹配；正确配置NvM块状态信息，以便BswM能够有效地管理这些状态；在系统设计时要考虑NvM块状态对系统行为的影响，特别是在故障恢复和数据一致性方面。|
|说明|True: Call BswM_NvM_CurrentBlockMode on changes False: Don't inform BswM at all|
|多实例个数|1 - 1|
|默认值|false|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|NvMCalcRamBlockCrc|
|描述|Defines CRC (re)calculation for the permanent RAM block or NVRAM blocks which are configured to use explicit synchronization mechanism.|
|描述|概述：NvMCalcRamBlockCrc 配置项用于指定是否在每次读取或写入非易失性内存（NVM）块之前和之后计算RAM块的CRC校验和，以确保数据的完整性。|
|描述|注意：CRC校验是数据一致性和错误检测的重要机制；配置时需考虑系统性能和数据安全性之间的平衡；CRC计算可能会增加RAM块处理的时间开销，特别是对于大型数据块。|
|说明|true: CRC will be (re)calculated for this permanent RAM block. false: CRC will not be (re)calculated for this permanent RAM block.|
|多实例个数|0 - 1|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|NvMResistantToChangedSw|
|描述|Defines whether a NVRAM block shall be treated resistant to configuration changes or not. If there is no default data available at configuration time then the application shall be responsible for providing the default initialization data. In this case the application has to use nvm_get_error_status()to be able to distinguish between first initialization and corrupted data.|
|描述|概述：NvMResistantToChangedSw 是一个配置参数，用于指示非易失性内存管理（NvM）模块的数据是否应该在软件版本更改后保持不变。|
|描述|注意：在使用此配置时，确保理解其对数据完整性和软件升级的影响；此配置项对于确保在软件更新后数据的一致性和可靠性至关重要；此配置项应当谨慎处理，以避免数据丢失或不一致。|
|说明|true: NVRAM block is resistant to changed software. false: NVRAM block is not resistant to changed software.|
|多实例个数|1 - 1|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|NvMSelectBlockForFirstInitAll|
|描述|Defines whether a block will be processed or not by NvM_FirstInitAll. A block can be configured to be processed even if it doesn't have permanent RAM and/or explicit synchronization.|
|描述|概述：NvMSelectBlockForFirstInitAll 配置项用于指定在执行 NvM_InitAll 函数时，哪些非易失性内存（NVM）块应该被选中进行首次初始化。|
|描述|注意：在配置时需确保只有那些需要在首次启动时初始化的NVM块被选中；不应该选择那些包含默认数据或不需要初始化的块；此配置项的使用应符合项目的内存初始化策略和要求。|
|说明|TRUE: block will be processed by NvM_FirstInitAll FALSE: block will not be processed by NvM_FirstInitAll|
|多实例个数|0 - 1|
|默认值|false|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|NvMSelectBlockForReadAll|
|描述|Defines whether a NVRAM block shall be processed during nvm_read_all or not. This configuration parameter has only influence on those NVRAM blocks which are configured to have a permanent RAM block or which are configured to use explicit synchronization mechanism.|
|描述|概述：NvMSelectBlockForReadAll配置项用于在NVM（非易失性内存管理）模块中选择特定的数据块进行全读操作，这使得在系统启动或特定条件下可以批量读取配置或状态数据。|
|描述|注意：在配置时需确保所选数据块已在NVM中定义且适用于ReadAll操作；ReadAll操作可能会影响系统启动时间，因此应谨慎选择必要的数据块；该配置项应与NvMBlockDescriptor配置项一致，以确保数据块的正确识别和访问。|
|说明|true: NVRAM block shall be processed by nvm_read_all false: NVRAM block shall not be processed by nvm_read_all|
|多实例个数|0 - 1|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|NvMSelectBlockForWriteAll|
|描述|Defines whether a NVRAM block shall be processed during nvm_write_all or not. This configuration parameter has only influence on those NVRAM blocks which are configured to have a permanent RAM block or which are configured to use explicit synchronization mechanism.|
|描述|概述：NvMSelectBlockForWriteAll 配置项用于指定在执行 nvm_write_all 操作时，哪些非易失性内存（NVM）块应被选中以进行写入操作。|
|描述|注意：在配置时需确保只有需要在 WriteAll 操作中被写入的 NVM 块被选中；不应选择那些仅在单独请求时才需要写入的块；此配置项对系统的备份策略和恢复机制有重要影响，因此需要谨慎配置以避免不必要的数据损失或性能问题。|
|说明|true: NVRAM block shall be processed by nvm_write_all false: NVRAM block shall not be processed by nvm_write_all|
|多实例个数|0 - 1|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|NvMStaticBlockIDCheck|
|描述|Defines if the Static Block ID check is enabled.|
|描述|概述：NvMStaticBlockIDCheck是一个配置参数，用于在非易失性内存管理（NvM）模块中启用或禁用静态块ID检查，以确保数据块的一致性和正确性。|
|描述|注意：必须确保NvM配置的BlockID与系统中定义的BlockID一致，以防止数据损坏；如果启用了静态BlockID检查，系统将在运行时验证BlockID，这可能会增加额外的开销；在生产环境中，通常建议启用此功能以提高系统的健壮性。|
|说明|false: Static Block ID check is disabled. true: Static Block ID check is enabled.|
|多实例个数|1 - 1|
|默认值|false|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|NvMWriteBlockOnce|
|描述|Defines write protection after first write. The NVRAM manager sets the write protection bit either after the NV block was written the first time or if the block was already written and it is detected as valid and consistent during a read for it. [NVM276].|
|描述|概述：NvMWriteBlockOnce 是一个配置项，用于指定非易失性内存（NVM）中的数据块是否应该只被写入一次，通常用于确保数据的一致性和防止重复写入。|
|描述|注意：在使用NvMWriteBlockOnce时，确保数据块的重要性和一次性写入需求明确；此配置项可能与数据块的重写策略冲突，需谨慎配置；应检查与其他NvM管理策略的兼容性。|
|说明|true: Defines write protection after first write is enabled. false: Defines write protection after first write is disabled.|
|多实例个数|1 - 1|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|NvMWriteVerification|
|描述|Defines if Write Verification is enabled.|
|描述|概述：NvMWriteVerification 是一个配置参数，用于指定非易失性内存管理（NvM）模块在写入数据到非易失性存储器后是否执行验证步骤，以确保数据的正确性。|
|描述|注意：必须确保NvMWriteVerification配置与系统的可靠性和性能要求相匹配；开启写入验证会增加数据持久化的时间，可能影响系统性能；关闭写入验证可能降低数据一致性保证，但可以提高系统的响应速度。|
|说明|false: Write verification is disabled. true: Write Verification is enabled.|
|多实例个数|1 - 1|
|默认值|false|

| 配置项属性 | 值（枚举参数配置项） |
|-|-|
|名称|NvMBlockCrcType|
|描述|Defines CRC data width for the NVRAM block. Default: NVM_CRC16, i.e. CRC16 will be used if NVM_BLOCK_USE_CRC==true|
|描述|概述：NvMBlockCrcType 是一个配置参数，用于指定非易失性内存（NVM）块的CRC（循环冗余校验）类型，以确保数据的完整性和一致性。|
|描述|注意：在选择CRC类型时，需要考虑系统对数据完整性的要求和性能的平衡；不同的CRC类型可能会对系统性能和校验效率产生不同的影响；应确保所选的CRC类型与标准支持的类型一致。|
|多实例个数|0 - 1|

| 配置项属性 | 值（枚举参数配置项） |
|-|-|
|名称|NvMBlockManagementType|
|描述|Defines the block management type for the NVRAM block.[NVM137]|
|描述|概述：NvMBlockManagementType 定义了非易失性内存（NVM）块的管理类型，指示块是由NvM模块管理还是由应用程序管理。|
|描述|注意：确保正确配置管理类型以符合系统的数据保护和错误处理需求；不正确的配置可能导致数据丢失或系统行为不稳定；管理类型的选择应基于系统的存储和访问需求。|
|多实例个数|1 - 1|

| 配置项属性 | 值（函数名配置项） |
|-|-|
|名称|NvMInitBlockCallback|
|描述|Entry address of a block specific callback routine which shall be called if no ROM data is available for initialization of the NVRAM block.|
|描述|概述：NvMInitBlockCallback 是一个配置项，用于定义在非易失性内存管理（NvM）模块初始化特定块时调用的回调函数。|
|描述|注意：回调函数应当仅用于初始化过程中的特定任务，不应包含复杂的逻辑或长时间执行的代码；在配置时应确保回调函数的正确性和有效性，避免系统启动时的错误。|
|说明|If not configured, no specific callback routine shall be called for initialization of the NVRAM block with default data.|
|多实例个数|0 - 1|

| 配置项属性 | 值（函数名配置项） |
|-|-|
|名称|NvMReadRamBlockFromNvCallback|
|描述|Entry address of a block specific callback routine which shall be called in order to let the application copy data from the NvM module's mirror to RAM block.|
|描述|概述：NvMReadRamBlockFromNvCallback是一个回调函数配置项，用于在非易失性内存管理模块（NvM）从非易失性存储器（NVM）读取数据到RAM后执行的用户定义函数。|
|描述|注意：用户需确保回调函数的执行时间尽可能短，避免影响系统性能；回调函数中不应调用可能导致阻塞的操作；此配置项应正确配置，以确保数据一致性和系统稳定性。|
|说明|Implementation type: Std_ReturnType E_OK: copy was successful E_NOT_OK: copy was not successful, callback routine to be called again|
|多实例个数|0 - 1|

| 配置项属性 | 值（函数名配置项） |
|-|-|
|名称|NvMSingleBlockCallback|
|描述|Entry address of the block specific callback routine which shall be invoked on termination of each asynchronous single block request [NVM113].|
|描述|概述：NvMSingleBlockCallback配置项用于定义一个回调函数，该函数在非易失性内存（NVM）管理模块完成单个块的读取、写入或擦除操作后被调用。|
|描述|注意：回调函数需要用户根据实际需求实现，确保其执行时间短且不影响系统性能；在配置时需确保回调函数的命名与实现符合项目规范；对回调函数的具体实现和使用场景有明确的指导，需要遵循相关规范以保证兼容性和可靠性。|
|多实例个数|0 - 1|

| 配置项属性 | 值（函数名配置项） |
|-|-|
|名称|NvMWriteRamBlockToNvCallback|
|描述|Entry address of a block specific callback routine which shall be called in order to let the application copy data from RAM block to NvM module's mirror.|
|描述|概述：NvMWriteRamBlockToNvCallback配置项用于指定在非易失性内存管理（NvM）模块将RAM块写入非易失性存储器之前调用的回调函数，以便执行必要的操作，如数据处理或校验。|
|描述|注意：确保回调函数的执行时间不会违反实时性要求；在配置回调时，应确保数据的一致性和完整性。|
|说明|Implementation type: Std_ReturnType E_OK: copy was successful E_NOT_OK: copy was not successful, callback routine to be called again|
|多实例个数|0 - 1|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|NvMBlockJobPriority|
|描述|Defines the job priority for a NVRAM block (0 = Immediate priority).|
|描述|概述：NvMBlockJobPriority配置项用于定义非易失性内存（NVM）块的作业优先级，确保在NVM管理器中处理存储和恢复操作时，能够根据优先级顺序执行。|
|描述|注意：优先级设置应考虑系统的实时性和数据重要性，避免低优先级作业长时间阻塞；在配置时需确保不同NVM块间的优先级分配合理，以防止优先级倒置问题；|
|多实例个数|1 - 1|
|取值范围|0 - 255|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|NvMMaxNumOfReadRetries|
|描述|Defines the maximum number of read retries.|
|描述|概述：NvMMaxNumOfReadRetries 配置项用于指定非易失性内存管理（NvM）模块在读取操作失败后可以重试的最大次数，以提高数据读取的可靠性。|
|描述|注意：该值应根据存储介质的可靠性和系统的容错需求来设置；设置过高可能会导致系统响应时间延迟；确保该配置项的值与系统定义的错误处理策略相匹配。|
|多实例个数|1 - 1|
|默认值|0|
|取值范围|0 - 7|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|NvMMaxNumOfWriteRetries|
|描述|Defines the maximum number of write retries for a NVRAM block with [ECUC_NvM_00061]. Regardless of configuration a consistency check (and maybe write retries) are always forced for each block which is processed by the request nvm_write_all and nvm_write_block.|
|描述|概述：NvMMaxNumOfWriteRetries 配置项用于指定非易失性内存管理（NvM）模块在写入操作失败后可以重试的最大次数，以提高数据存储的可靠性。|
|描述|注意：该值应根据存储介质的可靠性和系统的容错需求来设置；设置过高可能会导致系统响应时间变长；确保该配置项的值符合实际的内存硬件特性和系统需求。|
|多实例个数|1 - 1|
|取值范围|0 - 7|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|NvMNvBlockBaseNumber|
|描述|Configuration parameter to perform the link between the NVM_NVRAM_BLOCK_IDENTIFIER used by the SW-Cs and the FEE_BLOCK_NUMBER expected by the memory abstraction modules. The parameter value equals the FEE_BLOCK_NUMBER or EA_BLOCK_NUMBER shifted to the right by NvMDatasetSelectionBits bits. (ref. to chapter 7.1.2.1).|
|描述|概述：NvMNvBlockBaseNumber 用于定义非易失性内存块（NvM Block）的基础编号，这是一个全局唯一的标识符，用于区分存储在非易失性内存中的不同数据块。|
|描述|注意：确保每个NvM Block的NvMNvBlockBaseNumber是唯一的，以避免数据覆盖或错误访问；在系统设计阶段需要仔细规划这些编号，以保持系统的可扩展性和维护性；|
|说明|Calculation Formula: value = TargetBlockReference.[Ea/Fee]BlockConfiguration.[Ea/Fee]BlockNumber >> NvMDatasetSelectionBits|
|多实例个数|1 - 1|
|取值范围|1 - 65534|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|NvMNvBlockLength|
|描述|Defines the NV block data length in bytes.|
|描述|概述：NvMNvBlockLength 定义了非易失性内存块（NvM Block）的长度，用于存储特定数据。|
|描述|注意：确保NvMNvBlockLength与实际存储需求相匹配，避免数据溢出；长度应根据数据结构和存储需求进行精确配置；对于NvMNvBlockLength的配置应符合模块的内存管理策略。|
|说明|Note: The implementer can add the attribute 'withAuto' to the parameter definition which indicates that the length can be calculated by the generator automatically (e.g. by using the sizeof operator). When 'withAuto' is set to 'true' for this parameter definition the 'isAutoValue' can be set to 'true'. If 'isAutoValue' is set to 'true' the actual value will not be considered during ECU Configuration but will be (re-)calculated by the code generator and stored in the value attribute afterwards.|
|多实例个数|1 - 1|
|取值范围|1 - 65535|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|NvMNvBlockNum|
|描述|Defines the number of multiple NV blocks in a contiguous area according to the given block management type.|
|描述|概述：NvMNvBlockNum配置项用于定义非易失性内存（NVM）管理模块中的块数量，这是一个关键参数，用于指导NVM管理模块如何组织和管理内存块。|
|描述|注意：NvMNvBlockNum的值必须准确反映项目中使用的NVM块的总数；配置值过大或过小都会影响系统性能和内存使用效率；确保该配置项与实际NVM布局和需求相匹配。|
|说明|1-255 For NVRAM blocks to be configured of block management type NVM_BLOCK_DATASET. The actual range is limited according to SWS_NvM_00444. 1 For NVRAM blocks to be configured of block management type NVM_BLOCK_NATIVE 2 For NVRAM blocks to be configured of block management type NVM_BLOCK_REDUNDANT|
|多实例个数|1 - 1|
|取值范围|1 - 255|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|NvMNvramBlockIdentifier|
|描述|Identification of a NVRAM block via a unique block identifier.|
|描述|概述：NvMNvramBlockIdentifier用于唯一标识非易失性内存（NVRAM）管理模块中的一个NVRAM块，确保每个NVRAM块可以被准确识别和访问。|
|描述|注意：NvMNvramBlockIdentifier的值必须在整个系统中唯一，避免标识符冲突；在配置时应确保与系统中其他模块的标识符不重复；该标识符的配置和使用应遵循NVRAM管理模块的规范要求。|
|说明|Implementation Type: nvm_block_id_t. min = 2 max = 2^(16- NVM_DATASET_SELECTION_BITS)-1 Reserved NVRAM block IDs: 0 -> to derive multi block request results via nvm_get_error_status 1 -> redundant NVRAM block which holds the configuration ID (generation tool should check that this block is correctly configured from type,CRC and size point of view)|
|多实例个数|1 - 1|
|取值范围|1 - 65535|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|NvMNvramDeviceId|
|描述|Defines the NVRAM device ID where the NVRAM block is located.|
|描述|概述：NvMNvramDeviceId 是用于标识非易失性内存（NVRAM）管理模块中特定设备的唯一标识符，用于区分不同的存储设备。|
|描述|注意：在配置NvMNvramDeviceId时，必须确保每个NVRAM设备有一个唯一的标识符；该标识符通常由系统设计者分配，并在整个系统中保持一致；应检查该标识符是否符合规定的数据类型和取值范围。|
|说明|Calculation Formula: value = TargetBlockReference.[Ea/Fee]BlockConfiguration.[Ea/Fee]DeviceIndex|
|多实例个数|1 - 1|
|取值范围|0 - 1|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|NvMRomBlockNum|
|描述|Defines the number of multiple ROM blocks in a contiguous area according to the given block management type.|
|描述|概述：NvMRomBlockNum是一个配置项，用于指定非易失性内存（NVM）中只读存储器（ROM）块的数量，这些块通常用于存储默认或固定的数据。|
|描述|注意：在配置NvMRomBlockNum时，需要确保指定的块数量与实际在系统中实现的ROM块数量相匹配；超出实际数量的配置可能导致系统资源浪费或配置错误；|
|说明|0-254 For NVRAM blocks to be configured of block management type NVM_BLOCK_DATASET. The actual range is limited according to SWS_NvM_00444. 0-1 For NVRAM blocks to be configured of block management type NVM_BLOCK_NATIVE 0-1 For NVRAM blocks to be configured of block management type NVM_BLOCK_REDUNDANT|
|多实例个数|1 - 1|
|默认值|0|
|取值范围|0 - 254|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|NvMWriteVerificationDataSize|
|描述|Defines the number of bytes to compare in each step when comparing the content of a RAM Block and a block read back.|
|描述|概述：NvMWriteVerificationDataSize配置项指定了非易失性内存管理（NvM）模块在写操作后用于验证数据完整性的数据大小。|
|描述|注意：必须确保配置的数据大小不超过实际NvM块的大小；此外，考虑到性能和可靠性的平衡，应当根据存储介质的特性和系统的可靠性要求慎重选择验证数据的大小；如果配置的数据大小为零，则表示不执行写后验证。|
|多实例个数|1 - 1|
|取值范围|1 - 65535|

| 配置项属性 | 值（字符串参数配置项） |
|-|-|
|名称|NvMBlockHeaderInclude|
|描述|Defines the header file where the owner of the NVRAM block has the declarations of the permanent RAM data block, ROM data block (if configured) and the callback function prototype for each configured callback. If no permanent RAM block, ROM block or callback functions are configured then this configuration parameter shall be ignored.|
|描述|概述：NvMBlockHeaderInclude配置项用于指定是否为非易失性内存(NvM)块包含一个额外的头部信息，这有助于管理和识别存储的数据块。|
|描述|注意：确保当需要对NvM块进行版本控制或状态管理时启用此选项；过多使用头部信息可能会增加存储开销；正确配置头部信息以避免数据一致性问题。|
|多实例个数|0 - 1|

| 配置项属性 | 值（字符串参数配置项） |
|-|-|
|名称|NvMRamBlockDataAddress|
|描述|Defines the start address of the RAM block data.|
|描述|概述：NvMRamBlockDataAddress 用于定义非易失性内存块在RAM中的起始地址，这是数据在运行时被存储和访问的位置。|
|描述|注意：确保地址与其他内存管理配置不冲突；地址应符合硬件的内存寻址规范；在多任务或多核环境中，注意数据的同步和一致性问题。|
|说明|If this is not configured, no permanent RAM data block is available for the selected block management type.|
|多实例个数|0 - 1|

| 配置项属性 | 值（字符串参数配置项） |
|-|-|
|名称|NvMRomBlockDataAddress|
|描述|Defines the start address of the ROM block data.|
|描述|概述：NvMRomBlockDataAddress配置项用于指定非易失性内存（NVM）块的ROM区域地址，这是存储默认数据或固定数据的物理地址。|
|描述|注意：确保地址与实际的硬件内存映射一致，避免地址冲突；在配置时需考虑内存对齐要求；该地址应指向只读内存区域，以防止运行时数据被意外修改。|
|说明|If not configured, no ROM block is available for the selected block management type.|
|多实例个数|0 - 1|

### 2.1. NvMTargetBlockReference

| 容器属性 | 值（容器） |
|-|-|
|名称|NvMTargetBlockReference|
|描述|This parameter is just a container for the parameters for EA and FEE|
|描述|概述：NvMTargetBlockReference配置项用于指定非易失性内存管理（NvM）模块中目标块的引用，它确保了数据块在内存中的正确定位和管理。|
|描述|注意：在配置NvMTargetBlockReference时，必须确保引用的目标块已在系统中定义且配置正确；该配置项对于实现数据的持久存储至关重要，错误的配置可能导致数据丢失或损坏；|
|多实例个数|0 - 1|

#### 2.1.1. NvMEaRef

| 容器属性 | 值（容器） |
|-|-|
|名称|NvMEaRef|
|描述|EEPROM Abstraction|
|描述|概述：NvMEaRef 是一个配置参数，用于指定非易失性内存块（NvM Block）与底层的Eeprom Abstraction层的关联，确保数据正确存储到EEPROM或其他非易失性存储介质中。|
|描述|注意：在配置NvMEaRef时，必须确保引用的Eeprom Abstraction层的标识符与NvM Block兼容；如果系统中存在多个非易失性存储设备，需要正确映射以避免数据存储错误；|
|多实例个数|0 - 1|

| 配置项属性 | 值（关联引用配置项） |
|-|-|
|名称|NvMNameOfEaBlock|
|描述|reference to EaBlock|
|描述|概述：NvMNameOfEaBlock 配置项用于定义非易失性内存管理（NvM）模块中，每个Eeprom Abstraction（Ea）块的名称。|
|描述|注意：确保每个Ea块的名称在整个项目中是唯一的，以避免数据存储时的冲突；名称应符合项目的命名规范；对Ea块的命名没有特定的长度限制，但应保持合理以便于管理和维护。|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Ea/EaBlockConfiguration|

#### 2.1.2. NvMFeeRef

| 容器属性 | 值（容器） |
|-|-|
|名称|NvMFeeRef|
|描述|Flash EEPROM Emulation|
|描述|概述：NvMFeeRef 是一个配置参数，用于引用非易失性内存管理模块中的 FEE（Flash EEPROM Emulation）块，确保数据的持久存储。|
|描述|注意：确保引用的FEE块在系统中是唯一的，并且已经正确配置；在配置NvMFeeRef时，需要考虑数据的读写频率和存储容量需求；|
|多实例个数|0 - 1|

| 配置项属性 | 值（关联引用配置项） |
|-|-|
|名称|NvMNameOfFeeBlock|
|描述|reference to FeeBlock|
|描述|概述：NvMNameOfFeeBlock是一个配置参数，用于指定非易失性内存管理（NvM）模块中特定块的Flash EEPROM Emulation (FEE) 模块的块名称。|
|描述|注意：在配置时，必须确保NvMNameOfFeeBlock的值与FEE模块中定义的块名称完全匹配；该名称通常由系统生成，手动修改可能会导致数据不一致；在配置多个NvM块时，每个块的NvMNameOfFeeBlock应该是唯一的，以避免名称冲突。|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Fee/FeeBlockConfiguration|

## 3. NvMCommon

| 容器属性 | 值（容器） |
|-|-|
|名称|NvMCommon|
|描述|Container for common configuration options.|
|描述|概述：NvMCommon配置项是用于定义非易失性内存管理模块（NvM）的通用属性，如NvM模块的版本信息、多块管理策略以及客户端服务器通信机制等。|
|描述|注意：在配置多块管理策略时，考虑数据一致性和访问效率；客户端服务器通信配置需满足系统的实时性和可靠性要求。|
|多实例个数|1 - 1|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|NvMBswMMultiBlockJobStatusInformation|
|描述|This parameter specifies whether BswM is informed about the current status of the multiblock job.|
|描述|概述：NvMBswMMultiBlockJobStatusInformation配置项用于定义非易失性内存管理（NvM）模块中多块作业的状态信息，这有助于监控和控制多个块的读写作业的执行状态。|
|描述|注意：需要确保该配置项正确反映了所有相关NvM块的作业状态；此配置项通常与NvM的作业管理和错误检测机制紧密相关；在配置时，应注意与NvM块配置的一致性和数据类型的正确性，以确保系统的健壮性。|
|说明|True: call BswM_NvM_CurrentJobMode if ReadAll and WriteAll are started, finished, canceled False: do not inform BswM at all|
|多实例个数|1 - 1|
|默认值|true|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|NvMDevErrorDetect|
|描述|Switches the development error detection and notification on or off.|
|描述|概述：NvMDevErrorDetect 是一个配置参数，用于启用或禁用非易失性内存管理（NvM）模块的开发错误检测和报告机制。|
|描述|注意：在生产代码中通常禁用此功能以节省资源，但在开发和测试阶段应启用以便于故障诊断；确保与系统的诊断策略一致；此配置应与其他模块的错误检测配置保持一致性。|
|说明|* true: detection and notification is enabled. * false: detection and notification is disabled.|
|多实例个数|1 - 1|
|默认值|false|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|NvMDrvModeSwitch|
|描述|Preprocessor switch to enable switching memory drivers to fast mode during performing nvm_read_all and nvm_write_all|
|描述|概述：NvMDrvModeSwitch 配置项用于控制非易失性内存（NVM）驱动的模式切换，允许系统在不同的操作模式间切换，以适应不同的数据存储和管理需求。|
|描述|注意：确保NvMDrvModeSwitch配置与系统定义的模式管理策略一致；正确配置模式切换以避免数据一致性问题；在多模式系统中，注意模式切换对系统性能的影响。|
|说明|true: Fast mode enabled. false: Fast mode disabled.|
|多实例个数|1 - 1|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|NvMDynamicConfiguration|
|描述|Preprocessor switch to enable the dynamic configuration management handling by the nvm_read_all request.|
|描述|概述：NvMDynamicConfiguration 是用于描述非易失性内存（NvM）模块中动态配置参数的配置项，它允许在运行时更改NvM的某些行为和属性，如块管理类型、块大小等。|
|描述|注意：动态配置通常受限，因为大多数NvM参数在编译时就已确定；如果实现了动态配置，必须确保运行时的更改不会违反系统的安全和一致性要求；此外，动态配置可能需要额外的RAM资源和处理时间，因此在资源受限的系统中使用时应谨慎。|
|说明|true: Dynamic configuration management handling enabled. false: Dynamic configuration management handling disabled. This parameter affects all NvM processing related to Block with ID 1 and all processing related to Resistant to Changed Software. If the Dynamic Configuration is disabled, Block 1 cannot be used by NvM.|
|多实例个数|1 - 1|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|NvMJobPrioritization|
|描述|Preprocessor switch to enable job prioritization handling|
|描述|概述：NvMJobPrioritization配置项用于定义非易失性内存管理（NvM）作业的优先级，确保在资源竞争时，高优先级的作业可以优先执行。|
|描述|注意：在配置NvMJobPrioritization时，需要确保优先级设置反映了系统的实际需求和约束；不恰当的优先级分配可能导致低优先级作业饥饿；作业优先级的具体实现方式可能受到底层存储设备特性的影响。|
|说明|true: Job prioritization handling enabled. false: Job prioritization handling disabled.|
|多实例个数|1 - 1|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|NvMPollingMode|
|描述|Preprocessor switch to enable/disable the polling mode in the NVRAM Manager and at the same time disable/enable the callback functions useable by lower layers|
|描述|概述：NvMPollingMode配置项用于定义非易失性内存管理（NvM）模块中数据读写操作的完成检测方式，即是通过轮询（Polling）还是中断（Interrupt）来确认操作是否完成。|
|描述|注意：选择轮询模式可能会影响系统的实时性，因为CPU需要定期检查操作状态；轮询模式在处理大量或耗时的I/O操作时可能不如中断模式高效；选择合适的模式需考虑系统的实时性要求和资源消耗。|
|说明|true: Polling mode enabled, callback function usage disabled. false: Polling mode disabled, callback function usage enabled.|
|多实例个数|1 - 1|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|NvMSetRamBlockStatusApi|
|描述|Preprocessor switch to enable the API nvm_set_ram_block_status.|
|描述|概述：NvMSetRamBlockStatusApi是一个配置项，用于启用或禁用NvM模块中的API，该API允许应用程序改变RAM块的状态，例如将其标记为已改变或未改变。|
|描述|注意：确保在使用此API之前已经正确配置了NvM模块；此API的使用可能会影响NvM的性能，特别是在频繁更新数据时；使用此API需要确保对数据一致性和完整性的管理。|
|说明|true: API nvm_set_ram_block_status enabled. false: API nvm_set_ram_block_status disabled.|
|多实例个数|1 - 1|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|NvMVersionInfoApi|
|描述|Pre-processor switch to enable / disable the API to read out the modules version information [NVM285], [NVM286].|
|描述|概述：NvMVersionInfoApi 是一个配置参数，用于启用或禁用非易失性内存管理（NvM）模块的版本信息API，允许用户获取模块的版本信息。|
|描述|注意：如果启用了该配置项，必须确保NvM模块提供了一个函数来返回其版本信息；如果禁用，则不应该包含相关的版本信息API函数；此外，需要注意版本信息API的使用可能会增加代码的大小和复杂性。|
|说明|true: Version info API enabled. false: Version info API disabled.|
|多实例个数|1 - 1|
|默认值|false|

| 配置项属性 | 值（枚举参数配置项） |
|-|-|
|名称|NvMApiConfigClass|
|描述|Preprocessor switch to enable some API calls which are related to NVM API configuration classes.|
|描述|概述：NvMApiConfigClass 配置项用于指定NVRAM管理器（NvM）模块的API配置类别，它决定了NvM模块提供的API集合，以及这些API的功能和性能特性。|
|描述|注意：在选择NvMApiConfigClass时，需要根据系统需求和内存限制来确定合适的配置类别；不同的配置类别可能会影响系统的内存占用和API的执行时间；应确保所选配置类别与标准定义的API集合一致。|
|多实例个数|1 - 1|

| 配置项属性 | 值（浮点型参数配置项） |
|-|-|
|名称|NvMMainFunctionPeriod|
|描述|The period between successive calls to the main function in seconds.|
|描述|概述：NvMMainFunctionPeriod 配置项定义了非易失性内存管理模块（NvM）主函数的调用周期，即NvM_MainFunction的调度频率。|
|描述|注意：该值应与系统定时器和任务调度策略相匹配，以确保数据的及时处理和存储；过高的调用频率可能导致系统资源过度占用，而过低的频率可能导致数据存储延迟；在配置时需考虑到ECU的性能和内存操作的实时性要求。|
|多实例个数|1 - 1|
|取值范围|0 - Inf|

| 配置项属性 | 值（函数名配置项） |
|-|-|
|名称|NvMMultiBlockCallback|
|描述|Entry address of the common callback routine which shall be invoked on termination of each asynchronous multi block request|
|描述|概述：NvMMultiBlockCallback配置项用于定义在非易失性内存（NvM）模块中，当多个块的读写操作完成后触发的回调函数，以便进行后续处理或状态更新。|
|描述|注意：该回调函数应仅用于通知目的，避免在其中执行耗时或复杂的操作；确保回调函数的执行时间短，以不影响系统性能；在配置时需确保回调函数与NvM模块兼容|
|多实例个数|0 - 1|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|NvMCompiledConfigId|
|描述|Configuration ID regarding the NV memory layout. This configuration ID shall be published as e.g. a SW-C shall have the possibility to write it to NV memory.|
|描述|概述：NvMCompiledConfigId 是用于标识非易失性内存管理（NvM）模块配置的编译时配置ID，确保配置的一致性和正确性。|
|描述|注意：该ID应与生产环境中使用的配置ID匹配，以避免数据不一致问题；在软件升级或配置更改时需谨慎处理，确保新旧配置间的兼容性；确保该配置项的正确设置和使用，以符合标准要求。|
|多实例个数|1 - 1|
|取值范围|0 - 65535|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|NvMCrcNumOfBytes|
|描述|If CRC is configured for at least one NVRAM block, this parameter defines the maximum number of bytes which shall be processed within one cycle of job processing.|
|描述|概述：NvMCrcNumOfBytes 配置项用于指定非易失性内存（NVM）模块中用于计算循环冗余校验（CRC）的数据字节数。|
|描述|注意：必须确保此配置项与实际存储的数据块大小相匹配；CRC字节数的配置应考虑到数据完整性和性能之间的平衡；在配置时应遵循项目或组织的数据保护策略。|
|多实例个数|1 - 1|
|取值范围|1 - 65535|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|NvMDatasetSelectionBits|
|描述|Defines the number of least significant bits which shall be used to address a certain dataset of a NVRAM block within the interface to the memory hardware abstraction.|
|描述|概述：NvMDatasetSelectionBits 配置项用于定义非易失性内存（NvM）中数据集的选择位数，这些位数决定了可以区分的数据集的数量，从而支持多版本数据存储。|
|描述|注意：在配置NvMDatasetSelectionBits时，需要确保所选位数足以覆盖所有需要的数据集版本；此配置项的值会影响NvM模块的RAM和ROM占用，因为它决定了数据集索引的大小；应检查该配置项是否与NvM模块的其他配置参数兼容，以确保数据集管理的正确性。|
|说明|0..8: Number of bits which are used for dataset or redundant block addressing. 0: No dataset or redundant NVRAM blocks are configured at all, no selection bits required. 1: In case of redundant NVRAM blocks are configured, but no dataset NVRAM blocks.|
|多实例个数|1 - 1|
|取值范围|0 - 8|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|NvMRepeatMirrorOperations|
|描述|Defines the number of retries to let the application copy data to or from the NvM module's mirror before postponing the current job.|
|描述|概述：NvMRepeatMirrorOperations配置项用于定义是否在镜像块操作失败后重复尝试操作，以提高数据存储的可靠性。|
|描述|注意：在使用此配置时，需要考虑系统的容错需求和重试操作可能带来的额外时间开销；重试机制应与系统的诊断策略和恢复策略相协调；具体实现可能依赖于供应商的NvM模块实现。|
|多实例个数|1 - 1|
|默认值|0|
|取值范围|0 - 7|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|NvMSizeImmediateJobQueue|
|描述|Defines the number of queue entries for the immediate priority job queue. If NVM_JOB_PRIORITIZATION is switched OFF this parameter shall be out of scope.|
|描述|概述：NvMSizeImmediateJobQueue 定义了非易失性内存管理模块（NvM）中立即作业队列的大小，这个队列用于存储需要立即处理的内存作业请求。|
|描述|注意：队列大小应根据系统的存储需求和作业处理能力合理配置；过小的队列可能导致作业丢失或系统响应延迟；在配置时需考虑系统的最大并发作业数以确保效率和稳定性。|
|多实例个数|0 - 1|
|取值范围|1 - 65535|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|NvMSizeStandardJobQueue|
|描述|Defines the number of queue entries for the standard job queue.|
|描述|概述：NvMSizeStandardJobQueue 配置项用于定义非易失性内存管理（NvM）模块中标准作业队列的大小，这个队列负责存储等待处理的NvM作业请求。|
|描述|注意：在配置NvMSizeStandardJobQueue时，需要确保队列大小能够满足系统的作业处理需求，避免队列溢出；此外，队列大小的配置应当考虑到内存消耗与性能之间的平衡；如果配置的队列大小超出了ECU的内存限制或不符合模块的设计约束，可能会导致编译或运行时错误。|
|多实例个数|1 - 1|
|取值范围|1 - 65535|

## 4. NvmDemEventParameterRefs

| 容器属性 | 值（容器） |
|-|-|
|名称|NvmDemEventParameterRefs|
|描述|Container for the references to DemEventParameter elements which shall be invoked using the API Dem_SetEventStatus in case the corresponding error occurs. The EventId is taken from the referenced DemEventParameter's DemEventId symbolic value. The standardized errors are provided in this container and can be extended by vendor-specific error references.|
|描述|概述：NvmDemEventParameterRefs配置项用于将非易失性存储器(NVM)管理的配置参数与诊断事件管理器(DEM)中定义的事件参数关联起来，以便在发生特定诊断事件时触发NVM操作。|
|描述|注意：确保引用的DEM事件参数在DEM配置中已定义且有效；此配置项对于实现基于事件的NVM数据存储和恢复机制至关重要；对NvmDemEventParameterRefs的使用应遵循模块间通信和数据一致性的要求。|
|多实例个数|0 - 1|

| 配置项属性 | 值（关联引用配置项） |
|-|-|
|名称|NVM_E_HARDWARE|
|描述|Reference to the DemEventParameter which shall be issued when the hardware error has occured.|
|描述|概述：NVM_E_HARDWARE 是一个错误状态码，用于表示非易失性存储器（NVM）管理器在尝试访问底层硬件时遇到了硬件错误。|
|描述|注意：当底层存储硬件（如EEPROM或Flash）发生物理故障时，应报告此错误；该错误码通常与诊断事件、DEM（Diagnostic Event Manager）集成或错误处理策略相关联；在实现时，应确保硬件抽象层（HAL）能够正确识别并向NVM管理器报告硬件故障。|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Dem/DemConfigSet/DemEventParameter|

| 配置项属性 | 值（关联引用配置项） |
|-|-|
|名称|NVM_E_INTEGRITY_FAILED|
|描述|Reference to the DemEventParameter which shall be issued when the error "API request integrity failed" has occurred.|
|描述|概述：NVM_E_INTEGRITY_FAILED 是一个错误状态码，用于指示非易失性存储（NVM）管理器在校验数据完整性时检测到数据损坏或不一致。|
|描述|注意：在使用NVM管理器时，应确保数据的校验机制正确实现，以便能够检测到潜在的数据完整性问题；如果返回此错误码，需要有相应的错误处理策略来恢复或重新初始化受影响的数据；确保错误处理逻辑与系统的容错需求一致。|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Dem/DemConfigSet/DemEventParameter|

| 配置项属性 | 值（关联引用配置项） |
|-|-|
|名称|NVM_E_LOSS_OF_REDUNDANCY|
|描述|Reference to the DemEventParameter which shall be issued when the error "loss of redundancy" has occurred.|
|描述|概述：NVM_E_LOSS_OF_REDUNDANCY 是一个错误状态，用于指示非易失性内存（NVM）管理器在尝试访问冗余存储区域时检测到数据丢失或损坏，表明冗余机制未能提供预期的数据保护。|
|描述|注意：在使用NVM模块时，应确保冗余存储策略正确实施，以便在主存储区域损坏时提供备份；此错误状态通常需要开发者在软件中实现错误处理逻辑，以便在检测到冗余丢失时采取适当的恢复措施；应当遵循NVM模块的规范来配置和管理冗余存储，以确保系统的健壮性。|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Dem/DemConfigSet/DemEventParameter|

| 配置项属性 | 值（关联引用配置项） |
|-|-|
|名称|NVM_E_REQ_FAILED|
|描述|Reference to the DemEventParameter which shall be issued when the error "API request failed" has occurred.|
|描述|概述：NVM_E_REQ_FAILED 是一个错误状态宏，用于表示非易失性存储（NVM）管理器在尝试执行读取、写入或擦除操作时请求失败。|
|描述|注意：在使用该宏时，应确保错误处理逻辑能够妥善处理请求失败的情况；此宏通常与诊断事件管理器（DEM）集成，以报告和记录错误状态；应检查NVM块的重试策略和数据保护机制，以减少操作失败的风险。|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Dem/DemConfigSet/DemEventParameter|

| 配置项属性 | 值（关联引用配置项） |
|-|-|
|名称|NVM_E_VERIFY_FAILED|
|描述|Reference to the DemEventParameter which shall be issued when the error "Write Verification failed" has occurred.|
|描述|概述：NVM_E_VERIFY_FAILED是一个错误代码，表示非易失性存储（NVM）模块在验证写入操作的数据完整性时检测到数据不一致或损坏。|
|描述|注意：该错误代码用于指示数据未能通过完整性校验，可能需要重新尝试写入操作或采取恢复措施；确保NVM管理策略包括对此类错误的处理逻辑；在设计NVM数据存储和访问策略时，考虑增加额外的数据完整性校验机制以降低此类错误发生的风险。|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Dem/DemConfigSet/DemEventParameter|

| 配置项属性 | 值（关联引用配置项） |
|-|-|
|名称|NVM_E_WRITE_PROTECTED|
|描述|Reference to the DemEventParameter which shall be issued when the error "write attempt to NVRAM block with write protection" has occurred.|
|描述|概述：NVM_E_WRITE_PROTECTED 是一个错误状态码，用于指示请求写入非易失性存储器（NVM）时，目标区域被写保护，导致写入操作无法执行。|
|描述|注意：在处理NVM请求时，应检查存储区域的写保护状态；如果存储区域被意外地设置为写保护，可能需要重新配置或解除保护；在设计NVM管理策略时，应确保正确处理此类错误码，以便于系统稳定性和数据完整性。|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Dem/DemConfigSet/DemEventParameter|

| 配置项属性 | 值（关联引用配置项） |
|-|-|
|名称|NVM_E_WRONG_BLOCK_ID|
|描述|Reference to the DemEventParameter which shall be issued when the error "Static Block ID check failed" has occurred.|
|描述|概述：NVM_E_WRONG_BLOCK_ID 是一个错误代码，用于指示请求的NVRAM块标识符不存在或不正确。|
|描述|注意：在使用NVRAM管理服务时，确保所有块ID正确配置且与实际的存储块匹配；错误的块ID可能导致数据访问错误或数据丢失；在系统初始化或诊断过程中，应检查和验证所有NVRAM块ID的正确性。|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Dem/DemConfigSet/DemEventParameter|

