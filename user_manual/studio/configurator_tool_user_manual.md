# 配置工具开发者手册

## 1. 工具简介

Configurator 是配套 VCOS 操作系统提供给汽车控制器软件开发工程师使用的一款组件配置工具，此工具提供 VCOS 的各组件模块、以及 Task Mapping、Data Mapping、Port Mapping、Service Mapping 等功能进行配置的 UI 界面，并根据用户配置生成 RTE 及各功能组件的动态代码，配合应用软件代码、功能组件代码及芯片驱动代码、复杂驱动共同编译生成控制器软件镜像。同时 Configurator 还提供命令行接口以及 Python API 接口实现VCOS功能组件自动化配置以及软件自动化版本集成

## 2. 代码目录

vcos_studio源代码在haloosspace/vcos/vcos_studio目录下，目录结构如下图所示：

```plaintext
vcos_studio
└─ configurator                # 配置工具
    ├─ basic_func_module       # 基础功能模块，主要包括功能模块所使用的公用接口，如文件处理、autosar arxml解析编辑接口、日志接口等
    │  ├─ autosar_utils        # AUTOSAR相关工具
    │  ├─ base_common          # 基础通用功能
    │  ├─ base_logger          # 日志功能
    │  ├─ file_handler         # 文件处理
    │  ├─ file_management      # 文件管理
    │  ├─ file_validation      # 文件校验
    │  ├─ hash_utils           # 哈希工具
    │  └─ path_handler         # 路径处理
    ├─ cfg_gui                 # 前台 GUI 界面的用户操作交互功能代码，包括 BSW 配置编辑、Rte 配置编辑、导入导出、工程管理、二级菜单、搜索跳转、代码生成及校验等UI功能
    │  ├─ bsw_editor           # BSW 模块配置界面
    │  ├─ common               # 通用功能模块
    │  ├─ export_file          # 导出文件界面
    │  ├─ generator            # 代码生成界面
    │  ├─ import_file          # 导入文件界面
    │  ├─ main_window.py       # 主窗口
    │  ├─ project_management   # 工程管理界面
    │  ├─ resources            # 资源文件
    │  ├─ rte_editor           # Rte二级菜单，包含Task Mapping，Data Mapping，Port Mapping和Service Mapping
    │  ├─ search_jump          # 搜索跳转功能
    │  ├─ secondary_menu       # 二级菜单界面
    │  ├─ trace                # trace数据处理模块
    │  ├─ validation           # 校验界面
    │  └─ widgets              # UI组件
    ├─ ui_adaptor              # 前台 GUI 适配层，对上提供接口供 GUI 用户交互模块调用，对下调用功能模块层的具体模块业务功能，并管理 GUI 交互数据
    │  ├─ data_management      # 数据管理
    │  ├─ func_logic_layer     # 功能逻辑层
    │  ├─ launch_configurator.py # 启动配置器
    │  ├─ ui_adaptor.py        # UI适配器
    │  └─ ui_interaction       # UI交互
    ├─ cmd_api                 # 配置工具提供的 API 及命令行接口，包括供参考使用的演示代码
    │  ├─ api_demo             # 对外 API 使用演示
    │  ├─ cmd_demo             # 命令行接口演示
    │  ├─ auto_cli.py          # 命令行接口
    │  └─ auto_cli_api.py      # 对外API接口
    ├─ cmd_adaptor             # 前台命令行适配层，对上提供 API 及命令行接口，对下调用功能模块层的具体业务功能，管理交互数据
    │  ├─ cmd_interaction      # 命令行交互
    │  ├─ data_management      # 数据管理
    │  └─ func_logic_layer     # 功能逻辑层
    ├─ func_module             # 功能模块层，对前台命令行模块及 UI 界面提供具体功能实现，包括文件导入、导出、代码生成、配置校验、模块管理、mapping、工程管理等
    │  ├─ export_file          # 导出文件模块
    │  ├─ generator            # 代码生成模块
    │  ├─ health_monitor       # 健康监控模块
    │  ├─ import_file          # 导入文件模块
    │  ├─ mapping              # task mapping、data mapping、port mapping、service mapping等功能模块核心功能实现
    │  ├─ module_management    # 模块管理模块
    │  ├─ project_management   # 工程管理模块
    │  └─ validation           # 校验模块
    ├─ third_party             # 依赖的第三方库
    │  ├─ autosar44            # AUTOSAR 4.4 相关库
    │  ├─ cantools             # cantools库
    │  ├─ durable              # durable_rules_engine规则引擎库
    │  ├─ durable_rules_engine.cp38-win_amd64.pyd  # Windows 规则引擎
    │  └─ durable_rules_engine.cpython-38-x86_64-linux-gnu.so  # Linux 规则引擎
    ├─ configurator.bat        # Windows 环境下 Configurator 工具启动脚本（启动时会显示控制台窗口）
    ├─ configurator.ps1        # Windows 环境下 Configurator 工具启动脚本（无控制台版本）
    ├─ configurator.py         # Configurator 工具主程序入口
    ├─ configurator.sh         # Linux 环境下 Configurator 工具启动脚本
    ├─ init_env.py             # Configurator 工具环境配置脚本
    ├─ pyproject.toml          # Python 项目配置文件
    └─ requirements.txt        # Python 依赖包列表
```

## 3. 功能配置方法

### 3.1. 配置工具界面

![Configuration Tool Overview](../../_static/image/tool_chain/configuration/overview.png)

- 菜单栏
  - 主要实现工程操作，例如：新建工程、打开工程、工程历史记录、校验代码生成等。详细介绍见 3.2 章节
- 功能区
  - 主要实现 RTE、BSW 层模块配置以及 ARXML 导入。详细介绍见 3.3 章节
- 二级菜单
  - 主要实现 BswM 状态管理。详细介绍见 3.4 章节
- Log 输出
  - 主要实现 Configurator 运行状态信息打印、校验结果展示、配置项查找等功能。详细介绍见 3.5 章节

### 3.2. 菜单栏

#### 3.2.1. File 菜单

