# 服务器环境配置及Jupyter远程连接服务器

2025.6.26

**以实验室服务器为例**

## conda虚拟环境搭建

在自己的服务器账号的主目录下安装`conda`环境, 这里以`miniconda`为例

```bash
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
```

执行安装

```bash
bash ~/Miniconda3-latest-Linux-x86_64.sh
```

激活环境: 或切换到`conda`里的`bin`目录执行`activate`

```bash
source ~/conda/bin/activate
```

创建虚拟环境: `you_env_name`改成你自己的虚拟环境名称

```bash
conda create -n you_env_name python=3.12
```

安装相关依赖时用`pip`或者`conda`统一一下, 一些包用`pip`, 一些用`conda`后续可能会有点bug

## Jupyter连接服务器

服务器端安装Jupyter依赖

```bash
pip install Jupyter
```

生成配置文件(首次使用时配置)

```bash
jupyter notebook --generate-config
```

设置Jupyter密码

```bash
jupyter notebook password
```

查看`8888`端口是否被占用, 若被占用下一步就换一个端口, 本文下一步以1207端口为例

```bash
ss -tulpn | grep :8888
```

后台启动Jupyter (`关闭 SSH 会话后仍保持运行`)

```bash
nohup jupyter notebook --no-browser --port=1207 &
```

客户端连接服务器: 输入完这个以后会提示输入服务器用户密码,输入即可. 

注意: 

​	输入完成功命令行不会有别的提示

​	`Windows10`: 光标在顶格跳动

​	`MacOS`: 新起一行

```bash
ssh -N -f -L localhost:8888:localhost:1207 -p 22 fjl@10.2.1.60
```

成功后客户端浏览器输入`localhost:8888`看到Jupyter输入密码界面, 输入先前设置的密码即可