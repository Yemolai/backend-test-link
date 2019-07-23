# Teste Backend Developer

Este teste consiste no desenvolvimento de uma API REST para autenticação de cliente com JWT.

Desenvolva uma API REST em uma das opções abaixo:

  - Javascript ou Typescript usando Node.js
  - C# usando .NET Core 2.x
  - Java com Spring ou outro

Seja qual for a linguagem escolhida não há restrição de framework.

## Junior

A API deve ter a seguinte rota:

  - POST /login
    - Recebe user e password através do body da requisição
    - Responde com JWT caso user e senha sejam "user" e "t3st#"
    - JWT gerado deve conter payload com um id de usuário fixo (ex.: 1)
    - Responde com código 403 caso receba outros user e senha
    - Responde com código 400 caso não receba user e/ou senha

Solicitação de qualquer outra rota deve ser respondida com código 404

### Extras:

  - Implementar política de CORS
  - Responder sempre em JSON fixo como:
  ```json
  {
    "success": true/false,
    "errorMessage": "preenchida com erro apenas se success for true",
    "data": "preenchida com a resposta apenas se erro for false"
  }
  ```
  - Ter testes unitários
  - Ter testes de integração
  - Ter documentação OpenAPI com Swagger ou ferramenta equivalente
  - Ter implementação de compilação para imagem Docker

## Pleno

A API deve ter os seguintes models com as seguintes propriedades:

  - Book
    - id    : int     (primary key, autogerado)
    - title : string
    - isbn  : string  (com validação de formato padrão)
    - year  : int     (com validação de que é ano válido)
    - author: Author (foreign key, requerido)
  - Author
    - id    : int     (primary key, autogerado)
    - name  : string  (em minúsculas)
  - User
    - id    : int     (primary key)
    - name  : string
    - user  : string
    - email : string
    - pass  : string (com salt e hash)

Com as rotas:

  - /book
    - CRUD (usando verbos GET, POST, PUT e DELETE)
    - Requisições devem ter paginação por parâmetros page e limit
    - Aninhamento de Author na requisição
    - Associação de author em POST /book/author
    - Responde com código 400 caso receba dados inválidos ou incompletos
  - /author
    - CRUD (usando verbos GET, POST, PUT e DELETE)
    - Requisições devem ter paginação por parâmetros page e limit
    - Aninhamento de Books na requisição
    - Associação de Book em POST /author/books
    - Responde com código 400 caso receba dados inválidos ou incompletos
  - /user
    - CRUD (usando verbos GET, POST, PUT e DELETE)
    - Requisições devem ter paginação por parâmetros page e limit
    - Nunca retorna o campo password
    - Responde com código 400 caso receba dados inválidos ou incompletos
  - /login
    - Recebe user e password através do body da requisição
    - Responde com JWT caso user e senha estejam registrados
    - JWT gerado deve conter payload com id de user
    - Responde com código 403 caso receba user e senha inválidos
    - Responde com código 400 caso não receba user e/ou senha

Solicitação de qualquer rota desconhecida deve retornar código 404 com mensagem de erro "not-found".

Integração com banco de dados SQL em memória ou local.

Toda resposta da API deve ser no formato:

```json
{
  "success": true,
  "message": "mensagem de erro, caso exista erro",
  "data": {
    "pagination": {
      "total": 0, // total de itens (0 <= total)
      "page": 1, // página atualmente retornada (0 < page)
      "limit": 10 // limite atual aplicado (0 < limit)
    },
    "docs": [] // lista de objetos retornados
  }
}
```

Deve ter testes unitários e de integração.

Deve ter processos de compilação e execução descritos em README.MD.

Deve ter processo de compilação para imagem Docker com documentação de portas e execução de container descritos em README.MD.

### Extras

  - Ter documentação OpenAPI com Swagger ou ferramenta equivalente
  - Configurar conexão de banco de dados com variáveis de ambiente
  - Definir migrations para criação de estrutura de banco de dados
  - Definir seed para inserção de usuário padrão admin
  - Utilizar arquitetura DDD com IoC
  - Desenvolver em formato de microservices com docker-compose.yml
