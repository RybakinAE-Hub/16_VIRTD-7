# Домашнее задание к занятию 2. «Применение принципов IaaC в работе с виртуальными машинами» - Рыбакин Алексей

## Задача 1

- Опишите основные преимущества применения на практике IaaC-паттернов.
```
- проэкт не мертв, он обслуживается и развивается
- Скорость и уменьшение затрат
- Восстановление после сбоев
- удобно масштабировать
- легко вносить изменения
- сокращет время для подготовки площадки тестирования проэктов
- создаёт безопастную, изолированную систему друг от друга.
```

- Какой из принципов IaaC является основополагающим?

```Идемпотентность - свойство объекта или операции при повторном применении операции к объекту давать тот же результат,
что и при первом.```

## Задача 2

- Чем Ansible выгодно отличается от других систем управление конфигурациями?
```
- При неуспешной доставке конфигурации на сервер, предупредит.
- используется удобный код в формате YAML.
- Работает как есть без агентов.
- хорошо развит и развивается
```
- Какой, на ваш взгляд, метод работы систем конфигурации более надёжный — push или pull?
```
у каждого есть свои плюсы. Но вопрос задан о НАДЁЖНОСТИ.
- pull - надежный в том что, хосты сами запрашивают информацию об изменениях с центрального сервера. это гарантирует актуальность информации.
- push - надежный в том что, централный сервер отправляет информацию на хосты. это гарантирует одновременое изменение, но возможно понижения скорости
В этих случаях надежнее - push
```
## Задача 3

Установите на личный linux-компьютер(или учебную ВМ с linux):

- VirtualBox
```
Версия 7.0.4 r154605 (Qt5.15.2)
```
- Vagrant
```
Installed Version: 2.4.0
Latest Version: 2.4.1
```
- Terraform
```Terraform v1.5.7
on linux_amd64
```
- Ansible.
```
ansible 2.10.8
  config file = None
  configured module search path = ['/home/user/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']
  ansible python module location = /usr/lib/python3/dist-packages/ansible
  executable location = /usr/bin/ansible
  python version = 3.9.2 (default, Feb 28 2021, 17:03:44) [GCC 10.2.1 20210110]

```
*Приложите вывод команд установленных версий каждой из программ, оформленный в Markdown.*

## Задача 4 

Воспроизведите практическую часть лекции самостоятельно.

- Создайте виртуальную машину.
- Зайдите внутрь ВМ, убедитесь, что Docker установлен с помощью команды
```
docker ps,
```
Vagrantfile из лекции и код ansible находятся в [папке](https://github.com/netology-code/virt-homeworks/tree/virt-11/05-virt-02-iaac/src).

Примечание. Если Vagrant выдаёт ошибку:
```
URL: ["https://vagrantcloud.com/bento/ubuntu-20.04"]     
Error: The requested URL returned error: 404:
```

выполните следующие действия:

1. Скачайте с [сайта](https://app.vagrantup.com/bento/boxes/ubuntu-20.04) файл-образ "bento/ubuntu-20.04".
2. Добавьте его в список образов Vagrant: "vagrant box add bento/ubuntu-20.04 <путь к файлу>".

Важно!: Если ваша хостовая рабочая станция - это windows ОС, то у вас могут возникнуть проблемы со вложенной виртуализацией.  [способы решения](https://www.comss.ru/page.php?id=7726)  . Если вы устанавливали hyper-v или docker desktop то  все равно может возникать ошибка: Stderr: VBoxManage: error: AMD-V 
VT-X is not available (VERR_SVM_NO_SVM) . Попробуйте в этом случае выполнить в windows от администратора команду: "bcdedit /set hypervisorlaunchtype off" и перезагрузиться

Ответ:
PLAY [nodes] *******************************************************************

TASK [Gathering Facts] *********************************************************
ok: [server1.netology]

TASK [Create directory for ssh-keys] *******************************************
ok: [server1.netology]

TASK [Adding rsa-key in /root/.ssh/authorized_keys] ****************************
changed: [server1.netology]

TASK [Checking DNS] ************************************************************
changed: [server1.netology]

TASK [Installing tools] ********************************************************
ok: [server1.netology] => (item=git)
ok: [server1.netology] => (item=curl)

TASK [Installing docker] *******************************************************
changed: [server1.netology]

TASK [Add the current user to docker group] ************************************
changed: [server1.netology]

PLAY RECAP *********************************************************************
server1.netology           : ok=7    changed=4    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

infernofeniks@iaac:~/hw-5.2$ vagrant ssh
Welcome to Ubuntu 20.04.6 LTS (GNU/Linux 5.4.0-144-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

 System information disabled due to load higher than 1.0


This system is built by the Bento project by Chef Software
More information can be found at https://github.com/chef/bento
Last login: Wed January 10 10:10:54 2024 from 10.0.2.2
vagrant@server1:~$ docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES


***Приложите скриншоты в качестве решения на эту задачу. Допускается неполное выполнение данного задания если не сможете совладать с Windows.*** 
