MacOS SSH在使用终端连接云服务器时，如果每次连接后断开、再连不上，通常是因为SSH 连接没有正确释放或系统网络缓存未清理。

* 第一次连接可以正常：

  ```bash
  ssh root@<ip地址>
  ```

  ✅ 可以登录。

* 退出后再连接：

  ```bash
  ssh root@<ip地址>
  ```

  ❌ 卡住或提示：

  ```
  Connection closed by <ip> port 22
  Connection refused
  ```

* 只有重启 Mac 后才能再次连接。

---

### 1️⃣ **SSH 残留进程或 socket 未释放**

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

然后再尝试重新连接：

```bash
ssh root@<ip地址>
```

---