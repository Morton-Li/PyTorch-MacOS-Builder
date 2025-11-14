# PyTorch macOS Builder

> 🔧 自动构建 PyTorch 官方发行版本的 macOS 平台兼容 `.whl` 安装包。  
> 🔧 Automatically build official PyTorch release `.whl` packages for macOS

---

## 📦 项目简介 Project Introduction

[本项目](https://github.com/Morton-Li/PyTorch-MacOS-Builder)通过 GitHub Actions 定期获取 [PyTorch 官方仓库](https://github.com/pytorch/pytorch) 的最新稳定版本，并自动构建适用于 **macOS** 的 Python wheel 安装包。

构建产物为**多 Python 版本**的 `.whl` 文件，便于在老款 Mac 上继续使用高版本 PyTorch。

[This project](https://github.com/Morton-Li/PyTorch-MacOS-Builder) uses GitHub Actions to periodically fetch the latest stable release from the [official PyTorch repository](https://github.com/pytorch/pytorch), and automatically builds Python wheel packages for **macOS**.

The output includes `.whl` files for **multiple Python versions**, allowing users to continue using newer versions of PyTorch on older Mac machines.

---

## 🛠 使用方式 How to Use

1. 从 [Releases 页面](../../releases) 下载你所需版本的 `.whl`：  
   示例文件名：`torch-2.9.1-cp312-cp312-macosx_11_0_x86_64.whl`
2. 使用 `pip` 安装：
    ```bash
    pip install torch-2.9.1-cp312-cp312-macosx_11_0_x86_64.whl
    ```
3. 验证是否安装成功：
   ```bash
    python -c "import torch; print(torch.__version__)"
    ```

---

## 💡 为什么需要这个项目 Why This Project Matters

由于 PyTorch 从 2.3 版本开始不再支持 Intel 架构的 macOS，而部分旧款 Mac 用户仍需使用较新 PyTorch，本项目旨在填补官方构建缺失，**延续 PyTorch 对 Intel Mac 的支持周期**。

Starting from version 2.3, PyTorch has dropped support for Intel-based macOS. This project aims to fill the gap by **extending PyTorch support for Intel Macs**, helping users continue to benefit from newer versions.

---

## ⚙️ 构建特性 Build Features

本项目构建的 PyTorch 安装包具有以下特性：

* ✅ 使用 **Intel MKL** 作为 BLAS 后端，提供更高的数值计算性能
* ✅ 启用 **OpenMP** 并行支持，充分利用多核 CPU 加速张量运算
* ✅ 启用 **oneDNN** 支持，自动加速部分 CNN、线性层等算子，提升 CPU 上的推理性能

The PyTorch wheels built by this project have the following features:

* ✅ **Intel MKL** as the BLAS backend for high-performance numerical operations
* ✅ **OpenMP** support enabled to accelerate tensor computations on multi-core CPUs
* ✅ **oneDNN** support enabled to accelerate CPU inference for convolution and linear layers

---

## 🤝 鸣谢 Acknowledgements

- [PyTorch](https://github.com/pytorch/pytorch)
- [GitHub Actions](https://github.com/features/actions)
