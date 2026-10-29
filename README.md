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
   示例文件名：`torch-2.15.0-cp313-cp313-macosx_11_0_x86_64.whl`
2. 使用 `pip` 安装：
    ```bash
    pip install torch-2.15.0-cp313-cp313-macosx_11_0_x86_64.whl
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

构建矩阵为普通 CPython **3.11–3.15**、Intel **x86_64**，wheel 的部署目标为 **macOS 11.0**，不包含 free-threaded Python。Python 3.15 已于 [2026-10-09 正式发布](https://www.python.org/downloads/release/python-3150/)；[PyTorch 2.15.0 发布说明](https://github.com/pytorch/pytorch/releases/tag/v2.15.0)和[源码元数据](https://github.com/pytorch/pytorch/blob/v2.15.0/pyproject.toml)明确支持 Python 3.15。

工作流使用 [macos-15-intel（x64）](https://github.com/actions/runner-images#available-images)和 Xcode 16.4。最近一次构建使用的[镜像 20260824.0482.1](https://github.com/actions/runner-images/blob/macos-15/20260824.0482/images/macos/macos-15-Readme.md)尚未预装 Python 3.15，因此通过 `actions/setup-python@v6` 显式选择 x64 运行时；GitHub 已提供 [Python 3.15.2 的 darwin-x64 安装包](https://github.com/actions/python-versions/releases/tag/3.15.2-40340363276)。

截至 2026-10-29，[本项目 2.15.0 Release](https://github.com/Morton-Li/PyTorch-MacOS-Builder/releases/tag/v2.15.0)已有 Python 3.11–3.14 wheel；新增的 3.15 构建配置尚待 macOS CI 验证，没有已发布的 `cp315` wheel。现有逻辑会跳过已发布版本，新增矩阵不会自动补齐旧 Release；手动构建仅上传 artifact，不发布 Release。安装时以 Releases 的实际资产为准。

The build matrix targets regular CPython **3.11–3.15** on Intel **x86_64**, with a **macOS 11.0** wheel deployment target. PyTorch 2.15 officially supports Python 3.15. The `macos-15-intel` image does not preinstall it, so `actions/setup-python@v6` installs the available x64 runtime. As of 2026-10-29, this project's 2.15.0 Release contains only Python 3.11–3.14 wheels; the new 3.15 configuration still needs macOS CI validation. Existing releases are skipped, and manual builds upload artifacts without publishing releases. Free-threaded builds are not included.

本项目构建的 PyTorch 安装包具有以下特性：

* ✅ 使用 **Intel MKL** 作为 BLAS 后端，提供更高的数值计算性能
* ✅ 启用 **OpenMP** 并行支持，充分利用多核 CPU 加速张量运算
* ✅ 启用 **oneDNN** 支持，自动加速部分 CNN、线性层等算子，提升 CPU 上的推理性能
* ✅ 启用 **Metal Performance Shaders (MPS)** 后端；PyTorch 2.15 的 MPS 运行时要求 **macOS 15+** 及兼容 GPU，wheel 的 macOS 11.0 部署目标不代表 MPS 在旧系统上可用

The PyTorch wheels built by this project have the following features:

* ✅ **Intel MKL** as the BLAS backend for high-performance numerical operations
* ✅ **OpenMP** support enabled to accelerate tensor computations on multi-core CPUs
* ✅ **oneDNN** support enabled to accelerate CPU inference for convolution and linear layers
* ✅ **Metal Performance Shaders (MPS)** backend enabled; PyTorch 2.15 requires **macOS 15+** and a compatible GPU for MPS. The macOS 11.0 wheel deployment target does not imply MPS availability on older systems

---

## 🤝 鸣谢 Acknowledgements

- [PyTorch](https://github.com/pytorch/pytorch)
- [GitHub Actions](https://github.com/features/actions)
