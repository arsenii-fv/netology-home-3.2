1.
 cd is a shell builtin
 Это внутренняя команда оболочки. Выполняется быстрее чем внешняя команда. Ввод и вывод выполняется внутри
 оболочки bash, поэтому удобнее ее использовать как внутреннюю команду. 
 
2. 
  grep <some_string> <some_file> | wc -l
  поиск строки  some_string в файле some_file и передача результата команде wc -l (счетчик строк)
  альтернатива grep -с <some_string> <some_file>

3.
  DISTRIB_DESCRIPTION="Ubuntu 20.04.1 LTS"
  /sbin/init 

4.
  сначала определим tty
  ls -l /root/ 2>/dev/pts/1 (вторая сессия)
  
5.
  cat < file1 > file2

6. 
   putty ssh 127.0.0.1:2222
   $tty 
   /dev/pts/1
   
   $ls > /dev/pts/0 выводит

7. 
  добавляет файловый дескриптор номер 5 командному интерпретатору bash в 
  специальный символьный файл chr устройства /dev/pts/0 и перенаправляет его в поток вывода
  echo netology > /proc/$$/fd/5	выводит на экран надпись через текущий процесс дескриптора 5

8.
  &ls -l /root 3>&1 1>&2 2>&3 3>&- | tee -a file1  - меняются местами дескрипторы 1 и 2
  
  $ls -l /root 2>&1 >/dev/null | cat  - теряется 1 дескриптор 
  
  
9.
   содержит переменные окружения, заданные на этапе запуска текущего процесса
   команда $env and $printenv

10. 
   cmdline содержит полную  командную  строку  запуска  процесса,  кроме  тех
   процессов,  что  полностью  ушли в своппинг, а также тех, что превратились в зомби.
   exe является символьной ссылкой, содержащей фактическое полное имя выполняемого файла.

11.
   sse4_2

12. 
  При ввыполнении команды ssh localhost "tty" , не выделяется новый псевдо терминал и не отрабатывает на текущем.
  Можно решить: ssh -t localhost "tty" , or ssh user@localhost и выполнить команду $tty

13.
  $top
  $ctrl+z
  $bg
  another tty
  $ps -a 
  $screen
  $reptyr 1214
  
14. 
   команда echo выводит строку используя стандартный поток stdout 
   команда tee перемещает данные из stdin в stdout и записывает их в файл
   

4. Зомби процессы не занимают ресурсы ОС (CPU, RAM, IO)
   Ядро поддерживает мин набор информации о зомби PID, статус, информацию об использовании ресурсов. Но зомби процессы занимают место в таблице процессов ядра, 
   если она заполнится то новые процессы создаваться не будут.   
7. ; - после этого символа выполняется следующая команда, т.е. последовательное выполнение команд в одной строке.
    && логическое И , при успешном выполнении предыдущей команды будет выполнена следующая.
    set -e полностью прерывает выполнение команд при неуспешном выполнении предыдущей. 
    Да при выполнении команд последовательно set -e можно заменить && , если в скрипте то в этом случае будет выход из скрипта что возможно не желательно.

8. https://silentsokolov.github.io/safe-bash-sctipts
  -e полностью прерывает выполнение сценария при неуспешном  выполнении предыдущей команды.
  -u  оболочка проверяет инициализацию переменных в скрипте. Если переменной не будет, скрипт немедленно завершиться.
  -x печатает в стандартный вывод все команды перед их исполнением
  -o Bash возвращает только код ошибки последней команды в пайпе (конвейере), а параметр -e проверяет только его. 

9. ps -o stat 
  выводит два процесса пользователя с метками
 S 
 R+
 ps -eo stat 
  выводит все процессы системы
  Процессы S, Ss, Ssl interruptible sleep (waiting for an event to complete)
   s лидер сессии
   l является многопоточным
