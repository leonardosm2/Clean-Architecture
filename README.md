# Aplicação de criação e listagem de orders

Esta aplicação permite criar e listar orders usando três diferentes tipos de endpoint: **REST**, **gRPC** e **GraphQL**.

A aplicação possui duas funcionalidades principais: criar order (com calculo de preço final) (`create order`) e listar orders (`list orders`). Os endpoints estão disponíveis da seguinte forma: REST API em `/order` (porta 8000), gRPC na porta 50051 e GraphQL na porta 8080.

## Como executar a aplicação

1. Certifique-se de ter o Docker e o Go instalados.
2. Suba os containers necessários executando o comando:
    ```bash
    docker-compose up
    ```
3. Aguarde até que a mensagem de que a aplicação está rodando nas três portas seja exibida nos logs.
4. Pronto! A aplicação estará rodando nas seguintes portas:
   - REST API: **Porta 8000**
   - gRPC: **Porta 50051**
   - GraphQL: **Porta 8080**

## Testando a aplicação

### REST API
- Para criar uma order, envie uma requisição `POST` para `http://localhost:8000/order`, use o modelo disponível em `api/create_order.http`.
- Para listagem das orders, envie uma requisição `GET` para `http://localhost:8000/order`, use o modelo disponível em `api/list_orders.http`.

### gRPC
- Utilize um cliente como [Evans](https://github.com/ktr0731/evans).
- Execute os comandos (para Evans):
    ```bash
    evans -r repl --host localhost --port 50051
    ```

- Criação da order:
    ```bash
    call CreateOrder
    ```

- Listagem das orders:
    ```bash
    call ListOrders
    ```

### GraphQL
- Acesse o playground do GraphQL em `http://localhost:8080`.
- Para criar uma order, utilize a seguinte mutation (ajuste os valores de input):
    ```graphql
    mutation createOrder {
        createOrder(input: {id: "b", Price: 10, Tax: 2}){
            id
            Price
            Tax
            FinalPrice
        }
    }
    ```

- Para listagem das orders, utilize a query:
    ```graphql
    query listOrders {
        listOrders {
            id
            Price
            Tax
            FinalPrice
        }
    }
    ```

## Observações

Certifique-se de que todas as dependências estão instaladas e de que o `docker-compose` está em execução para garantir o funcionamento correto dos serviços.