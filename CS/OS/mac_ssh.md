MacOS SSH在使用终端连接云服务器时，如果每次连接后断开、再连不上，通常是因为SSH连接没有正确释放或系统网络缓存未清理。



macOS 在 SSH 断开时可能残留 socket 或占用端口。

**解决：**

```bash
# 结束所有 ssh 残留进程
sudo pkill ssh
sudo pkill -9 ssh

# 或者清理 SSH agent
eval "$(ssh-agent -k)"
eval "$(ssh-agent -s)"
```