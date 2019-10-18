# 基于 VirtualBox 的网络攻防基础环境搭建 #

----------

## 实验目的 ##
- 掌握 VirtualBox 虚拟机的安装与使用
- 掌握 VirtualBox 的虚拟网络类型和按需配置
- 掌握 VirtualBox 的虚拟硬盘多重加载
## 实验环境 ##
- VirtualBox 虚拟机
- 攻击者主机（Attacker）：Kali Rolling 2109.2
- 网关（Gateway, GW）：Debian Buster
- 靶机（Victim）：From Sqli to shell / xp-sp3 / Kali
## 实验要求 ##
- [ √ ] 靶机可以直接访问攻击者主机
- [ √ ] 攻击者主机无法直接访问靶机
- [ √ ] 网关可以直接访问攻击者主机和靶机
- [ √ ] 靶机的所有对外上下行流量必须经过网关
- [ √ ]所有节点均可以访问互联网
## 实验过程 ##
- 配置虚拟硬盘为多重加载
![](img/1.png)
![](img/2.png)
- 创建四个虚拟机，分别为Attacker，gateway,Victim,Victim2
![](img/3.png)
- 为虚拟机配置网卡
![](img/4.png)
![](img/5.png)
![](img/6.png)
![](img/7.png)
- Attacker（Kali，网卡1：NAT网络）
![](img/8.png)
- gateway（debian，网卡1：NAT网络，网卡2：仅主机，网卡3：内部网络，网卡4：内部网络）
![](img/9.png)
- victim（xp-sp3，网卡1：内部网络intnet1）
![](img/10.png)
- victim2（xp-sp3，网卡1：内部网络intnet2）
![](img/11.png)
## 网络连通性 ##
- 靶机（Victim，Victim2）可以直接访问攻击者主机
![](img/12.png)
![](img/13.png)
- 网关可以直接访问攻击者主机和靶机
![](img/14.png)
![](img/15.png)
- 攻击者主机无法直接访问靶机
![](img/16.png)
- 靶机的所有对外上下行流量必须经过网关
![](img/17.png)
![](img/18.png)
- 所有节点均可以访问互联网
![](img/19.png)
![](img/20.png)
![](img/21.png)
![](img/22.png)
## 问题总结 ##
- 网关网卡设置不对（少了“仅主机”），导致无法获取ip。解决方法：在NAT网卡后增加网卡“host-only”。
- 靶机IP为169开头的IP地址，且缺少默认网关。原因：未开启Gateway导致。解决方法：开启Gateway再查看靶机IP。
- 网关无法ping通靶机。解决方法：步步排查错误，最终关闭靶机防火墙后得以解决。