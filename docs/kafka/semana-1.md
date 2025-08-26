---
id: semana-1
title: Semana 1 - Fundamentos e Kafka
---

# Semana 1 - Fundamentos de Mensageria e Kafka

Compreender conceitos de mensageria, brokers, tópicos, filas e consumidores,  Conhecer Apache Kafka: arquitetura, vantagens, casos de uso. Instalar Kafka localmente usando Docker, Produzir e consumir mensagens usando CLI.



### 🏛️  1. Fundamentos de Mensageria e Arquitetura do Apache Kafka
1.1 O que é Mensageria?
É um padrão de comunicação assíncrona entre sistemas. Ao invés de uma aplicação chamar diretamente outra, ela envia mensagens para uma Broker que intermedia a comunicação.

1.2 Conceitos principais:

    1.2.2- Tópico: canal onde as mensagens são publicadas e de onde os consumidores leem. Kafka usa tópicos, não filas. Cada tópico pode ter várias partições, permitindo escalabilidade e paralelismo.

    1.2.3- Fila: conceito clássico onde uma mensagem é consumida por apenas um consumidor. No Kafka, isso é obtido através de particionamento e grupos de consumidores. Dessa maneira o conceito de fila, "by the book" não se aplica ao kafka ao invés da fila ele usa Tópicos permitindo assim que não apenas 1 único consumidor leia a fila mas um grupo de consumidores.

    1.2.4- Produtor: Aplicação que envia mensagens para o tópico. As Mensagens são replicadas entre brokers (para alta disponibilidade).

    1.2.5- Consumidor: Aplicações quem leem as mensagens para o tópico.

    1.2.6- Grupo de consumidores: consumidores agrupados para dividir o processamento de um tópico.

    1.2.7 Cluster: é o agrupamento de máquinas onde cada uma possui um broker.



1.3 Broker: servidor que recebe, armazena e entrega mensagens. (Ex.: Kafka, RabbitMQ). Pode haver múltiplos brokers em um cluster.

1.4 Zookeeper: gerencia o estado do cluster (nas versões antigas). Apartir da versão Kafka 3 Kafka não depende mais do Zookeeper como gerenciador de metadata nas versões mais recentes. utilizado o modo KRaft. 
* Até o Kafka 2.8, o Zookeeper ainda era necessário para produção, mas já estava disponível um modo opcional sem ele, chamado de KRaft Mode (Kafka Raft Metadata mode).

* A partir do Kafka 3.0, o suporte ao KRaft se tornou estável, mas o Zookeeper ainda podia ser usado.

* A partir do Kafka 3.5 (e planejado para ser definitivo no Kafka 4.0, que deve sair em 2025), o uso do Zookeeper será oficialmente removido.



### 💡 2. Vantagens do Kafka

#### 2.1. capabilities
✔️Alta performance (milhões de mensagens por segundo).

✔️Alta escalabilidade (horizontal via partições).

✔️Resiliência e tolerância a falhas (via replicação).

✔️Persistência de mensagens (mensagens ficam armazenadas por tempo configurado ou tamanho do log).

✔️Ecossistema robusto (Kafka Connect, Kafka Streams, ksqlDB).

#### 2.2 Casos de uso comuns:

✔️ Processamento de eventos (event-driven architecture).

✔️ Pipelines de dados (ETL em tempo real).

✔️ Log de atividades e monitoramento.

✔️ Integração de microsserviços.

✔️ Streaming de dados.

### 🐳 3. Instalação Kafka usando Docker
✔️ Crie um arquivo `docker-compose.yml`:

```
version: '3'

services:
  zookeeper:
    image: confluentinc/cp-zookeeper:latest
    environment:
      ZOOKEEPER_CLIENT_PORT: 2181
    ports:
      - "2181:2181"

  kafka:
    image: confluentinc/cp-kafka:latest
    ports:
      - "9092:9092"
    environment:
      KAFKA_BROKER_ID: 1
      KAFKA_ZOOKEEPER_CONNECT: zookeeper:2181
      KAFKA_ADVERTISED_LISTENERS: PLAINTEXT://localhost:9092
      KAFKA_OFFSETS_TOPIC_REPLICATION_FACTOR: 1
    depends_on:
      - zookeeper
```


✔️ Suba os serviços:
```
docker-compose up -d
```
✔️ Verifique se subiu:
```
docker ps
```
Deve aparecer o Kafka (cp-kafka) e o Zookeeper (cp-zookeeper).

### 🛠️ 4. Produzir e consumir mensagens via CLI
✔️ Acesse o container do Kafka:

```
docker exec -it <nome_do_container_kafka> bash
```
(Use docker ps para ver o nome do container.)

✔️ Criar um tópico:
```
kafka-topics --create \
  --topic meu-topico \
  --bootstrap-server localhost:9092 \
  --partitions 1 \
  --replication-factor 1
```
✔️ Listar tópicos:
```
kafka-topics --list --bootstrap-server localhost:9092
```
✔️ Produzir mensagens:

```
kafka-console-producer \
  --topic meu-topico \
  --bootstrap-server localhost:9092

  ```
Digite mensagens e pressione Enter para enviá-las. Use Ctrl+C para sair.

✔️ Consumir mensagens:
```
kafka-console-consumer \
  --topic meu-topico \
  --from-beginning \
  --bootstrap-server localhost:9092
  ```
Verá na tela as mensagens sendo lidas.

🔥 Dicas Finais:
Kafka não apaga mensagens automaticamente após o consumo (ao contrário de RabbitMQ). Ele mantém baseado em tempo ou tamanho do log.

Se quiser simular múltiplos consumidores, abra mais terminais rodando kafka-console-consumer.

