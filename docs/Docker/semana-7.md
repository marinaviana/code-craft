---
id: semana-7
title: Semana 5 - Tópico Adicional Gerenciamento de Volumes e Imagens

---

# Imagens
Listar Imagens Disponíveis
Use docker image ls para visualizar todas as imagens no host local.
Remover Imagens
Para remover uma imagem específica:
bash
Copiar código
`docker image rm [IMAGE_ID]`


Para remover imagens não usadas (dangling images):
bash
Copiar código
docker image prune


Para remover todas as imagens não associadas a containers:
bash
Copiar código
`docker image prune -a`


Quando excluir imagens?
Imagens antigas ou que não são mais necessárias para seus projetos podem ser removidas.
Use docker image prune regularmente para limpar imagens não utilizadas.

Volumes
Listar Volumes Criados
Use docker volume ls para listar os volumes existentes.
Remover Volumes
Para remover um volume específico:
bash
Copiar código
`docker volume rm [VOLUME_NAME]`


Para remover volumes não utilizados por nenhum container:
bash
Copiar código
`docker volume prune`


Quando excluir volumes?
Volumes associados a projetos antigos ou não utilizados podem ser excluídos para liberar espaço.
Evite excluir volumes que contenham dados críticos ou que ainda possam ser usados.

Dicas
Antes de excluir volumes ou imagens, revise se eles estão associados a algum projeto ativo.
Use docker system df para verificar o uso de espaço em disco e entender onde você pode liberar mais espaço.
Agende momentos periódicos para limpar recursos Docker, como imagens, volumes, e containers parados, para manter seu ambiente limpo e eficiente.
