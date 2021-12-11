## Домашнее задание к занятию "4.1. Командная оболочка Bash: Практические навыки"

### 1. Есть скрипт:
```
a=1
b=2
c=a+b
d=$a+$b
e=$(($a+$b))

    Какие значения переменным c,d,e будут присвоены?
    Почему?

1. c=a+b
   Выражение a+b bash воспринимает как строку
   
   d=1+2
   d присваиваивается строка со значениями: переменной a,  символ +, переменной b
  
   e=3
   ((..)) Выражение стоящее за двойными круглыми скобками BASH воспринимает как арифметическая операция. Переменной
   e=$((Сумма переменных a and b))
```   

### 2. На нашем локальном сервере упал сервис и мы написали скрипт, который постоянно проверяет его доступность, записывая дату проверок до тех пор, пока сервис не станет доступным. В скрипте допущена ошибка, из-за которой выполнение не может завершиться, при этом место на Жёстком Диске постоянно уменьшается. Что необходимо сделать, чтобы его исправить:
``` 
while ((1==1)
do
curl https://localhost:4757
if (($? != 0))
then
date >> curl.log
fi
done
```
```
2.
  while ((1==1))
  do
  dt=$(date +"%M-%S")
  curl https://localhost:4757
  if (($? != 0))
  then 
      date >> curl$dt.log
      echo "Host is unreachable" >> curl$dt.log
   else
      date >> curl$dt.log
      echo "Host is reachable" >> curl$dt.log
      break
  fi
  find curl*.log -cmin +30 -delete
  done
  
  1- Бесконечный цикл заменить на цикл с условием (например по времени создания)
  2- Удалять временные файлы старше определенного времени создания
  3- Прерывать по условию (если файл слишком сильно вырос, крайний случай)
  ```
  
### 3.Необходимо написать скрипт, который проверяет доступность трёх IP: 192.168.0.1, 173.194.222.113, 87.250.250.242 по 80 порту и записывает результат в файл log. Проверять доступность необходимо пять раз для каждого узла.  
  
3.
@bash@
  #!/bin/bash
  for ii in {0..4}
  do
  curl -sm 1 http://192.168.0.1
  if (($?==0))
        then
        echo "192... Host is reachable" >> curl192.log
        else
        echo "Host is unreachable" >> curl192.log
  fi
  curl -sm 1 http://173.194.222.113
  if (($?==0))
        then
        echo "173... Host is reachable" >> curl173.log
        else
        echo "Host is unreachable">>curl173.log
 fi
 curl -sm 1 http://87.250.250.242
 if (($?==0))
        then
        echo "87... Host is reacheble" >> curl87.log
        else
        echo "Host is unreachable">>curl187.log
 fi
done
```
### 4. Необходимо дописать скрипт из предыдущего задания так, чтобы он выполнялся до тех пор, пока один из узлов не окажется недоступным. Если любой из узлов недоступен - IP этого узла пишется в файл error, скрипт прерывается
```
4.
#!/bin/bash
# n=0
while ((1==1)) # Можно n==1
do
 curl -sm 1 http://192.168.0.1
 if (($?==0))
        then
        echo "192... Host is reachable" >> curl192.log
        else
        echo "192... Host is unreachable" >> curl192.log
        break # n=1
 fi
 curl -sm 1 http://173.194.222.113
 if (($? ==0))
        then
        echo "173... Host is reachable" >> curl173.log
        else
        echo "173... Host is unreachable">>curl173.log
        break # n=1
 fi
 curl -sm 1 http://87.250.250.242
 if (($? ==0))
        then
        echo "87... Host is reachable" >> curl87.log
        else
        echo "87... Host is unreachable">>curl187.log
        break # n=1
 fi
done
```
