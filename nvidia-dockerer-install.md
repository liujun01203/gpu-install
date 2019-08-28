#nvidia 驱动安装

1. 拷贝NVIDIA-Linux-x86_64-430.26.run
3. sudo apt-get -y install gcc make
4. sudo  ./NVIDIA-Linux-x86_64-430.26.run  -no-x-check -no-nouveau-check -no-opengl-files 



# nvidia-docker 安装


1. curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | sudo apt-key add -
2. curl -s -L https://nvidia.github.io/nvidia-docker/ubuntu16.04/nvidia-docker.list | sudo tee /etc/apt/sources.list.d/nvidia-docker.list
3. sudo apt-get update && sudo apt-get install -y nvidia-container-toolkit
4. sudo apt-get install -y nvidia-docker2
4. 修改／etc／docker／daemon.json
5. 重启docker
   sudo systemctl restart docker
