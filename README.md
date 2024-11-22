# Aplicação de criação e listagem de orders

Esta aplicação permite criar e listar orders usando três diferentes tipos de endpoint: **REST**, **gRPC** e **GraphQL**.

A aplicação possui duas funcionalidades principais: criar order (com calculo de preço final) (`create order`) e listar orders (`list orders`). Os endpoints estão disponíveis da seguinte forma: REST API em `/order` (porta 8000), gRPC na porta 50051 e GraphQL na porta 8080.

## Como executar a aplicação

1. Certifique-se de ter o Docker e o Go instalados.
2. Suba os containers necessários executando o comando:
    ```bash
    docker-compose up -d
    ```

3. Navegue até o diretório cmd/ordersystem 
4. Compile e execute o código Go com o comando:
    ```bash
    go run main.go wire_gen.go
    ```

4. Pronto! A aplicação estará rodando nas seguintes portas:
   - REST API: **Porta 8000**
   - gRPC: **Porta 50051**
   - GraphQL: **Porta 8080**

## Testando a aplicação

### REST API
- Para criar uma order, envie uma requisição `POST` para `http://localhost:8000/order`, use o modelo disponível em `api/create_order.http`.
- Para listar as orders, envie uma requisição `GET` para `http://localhost:8000/order`, use o modelo disponível em `api/list_orders.http`.

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
    Call ListOrders
    ```

### GraphQL
- Acesse o playground GraphQL em `http://localhost:8080`.
- Para criar uma order, utilize a seguinte mutation:
    ```graphql
    mutation createOrder {
        createOrder(input: {id: "cc", Price: 10, Tax: 2}){
            id
            Price
            Tax
            FinalPrice
        }
    }
    ```

- Para listar as orders, utilize a query:
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