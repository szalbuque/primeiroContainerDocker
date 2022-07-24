# Estudando docker

https://www.freecodecamp.org/portuguese/news/um-guia-para-iniciantes-em-docker-como-criar-sua-primeira-aplicacao-com-o-docker/

# Criei uma vm na Azure
- Azure<br>
-- grupo de recursos containersAvanade50<br>
--- vm docker1 (ip 20.206.76.7)<br>
--- ssh -i azure azureuser@20.206.76.7<br>
--- sudo apt update<br>
--- sudo apt upgrade<br>
--- sudo apt install docker.io<br>
--- sudo docker run hello-world<br>

# To generate this message (hello-world), Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.


## Criei um script pequeno em Python e salvei no arquivo main.py, numa pasta que criei no /home/azureuser/testepy:
>  Este é o script:<br>
azureuser@docker1:~/testepy$ cat main.py<br>
#!/usr/bin/env python3<br>
print("O Docker é mágico!")


# Criei um dockerfile para criar um container com este script Python:
### Este é o dockerfile (o símbolo # inicia uma linha de comentário dentro do dockerfile):
https://github.com/szalbuque/primeiroContainerDocker/blob/main/dockerfile

# Usei o comando docker build para criar a imagem:
> azureuser@docker1:~/testepy$ sudo docker build -t python-test .<br>
<br>
(para gerar a imagem que vou poder subir no Docker Hub)<br>
docker build -t szalbuque/python-test .<br>
<br>

Sending build context to Docker daemon  3.584kB<br>
Step 1/3 : FROM python:latest<br>
 ---> 930516bcf910<br>
Step 2/3 : COPY main.py /<br>
 ---> 830334214516<br>
Step 3/3 : CMD [ "python", "./main.py" ]<br>
 ---> Running in d50431a05db3<br>
Removing intermediate container d50431a05db3<br>
 ---> 69b59e6caf12<br>
Successfully built 69b59e6caf12<br>
Successfully tagged python-test:latest<br>

## Usei o comando docker run para executar o código do container
>azureuser@docker1:~/testepy$ sudo docker run python-test<br>
O Docker é mágico!

## Usei o comando docker images para ver as imagens que estão na máquina:
azureuser@docker1:~/testepy$ sudo docker images<br>
REPOSITORY    TAG       IMAGE ID       CREATED         SIZE<br>
python-test   latest    69b59e6caf12   2 minutes ago   920MB<br>
hello-world   latest    feb5d9fea6a5   10 months ago   13.3kB<br>

## Para enviar a imagem ao Docker Hub
docker login<br>
 sudo docker push szalbuque/python-test<br>
