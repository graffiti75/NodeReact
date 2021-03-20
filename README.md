# NodeReact

- [Ferramentas utilizadas no projeto](https://github.com/graffiti75/NodeReact#ferramentas-utilizadas-no-projeto)
- [Criando o projeto Backend](https://github.com/graffiti75/NodeReact#criando-o-projeto-backend)
- [SPA](https://github.com/graffiti75/NodeReact#spa)
- [Projeto Frontend](https://github.com/graffiti75/NodeReact#projeto-frontend)
- [Parâmetros de Backend](https://github.com/graffiti75/NodeReact#par%C3%A2metros-de-backend)
- [Nodemon](https://github.com/graffiti75/NodeReact#nodemon)
- [Banco de Dados](https://github.com/graffiti75/NodeReact#bancos-de-dados)
- [Banco de Dados do Projeto](https://github.com/graffiti75/NodeReact#banco-de-dados-do-projeto)
- [Migrations](https://github.com/graffiti75/NodeReact#migrations)
- [Criar os Webservices de ONGs](https://github.com/graffiti75/NodeReact#criar-os-webservices-de-ongs)
	- [@POST Create ONG](https://github.com/graffiti75/NodeReact#criar-os-webservices-de-ongs)
	- [@GET List ONGs](https://github.com/graffiti75/NodeReact#get-list-ongs)
- [Controllers](https://github.com/graffiti75/NodeReact#controllers)
- [Criar os Webservices de Casos (Incidents)](https://github.com/graffiti75/NodeReact#criar-os-webservices-de-casos-incidents)
	- [@POST Create Incident](https://github.com/graffiti75/NodeReact#post-create-incident)
	- [@GET List Incidents](https://github.com/graffiti75/NodeReact#get-list-incidents)
	- [@DELETE Incident](https://github.com/graffiti75/NodeReact#delete-incident)
- [Listar casos específicos de uma ONG](https://github.com/graffiti75/NodeReact#listar-casos-espec%C3%ADficos-de-uma-ong)
- [Login de uma ONG](https://github.com/graffiti75/NodeReact#login-de-uma-ong)
- [Paginação de Casos (Incidents)](https://github.com/graffiti75/NodeReact#pagina%C3%A7%C3%A3o-de-casos-incidents)

---

## Ferramentas utilizadas no projeto

- Notion.so: Anotações
- Figma: Design do aplicativo
- Visual Code Studio
- Insomnia
   
## Criando o projeto Backend

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
   
## Criar os Webservices de Casos (Incidents)

### @POST Create Incident

- No projeto Backend, criar o arquivo `IncidentControllers.js` na pasta `src/controllers/`.
- Adicionar a ele o seguinte código-fonte:
   ```javascript
   const connection = require('../database/connection');
   const crypto = require('crypto');

   module.exports = {
      async create(request, response) {
         const { title, description, value } = request.body;
      }
   };
   ```
- Agora, vamos abrir o Insomnia e criar uma pasta chamada `Casos`, e nela criar uma requisição POST chamada Create.
- Colocar como endereço da requisição: http://localhost:3333/incidents
- Colocar como Body da requisição o tipo JSON, com os seguintes dados:
   ```javascript
   {
	   "title": "Caso 1",
   	"description": "Detalhes do caso",
	   "value": 120
   }
  ```
- Criar um cabeçalho na aba "Header", e nele criar uma "Authorization" e inserir como seu valor o ID da ONG que estará conectada ao Incident.
   - Neste caso, o ID que utilizaremos será o ID da primeira ONG criada. Em nosso caso, este valor equivale a "83e64a32".
- Agora vamos atualizar o arquivo `IncidentControllers.js` com o seguinte código-fonte:
const connection = require('../database/connection');
const crypto = require('crypto');
   ```javascript
   module.exports = {
      async create(request, response) {
         const { title, description, value } = request.body;
         const ong_id = request.headers.authorization;
         const [id] = await connection('incidents').insert({
            title, description, value, ong_id
         });
         return response.json({ id });
      }
   };
   ```
- Atualizar o arquivo `routes.js` com o seguinte código:
   ```javascript
   const express = require('express');
   const OngController = require('./controllers/OngController');
   const IncidentController = require('./controllers/IncidentController');
   const routes = express.Router();

   routes.get('/ongs/', OngController.list);
   routes.post('/ongs/', OngController.create);
   routes.post('/incidents/', IncidentController.create);

   module.exports = routes;
   ```
- Agora, basta abrirmos o Insomnia e clicarmos no botão "Send". E pronto, criamos nosso primeiro Caso para a ONG de ID "83e64a32".

### @GET List Incidents

- Atualizar o arquivo `IncidentController.js`:
   ```javascript
   const connection = require('../database/connection');
   const crypto = require('crypto');

   module.exports = {
      async list(request, response) {
         const incidents = await connection('incidents').select('*');
         return response.json(incidents);
      },
      async create(request, response) {
         const { title, description, value } = request.body;
         const ong_id = request.headers.authorization;
         const [id] = await connection('incidents').insert({
            title, description, value, ong_id
         });
         return response.json({ id });
      }
   };
   ```
- Atualizar o arquivo `routes.js` com o seguinte código:
   ```javascript
   const express = require('express');
   const OngController = require('./controllers/OngController');
   const IncidentController = require('./controllers/IncidentController');
   const routes = express.Router();

   routes.get('/ongs/', OngController.list);
   routes.post('/ongs/', OngController.create);
   routes.get('/incidents/', IncidentController.list);
   routes.post('/incidents/', IncidentController.create);

   module.exports = routes;
   ```
- Agora vamos criar uma requisição GET chamada List.
- Colocar como endereço da requisição: http://localhost:3333/incidents
- Colocar como Body da requisição o tipo "No Body".
- Agora, vamos executar esse método `GET` no Insomnia. Fazemos isso clicando em "Send".
   - Desta forma, acabamos de obter uma listagem de Incidents:
   ```json
   [
      {
         "id": 1,
         "title": "Caso 1",
         "description": "Detalhes do caso",
         "value": 120,
         "ong_id": "83e64a32"
      }
   ]  
   ```

### @DELETE Incident

- Agora vamos criar uma requisição DELETE.
- Colocar como endereço da requisição algo como: http://localhost:3333/incidents/1
- Colocar como Body da requisição o tipo "No Body".
- Atentar para o campo "Authorization" na aba "Header".
	- **Este campo deve conter o ID de uma das ONG's já criadas.**
- Executar esse método `DELETE` no Insomnia. Fazemos isso clicando em "Send".
   - Desta forma, acabamos de deletar um Incident.
   - Neste caso específico, nenhuma informação é retornada ao usuário.
- Agora, vamos atualizar o arquivo `IncidentController.js`:
   ```javascript
   const connection = require('../database/connection');
   const crypto = require('crypto');

   module.exports = {
      async list(request, response) {
         const incidents = await connection('incidents').select('*');
         return response.json(incidents);
      },
      async create(request, response) {
         const { title, description, value } = request.body;
         const ong_id = request.headers.authorization;
         const [id] = await connection('incidents').insert({
            title, description, value, ong_id
         });
         return response.json({ id });
      },

      async delete(request, response) {
        const { id } = request.params;
        const ong_id = request.headers.authorization;
        const incident = await connection('incidents')
            .where('id', id)
            .select('ong_id')
            .first();

        if (incident.ong_id != ong_id) {
            return response.status(401).json({ error: 'Operation not permitted.' });
        }
        await connection('incidents').where('id', id).delete();
        return response.status(204).send();
      },
   };
   ```
- Atualizar o arquivo `routes.js` com o seguinte código:
   ```javascript
   const express = require('express');
   const OngController = require('./controllers/OngController');
   const IncidentController = require('./controllers/IncidentController');
   const routes = express.Router();

   routes.get('/ongs/', OngController.list);
   routes.post('/ongs/', OngController.create);
   routes.get('/incidents/', IncidentController.list);
   routes.post('/incidents/', IncidentController.create);
   routes.post('/incidents/:id', IncidentController.delete);

   module.exports = routes;
   ```

## Listar casos específicos de uma ONG

- No projeto Backend, criar o arquivo `ProfileControllers.js` na pasta `src/controllers/`.
- Adicionar a ele o seguinte código-fonte:
   ```javascript
   const connection = require('../database/connection');
   module.exports = {
      async list(request, response) {
         const ong_id = request.headers.authorization;
         const incidents = await connection('incidents')
            .where('ong_id', ong_id)
            .select('*');
         return response.json(incidents);
      }
   }
   ```
- Agora, vamos abrir o Insomnia (não será preciso aqui criar uma pasta), e nela criar uma requisição GET chamada Profile.
- Colocar como endereço da requisição: http://localhost:3333/profile
- Criar um cabeçalho na aba "Header", e nele criar uma "Authorization" e inserir como seu valor o ID da ONG que estará conectada ao Incident.
   - Neste caso, o ID que utilizaremos será o ID da primeira ONG criada. Em nosso caso, este valor equivale a "83e64a32".
- Atualizar o arquivo `routes.js` com o seguinte código:
   ```javascript
   const express = require('express');
   const OngController = require('./controllers/OngController');
   const IncidentController = require('./controllers/IncidentController');
   const ProfileController = require('./controllers/ProfileController');
   const routes = express.Router();

   routes.get('/ongs/', OngController.list);
   routes.post('/ongs/', OngController.create);

   routes.get('/incidents/', IncidentController.list);
   routes.post('/incidents/', IncidentController.create);
   routes.delete('/incidents/:id', IncidentController.delete);

   routes.get('/profile/', ProfileController.list);

   module.exports = routes;
   ```
- Agora, basta abrirmos o Insomnia e clicarmos no botão "Send". E pronto, listamos os casos específicos de uma ONG de ID "83e64a32".

## Login de uma ONG

- Esta rota apenas verifica se a ONG existe ou não.
- No projeto Backend, criar o arquivo `SessionControllers.js` na pasta `src/controllers/`.
- Adicionar a ele o seguinte código-fonte:
   ```javascript
   const connection = require('../database/connection');

   module.exports = {
      async create(request, response) {
         const { id } = request.body;
         const ong = await connection('ongs')
            .where('id', id)
            .select('name')
            .first();
         if (!ong) {
            return response.status(400).json({ error: 'No ONG found with this ID.' });
         }
         return response.json(ong);
      }
   }
   ```
- Agora, vamos abrir o Insomnia (não será preciso aqui criar uma pasta), e nela criar uma requisição POST chamada Login.
- Colocar como endereço da requisição: http://localhost:3333/sessions
- Colocar como Body da requisição o tipo JSON, com os seguintes dados:
   ```javascript
   {
      "id": "83e64a32"
   }
   ```
- Atualizar o arquivo `routes.js` com o seguinte código:
   ```javascript
   const express = require('express');
   const OngController = require('./controllers/OngController');
   const IncidentController = require('./controllers/IncidentController');
   const ProfileController = require('./controllers/ProfileController');
   const routes = express.Router();

   routes.get('/ongs/', OngController.list);
   routes.post('/ongs/', OngController.create);

   routes.get('/incidents/', IncidentController.list);
   routes.post('/incidents/', IncidentController.create);
   routes.delete('/incidents/:id', IncidentController.delete);

   routes.get('/profile/', ProfileController.list);
   
   routes.post('/sessions/', SessionController.create);

   module.exports = routes;
   ```
- Agora, basta abrirmos o Insomnia e clicarmos no botão "Send".
- Teremos como output:
   ```javascript
   {
      "name": "APAD"
   }
   ```

## Paginação de Casos (Incidents)

- Atualmente a listagem de Incidents não possui Paginação.
- Para implementar tal funcionalidade, precisamos atualizar o `IncidentController.js`:
   ```javascript
      async list(request, response) {
         const { page = 1 } = request.query;
         const incidents = await connection('incidents')
            .limit(5)
            .offset((page - 1) * 5)
            .select('*');
         return response.json(incidents);
      },
   ```
- Após isso, podemos testar no Insomnia, no endpoint de `@GET List Incidents`.
- Precisamos adicionar, como sufixo desse endpoint, o parâmetro `page`, tal qual mostrado ao lado: http://localhost:3333/incidents?page=1
- Agora, vamos alterar o código-fonte de `IncidentController.js` para incluir nele a informação de total de registros retornados.
- Tal informação será mostrada via comando `console.log`, tal qual mostrado abaixo:
   ```javascript
      async list(request, response) {
         const { page = 1 } = request.query;
         const [count] = await connection('incidents').count();
         console.log(count);
         const incidents = await connection('incidents')
            .limit(5)
            .offset((page - 1) * 5)
            .select('*');
         return response.json(incidents);
      },
   ```
- Quando queremos retornar o total de registros de uma query, o aconselhável é retornarmos tal informação dentro do Header da requisição.
- Isso pode ser feito através do comando `response.header('X-Total-Count', count['count(*)']);`.
- Dessa forma, atualizando nosso `IncidentController.js`, teríamos o seguinte:
   ```javascript
      async list(request, response) {
         const { page = 1 } = request.query;
         const [count] = await connection('incidents').count();
         console.log(count);
         const incidents = await connection('incidents')
            .limit(5)
            .offset((page - 1) * 5)
            .select('*');
         response.header('X-Total-Count', count['count(*)']);
         return response.json(incidents);
      },
   ```
   
## Join de ONG's com Casos (Incidents)

- Atualmente a listagem de Incidents traz como dados de ONG's apenas o atributo `ong_id`.
- Seria interessante trazer também dados das ONG's.
- Para isso, precisamos modificar o método `async list(request, response)` do `IncidentController.js`:
   ```javascript
   async list(request, response) {
      const { page = 1 } = request.query;
      const [count] = await connection('incidents').count();
      console.log(count);
      const incidents = await connection('incidents')
         .join('ongs', 'ongs.id', '=', 'incidents.ong_id')
         .limit(5)
         .offset((page - 1) * 5)
         .select([
            'incidents.*',
            'ongs.name',
            'ongs.email',
            'ongs.whatsapp',
            'ongs.city',
            'ongs.uf'
         ]);
      response.header('X-Total-Count', count['count(*)']);
      return response.json(incidents);
   },
   ```
- Assim, teremos como output:
   ```javascript
   [
      {
         "id": 2,
         "title": "Caso 1",
         "description": "Detalhes do caso",
         "value": 120,
         "ong_id": "68f6591a",
         "name": "Mimissauros",
         "email": "contato@mimissauros.com.br",
         "whatsapp": "4700000000",
         "city": "Lajeado",
         "uf": "RS"
      },
      ...
   ]
   ```
