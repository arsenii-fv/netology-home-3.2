## Домашнее задание к занятию "3.6. Компьютерные сети, лекция 1"

### 1. Работа c HTTP через телнет.
 ```
 Подключитесь утилитой телнет к сайту stackoverflow.com telnet stackoverflow.com 80
   отправьте HTTP запрос

GET /questions HTTP/1.0
HOST: stackoverflow.com
[press enter]
[press enter] 
1. 
HTTP/1.1 301 Moved Permanently
cache-control: no-cache, no-store, must-revalidate
location: https://stackoverflow.com/questions
x-request-guid: 3a876eb5-7b20-4782-b409-01e913abb6f2
feature-policy: microphone 'none'; speaker 'none'
content-security-policy: upgrade-insecure-requests; frame-ancestors 'self' https://stackexchange.com
Accept-Ranges: bytes
Date: Fri, 05 Nov 2021 20:32:17 GMT
Via: 1.1 varnish
Connection: close
X-Served-By: cache-hel1410021-HEL
X-Cache: MISS
X-Cache-Hits: 0
X-Timer: S1636144337.092114,VS0,VE126
Vary: Fastly-SSL
X-DNS-Prefetch-Control: off
Set-Cookie: prov=d67764cc-0612-807d-423d-19ce37c85d93; domain=.stackoverflow.com; expires=Fri, 01-Jan-2055 00:00:00 GMT; path=/; HttpOnly

Connection closed by foreign host.
```
### 2. Повторите задание 1 в браузере, используя консоль разработчика F12
```
2. 
 https://stackoverflow.com

HTTP/2 200 OK
cache-control: private
content-type: text/html; charset=utf-8
content-encoding: gzip
strict-transport-security: max-age=15552000
x-frame-options: SAMEORIGIN
x-request-guid: ec4cac40-177a-4c40-b324-33955fc443c1
feature-policy: microphone 'none'; speaker 'none'
content-security-policy: upgrade-insecure-requests; frame-ancestors 'self' https://stackexchange.com
accept-ranges: bytes
date: Fri, 05 Nov 2021 20:36:18 GMT
via: 1.1 varnish
```

### 3. Какой IP адрес у вас в интернете?
```
3.
 217.10.33.33
```

### 4. Какому провайдеру принадлежит ваш IP адрес? Какой автономной системе AS? Воспользуйтесь утилитой whois
```
4.
role:           AKADO-Stolitsa NOC
~$ whois -h whois.radb.net 217.10.32.0
route:          217.10.32.0/20
descr:          JSC "AKADO-Stolitsa"
descr:          DOCSIS ISP, Moscow
origin:         AS15582
mnt-by:         COMTV-MNT
notify:         netreg@akado-stolitsa.ru
created:        1970-01-01T00:00:00Z
last-modified:  2009-11-20T13:02:22Z
source:         RIPE
x-served-by: cache-hel1410021-HEL
x-cache: MISS
x-cache-hits: 0
x-timer: S1636144578.448195,VS0,VE129
vary: Accept-Encoding,Fastly-SSL
x-dns-prefetch-control: off
X-Firefox-Spdy: h2
```
### 5. Через какие сети проходит пакет, отправленный с вашего компьютера на адрес 8.8.8.8? Через какие AS? Воспользуйтесь утилитой traceroute
```
5.
 traceroute -An 8.8.8.8
traceroute to 8.8.8.8 (8.8.8.8), 30 hops max, 60 byte packets
 1  192.168.178.1 [*]  0.254 ms  0.263 ms  0.284 ms
 2  * * *
 3  10.244.3.162 [*]  22.940 ms  23.995 ms  23.995 ms
 4  10.254.249.41 [*]  16.149 ms  15.097 ms  17.174 ms
 5  * * *
 6  10.254.243.106 [*]  14.023 ms  12.532 ms  14.825 ms
 7  188.123.255.34 [AS15582]  14.796 ms  12.652 ms  12.633 ms
 8  62.117.100.161 [AS8732]  22.563 ms 62.117.100.163 [AS8732]  14.831 ms  14.812 ms
 9  72.14.194.74 [AS15169]  15.909 ms  15.915 ms  15.903 ms
10  108.170.250.51 [AS15169]  14.845 ms 108.170.250.130 [AS15169]  15.908 ms 108.170.250.113 [AS15169]  14.838 ms
11  172.253.66.116 [AS15169]  32.712 ms 209.85.255.136 [AS15169]  32.716 ms 172.253.66.116 [AS15169]  35.526 ms
12  172.253.66.108 [AS15169]  27.787 ms 172.253.65.159 [AS15169]  48.903 ms 72.14.235.69 [AS15169]  30.723 ms
13  72.14.237.201 [AS15169]  30.687 ms 216.239.46.139 [AS15169]  27.535 ms 172.253.51.221 [AS15169]  30.456 ms
14  * * *
15  * * *
16  * * *
17  * * *
18  * * *
19  * * *
20  * * *
21  * * *
22  * * *
23  8.8.8.8 [AS15169]  32.072 ms * *
```
### 6. Повторите задание 5 в утилите mtr. На каком участке наибольшая задержка - delay?
```
6. mtr  8.8.8.8
 10.254.249.41 Наимбольшее время задержки 38 ms 
```

### 7. Какие DNS сервера отвечают за доменное имя dns.google? Какие A записи? воспользуйтесь утилитой dig
```
7.
;; ANSWER SECTION:
dns.google.com.		3	IN	A	8.8.4.4
dns.google.com.		3	IN	A	8.8.8.8

;; AUTHORITY SECTION:
google.com.		47366	IN	NS	ns1.google.com.
google.com.		47366	IN	NS	ns3.google.com.
google.com.		47366	IN	NS	ns2.google.com.
google.com.		47366	IN	NS	ns4.google.com.
```

### 8.Проверьте PTR записи для IP адресов из задания 7. Какое доменное имя привязано к IP? воспользуйтесь утилитой dig
```
8.
 ;; QUESTION SECTION:
;8.8.8.8.in-addr.arpa.		IN	PTR

;; ANSWER SECTION:
8.8.8.8.in-addr.arpa.	61829	IN	PTR	dns.google.
```
