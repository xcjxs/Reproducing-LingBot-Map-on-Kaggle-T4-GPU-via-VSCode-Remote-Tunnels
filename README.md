# Kaggle-reproduction-of-LingBot-Map




https://github.com/user-attachments/assets/d5d92d5d-d5f4-4cf0-a71d-5247b65bd8db


硬件：Kaggle T4 GPU。

开发环境：本地VSCode + Remote-Tunnels插件，远程连接Kaggle Notebook。

连接方案：可采用VSCode官方Remote Tunnels方案。

软件依赖：LingBot-Map的官方环境要求。

Python 3.12.8（实验性，可兼容）

PyTorch 2.8.0

其他依赖见 requirements.txt



在kaggle创建一个新的notebook
在新建的单元格上输入一个脚本
让本地vscode连接kaggle云端

import subprocess
import os

# 下载 VS Code CLI
if not os.path.exists('code'):
    print("正在下载 VS Code CLI...")
    subprocess.run("curl -Lk 'https://code.visualstudio.com/sha/download?build=stable&os=cli-alpine-x64' --output vscode_cli.tar.gz", shell=True)
    subprocess.run("tar -xf vscode_cli.tar.gz", shell=True)
    subprocess.run("rm vscode_cli.tar.gz", shell=True)
    print("下载完成。")

# 启动隧道（会输出一个授权链接）
print("正在启动 Remote Tunnels，请稍候...")
subprocess.run("./code tunnel --accept-server-license-terms", shell=True)


执行后会输出To grant access to the server, please log into https://github.com/login/device and use code xxxx-xxxx
点击https://github.com/login/device链接输入代号 xxxx-xxxx

登陆github账号继续，需要与kaggle同账号

接着，打开vscode，点击扩展商店进行安装Remote - Tunnels
安装后同时按住窗口键+shift+p，输入隧道，点击连接至隧道，选择github，选择对应的隧道即可与kaggle成功连接

接着打开vscode终端就可以开始搭建环境了


apt-get install -y ffmpeg libsm6 libxext6
pip install torch==2.8.0 torchvision==0.23.0 --index-url https://download.pytorch.org/whl/cu128
pip install onnxruntime-gpu
pip install --index-url https://pypi.org/simple flashinfer-python#可以不安装，因为t4可能不支持，会出现报错


#克隆项目代码
git clone https://github.com/Robbyant/lingbot-map.git

#进入lingbot-map目录
cd lingbot-map


from kaggle_secrets import UserSecretsClient
import subprocess
user_secrets = UserSecretsClient()
mkdir checkpoints用来存放模型权重
#下载权重
wget -O checkpoints/lingbot-map.pt https://huggingface.co/robbyant/lingbot-map/resolve/main/lingbot-map.pt



mkdir video用来存放你的视频



pip install -e ".[vis]”安装可视化依赖





运行推理脚本
python demo.py \
    --model_path path/to/your.pt \
    --video_path path/to/your video \
    --use_sdpa


成功执行完后应该会有网址，但是这个网址由于kaggle的限制是打不开的

需要点击加号再开一个bash终端


进入lingbot-map目录
wget -q https://github.com/cloudflare/cloudflared/releases/latest/download/cloudflared-linux-amd64

#添加权限
chmod +x cloudflared-linux-amd64


./cloudflared-linux-amd64 tunnel --url http://localhost:8080 --protocol http2
执行后会输出很多INFO


选择https：//charitable-cable-cables-patents-openings.trycloudflore.com（具体域名会有区别）

打开链接后会进入viser可视化界面
就可以进行流式三维重建了





Attention！！！
视频不要超过70s，否则会导致OOM！




















