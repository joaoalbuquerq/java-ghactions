# Spring Hello API

API mínima com Spring Boot e Spring Web para praticar Docker e publicação no Docker Hub.

## Requisitos

- Java 17 (para executar localmente)
- Maven 3.9+ (para executar localmente)
- Docker (para construir e executar a imagem)

## Executar localmente

```bash
mvn spring-boot:run
```

Acesse:

```text
http://localhost:8080/hello
```

Resposta esperada:

```text
Hello, World!
```

## Gerar o JAR

```bash
mvn clean package
```

## Construir a imagem Docker

Troque `SEU_USUARIO` pelo seu usuário do Docker Hub:

```bash
docker build -t SEU_USUARIO/spring-hello-api:1.0 .
```

## Executar o container

```bash
docker run --name spring-hello-api -p 8080:8080 SEU_USUARIO/spring-hello-api:1.0
```

Teste em outro terminal:

```bash
curl http://localhost:8080/hello
```

Para acompanhar os logs:

```bash
docker logs -f spring-hello-api
```

Para parar e remover o container:

```bash
docker stop spring-hello-api
docker rm spring-hello-api
```

## Enviar para o Docker Hub

1. Faça login:

```bash
docker login
```

2. Envie a imagem:

```bash
docker push SEU_USUARIO/spring-hello-api:1.0
```

## Baixar e executar em outra máquina

```bash
docker pull SEU_USUARIO/spring-hello-api:1.0
docker run --name spring-hello-api -p 8080:8080 SEU_USUARIO/spring-hello-api:1.0
```

Depois, acesse `http://localhost:8080/hello`.

> Observação: o Dockerfile usa build em duas etapas (multi-stage). O Maven compila a aplicação na primeira etapa; a imagem final contém apenas o runtime Java e o JAR.
