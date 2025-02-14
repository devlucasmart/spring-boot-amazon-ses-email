![Arquitetura do Microserviço](https://miro.medium.com/v2/resize:fit:640/format:webp/1*2STZmGfuaBZEACgUTTJzeg.png)
# Microserviço de Envio de E-mails com Amazon SES e RabbitMQ

## Descrição

Este microserviço é responsável por consumir e-mails de uma fila do RabbitMQ e enviá-los para o Amazon SES (Simple Email Service) da AWS. Ele foi desenvolvido com o objetivo de facilitar a integração e o envio de e-mails em massa, utilizando a infraestrutura do RabbitMQ para desacoplar o processo de envio e o Amazon SES para garantir a entrega eficiente e escalável de e-mails.

## Funcionalidades

- **Consumo de mensagens da fila RabbitMQ**: O serviço escuta uma fila no RabbitMQ onde os e-mails são enviados para processamento.
- **Envio de e-mails via Amazon SES**: Os e-mails consumidos da fila são enviados utilizando a API SMTP do Amazon SES.
- **Escalabilidade e performance**: A integração com o RabbitMQ permite que o serviço seja altamente escalável e resiliente, com a fila garantindo que os e-mails sejam processados de forma eficiente.

## Arquitetura

A arquitetura do microserviço é baseada em três componentes principais:

1. **RabbitMQ**: Fila de mensagens que armazena os e-mails a serem enviados.
2. **Microserviço Spring Boot**: Consome mensagens da fila e envia os e-mails para o SES da AWS.
3. **Amazon SES**: Serviço da AWS que gerencia o envio e a entrega dos e-mails.

## Fluxo de Funcionamento

1. Um sistema externo ou componente envia um e-mail para uma fila do RabbitMQ.
2. O microserviço Spring Boot consome as mensagens da fila.
3. O serviço usa a interface SMTP do Amazon SES para enviar os e-mails para os destinatários.
4. O status de envio (sucesso ou falha) pode ser registrado ou processado conforme necessário.

## Requisitos

- **Spring Boot**: Framework utilizado para desenvolver o microserviço.
- **RabbitMQ**: Sistema de filas utilizado para enviar os e-mails para o microserviço.
- **Amazon SES**: Serviço de envio de e-mails da AWS.
- **Java 11+**: Para rodar o microserviço.
- **Dependências do projeto**:
  - Spring Boot
  - Spring AMQP (para RabbitMQ)
  - Amazon SDK para SES
  - Dependências de segurança e configuração

## Como Rodar

### Pré-requisitos

- Certifique-se de ter o RabbitMQ configurado e rodando.
- Configure as credenciais do Amazon SES na sua aplicação Spring Boot (usuário, senha, região, etc.).

### Passos

1. Clone o repositório:

    ```bash
    git clone https://github.com/usuario/spring-boot-amazon-ses-email.git
    ```

2. Acesse o diretório do projeto:

    ```bash
    cd spring-boot-amazon-ses-email
    ```

3. Configure as credenciais do Amazon SES no arquivo `application.properties` ou `application.yml`:

    ```properties
    aws.ses.access-key-id=YOUR_AWS_ACCESS_KEY
    aws.ses.secret-access-key=YOUR_AWS_SECRET_KEY
    aws.ses.region=YOUR_AWS_REGION
    ```

4. Execute o projeto:

    ```bash
    ./mvnw spring-boot:run
    ```

O microserviço agora estará escutando a fila do RabbitMQ e enviando os e-mails para o SES da AWS.

## Licença

Este projeto está licenciado sob a [MIT License](LICENSE).
