#  EcuC 配置项参考文档

| 容器属性 | 值（容器） |
|-|-|
|名称|EcuC|
|描述|Virtual module to collect ECU Configuration specific / global configuration information.|
|多实例个数|0 - 1|

## 1. EcucConfigSet

| 容器属性 | 值（容器） |
|-|-|
|名称|EcucConfigSet|
|描述|This container contains the configuration parameters and sub containers of the global PduCollection.|
|多实例个数|0 - 1|

### 1.1. EcucPduCollection

| 容器属性 | 值（容器） |
|-|-|
|名称|EcucPduCollection|
|描述|Collection of all Pdu objects flowing through the Com-Stack.|
|多实例个数|0 - 1|

| 配置项属性 | 值（枚举参数配置项） |
|-|-|
|名称|PduIdTypeEnum|
|描述|The PduIdType is used within the entire AUTOSAR Com Stack except for bus drivers. The size of this global type depends on the maximum number of PDUs used within one software module. If no software module deals with more PDUs that 256, this type can be set to uint8. If at least one software module handles more than 256 PDUs, this type must be set to uint16. See AUTOSAR_SWS_CommunicationStackTypes for more details.|
|多实例个数|1 - 1|

| 配置项属性 | 值（枚举参数配置项） |
|-|-|
|名称|PduLengthTypeEnum|
|描述|The PduLengthType is used within the entire AUTOSAR Com Stack except for bus drivers. The size of this global type depends on the maximum length of PDUs to be sent by an ECU. If no segmentation is used the length depends on the maximum payload size of a frame of the underlying communication system (for FlexRay maximum size is 255 bytes, therefore uint8). If segmentation is used it depends on the maximum length of a segmented N-SDU (in general uint16 is used). See AUTOSAR_SWS_CommunicationStackTypes for more details.|
|多实例个数|1 - 1|

#### 1.1.1. MetaDataType

| 容器属性 | 值（容器） |
|-|-|
|名称|MetaDataType|
|描述|Meta data serves to transport information through the AUTOSAR layers. It is transported by the PduInfoType structure via a separate pointer to a byte array alongside the length of and a pointer to the payload of the PDU. This container defines the content of the meta data.|
|多实例个数|0 - inf|

##### 1.1.1.1. MetaDataItem

| 容器属性 | 值（容器） |
|-|-|
|名称|MetaDataItem|
|描述|The content of meta data in a Pdu consists of an ordered list of meta data items.|
|说明|This container represents a meta data item that is contained in meta data of a Pdu.|
|多实例个数|1 - inf|

| 配置项属性 | 值（枚举参数配置项） |
|-|-|
|名称|MetaDataItemType|
|描述|This parameter defines the type of a meta data item.|
|多实例个数|1 - 1|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|MetaDataItemLength|
|描述|This parameter defines the length of a meta data item in bytes.|
|多实例个数|1 - 1|
|取值范围|1 - 64|

#### 1.1.2. Pdu

| 容器属性 | 值（容器） |
|-|-|
|名称|Pdu|
|描述|One Pdu flowing through the COM-Stack.|
|说明|This Pdu is used by all Com-Stack modules to agree on referencing the same Pdu.|
|多实例个数|0 - inf|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|DynamicLength|
|描述|This parameter defines whether the Pdu has dynamic length (true) or not (false). Please note that the usage of this attribute is restricted by [constr_3448].|
|多实例个数|0 - 1|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|J1939Requestable|
|描述|Pdu can be triggered by the J1939 request message.|
|多实例个数|0 - 1|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|PduLength|
|描述|Length of the Pdu in bytes. It should be noted that in former AUTOSAR releases (Rel 2.1, Rel 3.0, Rel 3.1, Rel 4.0 Rev. 1) this parameter was defined in bits.|
|多实例个数|1 - 1|
|取值范围|0 - 4294967295|

| 配置项属性 | 值（外部引用配置项） |
|-|-|
|名称|SysTPduToFrameTriggeringRef|
|描述|Reference to the FrameTriggering from the SystemTemplate which this Pdu belongs to.|
|说明|SysTPduToFrameTriggeringRef shall be used for UserDefinedPdus, NmPdus and NPdus which are not going through the Pdu Router. This reference shall not be used if SysTPduToPduTriggeringRef exists.|
|多实例个数|0 - 1|
|目标类型|FRAME-TRIGGERING|

| 配置项属性 | 值（外部引用配置项） |
|-|-|
|名称|SysTPduToPduTriggeringRef|
|描述|Reference to the PduTriggering from the SystemTemplate which this Pdu represents.|
|说明|SysTPduToPduTriggeringRef shall be used for all Pdus except UserDefinedPdus, NmPdus and NPdus which are not going through the Pdu Router. For these Pdus, SysTPduToFrameTriggeringRef shall be used.|
|多实例个数|0 - 1|
|目标类型|PDU-TRIGGERING|

| 配置项属性 | 值（关联引用配置项） |
|-|-|
|名称|MetaDataTypeRef|
|描述|Reference to meta data that is transported in the Pdu through the AUTOSAR layers.|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/EcuC/EcucConfigSet/EcucPduCollection/MetaDataType|

