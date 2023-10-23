## Construção do backend para uma aplicação de fórum

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