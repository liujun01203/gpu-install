# Ceph fuse 的使用
1. 登录跳板机10.10.9.52

   ```
   ssh slyang@101.89.87.30 -p 1022   // 需要找跳板机管理员，提前为自己创建一个具有sudo权限的用户。 这里和后面假定用户为slyang
   ```

2. 挂载volume到用户目录下
    
    1. 准备ceph.keyring 文件 ， 放在/home/slyang 目录下
       ```
       ceph.keyring  文件保存的是用户账号信息， 这个需要找ceph 集群管理员提供，方法与之前保持不变。
       ````
    
    2. 准备挂载点 /home/slyang/data    
       ```
       mkdir   /home/slyang/data
       ```
       
    3. 在/etc/fstab 追加如下信息： 
       ```
     none	/home/slyang/data	fuse.ceph	ceph.keyring=/home/slyang/ceph.keyring,ceph.client_mountpoint=/k8s-storageclass-pvc/kubernetes/kubernetes-dynamic-pvc-f1fa7163-c226-11e9-855b-7e55f28a0e41,ceph.id=kubernetes-dynamic-user-f1fa71dd-c226-11e9-855b-7e55f28a0e41,ceph.conf=/etc/ceph/ceph.conf,_netdev,defaults	0	0
       ```
     + /home/slyang/data   为步骤2准备的挂载点
     + ceph.keyring=/home/slyang/ceph.keyring  为步骤1准备的ceph.keyring 文件
     + ceph.client_mountpoint=/k8s-storageclass-pvc/kubernetes/kubernetes-dynamic-pvc-f1fa7163-c226-11e9-855b-7e55f28a0e41  为用户的volume信息， 是volume 相对cephfs 根的路径。可以在rancher的web 页面查看
     + ceph.id=kubernetes-dynamic-user-f1fa71dd-c226-11e9-855b-7e55f28a0e41  为创建volume时自动创建的用户， 可以在rancher的web 页面查看
     + ceph.conf=/etc/ceph/ceph.conf   为ceph配置文件所在位置， 在跳板机上大家可以共享一份，无需自己提供
     
    4. 挂载   
       ``` 
       sudo mount   /home/slyang/data
       ```
       
3. 办公电脑与volume之间的数据拷贝，在办公电脑上执行如下命令
    ```
    scp -P  1022 slyang@101.89.87.30:/home/slyang/data/xxx   ./xxx
    ```