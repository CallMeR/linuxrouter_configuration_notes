# Linux 路由器折腾手记

## 介绍
Linux 路由器的安装以及折腾手记。

- 适用 Linux 发行版（优先使用支持 `systemd` 的发行版）
    - Debian 12
    - Ubuntu Server 22.10
    - Arch Linux

- 演示机：
    - 虚拟化：Proxmox VE
    - CPU：host
    - 内存：2GB
    - 网卡：VirtIO
    - 磁盘：VirtIO SCSI Single

- 内部网络：
    - IPv4 网络
        - IP 地址：`172.16.1.1`
        - 子网掩码：`255.255.255.0` ( 即 `/24` )
        - 网关：`172.16.1.1`
        - DNS：`172.16.1.2` , `172.16.1.3`
    - IPv6 网络
        - 分配方式：SLAAC        
        - IP 地址：`fd10::1`
        - 前缀：`fd10::/64`
        - DNS：`fd10::2` , `fd10::3`

- 外网连接方式：PPPoE


### 系列章节

0.  [Ubuntu_PVE创建服务器](./00.Ubuntu_PVE创建服务器.md)  
1.  [Ubuntu_服务器安装](./01.Ubuntu_服务器安装.md)  
2.  [Ubuntu_服务器初始化](./02.Ubuntu_服务器初始化.md)  
3.  [Ubuntu_设置系统参数](./03.Ubuntu_设置系统参数.md)  
4.  [Ubuntu_设置系统网络](./04.Ubuntu_设置系统网络.md)  
5.  [Ubuntu_设置Dnsmasq](./05.Ubuntu_设置Dnsmasq.md)  


### 参考文档

