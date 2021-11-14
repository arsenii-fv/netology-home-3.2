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
