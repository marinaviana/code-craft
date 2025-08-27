---
id: semana-2
title: Semana 2 - Kafka Producer com C#
---

# Semana 2 - Produção de Mensagens com C#

## 🎯 Objetivos

- Criar um projeto .NET
- Instalar e configurar Confluent.Kafka
- Criar produtor Kafka com C#
- Enviar mensagens para tópico Kafka

1️⃣ Criar um projeto .NET

No terminal, rode:
```
dotnet new console -n KafkaProducerDemo
cd KafkaProducerDemo
```

Isso cria um app console chamado KafkaProducerDemo.

2️⃣ Instalar e configurar Confluent.Kafka

Dentro da pasta do projeto:
```
dotnet add package Confluent.Kafka
```

Isso baixa o client oficial Kafka para .NET.

3️⃣ Criar o produtor Kafka com C#

Abra o arquivo Program.cs e substitua o conteúdo por:
```
using Confluent.Kafka;

class Program
{
    static async Task Main(string[] args)
    {
        var config = new ProducerConfig
        {
            BootstrapServers = "localhost:9092" // endereço do Kafka
        };

        using var producer = new ProducerBuilder<Null, string>(config).Build();

       try
        {
            await producer.ProduceAsync(
                "topico-teste-tutorial",   // nome do tópico no Kafka
                new Message<Null, string> { Value = "treino kafka c#" }
            );
            for (int i = 0; i < 5; i++)
            {
                var message = $"Mensagem {i}";
                var result = await producer.ProduceAsync(
                    "topico-teste-tutorial",   // nome do tópico no Kafka
                    new Message<Null, string> { Value = message }
                );

                

                Console.WriteLine($"✔ Enviado: '{result.Value}' para {result.TopicPartitionOffset}");
            }
        }
        catch (ProduceException<Null, string> e)
        {
            Console.WriteLine($"❌ Erro ao enviar: {e.Error.Reason}");
        }
    }
}
```
4️⃣ Enviar mensagens para um tópico Kafka

Certifique-se de que o Kafka está rodando localmente (localhost:9092).
Se você usa Docker, pode iniciar assim:
```
docker compose up -d
```

(desde que tenha um docker-compose.yml do Kafka já configurado, caso ainda não tenha basta seguir a seção  [Instalação Kafka usando Docker](https://marinaviana.github.io/code-craft/docs/kafka/semana-1#-3-instala%C3%A7%C3%A3o-kafka-usando-docker) da semana 1: Fundamentos de Mensageria e Kafka).

Crie um tópico no Kafka (caso ainda não exista):
```
kafka-topics.sh --create --topic topico-teste-tutorial --bootstrap-server localhost:9092 --partitions 1 --replication-factor 1
```

Rode o programa:
```
dotnet run
```

Você deve ver as mensagens sendo enviadas e confirmadas no terminal.