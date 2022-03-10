# json-server-base

Esse é o repositório com a base de JSON-Server + JSON-Server-Auth já configurada, feita para ser usada no desenvolvimento das API's nos Capstones do Q2.

## Endpoints

Assim como a documentação do JSON-Server-Auth traz (https://www.npmjs.com/package/json-server-auth), existem 5 endpoints que podem ser utilizados para cadastro e 2 endpoints que podem ser usados para login.

## Rotas que não precisam de autenticação:

### Series

`GET /series - FORMATO DA RESPOSTA - STATUS 200`
```json
[
	{
		"name": "Rick and Morty"
	},
	{
		"name": "Peaky Blinders"
	},
	{
		"name": "Vikings"
	},
	{
		"name": "Suits"
	}
]
```

## Rotas que precisam de autentiação

### Comments

`GET /comments - FORMATO DA RESPOSTA - 200`
```json
[
	{
		"comment": "Muito bom",
		"serie": "Rick and Morty",
		"userId": 2,
		"id": 1
	}
]
```
`POST /comments - FORMATO DA RESPOSTA - 201`
```json
{
	"comment": "Entediante",
	"serie": "Suits",
	"userId": 2,
	"id": 2
}
```

## Rotas padrão

### Cadastro

POST /register <br/>
POST /signup <br/>
POST /users

Qualquer um desses 3 endpoints irá cadastrar o usuário na lista de "Users", sendo que os campos obrigatórios são os de email e password.
Você pode ficar a vontade para adicionar qualquer outra propriedade no corpo do cadastro dos usuários.


### Login

POST /login <br/>
POST /signin

Qualquer um desses 2 endpoints pode ser usado para realizar login com um dos usuários cadastrados na lista de "Users"
