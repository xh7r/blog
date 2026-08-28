# system resource
- htop
- nvidia-smi



# tmux
> SSH 远程连接断开后，希望当前终端里的命令继续运行，并且下次连回来还能继续看到原来的会话

 **`tmux`**

```bash
tmux new -s train
```

本地 Mac/PC 关闭 SSH、网络断开，都不会影响 `tmux` 里的训练。

下次重新 SSH：
然后：

```bash
tmux attach -t train
```

就能重新回到之前的终端。
