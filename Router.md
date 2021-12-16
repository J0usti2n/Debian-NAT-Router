# Router
1. Pakete installieren

```apt-get update && apt-get install sudo && apt-get install iptables```

2. Netzwerkkonfiguration

```nano /etc/network/interfaces```
```
auto enp0s8
iface enp0s8 inet static
    address 192.168.10.1
    network 192.168.10.0
    broadcast 192.168.10.255
    dns-nameservers 1.1.1.1 1.0.0.1
```
2.1. Neustarten

```sudo reboot now```

2.2. IP-Forwarding aktivieren - 

```nano /etc/sysctl.conf *Hashtag entfernen```

``` 
#net.ipv4.ip_forward = 1 -> net.ipv4.ip_forward = 1
```
2.3. Neustarten

```sudo reboot now```

2.4. Regeln hinzufügen

```sudo iptables --table nat --append POSTROUTING --out-interface enp0s3 -j MASQUERADE```

```sudo iptables --append FORWARD --in-interface enp0s8 -j ACCEPT```

2.5. IPTables speichern

```apt-get install iptables-persistent -y```


# Client
3. SSH Root-Anmeldung erlauben (Debian)

```nano /etc/ssh/sshd_config``` 
-> "PermitRootLogin yes" einfügen

# Windows SSH verbindung zu Root
```route add 192.168.10.0 MASK 255.255.255.0 192.168.10.1``` -> Syntax: route add <Netz-ID(enp0s8)> MASK <Netzmaske> <Gateway(enp0s3)>
