# Docker 核心技术与实现原理
https://draveness.me/docker/

1.Docker常用命令?

docker pull 拉取或者更新指定镜像

docker push 将镜像推送至远程仓库

docker rm 删除容器

docker rmi 删除镜像

docker images 列出所有镜像

docker ps 列出所有容器



2.docker是怎么工作的?

实际上docker使用了常见的CS架构，也就是client-server模式，docker client负责处理用户输入的各种命令，比如docker build、docker run，真正工作的其实是server，也就是docker demon，值得注意的是，docker client和docker demon可以运行在同一台机器上。

Docker是一个Client-Server结构的系统，Docker守护进程运行在主机上， 然后通过Socket连接从客户端访问，守护进程从客户端接受命令并管理运行在主机上的容器。守护进程和客户端可以运行在同一台机器上。



3.docker容器之间怎么隔离?

Linux中的PID、IPC、网络等资源是全局的，而NameSpace机制是一种资源隔离方案，在该机制下这些资源就不再是全局的了，而是属于某个特定的NameSpace，各个NameSpace下的资源互不干扰。

虽然有了NameSpace技术可以实现资源隔离，但进程还是可以不受控的访问系统资源，比如CPU、内存、磁盘、网络等，为了控制容器中进程对资源的访问，Docker采用control groups技术(也就是cgroup)，有了cgroup就可以控制容器中进程对系统资源的消耗了，比如你可以限制某个容器使用内存的上限、可以在哪些CPU上运行等等。

有了这两项技术，容器看起来就真的像是独立的操作系统了。



4.容器与主机之间的数据拷贝命令?

Docker cp命令用于穷奇与主机之间的数据拷贝

主机到哦容器：docker cp /www 96f7f14e99ab:/www/

容器到主机：docker cp 96f7f14e99ab:/www /tmp



5.如何在生产中监控docker?

Docker提供docker:stats和docker事件等工具来监控生产中的docker。我们可以使用这些命令获取重要统计数据的报告。

Docker统计数据：当我们使用容器ID调用docker stats时，我们获得容器的CPU，内存使用情况等。它类似于Linux中的top命令。

Docker事件：docker事件是一个命令，用于查看docker守护程序中正在进行的活动流。一些常见的docker事件是：attach，commit，die，detach，rename，destroy等。我们还可以使用各种选项来限制或过滤我们感性其的事件。



6.DockerFile中的命令COPY和ADD命令有什么区别?

COPY和ADD的区别时COPY的SRC只能是本地文件，其他用法一致。
一般而言，虽然ADD并且COPY在功能上类似，但是首选COPY。

那是因为它比ADD更易懂。COPY仅支持将本地文件复制到容器中，而ADD具有一些功能(如仅限本地的tar提取和远程URL支持)，这些功能并不是很明显。因此，ADD的最佳用途是将本地tar文件自动提取到镜像中，如ADD rootfs.tar.xz /。



7.一个完整的Docker由哪些部分组成?

1)DockerClient客户端

2)Docker Daemon守护进程

3)Docker Image镜像

D)4ockerContainer容器 



8.进入容器的方法有哪些?

1、使用 docker attach 命令

2、使用 exec 命令，例如docker exec -i -t 784fd3b294d7 /bin/bash



9.Docker与虚拟机有何不同?

Docker不是虚拟化方法。它依赖于实际实现基于容器的虚拟化或操作系统级虚拟化的其他工具。为此，Docker最初使用LXC驱动程序，然后移动到libcontainer现在重命名为runc。Docker主要专注于在应用程序容器内自动部署应用程序。应用程序容器旨在打包和运行单个服务，而系统容器则设计为运行多个进程，如虚拟机。因此，Docker被视为容器化系统上的容器管理或应用程序部署工具。

1)与虚拟机不同，容器不需要引导操作系统内核，因此可以在不到一秒的时间内创建容器。此功能使基于容器的虚拟化比其他虚拟化方法更加独特和可取。

