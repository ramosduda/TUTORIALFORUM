## Construção do backend para uma aplicação de fórum

#### Criando o banco de dados
* Abrir programa Workbench
* Criar database com o comando
```
create database app_forum_db;
```
* Definir a database 
```
use app_forum_db;
```

* Criar tabela users
```
create table users (
	id int not null auto_increment,
    name varchar(120) not null,
    email varchar(120) not null,
    password varchar(120) not null,
    status enum('A','I') default ('A'),
    created_at datetime default current_timestamp,
    primary key(id)
);
```
* Criar tabela posts
```
create table posts (
	id int not null auto_increment,
    descricao varchar(255) not null,
    user_id int not null
    created_at datetime default current_timestamp,
    primary key(id)
);
```
* Criar tabela comments
```
create table comments(
	id int not null auto_increment,
    descricao varchar(120) not null,
    post_id int not null,
    user_id int not null,
    primary key(id),
    foreign key (post_id) references posts(id),
    foreign key (user_id) references users(id)
);
```
* Criar tabela reactions
```
create table reactions(
	id int not null auto_increment,
    user_id int not null,
    post_id int not null,
    comment_id int,
    primary key(id),
    foreign key (post_id) references posts(id),
    foreign key (user_id) references users(id)
);
```

#### Passo a passo do desenvolvimento utilizando gitBash
* Clonar o repositório no computador
* Acessar a pasta
* Abrir a pasta no VSCode

#### Configurações iniciais
* Executar o comando 'npm i' para importar os pacotes da aplicação
```
npm i 
```

* Criar o arquivo '.env' na raiz do projeto e colar as variáveis do arquivo '.env.example'.
* Adicionar os valores às variáveis

#### Configurar inicialização da API
* Abrir o arquivo 'app.js' e colar o código
```
const express         = require('express');
const cors            = require('cors');
const app             = express();
require('dotenv').config();

app.use(cors());
app.use(express.json());
app.set('port', process.env.PORT);

module.exports = app;
```

* Abrir o arquivo 'server.js' e colar o código
```
const app = require('./app');
const port = app.get('port');

app.listen(port, () => console.log(`Running at port ${ port }`));
```