File 菜单主要包含：新建工程、打开工程、工程保存、导入 ARXML、导出 ARXML 和 Os 模块配置导入导出功能，详细介绍如下。

##### 3.2.1.1. 新建工程

1. 点击新建工程按钮

   ![New Project Button](../../_static/image/tool_chain/configuration/new_project.png)

2. 填写新工程信息

   新建工程时，填写工程名字及路径信息，并选择使用的芯片型号、编译器和编译器路径等。

   ![New Project Information](../../_static/image/tool_chain/configuration/new_project_info.png)

   配置参数说明：

   - Folder Structure:
     - Project Name: 工程名称；（创建以后在 Project Setting 页面不支持修改工程名称）
     - Project File：选择工程文件存放路径，自动在该路径下创建 Project Name 文件夹；
     - Config Path: 工程配置文件存放路径，选择 Project File 路径以后在 Project Name 文件夹下自动创建 Config 文件夹；
     - GenData Path: 动态代码生成路径，选择 Project File 路径以后在 Project Name 文件夹下自动创建 GenData 文件夹；
     - Application Path: SWC 代码路径，需要选择实际的 SWC 代码路径；
     - User Plugin GenDataPath: 用户模块代码生成路径
     - Bsw Internal Behavior Path: IB ARXML 生成路径，选择 Project File 路径以后在 Config 文件夹下自动创建 InternalBehavior 文件夹；
     - Log Files: 配置 Log 文件生成路径，选择 Project File 路径以后在 Project Name 文件夹下自动创建 Log 文件夹；
     - Configurator PlugIn Path: config_support 目录路径；
   - Target:
     - Select Target: 选择芯片型号，例如：AURIX2G_TC397 和 E3650 等；
     - MCAL VERSION: Mcal 支持“MC-ISAR_AS422_TC3xx_BASIC_1.40.0”版本
     - Select Compiler: 选择编译器
     - Compiler Path: 编译器路径选择 bin 文件夹的上一级目录，
       - gcc 编译器路径选择：GNUArmToolchain/windows 或 GNUArmToolchain/linux/gcc-arm
       - tasking 编译器路径选：TriCore_v6.3r1/ctc

##### 3.2.1.2. 打开工程

1. 点击打开工程按钮

   ![Open Project Button](../../_static/image/tool_chain/configuration/open_project.png)

2. 选择工程文件

   ![Open Project File](../../_static/image/tool_chain/configuration/open_project_file.png)

##### 3.2.1.3. 工程保存

![Project Save Button](../../_static/image/tool_chain/configuration/project_save.png)

##### 3.2.1.4. 工程另存为

![Project Save As Button](../../_static/image/tool_chain/configuration/project_as_save.png)

- 配置项同 3.2.1.1. 章节新建工程

##### 3.2.1.5. ARXML 导入/导出

1. ARXML 导入

   对于 ARXML 文件导入功能，支持 ASW、BSW 和 Mcal 三种类型的 ARXML 导入。其中 BSW 和 Mcal ARXML 可以通过界面勾选 ARXML 文件中的特定模块来进行导入，且支持同时选择 ASW、BSW 和 Mcal 三种 ARXML 文件进行导入。

   对于 ASW ARXML 工具还提供一种选择目录后，递归地将当前目录下所有 ARXML 文件进行导入的方式，见下图 Import Asw 按钮。

   鼠标点击 Configurator 工具 VCOS BSW 界面的 Import ARXML 按钮或者在菜单栏 File 中点击 Import ARXML，在弹出的窗口中可以对导入的文件进行管理。

   ![Import ARXML Button](../../_static/image/tool_chain/configuration/import_arxml_001.png)

   Import ARXML 按钮点击后，会出现如下弹窗，点击窗口左上角的按钮 "+" 后可以选择需要导入的文件，在选择文件的弹窗中确认需要导入的文件，文件信息会以文件的完整路径进行展示。在弹窗界面选中文件再点击 "X" 按钮后可以移除需要导入的文件。

   ![Import ARXML Dialog](../../_static/image/tool_chain/configuration/import_arxml_002.png)

   如果选择的是 ASW ARXML，直接点击 finish 按钮后，会对选择的 ASW ARXML 进行导入。

   > **注意**：导入 ASW ARXML 功能是将选择的 ASW ARXML 的数据直接覆盖当前工程的 ASW 数据。

   如果选择的是 BSW 或者 Mcal ARXML，点击 next 按钮后，可以对这些文件中的模块进行选择：

   - 第一列：Ecuc Module 表示可以选择的导入模块列表

   - 第二列：Import Mode 表示导入的模式：

   ![Import Mode Selection](../../_static/image/tool_chain/configuration/import_arxml_003.png)

   - replace 表示把导入的 ARXML 模块配置数据替换当前工程的对应模块配置数据；

   - add 表示当前工程未配置该模块，直接以 ARXML 中的模块数据添加模块；

   - merge 表示合并导入，用户可以在选择的 ARXML 与当前工程之间择保留哪个配置。

   - 点击 finish 按钮，完成 BSW / Mcal ARXML 的导入。

   如果存在模块选择的导入模式是 merge，则会出现相应模块的 ”冲突解决“ 界面，由用户自行选择需要保留哪个配置，“冲突解决” 界面中会显示 container 和参数的增删改情况，每个显示框中都会显示当前工程的配置情况和导入的 ARXML 的配置情况的信息，通过 “->” 来分隔当前工程和导入的 ARXML 的配置信值。如下图：

   ![Conflict Resolution Interface](../../_static/image/tool_chain/configuration/import_arxml_004.png)

   点击按钮 Apply 后，工具会根据用户选择的配置更新工程数据。

