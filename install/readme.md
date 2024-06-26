# Установка docker по шагам на Ubuntu 22.04

##  **1. Обновить пакеты**
```
sudo apt update
```
## **2. Утсановка доп пакетов**

curl — необходим для работы с веб-ресурсами;\
software-properties-common — пакет для управления ПО с помощью скриптов;\
ca-certificates — содержит информацию о центрах сертификации;\
apt-transport-https — необходим для передачи данных по протоколу HTTPS.

```
sudo apt install curl software-properties-common ca-certificates apt-transport-https -y
```
## **3. Импортируем GPG-ключ**

GPG-ключ нужен для верификации подписей ПО. Он понадобится для добавления репозитория докера в локальный список. Импортируем GPG-ключ
```
wget -O- https://download.docker.com/linux/ubuntu/gpg | gpg --dearmor | sudo tee /etc/apt/keyrings/docker.gpg > /dev/null
```

## **4. Добавляем репозиторий докера**

Добавим репозиторий для нашей версии Ubuntu, которая называется «Jammy». Для других версий ОС нужно использовать их кодовые имена, которые были перечислены в разделе «Системные требования». Выполняем команду:
```
echo "deb [arch=amd64 signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu jammy stable"| sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```
Во время выполнения терминал попросит подтвердить выполнение операции. Нажимаем Enter.

## **5. Обновляем индексы пакетов**
```
sudo apt update
```

## **6. Проверяем репозиторий**

Убедимся, что инсталляция будет осуществлена из нужного нам репозитория. Выполняем следующую команду:
```
apt-cache policy docker-ce
```
В зависимости от выхода новых версий докера вывод может иметь другой вид. Главное убедиться, что установка будет осуществляться из репозитория докера. 

## **7. Устанавливаем докер**

```
sudo apt install docker-ce -y
```

После выполнения команды начнется установка докера.

Убедимся в успешности установки, проверив статус докера в системе:
```
sudo systemctl status docker
```

## **8. Добавить имя пользователя в группу Docker**

```
sudo usermod -aG docker user
```
Где user — имя пользователя.

## **9. Перезапустить терминал**

Для применения изменений добавления пользователя в друппу, необходимо перезаупстить терминал или выполнить команду

```
su - user
```

## **(Опционально) Проверьте доступ к образам Docker**

```
docker run hello-world
```
## ССылки
https://help.reg.ru/support/servery-vps/oblachnyye-servery/ustanovka-programmnogo-obespecheniya/kak-ustanovit-docker-na-ubuntu
https://timeweb.cloud/tutorials/docker/kak-ustanovit-docker-na-ubuntu-22-04
