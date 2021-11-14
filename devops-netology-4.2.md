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
### 2. Мы устроились на работу в компанию, где раньше уже был DevOps Engineer. Он написал скрипт,
###    позволяющий узнать, какие файлы модифицированы в репозитории, относительно локальных изменений.
###    Этим скриптом недовольно начальство, потому что в его выводе есть не все изменённые файлы, а также непонятен полный путь к директории,
###    где они находятся. Как можно доработать скрипт ниже, чтобы он исполнял требования вашего руководителя?
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
 
 
