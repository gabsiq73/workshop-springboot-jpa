# 🚀 Projeto web services com Spring Boot e JPA / Hibernate 
Este projeto foi desenvolvido como parte de um curso de **Java com Spring Boot**, com o objetivo de praticar a construção de uma aplicação RESTful utilizando **Spring Boot**, **JPA/Hibernate** e **H2 Database**.  

O sistema implementa um modelo de domínio com entidades relacionadas (Usuário, Pedido, Produto, Categoria, Pagamento, etc.), permitindo operações básicas de **CRUD** e tratamento de exceções.  
<br><br>
## 🎯 Objetivos  
- Criar projeto **Spring Boot Java**  
- Implementar **modelo de domínio**  
- Estruturar camadas lógicas: `resource`, `service`, `repository`  
- Configurar banco de dados de teste (**H2**)  
- Povoar o banco de dados automaticamente  
- Implementar **CRUD** (Create, Retrieve, Update, Delete)  
- Tratar exceções personalizadas  
<br><br>
## 🛠️ Tecnologias  
- **Java 17**  
- **Spring Boot**  
  - Spring Web  
  - Spring Data JPA  
- **H2 Database** (ambiente de teste)  
- **Maven**  
<br><br>
## 💻 Instalação  

1. Clone este repositório:  
   ```bash
   git clone https://github.com/seu-usuario/seu-repo.git
   cd seu-repo
   ```

2. Compile o projeto com Maven:  
   ```bash
   mvn clean install
   ```

3. Execute a aplicação:  
   ```bash
   mvn spring-boot:run
   ```
<br><br>
## ⚙️ Configuração  

### `application.properties`  
```properties
spring.profiles.active=test
spring.jpa.open-in-view=true
```

### `application-test.properties`  
```properties
# Datasource H2
spring.datasource.driverClassName=org.h2.Driver
spring.datasource.url=jdbc:h2:mem:testdb
spring.datasource.username=sa
spring.datasource.password=

# H2 Console
spring.h2.console.enabled=true
spring.h2.console.path=/h2-console

# JPA
spring.jpa.database-platform=org.hibernate.dialect.H2Dialect
spring.jpa.defer-datasource-initialization=true
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.format_sql=true
```

🔗 Acesse o console do H2 em:  
```
http://localhost:8080/h2-console
```
<br><br>
## ▶️ API EndPoints


### Users  
```http
GET /users
GET /users/{id}
POST /users
PUT /users/{id}
DELETE /users/{id}
```
### Products
```http
GET /products
GET /products/{id}
```
### Orders
```http
GET /orders
GET /orders/{id}
```
### Categories
```http
GET /categories
GET /categories/{id}
```
<br><br>
## Uso/Exemplos
Exemplo de **busca de pedidos**

```http
GET /orders/{id}
```

```json
{
    "id": 1,
    "moment": "2019-06-20T19:53:07Z",
    "orderStatus": "PAID",
    "client": {
        "id": 1,
        "name": "Maria Brown",
        "email": "maria@gmail.com",
        "phone": "988888888",
        "password": "123456"
    },
    "items": [
        {
            "quantity": 2,
            "price": 90.5,
            "subTotal": 181.0,
            "product": {
                "id": 1,
                "name": "The Lord of the Rings",
                "description": "Lorem ipsum dolor sit amet, consectetur.",
                "price": 90.5,
                "imgUrl": "",
                "categories": [
                    {
                        "id": 2,
                        "name": "Books"
                    }
                ]
            }
        },
        {
            "quantity": 1,
            "price": 1250.0,
            "subTotal": 1250.0,
            "product": {
                "id": 3,
                "name": "Macbook Pro",
                "description": "Nam eleifend maximus tortor, at mollis.",
                "price": 1250.0,
                "imgUrl": "",
                "categories": [
                    {
                        "id": 3,
                        "name": "Computers"
                    }
                ]
            }
        }
    ],
    "payment": {
        "id": 1,
        "moment": "2019-06-20T21:53:07Z"
    },
    "total": 1431.0
}
```

Exemplo de **busca de produto**

```http
GET /products/${id}
```
```json
{
    "id": 1,
    "name": "The Lord of the Rings",
    "description": "Lorem ipsum dolor sit amet, consectetur.",
    "price": 90.5,
    "imgUrl": "",
    "categories": [
        {
            "id": 2,
            "name": "Books"
        }
    ]
}
```

Exemplo de **inserção de usuário**:  
```http
POST /users}
```
```json
{
  "name": "Bob Brown",
  "email": "bob@gmail.com",
  "phone": "977557755",
  "password": "123456"
}
```

Exemplo de **atualização de usuário** 
```http
PUT /users/{id}}
```
```json
{
  "name": "Bob Brown",
  "email": "bob@gmail.com",
  "phone": "977557755"
}
```
<br><br>

## 📊 Modelo de Domínio  
O projeto inclui as seguintes entidades principais:  
- **User** (Usuário)  
- **Order** (Pedido)  
- **Category** (Categoria)  
- **Product** (Produto)  
- **OrderItem** (Item do pedido, relacionamento N:N com atributos extras)  
- **Payment** (Pagamento, associação 1:1 com Pedido)

![Domain Model](https://raw.githubusercontent.com/gabsiq73/workshop-springboot-jpa/refs/heads/main/assets/domain%20model.png)
![Domain Instance](https://raw.githubusercontent.com/gabsiq73/workshop-springboot-jpa/refs/heads/main/assets/domain%20instance.png)

## 🏗️ Camadas Lógicas  
- **Resource (Controller):** expõe os endpoints REST  
- **Service:** contém as regras de negócio  
- **Repository:** abstração de acesso a dados com Spring Data JPA  
![Logical Layers](https://raw.githubusercontent.com/gabsiq73/workshop-springboot-jpa/refs/heads/main/assets/logical%20layers.png)
<br><br>
## ⚠️ Exceções  
O projeto trata exceções personalizadas para operações de:  
- **findById** → `ResourceNotFoundException`  
- **delete** → `DatabaseException`  
- **update** → `EntityNotFoundException`  
<br><br>
## Autores
- Gabriel Siqueira
[@gabsiq73](https://github.com/gabsiq73)
- Projeto desenvolvido como exercício do curso **Java COMPLETO - DevSuperior** ministrado por [Nelio Alves](https://devsuperior.com.br).  

<br><br>
## 📄 Licença  
Este projeto é apenas para **fins educacionais**.  