-  **CPU**  
    - [Microcode - Debian Wiki](https://wiki.debian.org/Microcode)
    - [CPU Performance Scaling](https://docs.kernel.org/admin-guide/pm/cpufreq.html)
    - [CPU frequency scaling - Arch Wiki](https://wiki.archlinux.org/title/CPU_frequency_scaling)

-  **DHCP** 
    - [dhcpcd | Roy's Projects](https://roy.marples.name/projects/dhcpcd/)
    - [dhcpcd - ArchWiki](https://wiki.archlinux.org/title/Dhcpcd)
    - [dhcpcd.conf(5) — Arch manual pages](https://man.archlinux.org/man/dhcpcd.conf.5)
    - [dhcpcd(8) — Arch manual pages](https://man.archlinux.org/man/dhcpcd.8.en)
    - [Kea Administrator Reference Manual](https://kea.readthedocs.io/en/latest/index.html)

-  **DNS** 
    - [resolv.conf - Debian Wiki](https://wiki.debian.org/resolv.conf)
    - [openresolv - ArchWiki](https://wiki.archlinux.org/title/Openresolv)
    - [dnsmasq - ArchWiki](https://wiki.archlinux.org/title/Dnsmasq)
    - [dnsmasq warnings - Pi-hole documentation](https://docs.pi-hole.net/ftldns/dnsmasq_warn/)
    - [[OpenWrt Wiki] DNS and DHCP configuration](https://openwrt.org/docs/guide-user/base-system/dhcp)
    - [Unbound - ArchWiki](https://wiki.archlinux.org/title/Unbound)
    - [SmartDNS · GitHub](https://github.com/pymumu/smartdns)

-  **IPv6** 
    - [IPv6 - ArchWiki](https://wiki.archlinux.org/title/IPv6)
    - [Dynamic Host Configuration Protocol for IPv6 (DHCPv6)](https://www.iana.org/assignments/dhcpv6-parameters/dhcpv6-parameters.xhtml)
    - [RFC4193 IPv6 Generator](https://cd34.com/rfc4193/)  
    - [Setting up IPv6 using a DHCP client - K3A](https://k3a.me/setting-up-ipv6-using-a-dhcp-client/)     
    - [Setting up IPv6 on a Linux Router](https://battlepenguin.com/tech/setting-up-ipv6-on-a-linux-router/) 
    - [Managing Address Spaces with NAT and IPv6 - Config Router](https://www.configrouter.com/managing-address-spaces-nat-ipv6-14629/)

-  **Network Interface** 
    - [Network bridge - Arch Wiki](https://wiki.archlinux.org/title/Network_bridge) 
    - [systemd-networkd - Arch Wiki](https://wiki.archlinux.org/title/Systemd-networkd)
    - [Systemd.Network](https://systemd.network/systemd.network.html)
    - [Systemd.Link](https://systemd.network/systemd.link.html)
    - [BRIDGE-UTILS-INTERFACES(5) - Debian Wiki](https://manpages.debian.org/stable/bridge-utils/bridge-utils-interfaces.5.en.html)
    - [Netplan configuration examples](https://netplan.io/examples/)
    - [Ubuntu Manpage: systemd.network ](https://manpages.ubuntu.com/manpages/jammy/man5/systemd.network.5.html)
    - [Bridge - Linux Foundation DokuWiki](https://wiki.linuxfoundation.org/networking/bridge)

-  **Nftables** 
    - [nftables - Debian Wiki](https://wiki.debian.org/nftables)
    - [nftables - ArchWiki](https://wiki.archlinux.org/title/Nftables)
    - [Simple ruleset for a home router](https://wiki.nftables.org/wiki-nftables/index.php/Simple_ruleset_for_a_home_router)
    - [Quick reference-nftables in 10 minutes](https://wiki.nftables.org/wiki-nftables/index.php/Quick_reference-nftables_in_10_minutes)
    - [Netfilter’s flowtable infrastructure](https://docs.kernel.org/networking/nf_flowtable.html)
    - [Firewall4 / NFtables Tips and Tricks](https://forum.openwrt.org/t/firewall4-nftables-tips-and-tricks/113704/8)

-  **PPPoE** 
    - [ppp - ArchWiki](https://wiki.archlinux.org/title/Ppp)
    - [pppd(8) — Arch manual pages](https://man.archlinux.org/man/core/ppp/pppd.8.en)
    - [PPP - Alpine Linux](https://wiki.alpinelinux.org/wiki/PPP)
    - [Debian / pppoeconf · GitLab](https://salsa.debian.org/debian/pppoeconf)
    - [add pppoe support to systemd-networkd · GitHub](https://github.com/systemd/systemd/issues/481)

-  **SYSCTL** 
    - [sysctl - ArchWiki](https://wiki.archlinux.org/title/Sysctl)
    - [sysctl - explorer](https://sysctl-explorer.net)
    - [Huge improve network performance by change TCP congestion control to BBR](https://djangocas.dev/blog/huge-improve-network-performance-by-change-tcp-congestion-control-to-bbr/)
    - [Optimizing TCP for high WAN throughput while preserving low latency](https://blog.cloudflare.com/optimizing-tcp-for-high-throughput-and-low-latency/)

-  **Linux Router Setup** 
    - [Router - ArchWiki](https://wiki.archlinux.org/title/router)
    - [debian-clearfog-gt-8k · GitHub](https://github.com/jimdigriz/debian-clearfog-gt-8k)
    - [Setting up Alpine Linux as a Home Router](https://riedstra.dev/2022/02/alpine-linux-home-router)
    - [DIY Linux Router Part 2: Interfaces, DHCP and VLAN](https://www.sherbers.de/diy-linux-router-part-2-interfaces-dhcp-and-vlan/)
    - [我的另类软路由方案——Alpine Linux改造](https://post.smzdm.com/p/ad2rx4dd/)
    - [X86 软路由配置 IPv6 踩坑小记](https://blog.otakusaikou.com/2020/11/11/x86-soft-router-and-ipv6/)
    - [自建Linux路由器--Debian篇](https://johnrosen1.com/2020/11/27/router/)    
    - [使用 Debian 服务器作为家庭网关](https://ichon.me/post/1033.html)
    - [Building Your Own Low Latency Home Router](https://jsravn.com/2018/06/12/building-your-own-low-latency-home-router/)


### 文章说明

1.  本系列文章涉及的部分参数需要手动调整来符合切实使用需求。
2.  随着 Linux 系统的迭代更新，截图中的内容和实际页面显示可能存在差异。
3.  不同的 Linux 发行版所使用的命令略有差异，但总体设置思路一致。
3.  如需引用，请注明本文出处。