2. ARXML 导出

   ARXML 导出功能是将当前工程中模块配置数据导出，并保存为 ARXML 文件。

   鼠标点击 Configurator 工具 VCOS BSW 界面的 Export ARXML 按钮，在弹出的窗口中选择需要导出的模块。

   ![Export ARXML Button](../../_static/image/tool_chain/configuration/export_arxml_001.png)

   ![Export ARXML Module Selection](../../_static/image/tool_chain/configuration/export_arxml_002.png)

   在上图中选择需要导出的模块，选择完成后点击 next 按钮，选择需要导出 ARXML 的路径和文件名称，点击保存按钮后，等待界面直到进度条消失，表示 ARXML 文件导出完成。

   ![Export ARXML Save Dialog](../../_static/image/tool_chain/configuration/export_arxml_003.png)

##### 3.2.1.6. Os 配置导入/导出

本功能支持通过 Configurator 对工程中的 Os 模块配置信息进行导入和导出：

- 用户可以通过 Configurator 导出工程的 Os 模块配置信息，输出到指定 Excel 文件中。
- 用户可以通过 Configurator 导入指定 Excel 文件来对工程的 Os 模块做自动配置。

1. 导出 Os 配置

   点击 File->Os Configuration->Export，选择文件路径，即可导出 Excel 文件，文件内包含当前工程中的 Os 配置信息。

   ![Os Configuration Export](../../_static/image/tool_chain/configuration/os_cfg_export_001.png)

2. 导入 Os 配置

   ![Os Configuration Import](../../_static/image/tool_chain/configuration/os_cfg_import_001.png)

   点击 File->Os Configuration->Import，选择 Excel 文件，即可自动配置当前 Os 模块。

3. Excel 文件使用建议

   在使用 Os 自动配置功能时，建议先把当前配置导出成 Excel，然后再基于 Excel 修改，最后导入修改后的 Excel 做自动配置。

   这样可以在原始工程的 Excel 文件中进行增量修改，不需要重新新建 Excel 文件，相对方便一些。

##### 3.2.1.7. MCAL配置文件导入VCOS

使用EB tresos工具配置MCAL层代码以及导出配置文件，再将配置文件导入VCOS Studio工具是开发过程中的一个重要步骤，本小节主要描述此过程的主要操作步骤：

1. 选中工程:在EB 工具中，选中你需要导出ARXML文件的配置工程。

2. 右键点击选中的工程，然后选择"Im- and Exporters"。

   ![EB config export](../../_static/image/tool_chain/configuration/eb_export_arxml_select.png)

3. 新建导出配置:点击"+" 按钮，在"Name" 字段中输入导出配置的名称，并将"Mode" 设为"Export only"。

   ![EB config export create](../../_static/image/tool_chain/configuration/eb_export_arxml_create.png)

4. 选择导出文件:点击"Next"，然后选择要导出的ARXML文件，并设置文件后缀为".arxml"。在"File Name" 字段中选择该文件，在"Content type" 中选择相应的AUTOSAR 版本。

   ![EB config export next](../../_static/image/tool_chain/configuration/eb_export_arxml_expconfig.png)

5. 完成导出:点击Run Export，最后点击"Finish" 完成导出配置。

   ![EB config export finish](../../_static/image/tool_chain/configuration/eb_export_arxml_finish.png)

6. 按照 3.2.1.5.的arxml文件导入操作，将上一步得到的arxml文件导入到VCOS Studio工具。导入时注意选择需要的模块：

   ![EB arxml import vcos](../../_static/image/tool_chain/configuration/eb_export_arxml_vcos_import.png)

   ![EB arxml import vcos result](../../_static/image/tool_chain/configuration/eb_export_arxml_vcos_impor_result.png)

#### 3.2.2. CodeGen 菜单

##### 3.2.2.1. Validation

工具提供工程配置校验的功能，可在代码生成前拦截配置错误。使用说明如下：

在工具菜单栏中的 CodeGen 菜单中，点击 Validation 这一栏，会弹出当前工程的校验页面。

![Validation Menu](../../_static/image/tool_chain/configuration/module_validation_001.png)

在如下的校验页面勾选需要校验的模块，然后点击页面右下角的 Validation 按钮，对相关模块进行校验。

![Validation Module Selection](../../_static/image/tool_chain/configuration/module_validation_002.png)

校验的结果会显示在工具界面下方的 Validation 菜单处，勾选模块的所有基础校验和语义校验的错误信息会在该区域显示。

![Validation Results Display](../../_static/image/tool_chain/configuration/module_validation_003.png)

校验分为基础校验和语义校验，基础校验是对于参数本身的配置情况进行校验，语义校验则是附带条件或者多个参数之间配置关系的校验(多个参数之间满足某种条件)。

校验结果会反应在两个位置：

1. 参数对应的配置值框的左下角 x 号，鼠标进入 ”X“ 后会有该参数相关的校验错误的详细信息窗口弹出；

   ![Parameter Validation Error](../../_static/image/tool_chain/configuration/module_validation_004.png)

2. 界面的 validation 区

   validation 区显示校验相关错误的详细信息，展开一条校验规则后，会显示自动解决信息和校验相关的参数路径信息。

   ![Validation Area Details](../../_static/image/tool_chain/configuration/module_validation_005.png)

##### 3.2.2.2. Generator

1. 模块代码生成

   1. 点击菜单栏中的 Generator 按钮

      ![Generator Button](../../_static/image/tool_chain/codegen/ui_overview_01.png)

   2. 在界面中勾选对应的模块，点击右下角 Generate 按钮，即可生成模块动态代码。

      ![Module Selection for Generation](../../_static/image/tool_chain/codegen/ui_overview_02.png)

2. 选择需要生成代码的模块，并配置以下参数：

   - Select Limit: 在执行代码生成前会先执行 validation，根据 validation 结果和该配置项决定是否执行代码生成；No Limit 表示不考虑 validation 结果，始终执行代码生成；Warning 表示 validation 结果包含 warning 或 error，不执行代码生成；Error 表示 validation 结果包含 error，不执行代码生成；
   - Select Mode: 选择代码生成模式；Release 模式生成的配置不包含测试代码；Debug 模式生成的代码配置包含测试代码。
   - Incremental generation: 是否增量代码生成，增量代码生成不会重新生成未改变配置的模块

#### 3.2.3. Project 菜单

