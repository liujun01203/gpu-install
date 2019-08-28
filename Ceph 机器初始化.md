# Ceph  迁移
## Ceph 机器初始化

1. ceph账号sudo免密码

   ```
   echo "ceph ALL = (root) NOPASSWD:ALL" |sudo tee /etc/sudoers.d/ceph
   sudo chmod 0440 /etc/sudoers.d/ceph
   ```
  
2. hostname 修改 
   sudo hostnamectl  set-hostname xxx
2. 无密码访问本机器
3. 修改／etc／hosts
4. sudo apt-get update 
   sudo apt install -y ntp
4. 升级内核到指定的版本
   sudo apt-get install -y linux-headers-4.15.0-52  linux-headers-4.15.0-52-generic  linux-image-4.15.0-52-generic

6. 修改ulimit 参数
   echo "*                hard    nofile          655360" |sudo  tee -a  /etc/security/limits.conf
   echo "*                soft    nofile          655360" |sudo  tee -a  /etc/security/limits.conf
   


## Ceph 添加osd

1.  安装ceph 包
    ceph-deploy install xxx

2.  部署osd
    ceph-deploy osd create  --data  /dev/sdc xxx
    
## ceph 删除osd
    ceph osd out 0
    systemctl stop ceph-osd.target
	    ceph osd purge 0  --yes-i-really-mean-it 
    
    
## Ceph 添加mon
    ceph-deploy  mon add xxx
    
## Ceph 删除mon
  1. 停止
  2. ceph mon remove 
    

## Ceph 添加RGW

## Ceph 添加mgr
    ceph-deploy  mgr create xxx

## ceph 添加mds
    ceph-deploy  mds create xxx
    
## ceph 删除mds
    停止进程
    
## 加快ceph recovery 速度
 
 1.  ceph --admin-daemon /var/run/ceph/ceph-osd.5.asok config show  |grep osd_max_backfills
 2.  ceph --admin-daemon /var/run/ceph/ceph-osd.5.asok config show|grep osd_recovery_max_active
 3.  ceph --admin-daemon /var/run/ceph/ceph-osd.5.asok config show|grep osd_recovery_max_single_start
 2.  ceph tell osd.* injectargs '--osd_max_backfills=100'
 3.  ceph tell osd.* injectargs '--osd_recovery_max_single_start=100'
 4.  ceph tell osd.* injectargs '--osd_recovery_max_active=1000'

 
 
ceph osd set nobackfill
ceph osd set norecover
ceph osd set norebalance

osd set full|pause|noup|nodown|noout|noin|nobackfill|norebalance|norecover|noscrub|
ceph osd unset nobackfill
ceph osd unset norecover

 

   
   
   
