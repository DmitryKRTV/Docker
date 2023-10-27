# Docker

*Docker* – это платформа для разработки, доставки и выполнения приложений с использованием контейнеризации.

Контейнеры Docker позволяют упаковывать приложения и их зависимости в изолированные окружения, которые могут быть запущены на любой машине, поддерживающей Docker, без проблем совместимости.

Основные компоненты Docker включают:
- **Docker Engine**: Это среда выполнения, которая управляет контейнерами Docker. Она включает в себя демон (dockerd), который работает на хост-машине, и клиентский интерфейс (docker), который предоставляет команды для взаимодействия с демоном.
- **Docker Images**: Образы Docker представляют собой исполняемые пакеты, которые содержат все необходимое для запуска приложения, включая код, зависимости, настройки и т.д. Образы могут быть созданы на основе Dockerfile, который описывает инструкции по сборке образа.
- **Docker Containers**: Контейнеры Docker являются экземплярами образов. Они создаются из образа и позволяют запустить приложение в изолированной среде. Контейнеры могут быть запущены, остановлены, перемещены и удалены.
- **Docker Compose**: Это инструмент, который позволяет определить и управлять многоконтейнерными приложениями с помощью файла конфигурации YAML. Docker Compose позволяет запускать и масштабировать несколько контейнеров вместе, определять их зависимости и настройки.

Часто используемые Команды:
- `ctrl + p и ctrl + q` - выйти из контейнера, не останавливая его
- `docker ps -a` — позволяет посмотреть, какие контейнеры находятся в системе;
- `docker ps -l` — показывает последние созданные контейнеры;
- `docker start` «CONTAINER ID» — запуск остановленного контейнера;
- `docker stop peaceful_minsky` — выключение активного контейнера;
- `docker stop «CONTAINER ID» && docker start «CONTAINER ID»` — перезагрузка контейнера без его отключения;
- `docker-compose up -d --no-deps –build` — запуск compose контейнера;
- `docker rm «ID OR NAME CONTAINER»` — удаление контейнера.
---
**Создать Dockerfile**
```
touch Dockerfile
```
---

**Заполнить Dockerfile**
```
FROM ubuntu
RUN apt update && apt install -y mc
```
Дополнительно:
- FROM — определяет, что будет использоваться в качестве базового образа (в данном случае образ ubuntu).
- RUN — запускает команду.
---
**Создать новый docker образ из Dockerfile**
```
docker build -t myapp:latest .
```
ИЛИ
```
docker build -f /path/to/Dockerfile --build-arg VERSION=1.0 -t myapp:v1.0 .
```

Дополнительно:
- `-t` -  созадёт тег(идентификатор), который связывает образ с конкретной версией или меткой.
- `-f` -  объявить полный путь к Dockerfile.
- `.` - путь к директории с Dockerfile
---

**Список образов**
```
docker images
```
---

**Запуск контейнера**

```
docker run <имя_образа>
```

Например, `docker run ubuntu` запустит контейнер на основе образа Ubuntu. По умолчанию контейнер будет запущен в интерактивном режиме и присоединится к текущему терминалу.

Флаги:
- `-it`: Создает интерактивный терминал (TTY) в контейнере, позволяя вам взаимодействовать с командной строкой внутри контейнера.
- `-d или --detach`: Запускает контейнер в фоновом режиме (detached mode), освобождая терминал после запуска контейнера.
- `-u или --user`: Устанавливает имя пользователя или UID (User Identifier), под которым будет выполняться процесс внутри контейнера.
- `-rem или --remote`: Указывает, что команда должна быть выполнена на удаленном Docker-хосте, а не на локальной машине.

**Запуск контейнера в фоновом режиме (detached mode):**

```
docker run -d <имя_образа>
```

Добавление флага `-d` позволяет запустить контейнер в фоновом режиме, без присоединения к текущему терминалу. Контейнер будет работать в фоновом режиме и вы получите обратно контроль над вашим терминалом.

**Присоединение к контейнеру и взаимодействие с его терминалом:**

```
docker run -it <имя_образа>
```

Флаги `-it` позволяют взаимодействовать с терминалом контейнера. Это полезно, например, для запуска интерактивной сессии внутри контейнера или выполнения команд в его контексте.

**Проброс портов между хостом и контейнером:**

```
docker run -p <хост_порт>:<контейнер_порт> <имя_образа>
```

С помощью флага `-p` можно пробросить порты между хостом и контейнером. Например, `docker run -p 8080:80 nginx` пробросит порт 80 внутри контейнера на порт 8080 на хосте.

**Монтирование томов (volumes):**

```
docker run -v <хост_путь>:<контейнер_путь> <имя_образа>
```

Флаг `-v` позволяет монтировать томы (volumes) между хостом и контейнером. Например, `docker run -v /host/path:/container/path nginx` монтирует хостовую директорию `/host/path` внутри контейнера по пути `/container/path`.

**Задание переменных среды:**

```
docker run -e <переменная>=<значение> <имя_образа>
```

Флаг `-e` позволяет задать переменные среды в контейнере. Например, `docker run -e MYSQL_ROOT_PASSWORD=secret mysql` задает переменную среды `MYSQL_ROOT_PASSWORD` со значением `secret` в контейнере MySQL.

**Подключиться к контейнеру:**

```
docker exec -i -t «CONTAINER ID»
```
ИЛИ
```
docker container attach «CONTAINER ID»
```

---

Создание контекста:

```
docker context create some-context-label --docker "host=ssh://user@remote_server_ip"

docker context use some-context-label

docker ps
# A list of remote containers on my local machine! It works!
```

Source: [Добавить в констект докера машину](https://stackoverflow.com/questions/60425053/vs-code-connect-a-docker-container-in-a-remote-server): смотри комментарий.