##### 3.2.3.1. ProjectSetting

当工程创建完成后，用户可以通过 ProjectSetting 修改工程配置，工程配置如下：

![Project Settings Interface](../../_static/image/tool_chain/configuration/project_setting_ui.png)

- 配置项同 3.2.1.1 章节新建工程

#### 3.2.4. User_Module_Plugin 菜单

Configurator 支持用户导入自定义模块，用户可以通过 Configurator 使用插件提供的功能，例如模块配置编辑、模块代码生成、模块校验等

##### 3.2.4.1. 导入用户模块

点击 Manage Plugins 按钮，选择用户自定义模块所在文件夹

![User Module Plugin Menu](../../_static/image/tool_chain/user_module/plugin_05.png)

支持选择多个模块目录同时导入

![User Module Selection](../../_static/image/tool_chain/user_module/plugin_01.png)

![User Module Import Process](../../_static/image/tool_chain/user_module/plugin_04.png)

![User Module Import Completion](../../_static/image/tool_chain/user_module/plugin_06.png)

##### 3.2.4.2. 删除用户模块

1. 点击 Manage Plugin 进入 plugin manager

   ![Manage Plugin Button](../../_static/image/tool_chain/user_module/plugin_05.png)

2. 选择要删除的模块插件，点击 Remove

   ![Remove Plugin Interface](../../_static/image/tool_chain/user_module/plugin_03.png)

##### 3.2.4.3. 插件功能使用

1. 模块配置编辑

   用户模块导入之后，可以选择添加此模块，双击模块即可进行模块配置编辑

   ![Add Module Selection](../../_static/image/tool_chain/user_module/plugin_add_module_02.png)

   ![Module Configuration Interface](../../_static/image/tool_chain/user_module/plugin_add_module_01.png)

2. 代码生成

   默认代码生成路径同 VCOS 模块一致，支持用户可配，配置项见 User Plugin GendataPath 配置项

   ![Code Generation Path Configuration](../../_static/image/tool_chain/user_module/plugin_add_module_05.png)

   ![Code Generation Interface](../../_static/image/tool_chain/user_module/plugin_add_module_04.png)

3. Validation

   ![Module Validation Interface](../../_static/image/tool_chain/user_module/plugin_add_module_03.png)

##### 3.2.4.4. 插件开发

###### 1. 插件目录结构(MemAcc1为例)

   ![Plugin Directory Structure](../../_static/image/tool_chain/user_module/plugin_develop_01.png)

**目录说明：**

- MemAcc1：插件的根目录，名称必须与模块名称一致。
- module_cfg.json：插件的系统配置文件。
- base_config：配置文件，包含初始化配置和模型文件。
- generator：包含代码生成相关文件，负责动态代码生成逻辑。
- ib_bswmd_process：处理InternalBehavior动态更新的模块。
- validation：校验模块逻辑

###### 2. 配置文件 module_cfg.json

```json
{
    "MemAcc1": {
        "group": [
            "Memory"
        ],
        "dependency_list": [],
        "support_ui": true,
        "support_validation": true,
        "support_generation": true,
        "internal_behavior": {
            "support": true,
            "dynamic": false
        },
        "user_plugin": true
    }
}
```

**字段说明：**

- MemAcc1: 插件的模块名称，必须与插件目录名称一致。
- group: 插件所属的功能组，例如 "Memory"。
- dependency_list: 列出该插件所依赖的其他插件或模块（如有）。
- support_ui: 布尔值，指示插件是否支持用户界面。
- support_validation: 布尔值，指示插件是否支持验证功能。
- support_generation: 布尔值，指示插件是否支持代码生成功能。
- internal_behavior: 该部分包含InternalBehavior支持信息：
  - support: 布尔值，指示是否支持InternalBehavior。
  - dynamic: 布尔值，指示是否支持动态更新InternalBehavior。

###### 3. 模块初始化配置文件plug_in/base_config

- base_ecuc 目录下的 MemAcc1_ecuc.arxml：用于模块初始化相关配置。
- bswmd 目录下的 MemAcc1_bswmd.arxml：用于 BSW 模块模型描述。
- internal_behavior 目录下的 MemAcc1_ib_bswmd.arxml：用于internal_behavior相关配置。

###### 4. 校验模块

- 如果插件支持校验，开发者必须实现一个校验模块，命名为 MemAcc1_rule.py。该模块应包含以下接口：

```python
class MemAcc1Rule():

    def __init__(self) -> None:
        self.logs = {}

    def validate(self, validation_data):
        # 在这里实现校验逻辑
        return self.logs
```

###### 5. 代码生成模块

- 如果插件支持代码生成，开发者必须实现代码生成模块，命名为 generator.py。下面是必需的接口：

```python
   def generate_dynamic_code():
      # 在这里实现代码生成逻辑
      return True
```

###### 6. Internal behavior动态更新模块

- 如果插件需要支持 Internal behavior动态更新模块，开发者必须实现此模块，命名为 memacc1_ib_bswmd_process.py。此模块应包含以下接口：

```python
   def update_ib_bswmd():
      # 在这里实现Internal behavior动态更新逻辑
      return True
```

### 3.3. 功能区

#### 3.3.1. 模块管理

##### 3.3.1.1. 添加模块

1. 点击 Add 按钮, 勾选需要添加的模块

   ![Add Module Button](../../_static/image/tool_chain/configuration/add_module.png)

2. 配置模块, 双击模块，进入配置界面

   ![Module Configuration Screen](../../_static/image/tool_chain/configuration/module_config.png)

#### 3.3.2. 通信/诊断配置文件导入

1. 点击Input files按钮

   ![Input Files Button](../../_static/image/tool_chain/configuration/input_files_001.png)

