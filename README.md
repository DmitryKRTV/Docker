# Docker
Docker hints

```
docker context create some-context-label --docker "host=ssh://user@remote_server_ip"

docker context use some-context-label

docker ps
# A list of remote containers on my local machine! It works!
```
Source: [Добавить в констект докера машину](https://stackoverflow.com/questions/60425053/vs-code-connect-a-docker-container-in-a-remote-server): смотри комментарий.
