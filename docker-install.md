# Docker 安装

1. sudo apt-get remove docker docker-engine docker.io containerd runc
2. sudo apt-get update
3. sudo apt-get install apt-transport-https ca-certificates curl gnupg-agent software-properties-common
4. curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
4. sudo apt-key fingerprint 0EBFCD88
5. sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
6. sudo apt-get update
7. sudo apt-get install docker-ce=19.03.1~3-0~ubuntu-xenial docker-ce-cli=19.03.1~3-0~ubuntu-xenial containerd.io=1.2.6-3
8. sudo docker run hello-world  //check
9. sudo groupadd docker
10. sudo usermod -aG docker nullmax
11. sudo systemctl enable  docker
12. sudo systemctl start docker 


