github地址：

https://github.com/chaosblade-io/chaosblade-box-agent/releases/tag/0.4.x-main

一般安装在/opt/chaos下，chaosagent可执行文件。

启动命令：

```
nohup /opt/chaos/chaosagent --namespace default --appInstance chaos-default-app --appGroup chaos-default-app-group --port 19527 --agentId 1534098642133823490 --transport.endpoint 10.18.30.79:9090 &
```

