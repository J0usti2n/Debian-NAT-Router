Router
apt-get update && apt-get install sudo && apt-get install iptables

nano /etc/network/interfaces
sudo reboot now
nano /etc/sysctl.conf
Hashtag entfernen bei "net.ipv4.ip_forward = 1"
sudo reboot now
sudo iptables --table nat --append POSTROUTING --out-interface enp0s3 -j MASQUERADE
sudo iptables --append FORWARD --in-interface enp0s8 -j ACCEPT
apt-get install iptables-persistent -y

Client
nano /etc/ssh/sshd_config
Hashtag entfernen -> "PermitRootLogin yes"