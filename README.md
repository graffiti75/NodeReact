# NodeReact

## Ferramentas utilizadas no projeto:

- Notion.so: Anotações
- Figma: Design do aplicativo
- Visual Code Studio
- Insomnia
   
## Criando o projeto Backend:

- Criar projeto NPM:
  `npm init -y`
- Instalar Express no NPM: `npm install express`
- Rodar servidor: `node index.js`
- Endereço do servidor Backend: http://localhost:3333/
- Baixar o Insomnia (software similar ao Postman): https://insomnia.rest/

## SPA

O conceito por trás do React Native é o SPA (Single Page Applications).

## Projeto Frontend

- Criar projeto React Native com `npx`:
   - `npx` não instala um pacote, como o `npm`; ao invés disso ele apenas executa um pacote).
   - Código para criar o projeto: `npx create-react-app frontend`
- Github do Create React App: https://github.com/facebook/create-react-app
- Na pasta Frontend, para rodar o projeto React Native:  `npm start`
- O projeto será rodado em: http://localhost:3000/
   
## Parâmetros de Backend

- Query Params: Parâmetros nomeados enviados na rota após "?" (filtros, paginação).
  - Acessado no Insomnia assim: `GET /users?name=Rodrigo&idade=25`
  - Acessado no Node assim:
    ```javascript
    app.get('/users/', (request, response) => {
      const query = request.query;
      console.log(query)
      return response.json({
        evento: 'Semana Omnistack 11.0',
        aluno: 'Rodrigo Cericatto'
      });
    });
    ```
- Route Params: Parâmetros utilizados para identificar recursos.
  - Acessado no Insomnia assim: `GET /users/1`
  - Acessado no Node assim:
    ```javascript
    app.get('/users/:id', (request, response) => {
      const params = request.params;
      console.log(params)
      return response.json({
        evento: 'Semana Omnistack 11.0',
        aluno: 'Rodrigo Cericatto'
      });
    });
    ```
- Request Body: Corpo da requisição, utilizado para criar ou alterar recursos.
  - Acessado no Insomnia assim:
    ```javascript
    POST /users/
    BODY (JSON):
    {
      "name": "Rodrigo Cericatto",
      "idade": 25
    }
    ```
  - Acessado no Node assim:
    ```javascript
    app.post('/users/', (request, response) => {
      const body = request.body;
      console.log(body)
      return response.json({
        evento: 'Semana Omnistack 11.0',
        aluno: 'Rodrigo Cericatto'
      });
    });
    ```
  - Para que esse tipo de requisição funcione, é necessário adicionar no cabeçalho do index.js: `app.use(express.json());`

## Nodemon

- Para não ficar reiniciando o Node toda vez que há alterações no código, usamos o Nodemon.
- Para instalá-lo, digitar: `npm install nodemon -D`
- `-D`implica em salvar o Nodemon, no arquivo package.json, na tag "devDependencies" ao invés da tag "dependencies".
  - Ou seja, essa ferramenta só será usada enquanto estivermos desenvolvendo uma aplicação.
  - Quando publicarmos essa aplicação em um servidor de Produção, não precisaremos ficar monitorando o código.
- No arquivo package.json, trocar o "script" de "test" para "start":
  ```javascript
  "scripts": {
    "start": "nodemon index.js"
  },
  ```
- Então, basta digitarmos `npm start` para rodar essa alteração.

## Bancos de Dados

- SQL: MySQL, SQLite, PostgreSQL, Oracle, Microsoft SQL Server
- NoSQL: MongoDb, CouchDb
- Configuração e comunicação com Bancos de Dados:
   - Driver:  `select * from users`
   - Query Builder:  `table('users').select('*').where()`
   - Qual Query Builder será utilizado no projeto? `knex.js`
   - Instalação do Knex: `npm install knex`
   - Instalação do Banco de Dados SQLite: `npm install sqlite3`
   - Criar o arquivo `knexfile.js`, que é o arquivo que contém as configurações de acesso ao Banco de Dados para os ambientes de "development", "staging" e "production": `npx knex init`