2. 选择要导入的文件（目前支持导入DBC/CDD）,导入DBC后，应选择需要的ECU Instance。

   ![Input Files Button](../../_static/image/tool_chain/configuration/input_files_002.png)

   1. "Add Files"按钮：从UI上添加新的DBC文件
   2. "Remove"按钮：从UI上移除DBC文件
   3. "Replace"按钮：从UI上替换选中的DBC文件

   **重要配置选项说明：**

   1. **CDD 文件导入配置**

      选择 `Import DIDs and RIDs as single signal for DCM (backward compatibility)` 选项时，会将 DID/RID 中的多个 Signal 合并为一个信号。
      > **注意**目前仅支持导入Candela13.0版本的cdd文件，不支持导入其他版本的cdd文件！

   2. **DBC 文件导入配置**

      选择 `Import DBC files with added channel name to the SystemSignals` 选项时，会将网段名作为后缀添加到自动生成的 SystemSignal 名字中，格式为：`<SystemSignal>_<网段名>`。

      **该配置项的勾选必须与应用层开发的 Port 命名保持一致：**

      - **勾选时**：应用层 Port 的名字需要加上对应的网段名作为后缀，格式为：`<Port>_<网段名>`
      - **不勾选时**：应用层 Port 不需要额外加网段名，格式为：`<Port>`

      > **重要提醒**：如果配置不一致，在进行 Port Mapping 时会匹配不到对应的 SystemSignal。
      >
      > **建议**：仅在 CAN 多核部署特性时勾选此选项（需与应用层设计配合使用），其他情况下建议不勾选，以避免不必要的命名后缀。

#### 3.3.3. ASW 导入、ARXML 文件导入/导出

##### 3.3.3.1. 导入 ASW 配置文件

点击 Import Asw 选择需要导入的 ASW 文件夹点击选择文件夹，就会导入文件夹下所有 Asw。

![Import ASW Button](../../_static/image/tool_chain/configuration/import_asw.png)

> **注意**：导入的 ASW 中有同名的 swc 会导致导入失败

##### 3.3.3.2. 导入 ARXML(Mcal 或 BSW 模块配置ARXML文件)

主界面中的 Import ARXML 与 3.3.1.5 节的 ARXML 导入导出功能一致。

![ARXML Import Export Buttons](../../_static/image/tool_chain/configuration/arxml_import_export.png)

#### 3.3.4. BSW 配置

##### 3.3.4.1. BSW 层模块

1. [VCOS内核开发者手册](../kernel/kernel_user_manual.md)
2. [以太协议栈开发者手册](../components/ethernet_user_manual.md)
3. [存储协议栈开发者手册](../components/non_volatile_storage_user_manual.md)

##### 3.3.4.2. 拆分模块配置

- 工具支持将同一模块的<模块名>\_ecuc.arxml 文件拆分为多份，每份各自保存该模块的部分配置，便于不同同事合作修改同一模块的配置。

1. UI 展示

   1. 未指定文件的节点，保存在默认的文件中（通常为<模块名>\_ecuc.arxml）

      ![Default File Node Display](../../_static/image/tool_chain/configuration/module_split_0.png)

   2. 已指定文件的节点，展示其将被保存至的文件（SystemApplication_Core0 被保存至 Os_ecuc1.arxml）

      ![Specified File Node Display](../../_static/image/tool_chain/configuration/module_split_1.png)

2. 拆分操作

   1. 选中 container，右键菜单中选择 Move to...

      ![Container Move To Menu](../../_static/image/tool_chain/configuration/module_split_2.png)

   2. 在弹出的文件选择页面中选中想要将 container 保存到的文件，并点击打开

      ![File Selection Dialog](../../_static/image/tool_chain/configuration/module_split_3.png)

      - 如文件不存在，可在此界面新建

      - 所选文件后缀必须为.arxml

   3. 此 container 将被标记为保存至对应文件

      ![Container Save Destination](../../_static/image/tool_chain/configuration/module_split_4.png)

      - 为了保证拆分后文件仍然是一个完整树形结构，当将一个 container 保存至某个文件时，其祖宗节点会同时保存至该文件

   4. 保存工程后，即可看到模块目录下文件中有对应内容

      ![Module Directory Files](../../_static/image/tool_chain/configuration/module_split_5.png)

#### 3.3.5. RTE 配置

##### 3.3.5.1. TaskMapping 配置

1. TaskMapping 主界面

   ![TaskMapping Main Interface](../../_static/image/tool_chain/configuration/taskmapping_main_window.png)

   左侧树形数据包括以下三类：

   - Application Components
   - Service Components
   - Schedulable Entities

   右侧表格中主要分两部分，第一行的表头，和其他行的映射表格；（注：若表头提示\<OsApp unassigned\>，则说明 Task 未被 Application 引用，需要用户在 Os 模块中进行绑定操作；）

   ![TaskMapping Table View](../../_static/image/tool_chain/configuration/taskmapping_table.png)

2. TaskMapping 的筛选功能

   输入 runnable 的查询关键词之后，会屏蔽掉不包含该关键词的行，如下图所示：

   ![TaskMapping Filter Example](../../_static/image/tool_chain/configuration/taskmapping_filter_01.png)

   点击 Clear All Filters，会清除所有的过滤查询信息，显示出所有行，如下图所示：

   ![TaskMapping Clear Filters](../../_static/image/tool_chain/configuration/taskmapping_filter_02.png)

3. TaskMapping map 操作

   从左侧页面拖动一个 runnable 到右侧表格中，这样就完成了一个 task mapping 的操作:

   ![TaskMapping Drag Operation](../../_static/image/tool_chain/configuration/taskmapping_map.png)

4. TaskMapping unmap 操作

   以下操作任选其一即可：

   1. 左侧树形数据中选中目标 runnable，然后右键点击 Unmap 操作:

      ![TaskMapping Unmap from Tree](../../_static/image/tool_chain/configuration/taskmapping_unmap_01.png)

   2. 右侧表格中选中目标行，然后右键点击 Unmap 操作:

      ![TaskMapping Unmap from Table](../../_static/image/tool_chain/configuration/taskmapping_unmap_02.png)