由于基于容器的虚拟化为主机增加了很少或没有开销，因此基于容器的虚拟化具有接近本机的性能

2)对于基于容器的虚拟化，与其他虚拟化不同，不需要其他软件。

主机上的所有容器共享主机的调度程序，从而节省了额外资源的需求。

3)与虚拟机映像相比，容器状态(Docker或LXC映像)的大小很小，因此容器映像很容易分发。

4)容器中的资源管理是通过cgroup实现的。Cgroups不允许容器消耗比分配给它们更多的资源。虽然主机的所有资源都在虚拟机中可见，但无法使用。

这可以通过在容器和主机上同时运行top或htop来实现。所有环境的输出看起来都很相似。



10.什么是联合文件系统(UnionFS)?

docker的镜像实际上由一层一层的文件系统组成，这种层级的文件系统就是UnionFS。UnionFS是一种分层、轻量级并且高性能的文件系统。联合加载会把各层文件系统叠加起来，这样最终的文件系统会包含所有底层的文件和目录。


11.Docker容器有几种状态
四种状态：运行、已暂停、重新启动、已退出。

12.解释一下dockerfile的ONBUILD指令
当镜像用作另一个镜像构建的基础时，ONBUILD指令向镜像添加将在稍后执行的触发指令。如果要构建将用作构建其他镜像的基础的镜像（例如，可以使用特定于用户的配置自定义的应用程序构建环境或守护程序），这将非常有用


13.CMD & ENTRYPONIT

都是容器操作指令：
CMD 用于指定容器启动时候默认执行的命令。可以被docker run指定的启动命令覆盖。ENTRYPONIT 指令可让容器以应用程序或者服务的形式运行。一般不会被docker run指定的启动命令覆盖。dockerfile中的多个CMD & ENTRYPONIT只有最后一个会生效。

注意区别docker run 和RUN 一个是容器启动命令，一个是镜像构建时候所用。


14.docker 网络模型是什么？有何局限
这里也经常会结合K8s网络原理进行考察，以及如下几个考点

docker的网络基础是什么？
docker的网络模型是？有什么局限？
docker如何实现容器间通信的？
Docker网络基础： Docker是在操作系统层上对应用的抽象，使用网络命名空间来对不同容器之间进行网络隔离，用Veth设备对来进行容器之间的通讯。

docker的网络模型： 有4种网络模型 分别是Bridge Container host none 默认使用bridge网络模型，容器的初次启动会虚拟化出来一个新的网卡名为docker0,在多机器部署下docker0地址可能会冲突。所以docker对多机部署支持的不够友好。


15.docker-compose & docker swarm
使用Docker compose可以用YAML文件来定义一组需要启动的容器，以及容器运行时的属性。docker-compose用来对这一组容器进行操作。
docker swarm 原生的Docker集群管理工具，依赖docker本身，很多重要功能依赖团队二次开发。且社区不够活跃，一般公司生产环境会选择k8s，个人项目或者容器数量较少可选swarm,只需要docker即可完成，相对较轻。

16.镜像构建时的缓存机制
在构建映像的过程中，Docker将按照指定的顺序逐步执行您的Dockerfile中的指令。随着每条指令的检查，Docker将在其缓存中查找可重用的现有映像，而不是创建一个新的（重复）映像。


17.Dockerfile中最常见的指令是什么？

答：FROM：指定基础镜像；LABEL：功能是为镜像指定标签；RUN：运行指定的命令；CMD：容器启动时要运行的命令。


18.什么类型的应用程序无状态或有状态更适合Docker容器？

答：最好为Docker Container创建无状态应用程序。我们可以从应用程序中创建一个容器，并从应用程序中取出可配置的状态参数。现在我们可以在生产环境和具有不同参数的QA环境中运行相同的容器。这有助于在不同场景中重用相同的镜像。另外，无状态应用程序比有状态应用程序更容易使用Docker容器进行扩展。
