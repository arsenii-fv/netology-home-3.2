## Домашнее задание к занятию "3.6. Компьютерные сети, лекция 1"

  #1. Работа c HTTP через телнет.
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