5. TaskMapping 信息导出

      ![TaskMapping Export Options](../../_static/image/tool_chain/configuration/taskmapping_export.png)

   1. 点击 "Export Os info" 按钮，可以导出 Core、Application、ISR、task 和 runnable 的全景表格文件;
   2. 点击 "Export" 按钮，可以导出同 UI 界面一致的 runnable 与 task 之间的映射关系表格文件（Excel 格式）；

##### 3.3.5.2. PortMapping和ServiceMapping配置

Port mapping界面中只显示is-service属性为false的port；Service mapping界面中只显示is-service属性为true的port；
除了上述区别，其他界面操作完全一致，下面的介绍以port mapping为例

1. 主界面

   ![PortMapping](../../_static/image/tool_chain/configuration/port_mapping_0.png)

   a. 在主界面上可以进行手动连接（Connect）或者断开（Disconnect）

   ![PortMapping](../../_static/image/tool_chain/configuration/port_mapping_1.png)

   b. 点击Connect后的界面

   ![PortMapping](../../_static/image/tool_chain/configuration/port_mapping_2.png)

2. 连接助手

   ![PortMapping](../../_static/image/tool_chain/configuration/port_mapping_3.png)

   a. 勾选Automatic Matching

   ![PortMapping](../../_static/image/tool_chain/configuration/port_mapping_4.png)

   b. 点击next后

   ![PortMapping](../../_static/image/tool_chain/configuration/port_mapping_5.png)

   c. 勾选要做mapping的port之后，点击next，可以在界面上看到自动mapping的结果，点击finish后mapping结果会被更新到主界面上。

   ![PortMapping](../../_static/image/tool_chain/configuration/port_mapping_6.png)

   d. 其他操作跟Automatic matching一致，勾选要mapping的SWC、port，在显示mapping结果后点击finish即可在主界面显示自动mapping结果。

   ![PortMapping](../../_static/image/tool_chain/configuration/port_mapping_7.png)

##### 3.3.5.3. DataMapping配置

1. DataMapping主界面筛选显示功能

   DataMapping功能目前支持SR Port，其他的Port类型暂不支持。如下图所示，DataMapping主界面支持筛选功能，可以根据**方向筛选**、**输入文本筛选**以及**每一列支持列筛选**，所有**筛选条件可以叠加**。也可以通过**重置筛选按钮**清除所有的筛选条件。

   ![DataMapping](../../_static/image/tool_chain/configuration/data_mapping_0.png)

   a. 方向筛选: 可以指定显示Tx方向、Rx方向或所有方向的SR Port

   b. 文本筛选: 可以输入任意文本，匹配的是每一行数据的所有列数据

   c. 列值筛选: 先反选->选择要显示的值->点Apply and close

   ![DataMapping](../../_static/image/tool_chain/configuration/data_mapping_1.png)

2. 导出功能

   DataMapping支持将界面的数据导出为Excel表，在Excel中可以进行更加灵活的查看连接关系。

   ![DataMapping](../../_static/image/tool_chain/configuration/data_mapping_2.png)

3. 手动连接/断开连接

   在选择的行数据上右键，可以看到连接和断开连接的选项，如果要断开连接，直接选择断开连接即可，下面重点介绍连接

   ![DataMapping](../../_static/image/tool_chain/configuration/data_mapping_3.png)

   a. 点击连接后弹出新的连接窗口

   ![DataMapping](../../_static/image/tool_chain/configuration/data_mapping_4.png)

   b. 完成后在主界面可以看到新的连接关系

4. 批量连接

   a. 点击链接打开连接助手

   ![DataMapping](../../_static/image/tool_chain/configuration/data_mapping_5.png)

   b. 选择Port和自动连接规则

   支持筛选功能，选择需要连接的Ports，且可以选择自动匹配或者手动设置匹配规则，点击Next>进入连接确认界面

   ![DataMapping](../../_static/image/tool_chain/configuration/data_mapping_6.png)

   c. 连接确认

   ![DataMapping](../../_static/image/tool_chain/configuration/data_mapping_7.png)

   d. 点击Finish完成连接，完成后可以在主界面看到新的连接关系

5. 信号组连接

   上述小节的操作都以信号为例进行了说明，DataMapping也支持信号组也支持手动连接、断开连接和批量连接操作，由于信号组的连接比较特殊，这里单独进行说明，Port的Element是结构体类型时在连接时需要连接信号组。
   下图是已连接的Port和信号组在DataMapping界面的显示，一对连接关系根据结构体成员的个数显示成多行，Port的Elment与结构体成员与信号组中的信号一一对应。

   ![DataMapping](../../_static/image/tool_chain/configuration/data_mapping_8.png)

   a. 断开连接操作

   断开操作在其中任意一行上右键Remove即可

   ![DataMapping](../../_static/image/tool_chain/configuration/data_mapping_9.png)

   b. 手动连接

   i. 选择Port右键Map

   ![DataMapping](../../_static/image/tool_chain/configuration/data_mapping_10.png)

   ii. 选择信号组和组信号

   在信号组选择界面可以看到Port根据结构体成员展开成了多行，与信号连接类似，如果有自动推荐的连接关系会自动显示，也可以根据需要修改连接的信号组：

   1. 第1步，先双击信号组的框选择想连接的信号组

   2. 第2步，将结构体成员根据需要依次连接至该信号组的组信号，连接须完整，如果有空的结构体成员没有连接，整个连接将无效

   ![DataMapping](../../_static/image/tool_chain/configuration/data_mapping_11.png)

   c. 批量连接

   主要遵循先选择信号组，再依次将结构体成员连接到该信号组的组信号的原则即可。其他的操作与信号的批量连接操作一样，也可以在批量连接时选择的Ports中既有信号也有信号组的，这里不再赘述。

### 3.4. 二级菜单

#### 3.4.1. 调度表配置

1. 在 Os 模块添加一个调度表

   ![Schedule Table Addition](../../_static/image/tool_chain/configuration/sch_tbl_sec_menu_0.png)

2. 点击创建的调度表，配置 Repeating 和 CounterRef

   ![Schedule Table Configuration](../../_static/image/tool_chain/configuration/sch_tbl_sec_menu_1.png)

