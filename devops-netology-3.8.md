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
  
2. Создайте dummy0 интерфейс в Ubuntu. Добавьте несколько статических маршрутов. Проверьте таблицу маршрутизации.

3. Проверьте открытые TCP порты в Ubuntu, какие протоколы и приложения используют эти порты? Приведите несколько примеров.

4. Проверьте используемые UDP сокеты в Ubuntu, какие протоколы и приложения используют эти порты?

5. Используя diagrams.net, создайте L3 диаграмму вашей домашней сети или любой другой сети, с которой вы работали. 
