## Домашнее задание к занятию "4.2. Использование Python для решения типовых DevOps задач"
### 1. Есть скрипт:
```
#!/usr/bin/env python3
a = 1
b = '2'
c = a + b

    Какое значение будет присвоено переменной c?
    Как получить для переменной c значение 12?
    Как получить для переменной c значение 3?
```
```
1. 
a = 1
b = '2'

a= str(a) #1 
  #a= int(a) #2
  #b= int(b) #2
c = a + b
print (c)
```
### 2. Мы устроились на работу в компанию, где раньше уже был DevOps Engineer. Он написал скрипт, позволяющий узнать, какие файлы модифицированы в репозитории, относительно локальных изменений. Этим скриптом недовольно начальство, потому что в его выводе есть не все изменённые файлы, а также непонятен полный путь к директории, где они находятся. Как можно доработать скрипт ниже, чтобы он исполнял требования вашего руководителя?
``` 
#!/usr/bin/env python3

import os

bash_command = ["cd ~/netology/sysadm-homeworks", "git status"]
result_os = os.popen(' && '.join(bash_command)).read()
is_change = False
for result in result_os.split('\n'):
    if result.find('modified') != -1:
        prepare_result = result.replace('\tmodified:   ', '')
        print(prepare_result)
        break
``` 
```
2.
bash_command = ["cd /home/vagrant/netology/sysadm-homeworks","git status"]
print (bash_command)

result_os = os.popen('&&'.join(bash_command)).read()
is_change = False
for result in result_os.split('\n'):
        if result.find('modified') !=-1:
                prepare_result = result.replace('\tmodified:  ','')
                print (prepare_result)
                #break

 devops-netology-3.3
 devops-netology-3.4
 devops-netology-3.4
 ```
### 3. Доработать скрипт выше так, чтобы он мог проверять не только локальный репозиторий в текущей директории, а также умел воспринимать путь к репозиторию, который мы передаём как входной параметр. Мы точно знаем, что начальство коварное и будет проверять работу этого скрипта в директориях, которые не являются локальными репозиториями.
```
3.
#!/usr/bin/env python3

import os
path_to_git = input('Введите полный путь до репозитория git: ')
path_to_git = 'cd '+path_to_git
bash_command = [path_to_git, "git status"]
#print (bash_command)
result_os = os.popen('&&'.join(bash_command)).read()
is_change = False
for result in result_os.split('\n'):
        if result.find('modified') !=-1:
                prepare_result = result.replace('\tmodified:  ','')
                print (prepare_result)
                #break
 ```
 ### 4. Наша команда разрабатывает несколько веб-сервисов, доступных по http. Мы точно знаем, что на их стенде нет никакой балансировки, кластеризации, за DNS прячется конкретный IP сервера, где установлен сервис. Проблема в том, что отдел, занимающийся нашей инфраструктурой очень часто меняет нам сервера, поэтому IP меняются примерно раз в неделю, при этом сервисы сохраняют за собой DNS имена. Это бы совсем никого не беспокоило, если бы несколько раз сервера не уезжали в такой сегмент сети нашей компании, который недоступен для разработчиков. Мы хотим написать скрипт, который опрашивает веб-сервисы, получает их IP, выводит информацию в стандартный вывод в виде: <URL сервиса> - <его IP>. Также, должна быть реализована возможность проверки текущего IP сервиса c его IP из предыдущей проверки. Если проверка будет провалена - оповестить об этом в стандартный вывод сообщением: [ERROR] <URL сервиса> IP mismatch: <старый IP> <Новый IP>. Будем считать, что наша разработка реализовала сервисы: drive.google.com, mail.google.com, google.com.
 ``` 
 4.
#!/usr/bin/env python3
import socket
all_hosts = ["drive.google.com", "mail.google.com", "google.com"]
old_ip = ["0","0","0"]
for i in range(0,len(all_hosts)):
        get_socket = socket.gethostbyname(all_hosts[i])
        print(all_hosts[i], " - ", get_socket)
        old_ip[i]= get_socket
print("----------------------------------------")
for i in range(0,len(all_hosts)):
        get_socket = socket.gethostbyname(all_hosts[i])
        if old_ip[i] != get_socket:
                print("[ERROR]",all_hosts[i],"IP mismatch:",old_ip[i],get_socket)
        else:
                print("Host`s ip is match: ",old_ip[i],get_socket)

vagrant@netology1:~$ ./host.t
drive.google.com  -  173.194.221.194
mail.google.com  -  173.194.222.83
google.com  -  74.125.131.139
----------------------------------------
Host`s ip is match:  173.194.221.194 173.194.221.194
[ERROR] mail.google.com IP mismatch: 173.194.222.83 173.194.222.18
[ERROR] google.com IP mismatch: 74.125.131.139 74.125.131.101
vagrant@netology1:~$
