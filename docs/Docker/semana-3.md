---
id: semana-3
title: Semana 3 - Docker Hub e Repositórios Privados
---

Tarefas:
Explorar o Docker Hub:
Criar uma conta gratuita no Docker Hub.
Fazer login via CLI:
bash
Copiar código
docker login


Fazer o push de uma imagem criada anteriormente:
bash
Copiar código
docker tag meu_nginx `<seu-usuario>`/meu_nginx
docker push `<seu-usuario>`/meu_nginx


Baixar a imagem de volta em outro local.
Aprender sobre repositórios privados:
Entender as diferenças entre o Docker Hub gratuito e pago.
Conceito de registro privado (ex.: usando ferramentas como Harbor ou AWS Elastic Container Registry - ECR).
Exercício:
Configurar um repositório privado local usando Docker Registry:
bash
Copiar código
docker run -d -p 5000:5000 --name registry registry:2
Fazer push e pull de uma imagem para o repositório local.

