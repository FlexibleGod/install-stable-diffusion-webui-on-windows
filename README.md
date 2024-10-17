# AI 绘图入门：搭建 Stable Diffusion WebUI

视频：[AI 绘图入门：搭建 Stable Diffusion WebUI](https://www.bilibili.com/video/BV1jPyuYMEuf/)

## 安装步骤

0. 国内访问 github.com 拉取代码可能会出现网络问题，强烈建议拉到本文档末尾，查看“修改系统 hosts 加速 GitHub 访问”

1. 安装工具 git 和 miniconda3

```
# 这里使用 scoop 来安装 git 和 miniconda3
# 不了解 scoop 请看我的这个短视频 https://www.bilibili.com/video/BV1ehtqesETb/

# 安装 git，用于从 GitHub 克隆/拉取项目代码
scoop install git

# 安装 miniconda3, 用于创建/管理 Python 程序运行环境
# 安装完成后需要执行一下 conda init 命令，添加 miniconda3 到环境变量
# 环境变量添加后，记得重新打开 PowerShell 窗口才能生效。
scoop install miniconda3
conda init
```

2. 克隆代码，创建 Python 运行环境

```
# 进入存放项目的文件夹，我这里是 .\Downloads\AI-Tools
cd .\Downloads\AI-Tools
# 克隆 stable-diffusion-webui 项目的代码仓库到本地 SD-WebUI 目录
git clone https://github.com/AUTOMATIC1111/stable-diffusion-webui.git SD-WebUI

# 创建一个名为 SD-WebUI 的 Python 运行环境，Python 版本为 3.10
# 注意：目前 SD WebUI 项目仅支持 Python 3.10，不要用太新的 Python 版本
conda create --name SD-WebUI python=3.10

# 这里推荐为 Python pip 配置一个阿里云下载源来加速依赖包下载
# 先激活运行环境，然后使用 `pip config` 来设置下载源
conda activate SD-WebUI
pip config set global.index-url https://mirrors.aliyun.com/pypi/simple/
```

3. 编辑新的启动文件

```
# Windows 下 SD WebUI 提供的默认启动文件是 webui-user.bat
# 由于我们使用了 conda 环境，需要在启动前激活运行环境
# 这里复制一份 webui-user.bat 并命名为 webui-user.custom.bat 作为新的启动文件
# 修改后的启动文件内容如下：

@echo off

set PYTHON=
set GIT=
set VENV_DIR=
set COMMANDLINE_ARGS=--xformers --opt-split-attention

set SAFETENSORS_FAST_GPU=1

call conda activate SD-WebUI
call webui.bat
```

双击运行 webui-user.custom.bat 即可启动 SD WebUI

```
# 初次启动 SD WebUI 时，会自动安装所需的 Python 依赖包，请耐心等待。
```

```
# 如何更新 SD-WebUI 到最新版本？
# 只要在 PowerShell 中进入 SD-WebUI 目录，执行 git pull 即可。
cd \PATH\TO\YOUR\SD-WebUI
git pull
```

## 修改系统 hosts 加速 GitHub 访问

打开 <https://gitlab.com/ineo6/hosts>，在文件列表找到它的 hosts 文件，把里面的内容复制粘贴到系统 hosts 文件 `C:\Windows\System32\drivers\etc\hosts` 的末尾即可。注意：系统 hosts 文件的修改需要管理员权限，可以`以管理员身份运行`记事本来打开编辑它。
