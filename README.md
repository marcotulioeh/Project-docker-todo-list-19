# Boas-vindas ao repositório do projeto Docker Todo List!

---

<details>
  <summary><strong>👨‍💻 O que deverá ser desenvolvido</strong></summary><br />

Neste projeto você irá:

1. **_Conteinerizar_** aplicações;
1. Criar uma conexão entre elas;
1. Orquestrar seu funcionamento.

</details>

---

# Requisitos obrigatórios do projeto

## Comandos docker

⚠ Lembre-se das instruções da seção [Entregáveis](#Entregáveis), especialmente no tópico `O que deverá ser desenvolvido`!

### 1. Crie um container em modo interativo, sem rodá-lo, nomeando-o como `01container` e utilizando a imagem `alpine` na versão `3.12`

<details>
  <summary>➕ Informações adicionais</summary><br />

O avaliador executará o comando no arquivo `command01.dc`.

#### Observações técnicas

- O container **não deve ser inicializado**, somente criado;
- O container deve estar preparado para acesso interativo.

#### Dicas

- Lembre-se que um parâmetro não é necessariamente aplicável a apenas um comando.

#### O que será testado

- O `nome` do container deve ser `01container`;
- O container deve usar a imagem `alpine` na versão `3.12`;
- O `status` do container deve ser `created`;
- O container **não deve** estar em execução após ter sido criado.

</details>

### 2. Inicie o container `01container`

<details>
  <summary>➕ Informações adicionais</summary><br />

O avaliador executará o comando no arquivo `command02.dc`.

#### Observações técnicas

- O container `01container`, que acabou de ser criado e está parado, deve ser iniciado;
- Se o container tiver sido iniciado de modo interativo, ele deve se manter ativo ao iniciá-lo.
  
#### O que será testado

- O avaliador verificará se o container está parado;
- O avaliador executará o comando criado neste requisito;
- O container **deve** estar em execução.

</details>

### 3. Liste os containers filtrando pelo nome `01container`

<details>
  <summary>➕ Informações adicionais</summary><br />

O avaliador executará o comando no arquivo `command03.dc`.

#### Dicas

- Praticamente todo comando de listagem no Docker possui uma forma de filtragem.

#### O que será testado

- O comando deve retornar uma lista contendo informações **apenas** do `01container`.

</details>

### 4. Execute o comando `cat /etc/os-release` no container `01container` sem se acoplar a ele

<details>
  <summary>➕ Informações adicionais</summary><br />

O avaliador executará o comando no arquivo `command04.dc`.

#### Observações técnicas

- O container deve estar rodando e você deve ser capaz de **executar um comando** nesse container.

#### Dicas

- É possível fazer isso sem usar o comando `attach`.

#### O que será testado

- Que o comando retornará os dados corretos da `distro` no container:
  - `NAME="Alpine Linux"`
  - `ID=alpine`
  - `VERSION_ID=3.12`

</details>

### 5. Remova o container `01container`

<details>
  <summary>➕ Informações adicionais</summary><br />

O avaliador executará os comandos nos arquivos `command05.dc` e `command03.dc`.

#### O que será testado

- O avaliador rodará o comando 5;
- O avaliador validará o processo com o comando 3.

</details>

### 6. Faça o download da imagem `nginx` com a versão `1.21.3-alpine` sem criar ou rodar um container

<details>
  <summary>➕ Informações adicionais</summary><br />

O avaliador executará o comando no arquivo `command06.dc`.

#### O que será testado

  - Que a imagem correta foi baixada;
  - Que nenhum container foi iniciado para isso.

</details>

### 7. Rode um novo container com a imagem  `nginx` com a versão `1.21.3-alpine` em segundo plano nomeando-o como `02images` e mapeando sua porta padrão de acesso para porta `3000` do sistema hospedeiro

<details>
  <summary>➕ Informações adicionais</summary><br />

O avaliador executará o comando no arquivo `command07.dc`.

#### O que será testado

  - Que o container foi iniciado corretamente;
  - Que é possível ter acesso ao container pelo endereço `localhost:3000`;
  - Que a página retorna o valor esperado.

</details>

### 8. Pare o container `02images` que está em andamento

<details>
  <summary>➕ Informações adicionais</summary><br />

O avaliador executará o comando no arquivo `command08.dc`.

#### O que será testado

  - Que não há nenhum container ativo após seu comando.

</details>

## Dockerfile

**⚠️ As aplicações a seguir contam com um [**README.md**](./docker/todo-app/README.md) próprio, que deve ser usado como referência na criação dos scripts!**

### 9. Gere uma build a partir do Dockerfile do `back-end` do `todo-app` nomeando a imagem para `todobackend`

<details>
  <summary>➕ Informações adicionais</summary><br />

O avaliador executará o comando no arquivo `command09.dc`.

#### Dicas 

- O comando `ADD` do Dockerfile, também pode ser utilizado para descompactar arquivos dentro do container.

#### O que será testado

- Se existe um arquivo `Dockerfile` em `./docker/todo-app/back-end/`:
  - O Dockerfile deve rodar uma imagem `node` utilizando a versão `14`;
    - Recomenda-se o uso da variante `-alpine`, pois ela é otimizada para desempenho;
    - Lembre-se de consultar o README do `todo-app` para validar os requisitos da aplicação.
  - Deve estar com a porta `3001` exposta;
  - Deve adicionar o arquivo `node_modules.tar.gz` a imagem;
  - Deve copiar todos os arquivos da pasta `back-end` para a imagem;
  - Ao iniciar a imagem deve rodar o comando `npm start`.
- Se ao *buildar* o Dockerfile o nome da imagem gerada é igual a `todobackend`.

</details>

### 10. Gere uma build a partir do Dockerfile do `front-end` do `todo-app` nomeando a imagem para `todofrontend`

<details>
  <summary>➕ Informações adicionais</summary><br />

O avaliador executará o comando no arquivo `command10.dc`.

#### Dicas

- O comando `ADD` do Dockerfile, também pode ser utilizado para descompactar arquivos dentro do container.

#### O que será testado

  - Se existe um arquivo `Dockerfile` em `./docker/todo-app/front-end/`:
    - O `Dockerfile` pode rodar uma imagem `node` utilizando a versão `14`;
      - Recomenda-se o uso da variante `-alpine`, pois ela é otimizada para desempenho;
      - Lembre-se de consultar o README do `todo-app` para validar os requisitos da aplicação.
    - Deve estar com a porta `3000` exposta;
    - Deve adicionar o arquivo `node_modules.tar.gz` a imagem, de maneira que ele seja extraído dentro do `container`;
    - Deve copiar todos os arquivos da pasta `front-end` para a imagem;
    - Ao iniciar a imagem deve rodar o comando `npm start`;
  - Se ao *buildar* o `Dockerfile` o nome da imagem gerada é igual a `todofrontend`.

</details>

### 11. Gere uma build a partir do Dockerfile dos `testes` do `todo-app` nomeando a imagem para `todotests`

<details>
  <summary>➕ Informações adicionais</summary><br />

O avaliador executará o comando no arquivo `command11.dc`.

#### Dicas

- O comando `ADD` do Dockerfile, também pode ser utilizado para descompactar arquivos dentro do container.

#### Observações técnicas

- A aplicação `todotests` só funciona corretamente se estiver dockerizada e dentro de uma rede docker configurada corretamente.

#### O que será testado

- Se existe um arquivo `Dockerfile` em `./docker/todo-app/tests/`:
  - O Dockerfile deve rodar a imagem `mjgargani/puppeteer:trybe1.0` para que os testes funcionem;
  - Deve adicionar o arquivo `node_modules.tar.gz` a imagem;
  - Deve copiar todos os arquivos da pasta `tests` para a imagem;
  - Ao iniciar a imagem deve rodar o comando `npm test`;
- Se ao *buildar* o Dockerfile o nome da imagem gerada é igual a `todotests`.

</details>

# Requisito bônus do projeto

## Docker-compose

### 12. Suba uma orquestração em segundo plano com o docker-compose de forma que `backend`, `frontend` e `tests` consigam se comunicar

<details>
  <summary>➕ Informações adicionais</summary><br />

O avaliador executará o comando no arquivo `command12.dc`. Este comando pressupõe a existência do arquivo `./docker/docker-compose.yml`.

O `docker-compose` deve rodar na versão 3 ou superior.

#### Dicas

- Use as imagens já **"buildadas"** que foram executadas nos requisitos 9, 10 e 11 para a criação do compose;
- Consulte a documentação em `./docker/todo-app/README.md`;
- É possível adicionar e extrair arquivos `.tar.gz` no `Dockerfile` com apenas um comando.

#### O que será testado

##### tests

- O container de `todotests` deve ter como dependencia os containers `frontend` e `backend`;
- O nome do _service_ deverá ser `todotests`;
- Deve ter uma variável de ambiente `FRONT_HOST` que recebe como valor o nome do container do `frontend`
  - Lembrando que, dentro de uma rede docker, o host de um container é indentificado pelo seu nome.

##### front-end

- O container de `todofrontend` deve rodar na porta `3000`;
- O nome do _service_ deverá ser `todofront`;
- Deve ter como dependencia o container `backend`;
- Deve ter uma variável de ambiente `REACT_APP_API_HOST` que recebe como valor o nome do container do `backend`.
  - Lembrando que, dentro de uma rede docker, o host de um container é indentificado pelo seu nome.

##### back-end

- O container de `todobackend` deve rodar na porta `3001`;
- O nome do _service_ deverá ser `todoback`;

</details>
