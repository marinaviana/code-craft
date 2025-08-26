---
id: semana-1
title: Semana 1 - Revisão dos Fundamentos
---

#Tarefas:
Revisar os conceitos básicos de Docker:
O que são containers, imagens e volumes.
Relação entre containers e imagens.
Praticar os comandos básicos:
docker container ls, docker ps, docker container ls -a.
docker image ls, docker volume ls.
Criar, parar e remover containers (docker run, docker stop, docker rm).
Exercício:
Baixar e rodar uma imagem simples do Docker Hub, como o Nginx:
bash
Copiar código
docker run -d -p 8080:80 nginx
Acessar o servidor web no navegador (http://localhost:8080).
Parar e remover o container.
