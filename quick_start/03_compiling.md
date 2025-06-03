# 工程编译

如果您仅需要编译VCOS相关代码，请按照本文介绍的方法，使用haloosspace/vcos/build/vcos_build.py指定工程进行编译，编译说明参考[VCOS工程编译说明](https://gitee.com/haloos/vcos_build/blob/master/README.md)；如果需要编译全量的HaloOS代码，请跳转至[HaloOS工程编译](https://gitee.com/haloos/docs/blob/master/quick_start/02_compiling.md)

## 1. 编译环境准备

### 1.1. 安装编译环境

> 安装编译环境前，需要先按照[配置工具安装](./02_installing.md)要求，执行Studio依赖插件的安装

在`haloosspace`根目录，执行以下命令安装编译工具链：

```bash
python ./vcos/build/compiling_env.py
```

该命令依次执行以下安装步骤：

- 安装CMake工具，并将安装路径添加到PATH环境变量
- 安装kconfiglib工具
- 安装make工具，并设置`MAKE_TOOL_PATH`环境变量
- 安装ninja工具，并设置`NINJA_TOOL_PATH`环境变量
- 安装tricore-gcc编译工具链，并将安装路径添加到PATH环境变量
- 安装arm-gcc编译工具链，并将安装路径添加到PATH环境变量
- 安装docker工具

## 2. 编译

### 2.1. 一键编译

> Windows系统需要以【管理员权限】打开PowerShell，并切换到`haloosspace`目录

- 切换到`haloosspace/vcos/build`目录：

  ```bash
  cd ./vcos/build
  ```

- 编译multicore_com_demo应用：配置使用E3650_DEV_KIT板级配置，使用gcc编译器，使用ninja作为make工具，使用实际开发板运行

  ```bash
  python vcos_build.py -app_name multicore_com_demo -board_name e3650_dev_kit -compiler gcc -maketool ninja -sim 0 -all
  ```

  该命令会依次执行以下操作：
  - 根据multicore_com_demo应用的E3650_DEV_KIT板级配置生成动态代码
  - 通过CMake调用Ninja工具自动化构建
  - 最终编译生成镜像文件
  - 编译结果默认保存在`haloosspace/output/multicore_com_demo_E3650_DEV_KIT_gcc`目录下

### 2.2. 编译命令说明

- 添加应用子目录，重新生成cmake：

  ```bash
  python vcos_build.py -app_name multicore_com_demo -board_name e3650_dev_kit -clean  # 清除编译产物
  python vcos_build.py -app_name multicore_com_demo -board_name e3650_dev_kit -gcmake  # 生成cmake
  python vcos_build.py -app_name multicore_com_demo -board_name e3650_dev_kit -fc  # 执行全量编译
  ```

- 修改应用代码后增量编译：

  ```bash
  python vcos_build.py -app_name multicore_com_demo -board_name e3650_dev_kit -ic
  ```
