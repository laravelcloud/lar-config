# lar-config

## 统一配置
> 配置管理组件，让你可以把配置放到远程服务器，集中化管理集群配置。

## 思路
采用修改本地的`.env`文件的方式， 从远程配置中心获取配置结果写入`.env`。
以`Consul`举例，当远程主动触发时，通过`Consul`通知到所有节点，节点通过curl的方式更新配置。

```sequence
participant 应用
participant 容器
participant 配置中心
participant Consul

    应用->>容器: 启动N个
    Note right of 容器: 启动laravelcloud守护进程
    应用容器->>配置中心: 注册
    配置中心->>Consul: 变更后主动触发
    
    loop 变更并行通知
        Consul->>容器: 通知变更
        Consul->>容器: 通知变更
        Consul->>容器: 通知变更
    end
    
    容器->>容器: 变更.env
    容器->>应用: 结束
```
## 方案
待补充

## 代办
Consul、ZooKeeper、etcd 应该怎样选择？

## 参考
- Consul和ZooKeeper、Doozerd、Etcd的区别(http://dockerone.com/article/300)
