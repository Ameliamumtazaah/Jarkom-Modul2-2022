# Jarkom-Modul2-2022
| Name | NRP |
| ------ | ------ |
| Amelia Mumtazah Karimah | 5025201128 |
| Shafina Chaerunisa | 5025201129 |
| Muhammad Fadli Azhar | 5025201157 |


## Opening Question
Twilight (〈黄昏 (たそがれ) 〉, <Tasogare>) is a spy who comes from a country named Westalis. For the sake of maintaining peace between Westalis and Ostania, Twilight with a pseudonym Loid Forger (ロイド・フォージャー, Roido Fōjā) under WISE organisation run his operation in Ostania by doing espionage, sabotage, tapping, and possibly murder. Here is a map of the Ostania country :

WISE will be used as DNS Master, Berlint as DNS Slave, and Eden will be used as Web Server. There are 2 clients, namely SSS and Garden. All nodes are connected to Ostania as the router, so they can access the internet.

### 1
WISE will be used as DNS Master, Berlint as DNS Slave, and Eden will be used as Web Server. There are 2 clients, namely SSS and Garden. All nodes are connected to Ostania as the router, so they can access the internet.
First we create the topology as follows:

then we do the configuration on each node :
Ostania as Router
```bash
auto eth0
iface eth0 inet dhcp

auto eth1
iface eth1 inet static
    address 10.36.1.1
    netmask 255.255.255.0

auto eth2
iface eth2 inet static
    address 10.36.2.1
    netmask 255.255.255.0

auto eth3
iface eth3 inet static
    address 10.36.3.1
    netmask 255.255.255.0
 ```
SSS and Garden as Client
```bash
apt-get update         
apt-get install dnsutils 
``` 
```bash
auto eth0
iface eth0 inet static
    address 10.36.1.2
    netmask 255.255.255.0
    gateway 10.36.1.1
```  
```bash
auto eth0
iface eth0 inet static
    address 10.36.1.3
    netmask 255.255.255.0
    gateway 10.36.1.1
```
Wise as DNS Master
```bash
auto eth2
iface eth2 inet static
    address 10.36.2.2
    netmask 255.255.255.0
    gateway 10.36.2.1
```  
Berlin as DNS Slave
```bash
auto eth0
iface eth0 inet static
    address 10.36.3.2
    netmask 255.255.255.0
    gateway 10.36.3.1
``` 
Eden as Web Server
```bash
auto eth0
iface eth0 inet static
    address 10.36.3.3
    netmask 255.255.255.0
    gateway 10.36.3.1
```  
Then each node is activated by clicking the start button. After that, run the command on the Ostania router to try to connect to the internet.
### 2
To make it easier to get information about the mission from Handler, help Loid create the main website by accessing wise.yyy.com with alias www.wise.yyy.com on the wise folder.
First, Eden Server configure the file /etc/bind/named.conf.local by adding
```bash
zone "wise.I05.com" {  
        type master;  
        file "/etc/bind/wise/.I05.com";
};
```
Create a new directory which is ```/etc/bind/wise```

Adding configuration to ``` /etc/bind/wise/wise.I05.com```
    
```bash
$TTL            604800
@               IN      SOA     wise.i05.com. root.wise.i05.com. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@                   IN      NS      wise.i01.com.
@                   IN      A       10.36.3.3
www                 IN      CNAME   wise.i01.com. ;
```
Restarting service bind9 with service bind9 restart
```bash
apt-get update  
apt-get install dnsutils -y  
echo "nameserver  10.36.3.3" > /etc/resolv.conf  
```
    
### 3   
