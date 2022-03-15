<h1 align="center">
  <img alt="KenzieHub" title="KenzieHub" src="https://kenzie.com.br/images/logoblue.svg" width="100px" />
</h1>

<h1 align="center">
  Nome que não decidimos ainda - API
</h1>

<p align = "center">
Este é o backend da aplicação Nome que não decidimos ainda - Uma aplicação para prestadores e consumidores de serviços feita pelos alunos da Kenzie. O objetivo dessa aplicação é facilitar a comunicação entre prestador/consumidor.
</p>

<p align="center">
  <a href="#endpoints">Endpoints</a>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</p>

## **Endpoints**

A API tem um total de 13 endpoints, sendo em volta principalmente do usuário (dev) - podendo cadastrar seu perfil, tecnologias que estuda e trabalhos realizados. <br/>
O JSON para utilizar no Insomnia é este aqui -> https://kenziehub.s3.amazonaws.com/requests_kenziehub.json
Para importar o JSON no Insomnia é só clicar na palavra "Insomnia" no canto superior esquerdo. Nesse dropdown é só clicar em "Import / Export > Import Data > From Url" e colocar o link acima :v:

O url base da API é http://localhost:3001/

## Rotas que não precisam de autenticação

<h2 align ='center'> Listando usuários </h2>

Nessa aplicação o usuário sem fazer login ou se cadastrar pode ver os devs já cadastrados na plataforma, na API podemos acessar a lista dessa forma:
Aqui conseguimos ver os usuários, suas tecnologias e seus trabalhos cadastrados.

`GET /services - FORMATO DA RESPOSTA - STATUS 200`

```json
[
  {
    "title": "Eu vou Divulgar Para Mais De 30mil Seguidores",
    "images": [
      "https://vinteconto.sfo2.cdn.digitaloceanspaces.com/listings/418420/09a3b7008f562804e64b7100799ce8cc.jpg"
    ],
    "price": 20,
    "desc": "Eu vou divulgar a sua empresa na minha página do Facebook com mais de 30 mil seguidores por 1 dia (Sem impulsionamento). Se precisar de mais e com impulsionamento, favor, verificar serviços extras abaixo.",
    "prazoEntrega": "2 dias",
    "tags": ["Publicidade", "Terror"],
    "userId": 1,
    "id": 1
  },
  {
    "title": "Eu vou desenhar você em estilo anime ou semi-realista",
    "images": [
      "https://vinteconto.sfo2.cdn.digitaloceanspaces.com/listings/223792/draw4hhrs.jpg",
      "https://vinteconto.sfo2.cdn.digitaloceanspaces.com/listings/223792/drawoc1t3h40min.jpg",
      "https://vinteconto.sfo2.cdn.digitaloceanspaces.com/listings/223792/draw3h20min.jpg",
      "https://vinteconto.sfo2.cdn.digitaloceanspaces.com/listings/223792/084545681e6b6b96e72a9256613a3d3b.jpg"
    ],
    "price": 40,
    "desc": "Vou fazer um desenho digital usando o mouse transformando você em estilo anime ou semi-realista.",
    "prazoEntrega": "2 dias",
    "tags": ["Dsenho", "Ilustração", "Anime"],
    "userId": 2,
    "id": 2
  }
]
```

<h2 align ='center'> Criação de usuário </h2>

`POST /users - FORMATO DA REQUISIÇÃO`

```json
{
  "email": "johndoe@email.com",
  "password": "123456",
  "name": "John Doe",
  "bio": "Lorem ipsum dolor emet",
  "contact": "linkedin/in/johndoe",
  "course_module": "Segundo Módulo (Frontend avançado)"
}
```

Caso dê tudo certo, a resposta será assim:

`POST /users - FORMATO DA RESPOSTA - STATUS 201`

