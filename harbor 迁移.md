# harbor 迁移
1. 将原harbor的data 目录完全拷贝到目的harbor
   
   ```
   sudo scp -pr  ／data／*     ceph@xx.xx.xx.xx:/data
   ```

2. 在目的节点上安装harbor, 使data指向拷贝过来的数据

