# 基础架构
智臻链BaaS平台主要组件：

后台服务：负责管理维护多个Kubernetes集群，负责BaaS平台与JDCloud资源层交互，负责监控及搜集用户区块链网络的运行状态。

区块链网络管理：负责处理用户通过界面配置的创建区块链网络的请求。当区块链网络创建完成后，与区块链网络中的agent实时通信，转发用户通过管理console对区块链网络的操作，并返回操作结果。

![图片](../../../../image/JD-Blockchain-Open-Platform/Introduction/Pic/TIM截图20190328185458.png)
