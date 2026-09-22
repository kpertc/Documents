OpenClaw — CLI 工具：把 agent 跑成常驻 gateway 服务，并接入 IM channel（Feishu 等）

```sh
# installed the gateway as a background service, automatically on boot, and keep running
openclaw onboard --install-daemon
```

```
openclaw onboard     

start
openclaw gateway

openclaw gateway restart

openclaw gateway stop

openclaw tui
openclaw dashboard
```
### Feishu
```
openclaw config set channels.feishu.appId "<YOUR_FEISHU_APP_ID>"
openclaw config set channels.feishu.appSecret "<YOUR_FEISHU_APP_SECRET>"
openclaw config set channels.feishu.enabled true
openclaw config set channels.feishu.connectionMode websocket
```
> secret 写在命令行会留在 shell history 和进程列表里 → 用环境变量或直接改配置文件