# cwz
ns culture
print "cwz"
sudo docker run -d \
  --name=code-server1 \
  -e PUID=1000 \
  -e PGID=1000 \
  -e TZ=China/Shanghai \
  -e PASSWORD=8899 `#optional` \
  -e HASHED_PASSWORD= `#optional` \
  -e SUDO_PASSWORD=cwz `#optional` \
  -e SUDO_PASSWORD_HASH= `#optional` \
  -e PROXY_DOMAIN=code-server.my.domain `#optional` \
  -p 33089:8443 \
  -v /data/my-code:/config \
  --restart unless-stopped \
  linuxserver/code-server

sudo docker run -d \
  --name=code-server \
  -e PUID=1000 \
  -e PGID=1000 \
  -e TZ=China/Shanghai \
  -e PASSWORD=8899 `#optional` \
  -e HASHED_PASSWORD= `#optional` \
  -e SUDO_PASSWORD=cwz `#optional` \
  -e SUDO_PASSWORD_HASH= `#optional` \
  -e PROXY_DOMAIN=code-server.my.domain `#optional` \
  -p 33086:8443 \
  -v /data/my-code:/config \
  --restart unless-stopped \
  linuxserver/code-server

  apt-get install python3-pip

sudo pip3 install Django -i https://pypi.tuna.tsinghua.edu.cn/simple
http://172.17.0.3:38000/
sudo ifconfig enp14s0:1 192.168.8.33/24
sudo route add -net 10.50.251.0/24 enp14s0:1


sudo ip route add 19.50.108.0/24 via 10.50.251.254
sudo ip route add 192.168.10.0/24 via 10.50.251.254
sudo ifconfig enp14s0:1 192.168.8.33 broadcast 192.168.8.255 netmask 255.255.255.0 up
sudo route add -net 192.168.8.0/24 enp14s0:1
iptables -t nat -A PREROUTING -d 192.168.8.33 -p tcp --dport 38000 -j DNAT --to-destination 172.17.0.3:38000
iptables -t nat -A POSTROUTING -d 192.168.8.33 -p tcp --dport 38000 -j SNAT --to 172.17.0.3:38000
问题：如何对运行中的Docker容器进行端口映射？
sudoiptables -t nat -A  DOCKER -p tcp --dport 38000 -j DNAT --to-destination 172.17.0.3:38000
sudo iptables -t nat -A POSTROUTING -j MASQUERADE -p tcp --source 172.17.0.3 --destination 172.17.0.3 --dport 38000
sudo iptables -A DOCKER -j ACCEPT -p tcp --destination 172.17.0.3 --dport 38000

sudoiptables -t nat -A  DOCKER -p tcp --dport 38000 -j DNAT --to-destination 172.17.0.3:35000
sudo iptables -t nat -A POSTROUTING -j MASQUERADE -p tcp --source 172.17.0.3 --destination 172.17.0.3 --dport 35000
sudo iptables -A DOCKER -j ACCEPT -p tcp --destination 172.17.0.3 --dport 35000


docker run -it --name code-server -p 127.0.0.1:8080:8080 \
  -v "$HOME/.config:/home/coder/.config" \
  -v "$PWD:/home/coder/project" \
  -u "$(id -u):$(id -g)" \
  -e "DOCKER_USER=$USER" \
  codercom/code-server:latest
