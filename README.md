# OpenWrt_on_Docker
在 docker 上运行 OpenWrt，参考https://openwrt.org/zh/docs/guide-user/virtualization/docker_openwrt_image

    # ip设置
    ip link set eth0 promisc on
    docker network create -d macvlan --subnet=192.168.1.0/24 --gateway=192.168.1.1 -o parent=eth0 macnet
    # 部署镜像
    docker run --restart always -d --network macnet --privileged yinping/openwrt /sbin/init

    # 使用以下命令导入基础镜像
    docker import http://downloads.openwrt.org/attitude_adjustment/12.09/x86/generic/openwrt-x86-generic-rootfs.tar.gz openwrt-x86-generic-rootfs
    
    # 使用以下命令在docker镜像中运行一个简单的cat
    docker run -i openwrt-x86-generic-rootfs cat /etc/banner
    docker run -i openwrt-x86-generic-rootfs ifconfig
    docker run -i openwrt-x86-generic-rootfs /sbin/init
    
    # 使用以下命令运行一个交互式命令行工具
    docker run -i -t openwrt-x86-generic-rootfs /bin/ash
    
    # 修改root的密码然后使用dropbear通过ssh建立连接
    passwd
    /etc/init.d/dropbear restart
    ifconfig
    
    # 打开控制台的同时，在另一个终端中尝试使用ssh方式连接到IP地址
    ssh root@172.17.0.45
    
    # 使用以下命令，发布docker镜像
    docker pull zoobab/openwrt-x86-attitude
    
    
