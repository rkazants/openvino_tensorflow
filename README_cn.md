[English](./README.md) | 简体中文

<p align="center">
  <img src="images/openvino_wbgd.png">
</p>

# **OpenVINO™ integration with TensorFlow**

该仓库包含 **OpenVINO™ integration with TensorFlow** 的源代码，该产品专为希望在推理应用中体验[OpenVINO™](https://software.intel.com/content/www/us/en/develop/tools/openvino-toolkit.html) 的TensowFlow*开发人员设计。TensorFlow*应用开发者只需添加2行代码，就可在各种英特尔<sup>®</sup> 计算设备上通过TensorFlow推理应用优化[OpenVINO™](https://software.intel.com/content/www/us/en/develop/tools/openvino-toolkit.html) 工具套件。

    import openvino_tensorflow
    openvino_tensorflow.set_backend('<backend_name>')

该产品优化行内[OpenVINO™](https://software.intel.com/content/www/us/en/develop/tools/openvino-toolkit.html) ，只需稍微修改代码，就可显著增强推理性能。**OpenVINO™ integration with TensorFlow** 可在各种英特尔<sup>®</sup> 芯片上加速很多AI模型**的推理速度，例如：

- 英特尔<sup>®</sup> CPU
- 英特尔<sup>®</sup> 集成 GPU
- 英特尔<sup>®</sup> Movidius™ 视觉处理单元 (VPU)
- 支持 8 颗英特尔 Movidius™ MyriadX VPU 的英特尔<sup>®</sup> 视觉加速器设计（称作 VAD-M 或 HDDL）

[注：为实现最佳的性能、效率、工具定制和硬件控制，我们建议开发人员使用原生 OpenVINO™ API 及其运行时。]

## 安装
### 前提条件

- Ubuntu 18.04, 20.04, macOS 11.2.3 or Windows<sup>1</sup> 10 - 64 bit
- Python* 3.7, 3.8 or 3.9
- TensorFlow* v2.9.1

<sup>1</sup>Windows安装包仅支持Python3.9 

请参阅我们的[交互式安装表](https://openvinotoolkit.github.io/openvino_tensorflow/)，查看安装选项菜单。该表格将帮助您配置安装过程。

**OpenVINO™ integration with TensorFlow** 安装包附带 OpenVINO™ 2022.1.0 版本的预建库，用户无需单独安装 OpenVINO™。该安装包支持：
- 英特尔<sup>®</sup> CPU
- 英特尔<sup>®</sup> 集成 GPU
- 英特尔<sup>®</sup> Movidius™ 视觉处理单元 (VPU)
  

        pip3 install -U pip
        pip3 install tensorflow==2.9.1
        pip3 install openvino-tensorflow==2.1.0

关于在Windows上的安装步骤，请参考 [**OpenVINO™ integration with TensorFlow** for Windows ](docs/INSTALL_cn.md#windows)

如果您想使用Intel<sup>®</sup> 集成显卡进行推理，请确保安装[Intel® Graphics Compute Runtime for OpenCL™ drivers](https://docs.openvino.ai/latest/openvino_docs_install_guides_installing_openvino_linux.html#install-gpu)

如果您想使用支持 Movidius™ (VAD-M)进行推理的英特尔® 视觉加速器设计 (VAD-M) 进行推理，请安装 [**OpenVINO™ integration with TensorFlow** 以及英特尔® OpenVINO™ 工具套件发布版](docs/INSTALL_cn.md#安装-openvino-integration-with-tensorflow-pypi-发布版与独立安装intel-openvino-发布版以支持vad-m)。

更多安装详情，请参阅 [INSTALL.md](docs/INSTALL_cn.md), 更多源构建选项请参阅 [BUILD.md](docs/BUILD_cn.md)

## 配置

安装 **OpenVINO™ integration with TensorFlow** 后，您可以在TensorFlow* 上对训练好的模型运行推理操作。

如要查看 **OpenVINO™ integration with TensorFlow** 是否安装正确，请运行

    python3 -c "import tensorflow as tf; print('TensorFlow version: ',tf.__version__);\
                import openvino_tensorflow; print(openvino_tensorflow.__version__)"

它会生成以下输出：

        TensorFlow version:  2.9.1
        OpenVINO integration with TensorFlow version: b'2.1.0'
        OpenVINO version used for this build: b'2022.1.0'
        TensorFlow version used for this build: v2.9.1
        CXX11_ABI flag used for this build: 1

默认情况下，英特尔<sup>®</sup> CPU 用于运行推理。您也可以将默认选项改为英特尔<sup>®</sup> 集成 GPU 或英特尔<sup>®</sup> VPU 来进行 AI 推理。调用以下函数，更改执行推理的硬件。

    openvino_tensorflow.set_backend('<backend_name>')

支持的后端包括‘CPU'、‘GPU'、‘GPU_FP16'、‘MYRIAD’和‘VAD-M'。

如要确定系统上的哪些处理单元用于推理，可使用以下函数：

    openvino_tensorflow.list_backends()
为了进一步提高性能，建议通过设置环境变量 `OPENVINO_TF_CONVERT_VARIABLES_TO_CONSTANTS=1` 来启用。如欲了解更多 API 调用和环境变量的信息，请查看 [USAGE.md](docs/USAGE_cn.md)。


## 示例

如欲了解 **OpenVINO™ integration with TensorFlow** 的具体功能，请查看[示例](./examples)目录中的演示。

## Docker支持
提供针对Ubuntu* 18.04、Ubuntu* 20.04和TensorFlow* Serving的Dockerfiles，可用来构建用于CPU、GPU、VPU和VAD-M上**OpenVINO™ integration with TensorFlow**的运行时Docker*镜像。
更多详情，请参阅[docker readme](docker/README_cn.md)。

### 预构建镜像

- [Ubuntu 18 runtime image on Docker* Hub](https://hub.docker.com/r/openvino/openvino_tensorflow_ubuntu18_runtime)
- [Ubuntu 20 runtime image on Docker* Hub](https://hub.docker.com/r/openvino/openvino_tensorflow_ubuntu20_runtime)
- [Azure* Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/intel_corporation.openvinotensorflow)

## 在Intel<sup>®</sup> DevCloud上尝试
示例教程也托管在[Intel<sup>®</sup> DevCloud](https://www.intel.com/content/www/us/en/developer/tools/devcloud/edge/build/ovtfoverview.html)。 演示应用程序是使用 Jupyter Notebooks实现的。 您可以在Intel<sup>®</sup> DevCloud节点上执行它们，比较 **OpenVINO™ integration with TensorFlow**、原生TensorFlow和OpenVINO™的性能结果。 

## 许可
**OpenVINO™ integration with TensorFlow** 依照 [Apache 许可版本 2.0](LICENSE)。通过贡献项目，您同意其中包含的许可和版权条款，并根据这些条款发布您的贡献。

## 支持


通过 [GitHub 问题](https://github.com/openvinotoolkit/openvino_tensorflow/issues)提交您的问题、功能请求和漏洞报告。

## 如何贡献

我们欢迎您为 **OpenVINO™ integration with TensorFlow** 做出社区贡献。如您在改进方面有好的想法：

* 请通过 [GitHub 问题](https://github.com/openvinotoolkit/openvino_tensorflow/issues)分享您的建议。
* 提交 [pull 请求](https://github.com/openvinotoolkit/openvino_tensorflow/pulls)。

我们将以最快的速度审核您的贡献！如果需要进行其他修复或修改，我们将为您提供引导和反馈。贡献之前，请确保您可以构建 **OpenVINO™ integration with TensorFlow** 并使用您的修复/补丁运行所有示例。如果您想推出重要特性，可以创建特性测试案例。您的 pull 请求经过验证之后，我们会将其合并到存储库中，前提是 pull 请求满足上述要求并经过认可。

---
\* 其他名称和品牌可能已被声明为他人资产。
