---

## Задача 1

Сценарий выполнения задачи:

- создайте свой репозиторий на https://hub.docker.com;
- выберите любой образ, который содержит веб-сервер Nginx;
- создайте свой fork образа;
- реализуйте функциональность:
запуск веб-сервера в фоне с индекс-страницей, содержащей HTML-код ниже:
```
<html>
<head>
Hey, Netology
</head>
<body>
<h1>I’m DevOps Engineer!</h1>
</body>
</html>
```
Опубликуйте созданный fork в своём репозитории и предоставьте ответ в виде ссылки на https://hub.docker.com/username_repo.  

https://hub.docker.com/r/maximofaa/netologyvirt/tags

![nginx](https://github.com/MaximovAA/devops_netology_term/blob/main/nginx1.jpg "Пример вывода команд")


## Задача 2

Посмотрите на сценарий ниже и ответьте на вопрос:
«Подходит ли в этом сценарии использование Docker-контейнеров или лучше подойдёт виртуальная машина, физическая машина? Может быть, возможны разные варианты?»

Детально опишите и обоснуйте свой выбор.

--

Сценарий:

- высоконагруженное монолитное Java веб-приложение;
- Nodejs веб-приложение;
- мобильное приложение c версиями для Android и iOS;
- шина данных на базе Apache Kafka;
- Elasticsearch-кластер для реализации логирования продуктивного веб-приложения — три ноды elasticsearch, два logstash и две ноды kibana;
- мониторинг-стек на базе Prometheus и Grafana;
- MongoDB как основное хранилище данных для Java-приложения;
- Gitlab-сервер для реализации CI/CD-процессов и приватный (закрытый) Docker Registry.

```
- высоконагруженное монолитное Java веб-приложение;
    Виртуальные машины - т.к. для обслуживания можно использовать инструменты высокой доступности системы виртуализации
- Nodejs веб-приложение;
    Docker-контейнеры - для удобства разработки и изменений
- мобильное приложение c версиями для Android и iOS;
    Docker-контейнеры - для удобства разработки и изменений
- шина данных на базе Apache Kafka;
    Docker-контейнеры или Виртуальные машины - основным требованиям тут будет являться доступность шины
- Elasticsearch-кластер для реализации логирования продуктивного веб-приложения — три ноды elasticsearch, два logstash и две ноды kibana;
    Виртуальные машины - большие объемы хранения данных или Docker-контейнеры с внешними хранилищами
- мониторинг-стек на базе Prometheus и Grafana;
    Docker-контейнеры для экономии ресурсов
- MongoDB как основное хранилище данных для Java-приложения;
    Виртуальные машины - т.к. для обслуживания можно использовать инструменты высокой доступности системы виртуализации
- Gitlab-сервер для реализации CI/CD-процессов и приватный (закрытый) Docker Registry.
    Docker-контейнеры и Виртуальные машины - гибридный вариант реализации, с учетом процесса разработки.
```


## Задача 3

- Запустите первый контейнер из образа ***centos*** c любым тегом в фоновом режиме, подключив папку ```/data``` из текущей рабочей директории на хостовой машине в ```/data``` контейнера.
- Запустите второй контейнер из образа ***debian*** в фоновом режиме, подключив папку ```/data``` из текущей рабочей директории на хостовой машине в ```/data``` контейнера.
- Подключитесь к первому контейнеру с помощью ```docker exec``` и создайте текстовый файл любого содержания в ```/data```.
- Добавьте ещё один файл в папку ```/data``` на хостовой машине.
- Подключитесь во второй контейнер и отобразите листинг и содержание файлов в ```/data``` контейнера.

```
root@deburunta:/home/amaksimov# docker images
REPOSITORY               TAG       IMAGE ID       CREATED             SIZE
maximofaa/netologyvirt   ver1      c5369a6ebd76   About an hour ago   143MB
debian                   latest    1ac99357ef21   4 days ago          124MB
centos                   latest    5d0da3dc9764   20 months ago       231MB

```
![mnt_data](https://github.com/MaximovAA/devops_netology_term/blob/main/mnt_data.jpg "Пример вывода команд")

## Задача 4 (*)

Воспроизведите практическую часть лекции самостоятельно.

Соберите Docker-образ с Ansible, загрузите на Docker Hub и пришлите ссылку вместе с остальными ответами к задачам.

```
Исправленная версия конфига:
```

```
FROM alpine:3.14
RUN  CARGO_NET_GIT_FETCH_WITH_CLI=1 && \
     apk --no-cache add \
sudo python3 py3-pip openssl ca-certificates sshpass openssh-client rsync git && \
     apk --no-cache add \
     --virtual build-dependencies python3-dev libffi-dev musl-dev gcc cargo openssl-dev \
        libressl-dev \
        build-base && \
     pip install --upgrade pip wheel && \
     pip install --upgrade cryptography cffi && \
     pip install ansible==2.9.24 && \
     pip install mitogen ansible-lint jmespath --ignore-installed && \
     pip install --upgrade pywinrm && \
     apk del build-dependencies && \
     rm -rf /var/cache/apk/* && \
     rm -rf /root/.cache/pip && \
     rm -rf /root/.cargo

RUN  mkdir /ansible && \
     mkdir -p /etc/ansible && \
     echo 'localhost' > /etc/ansible/hosts

WORKDIR /ansible
COPY ./ansible.cfg /ansible/

CMD  [ "ansible-playbook", "--version" ]

```
![ansible](https://github.com/MaximovAA/devops_netology_term/blob/main/ansible.jpg "Пример вывода команд")

