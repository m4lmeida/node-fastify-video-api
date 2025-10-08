# API de Vídeos com Node.js e Fastify

![Status](https://img.shields.io/badge/status-concluído-green)
![Node.js](https://img.shields.io/badge/Node.js-339933?style=flat&logo=nodedotjs&logoColor=white)
![Fastify](https://img.shields.io/badge/Fastify-000000?style=flat&logo=fastify&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat&logo=postgresql&logoColor=white)

Este é um projeto de estudo desenvolvido para praticar a criação de uma API RESTful utilizando o ecossistema Node.js. O foco foi construir um CRUD (Create, Read, Update, Delete) completo para gerenciar uma lista de vídeos.

Um dos principais conceitos aplicados foi a **abstração da camada de dados**, permitindo que a aplicação opere tanto com um banco de dados em memória (`database-memory.js`) quanto com um banco de dados persistente **PostgreSQL** (`database-postgres.js`), com alteração mínima no código principal do servidor.

---

## 🚀 Funcionalidades

- **Criação de vídeos:** Adiciona um novo vídeo ao banco de dados.
- **Listagem de vídeos:** Retorna todos os vídeos, com a opção de busca por título.
- **Atualização de vídeos:** Altera as informações de um vídeo existente pelo seu ID.
- **Exclusão de vídeos:** Remove um vídeo do banco de dados pelo seu ID.

---

## 🛠️ Tecnologias Utilizadas

- **Runtime:** [Node.js](https://nodejs.org/)
- **Framework:** [Fastify](https://www.fastify.io/)
- **Banco de Dados:** [PostgreSQL](https://www.postgresql.org/)
- **Driver de Conexão (Postgres):** [node-postgres](https://node-postgres.com/)
- **Gerenciamento de Ambiente:** [Dotenv](https://github.com/motdotla/dotenv)

---

## ⚙️ Como Executar o Projeto

Para executar este projeto localmente, siga os passos abaixo:

**Pré-requisitos:**
- [Node.js](https://nodejs.org/) (versão 18 ou superior)
- [PostgreSQL](https://www.postgresql.org/) instalado e rodando.
- Um cliente de banco de dados para criar a base de dados (ex: DBeaver, pgAdmin).

**Passo a Passo:**

1.  **Clone o repositório:**
    ```bash
    git clone [https://github.com/SEU-USUARIO/NOME-DO-REPOSITORIO.git](https://github.com/SEU-USUARIO/NOME-DO-REPOSITORIO.git)
    cd NOME-DO-REPOSITORIO
    ```

2.  **Instale as dependências:**
    ```bash
    npm install
    ```

3.  **Configure o banco de dados:**
    - Crie um banco de dados no seu PostgreSQL (ex: `api_videos`).
    - Crie um arquivo `.env` na raiz do projeto, baseado no `.env.example` (crie este arquivo se não existir):
      ```
      # .env.example
      PORT=3333
      PG_HOST=localhost
      PG_PORT=5432
      PG_USER=seu_usuario_postgres
      PG_PASSWORD=sua_senha_postgres
      PG_DATABASE=api_videos
      ```
    - Execute o script para criar a tabela `videos` no banco:
      ```bash
      node create-table.js
      ```

4.  **Inicie o servidor:**
    ```bash
    npm run dev
    ```
    O servidor estará rodando em `http://localhost:3333`.

---

## 🔌 Endpoints da API

Aqui estão os endpoints disponíveis e como utilizá-los:

#### `POST /videos`
Cria um novo vídeo.

**Request Body:**
```json
{
  "title": "Primeiros passos com Fastify",
  "description": "Um vídeo incrível sobre como iniciar com o framework Fastify.",
  "duration": 180
}
```
**Success Response:** `Status: 201 Created`

---

#### `GET /videos`
Lista todos os vídeos.

**Exemplo de Requisição:** `GET http://localhost:3333/videos`

**Busca por Título (Query Param):** `GET http://localhost:3333/videos?search=Fastify`

**Success Response:** `Status: 200 OK`
```json
[
  {
    "id": "a1b2c3d4-e5f6-7890-1234-567890abcdef",
    "title": "Primeiros passos com Fastify",
    "description": "Um vídeo incrível sobre como iniciar com o framework Fastify.",
    "duration": 180
  }
]
```

---

#### `PUT /videos/:id`
Atualiza um vídeo existente.

**Exemplo de Requisição:** `PUT http://localhost:3333/videos/a1b2c3d4-e5f6-7890-1234-567890abcdef`

**Request Body:**
```json
{
  "title": "Título Atualizado",
  "description": "Descrição Atualizada",
  "duration": 200
}
```
**Success Response:** `Status: 204 No Content`

---

#### `DELETE /videos/:id`
Deleta um vídeo.

**Exemplo de Requisição:** `DELETE http://localhost:3333/videos/a1b2c3d4-e5f6-7890-1234-567890abcdef`

**Success Response:** `Status: 204 No Content`
