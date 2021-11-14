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