| 配置项属性 | 值（关联引用配置项） |
|-|-|
|名称|EcucPduDefaultCoreRef|
|描述|Reference to EcucCoreDefinition, where the according Pdu is assigned to.|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/EcuC/EcucHardware/EcucCoreDefinition|

## 2. EcucHardware

| 容器属性 | 值（容器） |
|-|-|
|名称|EcucHardware|
|描述|Hardware definition of this Ecu.|
|多实例个数|0 - 1|

### 2.1. EcucCoreDefinition

| 容器属性 | 值（容器） |
|-|-|
|名称|EcucCoreDefinition|
|描述|Definition of one Core on this Ecu.|
|多实例个数|0 - inf|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|EcucCoreId|
|描述|ID of the core.|
|多实例个数|1 - 1|
|取值范围|0 - 65535|

| 配置项属性 | 值（关联引用配置项） |
|-|-|
|名称|EcucCoreHwRef|
|描述|Optional reference to the HwElement of HwCategory ProcessingUnit that represents this Core in the ECU Resource Template.|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Os/OsPublishedInformation/OsDerivativeInformation/OsPhysicalCore|

## 3. EcucPartitionCollection

| 容器属性 | 值（容器） |
|-|-|
|名称|EcucPartitionCollection|
|描述|Collection of Partitions defined for this ECU.|
|多实例个数|0 - 1|

### 3.1. EcucPartition

| 容器属性 | 值（容器） |
|-|-|
|名称|EcucPartition|
|描述|Definition of one Partition on this ECU.|
|说明|One Partition will be implemented using one Os-Application.|
|多实例个数|0 - inf|

| 配置项属性 | 值（枚举参数配置项） |
|-|-|
|名称|ASIL|
|描述|This parameter defines the ASIL of a meta data item.|
|多实例个数|1 - 1|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|EcucPartitionBswModuleExecution|
|描述|Denotes that this partition will execute BSW Modules. BSW Modules can only be executed in such partitions.|
|多实例个数|1 - 1|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|EcucPartitionQmBswModuleExecution|
|描述|Denotes that this partition will execute QM BSW.|
|多实例个数|1 - 1|
|默认值|true|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|PartitionCanBeRestarted|
|描述|Specifies the requirement whether the Partition can be restarted. If set to true all software executing in this partition shall be capable of handling a restart.|
|多实例个数|1 - 1|
|默认值|false|

| 配置项属性 | 值（外部引用配置项） |
|-|-|
|名称|EcucPartitionBswModuleDistinguishedPartition|
|描述|This maps the abstract partition of the Bsw Module to a concrete Partition existing in the ECU.|
|多实例个数|0 - inf|
|目标类型|BSW-DISTINGUISHED-PARTITION|

| 配置项属性 | 值（实例引用配置项） |
|-|-|
|名称|EcucPartitionSoftwareComponentInstanceRef|
|描述|References the SW Component instances from the Ecu Extract that shall be executed in this partition.|
|多实例个数|0 - inf|
|目标上下文|ROOT-SW-COMPOSITION-PROTOTYPE|
|目标类型|SW-COMPONENT-PROTOTYPE|

## 4. EcucPostBuildVariants

| 容器属性 | 值（容器） |
|-|-|
|名称|EcucPostBuildVariants|
|描述|Collection of toplevel PostBuildSelectable variants. The PredefinedVariants linked inside this container will determine how many PostBuildSelectableVariants exist. If this container exist the name pattern for initialization of BSW modules will be <Mip>_Config_<PredefinedVariant.shortName>. If this container does not exist the name pattern for initialization of BSW modlues will be <Mip>_Config.|
|多实例个数|0 - 1|

| 配置项属性 | 值（外部引用配置项） |
|-|-|
|名称|EcucPostBuildVariantRef|
|描述|Reference to a PredefinedVariant that defines one toplevel postBuild configuration set (covering all post-build capable BSW modules). PredefinedVariants that are referenced here shall contain only PostBuildVariantCriterionValueSets.|
|多实例个数|0 - inf|
|目标类型|PREDEFINED-VARIANT|

## 5. EcucUnitGroupAssignment

| 容器属性 | 值（容器） |
|-|-|
|名称|EcucUnitGroupAssignment|
|描述|Collection of UnitGroup references to support the generation of ASAM MCD file.|
|多实例个数|0 - 1|

| 配置项属性 | 值（外部引用配置项） |
|-|-|
|名称|EcucUnitGroupRef|
|描述|Optional reference to the UnitGroup to support the generation of ASAM MCD file. These UnitGroups are selecting a set of units for a specific country.|
|多实例个数|0 - inf|
|目标类型|UNIT-GROUP|

## 6. EcucVariationResolver

| 容器属性 | 值（容器） |
|-|-|
|名称|EcucVariationResolver|
|描述|Collection of PredefinedVariant elements containing definition of values for SwSystemconst which shall be applied when resolving the variability during ECU Configuration.|
|多实例个数|0 - 1|

| 配置项属性 | 值（外部引用配置项） |
|-|-|
|名称|PredefinedVariantRef|
|多实例个数|0 - inf|
|目标类型|PREDEFINED-VARIANT|