```json
{
  "id": "c110dbb6-beb9-4682-ab63-2c12a570d66b",
  "name": "John Doe",
  "email": "johndoe@email.com",
  "course_module": "Segundo Módulo (Frontend avançado)",
  "bio": "Lorem ipsum dolor emet",
  "contact": "linkedin/in/johndoe",
  "created_at": "2020-12-05T14:38:02.019Z",
  "updated_at": "2020-12-05T14:38:02.019Z",
  "avatar_url": null
}
```

1. O campo - "contact": Pode receber as redes sociais da pessoa, ou numero de telefone, algum método de contato fora da aplicação.

2. O campo - "course_module" deve receber respectivamente os 4 módulos do curso da kenzie, devendo ser escritos dessa forma:
   1. "Primeiro módulo (Introdução ao Frontend)"
   2. "Segundo módulo (Frontend Avançado)"
   3. "Terceiro módulo (Introdução ao Backend)"
   4. "Quarto módulo (Backend Avançado)"

<h2 align ='center'> Possíveis erros </h2>

Caso você acabe errando e mandando algum campo errado, a resposta de erro será assim:
No exemplo a requisição foi feita faltando o campo "contact" e "course_module".

`POST /users - `
` FORMATO DA RESPOSTA - STATUS 400`

```json
{
  "status": "error",
  "message": ["contact is required", "course_module is required"]
}
```

A senha necessita de 6 caracteres.

`POST /users - `
` FORMATO DA RESPOSTA - STATUS 400`

```json
{
  "status": "error",
  "message": ["password: minimum is 6 characters"]
}
```

Email já cadastrado:

`POST /users - `
` FORMATO DA RESPOSTA - STATUS 400`

```json
{
  "status": "error",
  "message": "Email already exists"
}
```

<h2 align = "center"> Login </h2>

`POST /sessions - FORMATO DA REQUISIÇÃO`

```json
{
  "email": "johndoe@email.com",
  "password": "123456"
}
```

Caso dê tudo certo, a resposta será assim:

`POST /sessions - FORMATO DA RESPOSTA - STATUS 201`

```json
{
  "user": {
    "id": "2a75e12d-fd1c-481d-ba88-4d8b17103b2a",
    "name": "John Doe",
    "email": "johndoe@email.com",
    "course_module": "Segundo Módulo (Frontend avançado)",
    "bio": "Lorem ipsum dolor emet",
    "contact": "linkedin/in/johndoe",
    "created_at": "2020-12-05T17:45:04.207Z",
    "updated_at": "2020-12-05T17:45:04.207Z",
    "techs": [],
    "works": [],
    "avatar_url": null
  },
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpYXQiOjE2MDcxODM3NzYsImV4cCI6MTYwNzQ0Mjk3Niwic3ViIjoiMmE3NWUxMmQtZmQxYy00ODFkLWJhODgtNGQ4YjE3MTAzYjJhIn0.UY67X23mPYAAzT43uFWZDHPUakd2STo5w4AuOcppkyQ"
}
```

Com essa resposta, vemos que temos duas informações, o user e o token respectivo, dessa forma você pode guardar o token e o usuário logado no localStorage para fazer a gestão do usuário no seu frontend.

## Rotas que necessitam de autorização

Rotas que necessitam de autorização deve ser informado no cabeçalho da requisição o campo "Authorization", dessa forma:

> Authorization: Bearer {token}

<h2 align ='center'> Listar seu usuário </h2>

Podemos acessar um usuário específico utilizando o endpoint:

`GET /users/:user_id - FORMATO DA RESPOSTA - STATUS 200`

```json
{
  "email": "felipe@teste.com",
  "password": "$2a$10$tgx/T1/qfq3DpjeqvRwWnO13pzXVsnD2Ne3UbaRKMjsUiM1XQxWDi",
  "name": "Felipe",
  "age": 20,
  "type": "Consumidor",
  "id": 2
}
```

<h2 align ='center'> Criar serviços para o seu perfil </h2>

`POST /services - FORMATO DA REQUISIÇÃO`

