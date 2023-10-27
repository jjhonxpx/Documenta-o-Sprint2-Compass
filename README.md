
# Descrição das atividades solicitadas.

Uma documetação sobre a sprint 2.


## Instalação do Docker.
Atualizar o servidor.
```bash
  dnf update -y
```
Instale o Docker CE (edição comunitária)
Por padrão, a versão mais recente do pacote Docker não está incluída no repositório padrão do Oracle Linux, portanto, você precisará criar um repositório Docker CE.

Você pode criá-lo usando o seguinte comando:
```bash
dnf config-manager --add-repo=https://download.docker.com/linux/centos/docker-ce.repo
```
Em seguida, execute o seguinte comando para instalar o Docker CE em seu servidor.
```bash
dnf install docker-ce -y
```
Após a instalação, inicie o serviço Docker e habilite-o para iniciar na reinicialização do sistema.
```bash
systemctl start docker
systemctl enable docker
```
Em seguida, verifique o status de execução do serviço Docker usando o seguinte comando:
```bash
systemctl status docker
```
Exemplo de saída:
```bash
● docker.service - Docker Application Container Engine
   Loaded: loaded (/usr/lib/systemd/system/docker.service; disabled; vendor preset: disabled)
   Active: active (running) since Sat 2022-04-30 08:35:46 EDT; 6s ago
     Docs: https://docs.docker.com
 Main PID: 8554 (dockerd)
    Tasks: 8
   Memory: 31.7M
   CGroup: /system.slice/docker.service
           └─8554 /usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock

Apr 30 08:35:45 oraclelinux dockerd[8554]: time="2022-04-30T08:35:45.932297676-04:00" level=error msg="Failed to built-in GetDriver graph btr>
Apr 30 08:35:46 oraclelinux dockerd[8554]: time="2022-04-30T08:35:46.249687493-04:00" level=warning msg="Your kernel does not support cgroup >
Apr 30 08:35:46 oraclelinux dockerd[8554]: time="2022-04-30T08:35:46.249732672-04:00" level=warning msg="Your kernel does not support cgroup >
Apr 30 08:35:46 oraclelinux dockerd[8554]: time="2022-04-30T08:35:46.249960144-04:00" level=info msg="Loading containers: start."
Apr 30 08:35:46 oraclelinux dockerd[8554]: time="2022-04-30T08:35:46.682620546-04:00" level=info msg="Default bridge (docker0) is assigned wi>
Apr 30 08:35:46 oraclelinux dockerd[8554]: time="2022-04-30T08:35:46.861304346-04:00" level=info msg="Loading containers: done."
Apr 30 08:35:46 oraclelinux dockerd[8554]: time="2022-04-30T08:35:46.884014323-04:00" level=info msg="Docker daemon" commit=87a90dc graphdriv>
Apr 30 08:35:46 oraclelinux dockerd[8554]: time="2022-04-30T08:35:46.884186171-04:00" level=info msg="Daemon has completed initialization"
Apr 30 08:35:46 oraclelinux systemd[1]: Started Docker Application Container Engine.
Apr 30 08:35:46 oraclelinux dockerd[8554]: time="2022-04-30T08:35:46.934543023-04:00" level=info msg="API listen on /var/run/docker.sock"
```
Você também pode verificar a versão do Docker com informações adicionais usando o seguinte comando:
```bash
docker info
```
Verifique a instalação do Docker
Neste ponto, o Docker está instalado e em execução. Agora é hora de testar se está funcionando ou não.

Você pode baixar e executar o contêiner hello-world do Docker para testar o Docker.
```bash
docker run hello-world
```
Isso fará o download e executará o contêiner Docker hello-world em seu sistema
```bash
latest: Pulling from library/hello-world
2db29710123e: Pull complete 
Digest: sha256:10d7d58d5ebd2a652f4d93fdd86da8f265f5318c6a73cc5b6a9798ff6d2b2e67
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/
```
Você pode usar o comando “docker images” para verificar a imagem baixada:

Você obterá a seguinte saída:
```bash
REPOSITORY    TAG       IMAGE ID       CREATED        SIZE
hello-world   latest    feb5d9fea6a5   7 months ago   13.3kB
```
Instalando o Docker Compose
Por padrão, a versão mais recente do Docker Compose não está disponível no repositório padrão do Oracle Linux, portanto, você precisará baixá-la do repositório Git Hub.

Primeiro, instale o utilitário de comando curl com o seguinte comando:
```bash
dnf install -y curl
```
A seguir, baixe a versão mais recente do Docker Compose usando o seguinte comando:
```bash
curl -L https://github.com/docker/compose/releases/download/v2.21.0/docker-compose-linux-x86_64 -o /usr/local/bin/docker-compose
```
Em seguida, defina a permissão executável no binário Docker Compose:
```bash
chmod +x /usr/local/bin/docker-compose
```
Em seguida, verifique a versão do Docker Compose usando o seguinte comando:
```bash
docker-compose --version
```

## Instalação do Postgres no docker.
Baixe a imagem do Postgres
```bash
docker pull postgres
```
Crie um volume para persistência de dados
Antes de executar o contêiner, é importante criar um volume para persistência de dados. Isso garantirá que os dados do Postgres não sejam perdidos quando o contêiner for interrompido ou excluído. Para criar um volume, execute o seguinte comando em seu terminal:
```bash
docker volume create pgdata
```
Execute o contêiner Postgres
Com o volume criado, agora você pode executar o contêiner Postgres. Para fazer isso, execute o seguinte comando em seu terminal:

```bash
docker run -d --name postgres -p 5432:5432 -e POSTGRES_PASSWORD=sua-senha -v pgdata:/var/lib/postgresql/data postgres
```
Gerencie o contêiner Postgres
Você pode gerenciar o contêiner Postgres utilizando comandos Docker. Aqui estão alguns dos comandos mais úteis:

docker start postgres: esse comando é utilizado para iniciar o contêiner Postgres se ele estiver parado.

docker stop postgres: esse comando para o contêiner quando ele estiver em execução.

docker rm postgres: quando o contêiner estiver parado, esse comando remove o contêiner.

## Instalação do Wordpress no Docker
Criar um diretorio para o Wordpress
```bash
mkdir wordpress
```
Assim que estiver no diretório, abra qualquer editor de texto e crie um novo arquivo de nome docker-compose.yml.
```bash
touch docker-compose.yml
```
Abra o arquivo com o nano.
```bash
nano docker-compose.yml 
```
Cole o texto no arquivo .yml e salve as alterações:
```bash
version: '2'

services:
   db:
     image: mysql:5.7
     volumes:
       - db_data:/var/lib/mysql
     restart: always
     environment:
       MYSQL_ROOT_PASSWORD: somewordpress
       MYSQL_DATABASE: wordpress
       MYSQL_USER: wordpress
       MYSQL_PASSWORD: wordpress

   wordpress:
     depends_on:
       - db
     image: wordpress:latest
     ports:
       - "8000:80"
     restart: always
     environment:
       WORDPRESS_DB_HOST: db:3306
       WORDPRESS_DB_USER: wordpress
       WORDPRESS_DB_PASSWORD: wordpress
volumes:
    db_data:

```
Isso vai iniciar um serviço de base de dados MySQL, providenciando credenciais para a base de dados e puxar a imagem para instalar WordPress do Docker Hub.

Para rodar o arquivo, execute o comando:
```bash
docker-compose up -d
```
Agora em seu navegador entre localhost:8000 ou http://127.0.0.1:8000.