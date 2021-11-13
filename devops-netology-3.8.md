# Домашнее задание к занятию "3.8. Компьютерные сети, лекция 3"
1. Подключитесь к публичному маршрутизатору в интернет. Найдите маршрут к вашему публичному IP
```
telnet route-views.routeviews.org
Username: rviews
show ip route x.x.x.x/32
show bgp x.x.x.x/32
```
User Access Verification

Username: rviews
route-views>show ip route 217.10.33.33/32
                                      ^
% Invalid input detected at '^' marker.

route-views>show ip route 217.10.33.33
Routing entry for 217.10.32.0/20, supernet
  Known via "bgp 6447", distance 20, metric 0
  Tag 6939, type external
  Last update from 64.71.137.241 1w6d ago
  Routing Descriptor Blocks:
  * 64.71.137.241, from 64.71.137.241, 1w6d ago
      Route metric is 0, traffic share count is 1
      AS Hops 3
      Route tag 6939
      MPLS label: none
route-views>show bgp  217.10.33.33
BGP routing table entry for 217.10.32.0/20, version 1208190311
Paths: (24 available, best #23, table default)
  Not advertised to any peer
  Refresh Epoch 1
  7018 6762 8732 15582, (aggregated by 15582 83.167.99.102)
    12.0.1.63 from 12.0.1.63 (12.0.1.63)
      Origin IGP, localpref 100, valid, external
      Community: 7018:5000 7018:37232
      path 7FE16C333E88 RPKI State not found
      rx pathid: 0, tx pathid: 0
  Refresh Epoch 1
  3267 2603 8732 15582, (aggregated by 15582 83.167.99.108)
    194.85.40.15 from 194.85.40.15 (185.141.126.1)
      Origin IGP, metric 0, localpref 100, valid, external
      path 7FE12B7105D8 RPKI State not found
      rx pathid: 0, tx pathid: 0
  Refresh Epoch 1
  3333 6762 8732 15582, (aggregated by 15582 83.167.99.102)
    193.0.0.56 from 193.0.0.56 (193.0.0.56)
      Origin IGP, localpref 100, valid, external
      Community: 6762:1 6762:92 6762:14900
      path 7FE15C043A30 RPKI State not found
      rx pathid: 0, tx pathid: 0
  Refresh Epoch 1
```  
2. Создайте dummy0 интерфейс в Ubuntu. Добавьте несколько статических маршрутов. Проверьте таблицу маршрутизации.
root@lite:/home/arsen# routel
         target            gateway          source    proto    scope    dev tbl
        default      192.168.178.1                                  enp37s0 
    172.17.0.0/ 16                      172.17.0.1   kernel     linkdocker0 
 192.168.100.0/ 24                   192.168.100.1   kernel     link virbr0 
 192.168.111.0/ 24                   192.168.111.1   kernel     link virbr1 
 192.168.111.0/ 24   192.168.111.1                                   virbr1 
 192.168.178.0/ 24                  192.168.178.22   kernel     linkenp37s0 
       10.8.8.8              local        10.8.8.8   kernel     host dummy0 local
       10.8.8.8          broadcast        10.8.8.8   kernel     link dummy0 local
      127.0.0.0          broadcast       127.0.0.1   kernel     link     lo local
     127.0.0.0/ 8            local       127.0.0.1   kernel     host     lo local
      127.0.0.1              local       127.0.0.1   kernel     host     lo local
127.255.255.255          broadcast       127.0.0.1   kernel     link     lo local
     172.17.0.0          broadcast      172.17.0.1   kernel     linkdocker0 local
     172.17.0.1              local      172.17.0.1   kernel     hostdocker0 local
 172.17.255.255          broadcast      172.17.0.1   kernel     linkdocker0 local
  192.168.100.0          broadcast   192.168.100.1   kernel     link virbr0 local
  192.168.100.1              local   192.168.100.1   kernel     host virbr0 local
192.168.100.255          broadcast   192.168.100.1   kernel     link virbr0 local
  192.168.111.0          broadcast   192.168.111.1   kernel     link virbr1 local
  192.168.111.1              local   192.168.111.1   kernel     host virbr1 local
192.168.111.255          broadcast   192.168.111.1   kernel     link virbr1 local
  192.168.178.0          broadcast  192.168.178.22   kernel     linkenp37s0 local
 192.168.178.22              local  192.168.178.22   kernel     hostenp37s0 local
192.168.178.255          broadcast  192.168.178.22   kernel     linkenp37s0 local
            ::1                                      kernel              lo 
        fe80::/ 64                                   kernel         enp37s0 
        fe80::/ 64                                   kernel          dummy0 
            ::1              local                   kernel              lo local
fe80::2ef0:5dff:fe33:fa3c              local                   kernel         enp37s0 local
fe80::9474:e0ff:fe59:2558              local                   kernel          dummy0 local

auto lo
iface lo inet loopback
auto enp37s0
iface enp37s0 inet dhcp
auto dummy0
iface dummy0 inet static
        address 10.8.8.8/32
        pre-up ip link add dummy0 type dummy
        post-down ip link del dummy0


3. Проверьте открытые TCP порты в Ubuntu, какие протоколы и приложения используют эти порты? Приведите несколько примеров.
sudo ss -tlpn
State         Recv-Q        Send-Q               Local Address:Port               Peer Address:Port       Process
LISTEN        0             4096                 127.0.0.53%lo:53                      0.0.0.0:*           users:(("systemd-resolve",pid=548,fd=13))
LISTEN        0             128                        0.0.0.0:22                      0.0.0.0:*           users:(("sshd",pid=1155,fd=3))
LISTEN        0             4096                       0.0.0.0:111                     0.0.0.0:*           users:(("rpcbind",pid=547,fd=4),("systemd",pid=1,fd=35))
LISTEN        0             128                           [::]:22                         [::]:*           users:(("sshd",pid=1155,fd=4))
LISTEN        0             4096                          [::]:111                        [::]:*           users:(("rpcbind",pid=547,fd=6),("systemd",pid=1,fd=37))

4. Проверьте используемые UDP сокеты в Ubuntu, какие протоколы и приложения используют эти порты?
 sudo ss -ulpn
State         Recv-Q        Send-Q                Local Address:Port               Peer Address:Port       Process
UNCONN        0             0                     127.0.0.53%lo:53                      0.0.0.0:*           users:(("systemd-resolve",pid=548,fd=12))
UNCONN        0             0                    10.0.2.15%eth0:68                      0.0.0.0:*           users:(("systemd-network",pid=3501,fd=20))
UNCONN        0             0                           0.0.0.0:111                     0.0.0.0:*           users:(("rpcbind",pid=547,fd=5),("systemd",pid=1,fd=36))
UNCONN        0             0                              [::]:111                        [::]:*           users:(("rpcbind",pid=547,fd=7),("systemd",pid=1,fd=38))
5. Используя diagrams.net, создайте L3 диаграмму вашей домашней сети или любой другой сети, с которой вы работали. 
 [*ссылка на диаграмму*](https://drive.google.com/file/d/1ZdazPz2Ul7uFivf-vcxrQhOsDqHdPfER/view?usp=sharing)
 
