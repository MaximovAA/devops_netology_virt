---

## Задача 1

- Опишите основные преимущества применения на практике IaaC-паттернов.
- Какой из принципов IaaC является основополагающим?
```
- Опишите основные преимущества применения на практике IaaC-паттернов.
1. Ускорение производства и вывода продукта на рынок
2. Стабильность среды, устранение дрейфа конфигураций
3. Более быстрая и эффективная разработка
- Какой из принципов IaaC является основополагающим?
Идемпотентность — это свойство объекта или операции, при повторном выполнении
которой мы получаем результат идентичный предыдущему и всем последующим выполнениям
```

## Задача 2

- Чем Ansible выгодно отличается от других систем управление конфигурациями?
- Какой, на ваш взгляд, метод работы систем конфигурации более надёжный — push или pull?
```
- Чем Ansible выгодно отличается от других систем управление конфигурациями?
Для Ansible нетребуется устанавливать агентов в управляемые системы. 
В linux системах например подключение осуществляется средствами SSH.

- Какой, на ваш взгляд, метод работы систем конфигурации более надёжный — push или pull?
По мне более надежным является метод push, так как он позволяет централизованно 
и единообразно настраивать большое количество систем. И мы может сразу отследить успешность выполнения.
```

## Задача 3

Установите на личный компьютер:

- [VirtualBox](https://www.virtualbox.org/),
- [Vagrant](https://github.com/netology-code/devops-materials),
- [Terraform](https://github.com/netology-code/devops-materials/blob/master/README.md),
- Ansible.

*Приложите вывод команд установленных версий каждой из программ, оформленный в Markdown.*
```
amaksimov@deburunta:~$ vboxmanage --version
7.0.8r156879

amaksimov@deburunta:~$ vagrant --version
Vagrant 2.2.14

amaksimov@deburunta:~$ terraform version
Terraform v1.4.6
on linux_amd64

amaksimov@deburunta:~$ ansible --version
ansible 2.10.8
  config file = /home/amaksimov/ansible.cfg
  configured module search path = ['/home/amaksimov/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']
  ansible python module location = /usr/lib/python3/dist-packages/ansible
  executable location = /usr/bin/ansible
  python version = 3.9.2 (default, Feb 28 2021, 17:03:44) [GCC 10.2.1 20210110]

```

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
```
amaksimov@deburunta:~/vagrant$ vagrant provision
==> server1.netology: Running provisioner: ansible...
    server1.netology: Running ansible-playbook...

PLAY [Playbook] ****************************************************************

TASK [Gathering Facts] *********************************************************
ok: [server1.netology]

TASK [Installing tools] ********************************************************
ok: [server1.netology] => (item=['git', 'curl'])

TASK [Installing docker] *******************************************************
changed: [server1.netology]

TASK [Add the current user to docker group] ************************************
changed: [server1.netology]

PLAY RECAP *********************************************************************
server1.netology           : ok=4    changed=2    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```
```
vagrant@server1:~$ sudo docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```