## Banco de Dados do Projeto

- Entidades
  - ONG
  - Caso (Incident)
- Funcionalidades
  - Login de ONG
  - Logout de ONG
  - Cadastro de ONG
  - Cadastrar novos casos
  - Deletar casos
  - Listar casos específicos de uma ONG
  - Listar todos os casos
  - Entrar em contato com a ONG
      
## Migrations

- Migrations é um conceito muito similar a um versionador de mudanças no Banco de Dados do projeto.
- Inserir, no arquivo knexfile.js, a tag "migrations":
  ```javascript
  development: {
    client: 'sqlite3',
    connection: {
      filename: './src/database/db.sqlite'
    },
    migrations: {
      directory: './src/database/migrations'
    }
  },
  ```   
- Para criar a 1ª migração, digitar o comando abaixo na pasta Backend: `npx knex migrate:make migration_name`
  - Neste caso, o nome da migração será "create_ongs". Logo, o comando ficará assim: `npx knex migrate:make create_ongs`
- Adicionar a tag "useNullAsDefault" na tag "development" do knexfile.js, a fim de sumir com o seguinte warning "sqlite does not support inserting default values. Set the `useNullAsDefault` flag to hide this warning. (see docs http://knexjs.org/#Builder-insert)."
  ```javascript
  development: {
    client: 'sqlite3',
    connection: {
      filename: './src/database/db.sqlite'
    },
    migrations: {
      directory: './src/database/migrations'
    },
    useNullAsDefault: true
  },
  ```
- Atualizar o arquivo de migrações. No meu caso, o nome do arquivo é "20200813231416_create_ongs.js":
  ```javascript
  exports.up = function(knex) {
    return knex.schema.createTable('ongs', function(table){
      table.string('id').primary();
      table.string('name').notNullable();
      table.string('email').notNullable();
      table.string('whatsapp').notNullable();
      table.string('city').notNullable();
      table.string('uf', 2).notNullable();
  });
  };
  exports.down = function(knex) {
    return knex.schema.dropTable('ongs');
  };
  ```
- Para criar a tabela, digitar: `npx knex migrate:latest`
- Agora criaremos a 2ª migração, onde criaremos os Casos das ONGs: `npx knex migrate:make create_incidents`
  - Eis o conteúdo do arquivo "20200813232725_create_incidents.js":
    ```javascript
    exports.up = function(knex) {
      return knex.schema.createTable('incidents', function(table){
        table.increments();
        table.string('title').notNullable();
        table.string('description').notNullable();
        table.decimal('value').notNullable();
        table.string('ong_id').notNullable();
        table.foreign('ong_id').references('id').inTable('ongs');
      });
    };
    exports.down = function(knex) {
      return knex.schema.dropTable('incidents');
    };
    ```
  - Para criar a tabela, rodamos: `npx knex migrate:latest`
- Para desfazer alguma migration: `npx knex migrate:rollback`
- Para saber todas as migrations já criadas: `npx knex migrate:status`
    
## Criar os Webservices de ONGs

### @POST Create ONG

- Criar um Folder no Insomnia, com o nome "ONGs", e nele criar uma requisição POST chamada Create.
- Colocar como endereço da requisição: http://localhost:3333/ongs
- Colocar como Body da requisição o tipo JSON, com os seguintes dados:
  ```javascript
  {
    "name": "APAD",
    "email": "contato@apad.com.br",
    "whatsapp": "4700000000",
    "city": "Rio do Sul",
    "uf": "SC"
  }
  ```
- Criar o ID a ser inserido, com o comando abaixo: `const id = crypto.randomBytes(4).toString('HEX');`
- Criar o arquivo `connection.js` dentro da pasta database. Inserir nele o seguinte código:
  ```javascript
  const knex = require('knex');
  const configuration = require('../../knexfile');
  const connection = knex(configuration.development);
  module.exports = connection;
  ```