3. 将调度表关联至 OsApplication

   在 OsApplication 的 OsAppScheduleTableRef 中引用刚创建的调度表

   ![Schedule Table Application Reference](../../_static/image/tool_chain/configuration/sch_tbl_sec_menu_2.png)

4. 点击 Runtime system->Os Configuration，点击刚才创建的调度表

   ![Schedule Table Navigation](../../_static/image/tool_chain/configuration/sch_tbl_sec_menu_3.png)

5. 配置调度表二级菜单

   配置调度表每一列的 Offset 和 Task

   ![Schedule Table Column Configuration](../../_static/image/tool_chain/configuration/sch_tbl_sec_menu_4.png)

   右键添加移除 Task，插入删除行列

   ![Schedule Table Context Menu](../../_static/image/tool_chain/configuration/sch_tbl_sec_menu_5.png)

6. 生成调度表

   生成当前调度表配置

   ![Generate Current Schedule Table](../../_static/image/tool_chain/configuration/sch_tbl_sec_menu_6.png)

   生成所有调度表配置

   ![Generate All Schedule Tables](../../_static/image/tool_chain/configuration/sch_tbl_sec_menu_7.png)

   > **注意**：在进行 Import ASW、TaskMapping 等与周期调度相关的操作后需要重新生成调度表

### 3.5. Log 输出区域

#### 3.5.1. 工具 Log 输出窗口

工具 Log 输出用于记录工具运行日志

![Log Output Window](../../_static/image/tool_chain/configuration/log.png)

#### 3.5.2. Validation 输出窗口

Validation 输出窗口用于记录工具校验结果，在该窗口中存在五个按钮：Warning, Error, All, Ignored 以及 AutoFix 等按钮，相关按钮的功能说明如下：

- 点击 Warning 后，工具会将除警告等级的校验错误过滤掉。
- 点击 Error 后，工具会将除错误等级的校验错误过滤掉。
- 点击 All 后，工具将显示所有等级的校验错误。
- 点击 Ignored 后，工具会显示当前工程已经被忽略的校验错误。
- 点击 AutoFix 后，工具会将按照每条校验错的自动解决建议的第一条的信息，对校验错误进行自动解决，当前自动解决后，ui 不会刷新错误，因此需要手动校验才能显示最新的校验错误信息。

![Validation Output Window](../../_static/image/tool_chain/configuration/validation_output.png)

#### 3.5.3. Properties 输出窗口

Properties 输出用于输出配置项的特性

![Properties Output Window](../../_static/image/tool_chain/configuration/properties.png)

#### 3.5.4. Find 输出窗口

1. Find 输出支持搜索 BSW 模块的配置项及其中的属性。

   ![Find Search Interface](../../_static/image/tool_chain/configuration/find_001.png)

2. 搜索出来的内容，可以用鼠标双击跳转到配置项处。

   ![Find Results Navigation](../../_static/image/tool_chain/configuration/find_002.png)

3. 对于搜索出来的内容，也可以用鼠标右键单击，然后点击"VSCode 打开"，会打开配置项所在的 ARXML 文件，并直接跳转到配置项所在行。

   ![Find VSCode Open Option](../../_static/image/tool_chain/configuration/find_003.png)
   ![Find Output Example in VSCode](../../_static/image/tool_chain/configuration/find_004.png)

## 4. 应用接口参考规范

### 4.1. API 使用说明

#### 4.1.1. API 接口

1. load_project

   | **函数项** | **描述**                                              |
   | :--------- | :---------------------------------------------------- |
   | 函数名     | load_project(project_path:str) -> bool                |
   | 功能       | 按照工程文件的路径去加载工程，初始化 CMD 数据管理模块 |
   | 输入参数   | project_path：工程文件的路径                          |
   | 输出参数   | 无                                                    |
   | 返回值     | True：加载工程成功/False：加载工程失败                |

2. save_project

   | **函数项** | **描述**                                                 |
   | :--------- | :------------------------------------------------------- |
   | 函数名     | save_project(project_path:str) -> bool                   |
   | 功能       | 按照 project_path 存储的各种路径去保存 ARXML 和 log 日志 |
   | 输入参数   | project_path：工程文件的路径                             |
   | 输出参数   | 无                                                       |
   | 返回值     | True：保存成功/False：保存失败                           |

3. import_asw

   | **函数项** | **描述**                                    |
   | :--------- | :------------------------------------------ |
   | 函数名     | import_asw(asw_dir:str) -> bool             |
   | 功能       | 根据 ASW 文件夹路径去导入 ASW 的 ARXML 文件 |
   | 输入参数   | asw_dir：asw 所在的文件夹路径               |
   | 输出参数   | 无                                          |
   | 返回值     | True：导入成功/False：导入失败              |

4. excute_validation

   | **函数项** | **描述**                                                                                                    |
   | :--------- | :---------------------------------------------------------------------------------------------------------- |
   | 函数名     | excute_validation(validation_module_list:list，validation_level:str) -> Union[bool, Tuple[dict, dict]][dict]                          |
   | 功能       | 对关注的模块进行校验得到完整校验详情                                                                        |
   | 输入参数   | 1. validation_module_list(list)：关注的模块列表; 2. validation_level(str)：校验等级，详情见参数说明         |
   | 输出参数   | 无                                                                                                          |
   | 返回值     | 执行失败返回False 或 返回2个字典：1. validation_dict 校验结果字典，key 为模块名，value 为校验结果 True/False; 2. validation_logs 校验结果详情 |

   validation_level 参数说明：

   - "no limit"，只有出现重要校验规则的错误校验项时，认为有校验错误
   - "error"，出现重要校验规则或 error 等级的错误校验项时，认为有校验错误
   - "warnning"，出现重要校验规则、error 等级或 warning 等级的错误校验项时，认为有校验错误

