# rancher server 迁移步骤

## backup
1.  登录rancher server节点， 停止rancher server
2.  docker ps |grep rancher/rancher
3.  docker stop laughing_hamilton
4.  docker create --volumes-from laughing_hamilton --name rancher-data-20190823 rancher/rancher:v2.2.4
5.  docker run  --volumes-from rancher-data-20190823 -v $PWD:/backup:z busybox tar zcvf /backup/rancher-data-backup-v2.2.4-20190823.tar.gz /var/lib/rancher
6.  scp rancher-data-backup-v2.2.4-20190823.tar.gz  10.10.9.197:/home/nullmax
7.  docker start laughing_hamilton

## restore
1、  通过旧的rancher server 登录web 页面
     在system项目\资源\密文 路径页面下，找到并编辑密文cattle-credentials-xxxx， 修改url 为新的url， 有两个
     在system项目下找到cattle-system命名空间，分别编辑`cattle-cluster-agent`和cattle-node-agent, 修改Catter-server 部分
     
     停止旧的rancher server

1.  登录新的rancher server 节点 启动一个rancher server
    docker run -d --restart=unless-stopped -p 1080:80  -p 7443:443 rancher/rancher:v2.2.4 
2.  docker stop  musing_mayer
3.  docker run  --volumes-from sharp_shtern -v $PWD:/backup busybox sh -c "rm /var/lib/rancher/* -rf  && tar zxvf /backup/rancher-data-backup-v2.2.4-20190823.tar.gz"
4.  docker start sharp_shtern
5.  进入rancher web 页面修改server-url
6.  在system项目下找到cattle-system命名空间，分别编辑`cattle-cluster-agent`和cattle-node-agent, 修改Catter-server 部分
