VPC虚拟机是现今云计算最主要的结合虚拟化网络和虚拟化计算的结构，提供了用户（租户）在公有云上构建私有网络的功能，并且对云计算多数据中心提供了跨集群、跨网络、跨数据中心的虚拟局域网，支持虚拟机跨集群、跨网络、跨数据中心的迁移（无需改变虚拟机网络配置）。

VPC网络虚拟化的底层是一种新型的基于三层网络overlay二层网络的架构，是由Arista和VMware共同开发的VXLAN协议。

# VXLAN协议

VXLAN协议是用于支持超越数据中心L3边界持续的VM迁移而发明的新型网络技术。

对于虚拟机在不同host（物理服务器）之间迁移，通常有如下限制：

* 虚拟化带来了(虚拟)主机使用的IP地址急剧膨胀，单个LAN网段能够分配的IP地址有限，所以不同的集群、数据会分配不同网段的IP地址。即使这样，单个网段能够容纳的IP地址也有限，造成无法扩展更多的虚拟机。
* 当虚拟机需要跨越集群、数据中心迁移的时候，无法保证迁移以后虚拟机IP地址不变。原因同上：为了能够运行更多的虚拟机，各集群会采用不同的网段，一方面有更多IP，另一方面也为降低网络广播。

虚拟化动态热迁移为了保障用户服务不中断，对用户无感知，也同样要求迁移前后VM IP不能改变。

为了克服平面、Layer 2网络的局限，我们需要使用更为可伸缩的Layer 3网络，也就是IP网络路由。Arista和VMware共同开发的VXLAN提供了更具伸缩性、服务集成、虚拟化按需管理记账的网络功能。

VXLAN即`V`irtual e`X`tensible `LAN`，也就虚拟化可扩展局域网。VXLAN是一个隧道机制（tunneling mechanism）运行在虚拟化或者物理交换机之间，是的应用程序能够部署以及在不同数据中心的服务器上运行和迁移，无需修改IP子网。这对于IT部署和按需动态伸缩网络结构及其重要，突破了地理和IP地址的限制。

VXLAN也克服了现有数据中心协议的伸缩性限制，例如TRILL，生成树协议（Spanning Tree）等。和其他网络虚拟化overlay模式不同，VXLAN使用了久经验证的IP协议，不需要改变底层的Ip结构或者数据中心架构。

# 参考

* [VXLAN Bridges Virtual and Physical Networks to the Cloud](https://www.arista.com/assets/data/pdf/TechBulletins/VXLAN_Overview.pdf)