- Inserir a referência ao `connection.js` no header no arquivo `routes.js`:
  ```javascript
  const express = require('express');
  const crypto = require('crypto');
  const connection = require('./database/connection');     <<<<<-------------------- header adicionado
  const routes = express.Router();
  ```
- Inserir dados da ONG no Banco de Dados:
  ```javascript
  connection('ongs').insert({
    id, name, email, whatsapp, city, uf
  })
  ```
- Como essa operação de inserção é assíncrona, temos de modificar o código, inserindo nele os comandos `async` e `await`.
  ```javascript
  routes.post('/ongs/', async (request, response) => {
    // const data = request.body;
    const { name, email, whatsapp, city, uf } = request.body;
    const id = crypto.randomBytes(4).toString('HEX');  
    await connection('ongs').insert({     <<<<<-------------------- código adicionado
      id, name, email, whatsapp, city, uf
    })
    return response.json();
  });
  ```
- Este método pode retornar qualquer um dos campos, mas no nosso caso, retornaremos um JSON com seu ID: `return response.json({ id });`
   - Assim, o método completo ficará:
   ```javascript
   routes.post('/ongs/', async (request, response) => {
    // const data = request.body;
    const { name, email, whatsapp, city, uf } = request.body;
    const id = crypto.randomBytes(4).toString('HEX');  
    await connection('ongs').insert({     <<<<<-------------------- código adicionado
      id, name, email, whatsapp, city, uf
    })
    return response.json({ id });
  });
  ```
- Agora, vamos abrir o Insomnia e executar o método `POST` para criar ONGs. Fazemos isso clicando em "Send".
   - Desta forma, acabamos de criar uma ONG.

### @GET List ONGs

- Agora vamos criar uma requisição GET chamada List.
- Colocar como endereço da requisição: http://localhost:3333/ongs
- Obter dados das ONGs no no Banco de Dados:
   ```javascript
   routes.get('/ongs/', async (request, response) => {
       const ongs = await connection('ongs').select('*');
       return response.json(ongs);
   });
   ```
- Colocar como Body da requisição o tipo "No Body".
- Agora, vamos executar esse método `GET` no Insomnia. Fazemos isso clicando em "Send".
   - Desta forma, acabamos de obter uma listagem de ONGs:
   ```json
   [
     {
       "id": "83e64a32",
       "name": "APAD",
       "email": "contato@apad.com.br",
       "whatsapp": "4700000000",
       "city": "Rio do Sul",
       "uf": "SC"
     },
     {
       "id": "47d91920",
       "name": "APAD",
       "email": "contato@apad.com.br",
       "whatsapp": "4700000000",
       "city": "Rio do Sul",
       "uf": "SC"
     },
     {
       "id": "d3bcaf33",
       "name": "APAD",
       "email": "contato@apad.com.br",
       "whatsapp": "4700000000",
       "city": "Rio do Sul",
       "uf": "SC"
     }
   ]
   ```
   
## Controllers

- Agora, vamos dar uma reorganizada em nosso código.
- Vamos criar uma pasta `controllers` dentro do diretório `src`, e nela criar o arquivo `OngController.js`.
- Neste arquivo teremos o seguinte código:
   ```javascript
   const connection = require('../database/connection');
   const crypto = require('crypto');
   module.exports = {
       async list(request, response) {
           const ongs = await connection('ongs').select('*');
           return response.json(ongs);
       },
       async create(request, response) {
           const { name, email, whatsapp, city, uf } = request.body;
           const id = crypto.randomBytes(4).toString('HEX');
           await connection('ongs').insert({
               id, name, email, whatsapp, city, uf
           })
           return response.json({ id });
       }
   };
   ```
- Desta forma, o código do arquivo `routes.js` ficará assim:
   ```javascript
   const express = require('express');
   const OngController = require('./controllers/OngController');
   const routes = express.Router();

   routes.get('/ongs/', OngController.list);
   routes.post('/ongs/', OngController.create);

   module.exports = routes;
   ```
