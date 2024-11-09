# Wiremock

Este README fornece uma visão geral das configurações básicas e exemplos práticos de uso do Wiremock para simulação de APIs.


Wiremock é uma ferramenta poderosa para simular APIs e auxiliar em testes de integração e desenvolvimento de software. 

## Recursos

- [Documentação Wiremock](https://wiremock.org/docs/overview/)
- [Download do JAR Standalone](https://wiremock.org/docs/standalone/java-jar/)
- [Gerador de UUID Online](https://www.uuidgenerator.net/version4)

---

## Execução Standalone

Para rodar o Wiremock no modo standalone, use o seguinte comando:

```bash
java -jar <name_jar>.jar --global-response-templating --no-request-journal --port <port>
```

### Exemplo:
```bash
java -jar wiremock-standalone-3.9.1.jar --global-response-templating --no-request-journal --port 9090 --verbose
```

---

## Exemplos de Configuração de Mocks

### 1. Simulação de Requisição GET - Sem Arquivo

Arquivo: `get_data_basic.json`

```json
{
    "id" : "1768945d-c8f4-45f3-ad69-f80237ae8fa3",
    "name" : "get-resource-example1-return-200",
    "request" : {
      "urlPattern" : "/v1/tests",
      "method" : "GET"
    },
    "response" : {
      "status" : 200,
	    "body": "{\"id\": \"1\", \"result\": \"data\" }",
      "headers" : {
        "Content-Type" : "application/json;charset=UTF-8"
      }
    },
    "uuid" : "1768945d-c8f4-45f3-ad69-f80237ae8fa3",
    "persistent" : true,
    "priority": 1
}
```

### 2. Simulação de Requisição GET - Usando Arquivo

Arquivo: `get_data_file.json`

```json
{
    "id" : "357d4984-eb5b-49cb-9f02-f85b65b9b6d3",
    "name" : "get-resource-example2-return-200",
    "request" : {
      "urlPattern" : "/v1/tests",
      "method" : "GET"
    },
    "response" : {
      "status" : 200,
	  "bodyFileName" : "get_data_file.json",
      "headers" : {
        "Content-Type" : "application/json;charset=UTF-8"
      }
    },
    "uuid" : "357d4984-eb5b-49cb-9f02-f85b65b9b6d3",
    "persistent" : true,
    "priority": 2 
}  
```

---

## Exemplos de Requisições

### Health Check
```bash
curl --location 'http://localhost:9090/health'
```

### Get Data Basic
```bash
curl --location 'http://localhost:9090/v1/tests'
```

### Get Data Error 404 With Response Delay
```bash
curl --location 'http://localhost:9090/v1/tests/1'
```

### Get Data File Match Header
```bash
curl --location 'http://localhost:9090/v1/tests' \
--header 'Channel: APP'
```

### Get Data File
```bash
curl --location 'http://localhost:9090/v1/tests'
```

### Get Data Proxy
```bash
curl --location 'http://localhost:9090/v1/employees'
```

### Post Data With Pattern
```bash
curl --location 'http://localhost:9090/v1/product/12345/validate' \
--header 'Content-Type: application/json' \
--data '{
    "name": "Product 1",
    "status": "PROCESSING"
}'
```

### Post Data
```bash
curl --location --request POST 'http://localhost:9090/v1/tests'
```

---
