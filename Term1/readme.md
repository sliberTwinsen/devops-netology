1. Установите средство виртуализации Oracle VirtualBox.
Ответ:
--------------------
sudo apt install virtualbox
2. Установите средство автоматизации Hashicorp Vagrant.
Ответ:
--------------------
sudo apt-get install vagrant
В вашем основном окружении подготовьте удобный для дальнейшей работы терминал.
Ответ:Hyper
--------------------
В приглашении добавлено текущее время и число фоновых процессов:
PS1='${debian_chroot:+($debian_chroot)}\t \[\033[01;32m\]\u@\h(\j)\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]\$ '
4. С помощью базового файла конфигурации запустите Ubuntu 20.04 в VirtualBox посредством Vagrant:
Ответ:
--------------------    
5. Ознакомьтесь с графическим интерфейсом VirtualBox, посмотрите как выглядит виртуальная машина, которую создал для вас Vagrant, какие аппаратные ресурсы ей выделены. Какие ресурсы выделены по-умолчанию?
Ответ:
--------------------:
RAM:1024mb
CPU:1 cpu
HDD:64gb
video:8mb
6. Ознакомьтесь с возможностями конфигурации VirtualBox через Vagrantfile: документация. Как добавить оперативной памяти или ресурсов процессора виртуальной машине?
Ответ:
добавлением комманд в VagrantFile:
короткие линки
  v.memory = 1024
  v.cpus = 2
или командами ВМ
   config.vm.provider "virtualbox" do |vb|
     vb.memory = "1024"
     vb.cpu = "2"
   end
  
7. Команда vagrant ssh из директории, в которой содержится Vagrantfile, позволит вам оказаться внутри виртуальной машины без каких-либо дополнительных настроек. Попрактикуйтесь в выполнении обсуждаемых команд в терминале Ubuntu.
Ответ:
--------------------    
8. Ознакомиться с разделами man bash, почитать о настройках самого bash:
 
8.2. какой переменной можно задать длину журнала history, и на какой строчке manual это описывается?
1. HISTFILESIZE - максимальное число строк в файле истории для сохранения, 
строка 1155
2. HISTSIZE - число команд для сохранения  , 
строка 1178
8.2. что делает директива ignoreboth в bash?
ignoreboth это сокращение для 2х директив ignorespace and ignoredups, 
    ignorespace - не сохранять команды начинающиеся с пробела, 
    ignoredups - не сохранять команду, если такая уже имеется в истории
9. В каких сценариях использования применимы скобки {} и на какой строчке man bash это описано?
Ответ:
{} - зарезервированные слова, список, в т.ч. список команд команд в отличии от "(...)" исполнятся в текущем инстансе, 
используется в различных условных циклах, условных операторах, или ограничивает тело функции, 
В командах выполняет подстановку элементов из списка , если упрощенно то  цикличное выполнение команд с подстановкой 
например mkdir ./DIR_{A..Z} - создаст каталоги сименами DIR_A, DIR_B и т.д. до DIR_Z
строка 343
10. Основываясь на предыдущем вопросе, как создать однократным вызовом touch 100000 файлов? А получилось ли создать 300000?
Ответ:
touch {000001..100000}.txt - создаст в текущей директории соответсвющее число фалов

300000 - создать не удасться, это слишком дилинный список аргументов, максимальное число получил экспериментально - 110188
11. В man bash поищите по /\[\[. Что делает конструкция [[ -d /tmp ]]
Ответ:
проверяет условие у -d /tmp и возвращает ее статус (0 или 1), наличие катаолга /tmp

Например в скрипте можно так:

if [[ -d /tmp ]]
then
    echo "каталог есть"
else
    echo "каталога нет"
fi
12. Основываясь на знаниях о просмотре текущих (например, PATH) и установке новых переменных; командах, которые мы рассматривали, добейтесь в выводе type -a bash в виртуальной машине наличия первым пунктом в списке:
Ответ:
root@ubuntu:~$ mkdir /tmp/new_path_dir/
root@ubuntu:~$ cp /bin/bash /tmp/new_path_dir/
root@ubuntu:~$ type -a bash
bash is /usr/bin/bash
bash is /bin/bash
root@ubuntu:~$ PATH=/tmp/new_path_dir/:$PATH
root@ubuntu:~$ type -a bash
bash is /tmp/new_path_dir/bash
bash is /usr/bin/bash
bash is /bin/bash
  
    
13. Чем отличается планирование команд с помощью batch и at?
Ответ:
at - команда запускается в указанное время (в параметре)
batch - запускается когда уровень загрузки системы снизится ниже 1.5.
14. Завершите работу виртуальной машины чтобы не расходовать ресурсы компьютера и/или батарею ноутбука.
Ответ:
--------------------: vagrant suspend
