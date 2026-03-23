# Contacts API

API REST simples para gerenciamento de contactos, construída com Node.js, Express, Sequelize e SQLite.

## Visão geral

Este projeto expõe rotas para:

- listar todos os contactos;
- pesquisar contactos por nome;
- criar novo contacto;
- obter contacto por ID;
- atualizar contacto por ID;
- apagar contacto por ID.

Banco de dados utilizado: SQLite local em `db/app.db`.

## Tecnologias

- Node.js 18.x
- Express 4
- Sequelize 6
- SQLite3
- CORS
- body-parser

## Estrutura do projeto

```text
contacts_API/
├─ app.js
├─ db/
│  ├─ connection.js
│  └─ app.db
├─ models/
│  └─ Contact.js
├─ routes/
│  └─ contacts.js
├─ package.json
└─ vercel.json
```

## Modelo de dados

Modelo `Contact`:

- `name` (STRING)
- `number` (INTEGER)
- `email` (STRING)

## Pré-requisitos

- Node.js 18.x
- npm

## Instalação

```bash
npm install
```

## Como executar

```bash
npm start
```

A aplicação sobe em:

- `http://localhost:3000`

## Rotas da API

Base URL local: `http://localhost:3000`

### Rota principal

**GET** `/`

Resposta:

```json
"ESTA É A ROTA PRINCIPAL DA APLICAÇÃO!"
```

### Teste

**GET** `/contacts/teste`

Resposta:

```json
"ESTA É UMA ROTA DE TESTE DA NOSSA APLICAÇÃO!"
```

### Listar todos os contactos

**GET** `/contacts/list`

Resposta (200):

```json
[
  {
    "id": 1,
    "name": "Ana",
    "number": 923456789,
    "email": "ana@email.com",
    "createdAt": "2026-03-23T10:00:00.000Z",
    "updatedAt": "2026-03-23T10:00:00.000Z"
  }
]
```

### Pesquisar contactos por nome

**GET** `/contacts/list?searchForm=ana`

Resposta (200):

```json
{
  "contacts": [
    {
      "id": 1,
      "name": "Ana",
      "number": 923456789,
      "email": "ana@email.com",
      "createdAt": "2026-03-23T10:00:00.000Z",
      "updatedAt": "2026-03-23T10:00:00.000Z"
    }
  ],
  "search": "ana"
}
```

### Criar contacto

**POST** `/contacts/add`

Body (JSON):

```json
{
  "name": "Ana",
  "number": "923456789",
  "email": "ana@email.com"
}
```

Resposta de sucesso:

```json
{
  "message": "Contacto adicionado com sucesso!"
}
```

### Obter contacto por ID

**GET** `/contacts/:id`

Exemplo: **GET** `/contacts/1`

Resposta (200):

```json
{
  "id": 1,
  "name": "Ana",
  "number": 923456789,
  "email": "ana@email.com",
  "createdAt": "2026-03-23T10:00:00.000Z",
  "updatedAt": "2026-03-23T10:00:00.000Z"
}
```

Resposta quando não encontra (422):

```json
{
  "message": "O contacto não foi encontrado!"
}
```

### Atualizar contacto

**PUT** `/contacts/:id`

Body (JSON):

```json
{
  "name": "Ana Silva",
  "number": "923456789",
  "email": "ana.silva@email.com"
}
```

Resposta de sucesso:

```json
{
  "message": "Contacto atualizado com sucesso!"
}
```

### Apagar contacto

**DELETE** `/contacts/:id`

Resposta de sucesso:

```json
{
  "message": "Contacto apagado com sucesso!"
}
```

## Códigos de estado usados

- `200` sucesso em listagem/consulta
- `422` registo não encontrado
- `500` erro interno no servidor

## Observações importantes

- A API usa CORS liberado para qualquer origem (`origin: "*"`)
- O projeto conecta ao SQLite, mas não executa `sync()` automaticamente no arranque
- Algumas validações retornam apenas `message` sem padronização de `status code`
- O campo `number` no modelo está como `INTEGER`, mas algumas validações tratam como string (ex.: `length`)

## Deploy

Há configuração para Vercel em `vercel.json`.

## Sugestões de melhoria

- padronizar respostas de erro com `status code` consistente;
- corrigir validações para evitar múltiplos `res.send` no mesmo fluxo;
- usar `express.json()` sem necessidade de `body-parser` separado;
- adicionar script de testes e coleção de requests (Postman/Insomnia).