5. excute_generation

   | **函数项** | **描述**                                                                                                                                                                        |
   | :--------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
   | 函数名     | excute_generation(generation_module_list:list, is_debug: bool, forced_codegen: bool) -> list                                                                                    |
   | 功能       | 对关注的模块生成代码                                                                                                                                                            |
   | 输入参数   | 1. generation_module_list：关注的模块列表; 2. is_debug：可选项，生成模式为 debug 或 release 模式，默认值为 release 模式; 4. forced_codegen：可选项，强制生成代码，默认值为 True |
   | 输出参数   | 无                                                                                                                                                                              |
   | 返回值     | 包含关注模块的的生成代码结果的字典，key 为模块名，value 为生成代码结果 True/False                                                                                               |

#### 4.1.2. API 使用示例

通过使用 API 实现同 ui 操作等效的自动化流程，提升用户使用效率

```python
import os
import sys
import time

# 添加python包
CUR_FILE_PATH = os.path.dirname(os.path.realpath(__file__))
sys.path.append(os.path.join(CUR_FILE_PATH, "..", ".."))
sys.path.append(os.path.abspath(os.path.join(CUR_FILE_PATH, "..", "..", "third_party")))

# 导入API包和性能统计包
from cmd_api.auto_cli_api import AutoCliApi
from func_module.health_monitor.perf_record import log_function_stats, record_function_stats
from cmd_adaptor.cmd_interaction.cmd_logger import logger

# 一键集成工程文件路径, PROJECT_PATH字段需要根据用户工程路径进行适配
PROJECT_PATH = os.path.abspath(os.path.join(CUR_FILE_PATH, "../../../../examples/tc397_demo/cfg_prj"))
PROJECT_FILE_PATH = os.path.join(PROJECT_PATH, "tc397_demo.vcosproject")
LOG_APTH = os.path.join(CUR_FILE_PATH)


@log_function_stats
def execute_auto_cli_api_demo_command():
    # 初始化Logger
    # logger.init_default_handler(log_path="")指定Log路径
    logger.init_default_handler()
    logger.info(f"load {PROJECT_FILE_PATH}")

    # 加载工程
    start_time = time.time()
    result = AutoCliApi.load_project(PROJECT_FILE_PATH)
    end_time = time.time()
    if result is False:
        logger.info("load project failed")
    else:
        runtime = end_time - start_time
        logger.info(f"load project succeeded: {runtime}")

    # 导入ASW
    asw_path = os.path.join(PROJECT_PATH, "config", "asw")
    start_time = time.time()
    result = AutoCliApi.import_asw(asw_path)
    end_time = time.time()
    if result is False:
        logger.info("excute import asw failed")
    else:
        runtime = end_time - start_time
        logger.info(f"excute import asw succeeded: {runtime}")


    # 执行Validation
    start_time = time.time()
    result, _ = AutoCliApi.excute_validation(['Rte','Os'], "warnning")
    if not result['Rte']:
        print("validation failed, please check the settings")

    end_time = time.time()
    runtime = end_time - start_time
    logger.info(f"excute validation: {runtime}")


    # 执行代码生成
    start_time = time.time()
    result = AutoCliApi.excute_generation([])
    end_time = time.time()
    runtime = end_time - start_time
    logger.info(f"excute generation c code: {runtime}")

    # 保存工程
    start_time = time.time()
    result = AutoCliApi.save_project()
    end_time = time.time()
    if result is False:
        logger.info("save project failed")
    else:
        runtime = end_time - start_time
        logger.info(f"excute save project succeeded {runtime}")

if __name__ == "__main__":
    execute_auto_cli_api_demo_command()
    record_function_stats()

```

### 4.2. 命令行使用说明

命令行脚本位于：vcos_studio/configurator/cmd_api/auto_cli.py
通过命令行脚本可以执行导入 ARXMl、TaskMapping、校验与代码生成等任务。

#### 4.2.1. 主命令参数

| **选项**      | **必填** | **类型** | **默认值** | **说明**     |
| :------------ | :------- | :------- | :--------- | :----------- |
| -p, --Project | 是       | str      | None       | 指定项目名称 |

示例：

```bash
python auto_cli.py -p demo_project.vcosproject
```

#### 4.2.2. 子命令列表

1. Import

   导入 ASW 或 Mcal 模块到项目中。

   | **选项** | **类型** | **默认值** | **说明**                           |
   | :------- | :------- | :--------- | :--------------------------------- |
   | --asw    | str      | None       | ASW 目录路径                       |
   | --mcal   | str      | None       | Mcal 文件路径                      |
   | --module | str      | None       | 需导入的 Mcal 模块，多个用空格分隔 |

   示例：

   ```bash
   python auto_cli.py -p demo_project.vcosproject Import --asw /path/to/asw
   python auto_cli.py -p demo_project.vcosproject Import --mcal /path/to/mcal.arxml --module "Can,Lin"

   ```

2. AutoMapping

   配置任务与 SWC/Runnable 的映射关系。

   | **选项**      | **类型** | **默认值**  | **说明**                             |
   | :------------ | :------- | :---------- | :----------------------------------- |
   | -m, --Mapping | str      | TaskMapping | 映射类型（如 AutoTaskMappingByFile） |

   示例：

   ```bash
   python auto_cli.py -p demo_project.vcosproject AutoMapping -m AutoTaskMappingByFile
   ```

3. Validate

   验证项目配置。

   | **选项** | **类型** | **默认值** | **说明**                  |
   | :------- | :------- | :--------- | :------------------------ |
   | --module | str      | None       | 需验证的模块（如 Os,Rte） |

   示例：

   ```bash
   python auto_cli.py -p demo_project.vcosproject Validate --module "Os,Rte"
   ```

4. Generate

   生成项目代码。

   | **选项** | **类型** | **默认值** | **说明**                  |
   | :------- | :------- | :--------- | :------------------------ |
   | --module | str      | None       | 需生成的模块（如 Os,Rte） |
   | --debug  | bool     | False      | 生成调试用代码            |
   | --force  | bool     | False      | 强制全量生成（默认增量）  |

   示例：

   ```bash
   python auto_cli.py -p demo_project.vcosproject Generate --force
   ```
