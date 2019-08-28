# rke 安装   

1. 关闭swap  

    ``` 
    sudo sed  -i 's/^UUID.*swap/#&/g' /etc/fstab
    ```

2.  安装需要的内核模块     
    
    ```
    for module in br_netfilter ip6_udp_tunnel ip_set ip_set_hash_ip ip_set_hash_net iptable_filter iptable_nat iptable_mangle iptable_raw nf_conntrack_netlink nf_conntrack nf_conntrack_ipv4 nf_defrag_ipv4 nf_nat nf_nat_ipv4 nf_nat_masquerade_ipv4 nfnetlink udp_tunnel veth vxlan x_tables xt_addrtype xt_conntrack xt_comment xt_mark xt_multiport xt_nat xt_recent xt_set xt_statistic xt_tcpudp;
    do 
        if ! lsmod | grep -q $module; 
           then sudo modprobe $module
        fi 

        if ! lsmod | grep -q $module;
            then echo "module $module is not present" 
        fi
    done;
    ```
 
3.  设置系统配置
  
     ```
     sudo echo "net.bridge.bridge-nf-call-iptables=1" |sudo tee -a /etc/sysctl.conf
     ```
 
4.  修改sshd配置  

     ```
     sudo echo "AllowTcpForwarding yes" |sudo tee -a /etc/ssh/sshd_config
     ``` 
     
5.  下载rke二进制文件

6.  准备 rke 配置文件 cluster.yml

7.  安装k8s 集群
    
    ```
    rke up
    ``` 
    
8. rancher server 安装

    ```
    sudo docker run -d --restart=unless-stopped -p 1080:80  -p 7443:443 rancher/rancher:v2.2.4
    ```