```json
{
  "title": "Eu vou desenhar você em estilo anime ou semi-realista",
  "images": [
    "https://vinteconto.sfo2.cdn.digitaloceanspaces.com/listings/223792/draw4hhrs.jpg",
    "https://vinteconto.sfo2.cdn.digitaloceanspaces.com/listings/223792/drawoc1t3h40min.jpg",
    "https://vinteconto.sfo2.cdn.digitaloceanspaces.com/listings/223792/draw3h20min.jpg",
    "https://vinteconto.sfo2.cdn.digitaloceanspaces.com/listings/223792/084545681e6b6b96e72a9256613a3d3b.jpg"
  ],
  "price": 40,
  "desc": "Vou fazer um desenho digital usando o mouse transformando você em estilo anime ou semi-realista.",
  "prazoEntrega": "2 dias",
  "tags": ["Dsenho", "Ilustração", "Anime"],
  "userId": 2
}
```

`PUT /services - FORMATO DA REQUISIÇÃO`

```json
{
  "title": "Eu vou desenhar você em estilo totalmente realista",
  "images": [
    "https://vinteconto.sfo2.cdn.digitaloceanspaces.com/listings/223792/draw4hhrs.jpg",
    "https://vinteconto.sfo2.cdn.digitaloceanspaces.com/listings/223792/drawoc1t3h40min.jpg",
    "https://vinteconto.sfo2.cdn.digitaloceanspaces.com/listings/223792/draw3h20min.jpg",
    "https://vinteconto.sfo2.cdn.digitaloceanspaces.com/listings/223792/084545681e6b6b96e72a9256613a3d3b.jpg"
  ],
  "price": 40,
  "desc": "Vou fazer um desenho digital usando o mouse transformando você em estilo anime ou semi-realista.",
  "prazoEntrega": "4 dias",
  "tags": ["Desenho", "Ilustração", "Anime"],
  "userId": 2
}
```

`DELETE /services/:service_id`

```
Não é necessário um corpo da requisição.
```

<h2 align ='center'> Atualizando os dados do perfil </h2>

`PUT /users/:user_id - FORMATO DA REQUISIÇÃO`

```json
{
  "email": "felipe@teste.com",
  "password": "123456",
  "name": "Felipe",
  "age": 21,
  "type": "Consumidor",
  "img": "https://static.wikia.nocookie.net/naruto-pedia/images/e/ea/Naruto.png/revision/latest?cb=20120407114822&path-prefix=pt-br",
  "userId": 2
}
```

`POST /users/:user_id - FORMATO DA RESPOSTA - STATUS 200`

 É necessário a autorização via token para a requisição.

 > Authorization: Bearer {token}

```json
{
	"email": "felipe@teste.com",
	"password": "$2a$10$p0/vzpPRLdMzoZH2Sz5sPe50VqBi6RySOjlVkWSUw05gI7qr4dxZi",
	"name": "Felipe",
	"age": 21,
	"type": "Consumidor",
	"img": "https://static.wikia.nocookie.net/naruto-pedia/images/e/ea/Naruto.png/revision/latest?cb=20120407114822&path-prefix=pt-br",
	"userId": 2,
	"id": 2
}
```

<h2 align ='center'> Vizualizando os serviços contratados para o usuário</h2>

 É necessário a autorização via token para a requisição.

para vizualizar os serviços que foram contratados para um especifico prestador de serviço é necessario realiazar:

`GET/servicescontracts/?userId_prestador={numero do id do prestador} - FORMATO DA RESPOSTA - STATUS 200`

```json
{
	"name_contrante": "Kenzinho",
		"name_service": "Eu vou Divulgar Para Mais De 30mil Seguidores",
		"userId_contratante": 1,
		"userId_prestador": 2
	},
	{
		"name_contrante": "Bruno",
		"name_service": "Eu vou Divulgar Para Mais De 30mil Seguidores",
		"userId_contratante": 1,
		"userId_prestador": 2
}
```


---

Feito com ♥ by araujooj :wave:Atu
