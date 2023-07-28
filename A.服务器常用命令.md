## 网络

```shell
## 查看网卡驱动
$ sudo ethtool -i enp6s18

## 查看网卡 Ring
$ sudo ethtool -g enp6s18

## 查看网卡 Offload
$ sudo ethtool -k enp6s18

## 查看网卡数据统计
$ sudo ethtool -S enp6s18

## 查看网络配置情况
$ sudo networkctl status -a

## 查看端口占用
$ sudo lsof | grep dnsmasq | grep domain

$ sudo lsof -i:8053

## 查看本机 IP 地址
$ ip a

## 查看 IPv4 路由表
$ ip route show

## 查看 IPv6 路由表
$ ip -6 route show

## 查看系统当前链接
$ watch "ss -antu"

## 查看系统 nf_conntrack
$ cat /proc/net/nf_conntrack

## 查看 Nftables 防火墙
$ sudo nft list ruleset

## 动态查看 Nftables 防火墙数据包 Drop
$ sudo watch -d "nft list ruleset | grep drop"

## 动态查看 Nftables 防火墙数据包 Redirect
$ sudo watch -d "nft list ruleset | grep dport"

## 动态查看接口 QoS
$ sudo watch -d "tc -s qdisc show dev pppoe1"

$ sudo watch -d "tc -s qdisc show dev bridge1"

## 查询域名
$ dig baidu.com @223.5.5.5
$ dig AAAA www.qq.com @223.5.5.5

$ drill baidu.com @223.5.5.5
$ drill AAAA www.qq.com @223.5.5.5

$ nslookup baidu.com 223.5.5.5
$ nslookup -qt=AAAA www.qq.com 223.5.5.5
```

## 日志

```shell
## 查看系统日志
$ sudo dmesg

## 查看系统日志
$ sudo journalctl -e

## 查看拨号服务日志
$ sudo journalctl -eu pppd-enp6s18@pppoe1.service

## 动态查看 Dnsmasq 最后 30 行日志
$ sudo tail -n 30 -f /var/log/dnsmasq.log

## 动态查看 SmartDNS 最后 30 行日志
$ sudo tail -n 30 -f /var/log/smartdns/smartdns.log

## 动态查看系统自动更新最后 30 行日志
$ sudo tail -n 30 -f /var/log/unattended-upgrades/unattended-upgrades.log
```

## 系统

```shell
## 关闭系统
$ sudo shutdown now

## 重启系统
$ sudo shutdown now -r

## 重启系统
$ sudo reboot

## 查看系统资源
$ sudo htop

## 查看硬盘用量
$ df -hT

## 查看硬盘 Inodes 用量
$ df -hiT

## 查看 NVMe 硬盘 SMART 信息
$ sudo smartctl -a /dev/nvme0

## 更新软件源
$ sudo apt update

## 查看可更新软件包
$ sudo apt list --upgradable

## 更新系统
$ sudo apt upgrade

## 更新系统
$ sudo apt dist-upgrade

## 自动移除不必要软件包
$ sudo apt clean && sudo apt autoclean && sudo apt autoremove --purge

## 查看系统 PCI 设备
$ sudo lspci

## 更新 PCI 数据库
$ sudo update-pciids

## 设置系统时区
$ sudo timedatectl set-timezone Asia/Shanghai

## 查看系统时区
$ date -R

## 查看系统参数
$ sudo sysctl -a

## 查看系统模块
$ sudo lsmod

## 查看 CPU 微码
$ cat /proc/cpuinfo | grep 'microcode\|model name'

## 查看 CPU 频率
$ cat /proc/cpuinfo | grep MHz

## 查看 CPU 当前调度器
$ sudo cpufreq-info

## 动态查看温度传感器
$ sudo watch -d "sensors"

## 清理系统缓存
$ sudo rm -rvf /var/cache/apt/* /var/lib/apt/lists/* /tmp/*

## 清理系统日志
$ sudo find /var/log/ -type f | xargs sudo rm -rvf

## 使用 curl 安装 oh-my-zsh
$ sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"

## 使用 wget 安装 oh-my-zsh
$ sh -c "$(wget https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh -O -)"

## 更新 oh-my-zsh
$ omz update

## DNS 配置文件防篡改
$ sudo chattr +i /etc/resolv.conf

## 查看 DNS 配置文件权限
$ lsattr /etc/resolv.conf

## 查看命令历史记录
history

## 清理命令历史记录文件
$ rm -rvf ~/.bash_history ~/.zsh_history

## 清理命令历史
$ history -c
```

## 服务

```shell
## 查看系统服务状态
$ sudo systemctl status systemd-timesyncd.service

$ sudo systemctl status systemd-networkd.service

$ sudo systemctl status pppd-enp6s18@pppoe1.service

$ sudo systemctl status nftables.service

$ sudo systemctl status sshguard.service

$ sudo systemctl status systemd-resolved.service

$ sudo systemctl status dnsmasq.service

$ sudo systemctl status smartdns.service

## 查看系统启动时间分布
$ sudo systemd-analyze blame

$ sudo systemd-analyze critical-chain systemd-networkd-wait-online.service

## 服务重载
$ sudo systemctl daemon-reload

## 配置自动更新策略
$ sudo dpkg-reconfigure -plow unattended-upgrades

## 查看系统自动更新定时器
$ sudo systemctl status apt-daily-upgrade.timer

## 显示系统 crontab
$ sudo crontab -l
```
