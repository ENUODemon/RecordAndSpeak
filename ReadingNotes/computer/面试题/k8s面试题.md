https://www.cnblogs.com/threecha/p/13709482.html

https://www.cnblogs.com/threecha/p/13649320.html

1 什么是k8s 为什么用k8s：
一个开源的容器集群管理平台【容器编排工具】，可提供容器集群的自动部署，扩缩容，维护等功能。分为管理节点Master和工作节点Node。在我们的项目中主要解决了环境一致性的问题，通过CI/CD使得运维部署变得简单起来，以及自动部署，故障监控，自动扩缩容。可以提升开发效率。

2 k8s有那些组件：

etcd保存了整个集群的状态；
apiserver提供了资源操作的唯一入口，并提供认证、授权、访问控制、API注册和发现等机制；
controller manager负责维护集群的状态，比如故障检测、自动扩展、滚动更新等；
scheduler负责资源的调度，按照预定的调度策略将Pod调度到相应的机器上；
kubelet负责维护容器的生命周期，同时也负责Volume（CVI）和网络（CNI）的管理；
Container runtime负责镜像管理以及Pod和容器的真正运行（CRI）；
kube-proxy负责为Service提供cluster内部的服务发现和负载均衡

3 Node&Pod&container之间的关系：Node一般指工作节点包含多个Pod Pod中包含多个Container,Pod中的container共享同一个网络命名空间。

4 什么是SVC: SVC是对一组功能相似的Pod资源的抽象，相当于一组服务的负载均衡

5 k8s的网络模型：IP-Per-Pod 每个Pod有独立的Ip地址，无论是否处于同一个Node节点，Pod可以通过IP相互访问，且Pod和容器的地址和外部看到的地址是同一个地址

6 Pod SVC Node Container 之间如何相互访问：

同Pod内的容器：同一个Pod的容器共享同一个网络命名空间可以直接进行通讯
同Node内不同Pod的容器：多个Pod都关联在同一个Docker0网桥上，通过docker0网桥完成相互通讯。
不同Node内Pod的容器：不同Node上的docker0可能会相同，PodIP和docker0是同网段的，所以需要将PodIP和NodeIP进行关联且保障唯一，不同Pod之间的数据通过物理机的端口进行转发即可完成通讯。


对SVC的考察
SVC是k8s中的核心概念 这里涉及知识点众多 常见的面试考点如下

什么是SVC? 如何创建SVC?
使用SVC创建多个副本和使用RC创建多个副本有什么差异？
SVC有哪几种类型？
SVC 负载分发策略有那些？
集群外如何访问SVC?
SVC:是对一组功能相似的Pod资源的抽象，相当于一组服务的负载均衡。可以使用配置文件的方式创建也可以使用命令创建kubectl expose
SVC和RC提供服务的差距： RC创建的服务PodIP可能会变。SVC提供的clusterIP不会。通过Iptables的NAT转换重定向到本地端口，在均衡到后端Pod。
svc的几种类型： ClusterIp/NodePort/LoadBalancer/ExternalName

ClusterIp 默认类型 分配的一个虚拟地址，内部可以相互访问，外部不行
NodePort 将SVC端口号映射到物理机
LoadBalancer 基于NodePort，云服务商在外部创建了一个负载均衡到Pod
ExternalName 将外部地址经过集群内部的再一次封装(实际上就是集群DNS服务器将CNAME解析到了外部地址上)，实现了集群内部访问即可。

svc负载分发策略： RoundRobin/SessionAffinity/自定义实现【基于标签选择器】

集群外部访问： 端口映射到物理机即可

5.2 Pod考察
Pod和静态Pod的区别
生命周期和重启策略 【这里可扩展 不同控制器对Pod的重启策略要求】
Pod如何健康检查？
Pod的调度方式？【扩展调度算法】
Pod如何扩缩容？【扩展 RC和RS的差异】

5.3 基础原理类考察
主要考察对基本组件的理解 和原理分析

API Server
Controller Manager【Replication Controller/Node Controller/ResourceQuota Controller/Namespace Controller/SVC Controller& Endpoint Controller】
Scheduler
Kubelet 【Pod健康检查 资源监控】
Kube-Proxy
k8s-DNS & Iptables差异
k8s中Ingress是什么
简述k8s中的如下属性及其作用resources tolerations affinity
k8s中pod、rs、deployment、hpa的基本概念，以及他们之间的关系
答案
待补充 --详见《k8s权威指南》读书笔记

5.4 网络原理类考察
主要考察对基本组件的理解 和原理分析

k8s的网络模型是什么？
Docker的网络基础是什么？
Docker的网络模型和局限？
k8s的网络组件之间是如何通讯的？
外部如何访问k8s集群？
有那些开源组件支持k8s网络模型？
答案
待补充 --详见《k8s权威指南》读书笔记