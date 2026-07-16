

https://github.com/user-attachments/assets/eb026c40-51e1-47bb-b0c1-bc6235a54679





# Kaggle-reproduction-of-LingBot-Map




https://github.com/user-attachments/assets/d5d92d5d-d5f4-4cf0-a71d-5247b65bd8db






https://github.com/user-attachments/assets/de13fe4a-a6dc-4b84-8cee-cc724dcecd18






原视频

https://github.com/user-attachments/assets/a8925bd5-bdf7-410f-8f83-05a44e534dab






硬件：Kaggle T4 GPU。

开发环境：本地VSCode + Remote-Tunnels插件，远程连接Kaggle Notebook。

连接方案：可采用VSCode官方Remote Tunnels方案。

软件依赖：LingBot-Map的官方环境要求。

Python 3.12.8（实验性，可兼容）

PyTorch 2.8.0




在kaggle创建一个新的notebook
在新建的单元格上输入一个脚本
让本地vscode连接kaggle云端
# 下载 VS Code CLI
# 启动隧道（会输出一个授权链接）

```python
import subprocess
import os

if not os.path.exists('code'):
    print("正在下载 VS Code CLI...")
    subprocess.run("curl -Lk 'https://code.visualstudio.com/sha/download?build=stable&os=cli-alpine-x64' --output vscode_cli.tar.gz", shell=True)
    subprocess.run("tar -xf vscode_cli.tar.gz", shell=True)
    subprocess.run("rm vscode_cli.tar.gz", shell=True)
    print("下载完成。")

print("正在启动 Remote Tunnels, 请稍候...")
subprocess.run("./code tunnel --accept-server-license-terms", shell=True)
```

执行后会输出To grant access to the server, please log into https://github.com/login/device and use code xxxx-xxxx
点击https://github.com/login/device链接输入代号 xxxx-xxxx

登陆github账号继续，需要与kaggle同账号

接着，打开vscode，点击扩展商店进行安装Remote - Tunnels
安装后同时按住窗口键+shift+p，输入隧道，点击连接至隧道，选择github，选择对应的隧道即可与kaggle成功连接

接着打开vscode终端就可以开始搭建环境了

```python
apt-get install -y ffmpeg libsm6 libxext6
```

```python
pip install torch==2.8.0 torchvision==0.23.0 --index-url https://download.pytorch.org/whl/cu128
```

```python
pip install onnxruntime-gpu
```



```python
pip install --index-url https://pypi.org/simple flashinfer-python#可以不安装，因为t4可能不支持，会出现报错
```


#克隆项目代码

```python
git clone https://github.com/Robbyant/lingbot-map.git
```

```python
pip install --index-url https://pypi.org/simple flashinfer-python#可以不安装，因为t4可能不支持，会出现报错
```



#进入lingbot-map目录

```python
cd lingbot-map
```


#创建checkpoints并下载权重文件

```python
from kaggle_secrets import UserSecretsClient
import subprocess
user_secrets = UserSecretsClient()
mkdir checkpoints
wget -O checkpoints/lingbot-map.pt https://huggingface.co/robbyant/lingbot-map/resolve/main/lingbot-map.pt
```




#用来存放你的视频
```python
mkdir video
```

#安装可视化依赖

```python
pip install -e ".[vis]”
```

运行推理脚本

```python
python demo.py \
    --model_path path/to/your.pt \
    --video_path path/to/your video \
    --use_sdpa
```




```python
wget -q https://github.com/cloudflare/cloudflared/releases/latest/download/cloudflared-linux-amd64
```

成功执行完后应该会有网址，但是这个网址由于kaggle的限制是打不开的

需要点击加号再开一个bash终端


进入lingbot-map目录

```python
wget -q https://github.com/cloudflare/cloudflared/releases/latest/download/cloudflared-linux-amd64
```

#添加权限

```python
chmod +x cloudflared-linux-amd64
```



#执行后会输出很多INFO

```python
./cloudflared-linux-amd64 tunnel --url http://localhost:8080 --protocol http2
```



选择https：//charitable-cable-cables-patents-openings.trycloudflore.com（具体域名会有区别）

打开链接后会进入viser可视化界面
就可以进行流式三维重建了





Attention！！！
视频不要超过70s，否则会导致OOM！




















