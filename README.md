# Docker
Docker hints

Создание контекста:

```
docker context create some-context-label --docker "host=ssh://user@remote_server_ip"

docker context use some-context-label

docker ps
# A list of remote containers on my local machine! It works!
```
Команды:
- `-it`: Создает интерактивный терминал (TTY) в контейнере, позволяя вам взаимодействовать с командной строкой внутри контейнера.
- `-d или --detach`: Запускает контейнер в фоновом режиме (detached mode), освобождая терминал после запуска контейнера.
- `-u или --user`: Устанавливает имя пользователя или UID (User Identifier), под которым будет выполняться процесс внутри контейнера.
- `-rem или --remote`: Указывает, что команда должна быть выполнена на удаленном Docker-хосте, а не на локальной машине.

Source: [Добавить в констект докера машину](https://stackoverflow.com/questions/60425053/vs-code-connect-a-docker-container-in-a-remote-server): смотри комментарий.
