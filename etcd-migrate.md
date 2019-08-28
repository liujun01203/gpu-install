#etcd 迁移

1. 备份etcd
   
   ```
   rke etcd snapshot-save --name snapshot.db --config cluster.yml
   ```
   
2.  修改 cluster.yml  添加新的节点为etcd role

3.  在新节点上恢复etcd数据  
    
    ```
    
    rke etcd snapshot-restore --config cluster.yml --name snapshot.db

    ```
    
4.  通知k8s api server  etcd 集群已经发生了改变
    rke up --config cluster.yml
    
    
# k8s 扩容
1. 免密码访问配置
2. 修改cluster.yml
3. rke up 不要用root 账号
