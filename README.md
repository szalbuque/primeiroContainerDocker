# Estudando docker

https://www.freecodecamp.org/portuguese/news/um-guia-para-iniciantes-em-docker-como-criar-sua-primeira-aplicacao-com-o-docker/

# Criei uma vm na Azure
- Azure
-- grupo de recursos containersAvanade50
--- vm docker1 (ip 20.206.76.7)
--- ssh -i azure azureuser@20.206.76.7
--- sudo apt update
--- sudo apt upgrade
--- sudo apt install docker.io
--- sudo docker run hello-world

# To generate this message (hello-world), Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.


# criei um script pequeno em Python e salvei no arquivo main.py, numa pasta que criei no /home/azureuser/testepy:
>  Este é o script:
azureuser@docker1:~/testepy$ cat main.py
#!/usr/bin/env python3
print("O Docker é mágico!")


# Criei um dockerfile para criar um container com este script Python:
### Este é o dockerfile (o símbolo # inicia uma linha de comentário dentro do dockerfile):
### 

# Usei o comando docker build para criar a imagem:
azureuser@docker1:~/testepy$ sudo docker build -t python-test .
Sending build context to Docker daemon  3.584kB
Step 1/3 : FROM python:latest
 ---> 930516bcf910
Step 2/3 : COPY main.py /
 ---> 830334214516
Step 3/3 : CMD [ "python", "./main.py" ]
 ---> Running in d50431a05db3
Removing intermediate container d50431a05db3
 ---> 69b59e6caf12
Successfully built 69b59e6caf12
Successfully tagged python-test:latest

--- Usei o comando docker run para executar o código do container
azureuser@docker1:~/testepy$ sudo docker run python-test
O Docker é mágico!

--- Usei o comando docker images para ver as imagens que estão na máquina:
azureuser@docker1:~/testepy$ sudo docker images
REPOSITORY    TAG       IMAGE ID       CREATED         SIZE
python-test   latest    69b59e6caf12   2 minutes ago   920MB
hello-world   latest    feb5d9fea6a5   10 months ago   13.3kB


