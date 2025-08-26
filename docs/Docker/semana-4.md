---
id: semana-4
title: Semana 4 - Deploy e Volumes
---

# Tarefas:
Volumes:
Criar e usar volumes persistentes:
bash
Copiar código
docker volume create meu_volume
docker run -v meu_volume:/dados ubuntu touch /dados/arquivo.txt


Verificar os dados no volume.
Deploy usando Docker Compose:
Criar um arquivo docker-compose.yml para rodar múltiplos containers, como Nginx e MySQL.
Comando:
bash
Copiar código
docker-compose up -d


Exercício:
Criar um projeto básico com Docker Compose para uma aplicação web com frontend e backend.
