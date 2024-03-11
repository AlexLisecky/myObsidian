**Обновляем Ubuntu**
```console
sudo apt update
```
***

**Устанавливаем дополнительные пакеты**
```console
sudo apt install curl software-properties-common ca-certificates apt-transport-https -y
```
***

**Импортируем `GPG-ключ`**
```console
wget -O- https://download.docker.com/linux/ubuntu/gpg | gpg --dearmor | sudo tee /etc/apt/keyrings/docker.gpg > /dev/null
```
***

**Добавляем репозиторий докера**
```console
echo "deb [arch=amd64 signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu jammy stable"| sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```
***
**Обновляем Ubuntu**
```console
sudo apt update
```
***
**Проверяем репозиторий**
```console
apt-cache policy docker-ce
```
***

**Устанавливаем докер**
```console
sudo apt install docker-ce -y
```
***
**Проверяем**
```console
sudo systemctl status docker
```
***
**Устанавливаем Docker-compose**
```console
sudo apt-get install docker-compose
```
***
**Проверяем версию**
```
docker-compose --version
```

**Пример вывода**
```console
>>> docker-compose version 1.29.2, build unknown
```