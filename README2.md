<h1 align="center">
  <img alt="KenzieHub" title="KenzieHub" src="https://kenzie.com.br/images/logoblue.svg" width="100px" />
</h1>

<h1 align="center">
  Jobinhos - API
</h1>

<p align = "center">
Este é o backend da aplicação Jobinhos - Uma aplicação para prestadores e consumidores de serviços feita pelos alunos da Kenzie. O objetivo dessa aplicação é facilitar a comunicação entre prestador/consumidor.
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

<h2 align ='center'> Listando serviços </h2>

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
    "deliveryTime": "2 dias",
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
    "deliveryTime": "2 dias",
    "tags": ["Dsenho", "Ilustração", "Anime"],
    "userId": 2,
    "id": 2
  }
]
```

<h2 align ='center'> Criação de usuário </h2>

`POST /register - FORMATO DA REQUISIÇÃO`

```json
{
  "email": "felipe@teste.com",
  "password": "123456",
  "name": "Felipe",
  "age": 20,
  "type": "Consumidor",
  "img": "https://static.wikia.nocookie.net/naruto-pedia/images/e/ea/Naruto.png/revision/latest?cb=20120407114822&path-prefix=pt-br"
}
```

Caso dê tudo certo, a resposta será assim:

```json
{
  "email": "felipe@teste.com",
  "password": "123456",
  "name": "Felipe",
  "age": 20,
  "type": "Consumidor",
  "img": "https://static.wikia.nocookie.net/naruto-pedia/images/e/ea/Naruto.png/revision/latest?cb=20120407114822&path-prefix=pt-br",
  "id": 2
}
```

O campo - "type": Pode receber "Prestador" ou "Consumidor" para definir o tipo de usuário.

<h2 align = "center"> Login </h2>

`POST /login - FORMATO DA REQUISIÇÃO`

```json
{
  "email": "felipe@teste.com",
  "password": "123456"
}
```

Caso dê tudo certo, a resposta será assim:

`POST /login - FORMATO DA RESPOSTA - STATUS 200`

```json
{
  "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6ImZlbGlwZUB0ZXN0ZS5jb20iLCJpYXQiOjE2NDczNjY4MzgsImV4cCI6MTY0NzM3MDQzOCwic3ViIjoiMiJ9.vP0O5aqf0oTrtKKqxFbiaeHDb2NRplchadS5JJJlmzQ",
  "user": {
    "email": "felipe@teste.com",
    "name": "Felipe",
    "age": 20,
    "type": "Consumidor",
    "img": "https://static.wikia.nocookie.net/naruto-pedia/images/e/ea/Naruto.png/revision/latest?cb=20120407114822&path-prefix=pt-br",
    "id": 2
  }
}
```

Com essa resposta, vemos que temos duas informações, o user e o accessToken respectivo, dessa forma você pode guardar o token e o usuário logado no localStorage para fazer a gestão do usuário no seu frontend.

<h2 align ='center'> Possíveis erros </h2>

Caso você acabe errando e mandando algum campo errado, a resposta de erro será assim:

A senha necessita ter no mínimo 3 caracteres:

`POST /register - `
` FORMATO DA RESPOSTA - STATUS 400`

```json
"Password is too short"
```

Email já cadastrado:

`POST /register - `
` FORMATO DA RESPOSTA - STATUS 400`

```json
"Email already exists"
```

## Rotas que necessitam de autorização

Rotas que necessitam de autorização deve ser informado no cabeçalho da requisição o campo "Authorization", dessa forma:

> Authorization: Bearer {token}

<h2 align ='center'> Listar seu usuário </h2>

Podemos acessar as informações do seu usuário utilizando o endpoint:

`GET /users/:user_id - FORMATO DA RESPOSTA - STATUS 200`

```json
{
  "email": "felipe@teste.com",
  "password": "$2a$10$teMYCQGyhkwqXw3YruottOI0tNAshiKtS8dLCWk47EDYyB9dh1hbu",
  "name": "Felipe",
  "age": 20,
  "type": "Consumidor",
  "img": "https://static.wikia.nocookie.net/naruto-pedia/images/e/ea/Naruto.png/revision/latest?cb=20120407114822&path-prefix=pt-br",
  "id": 2
}
```

Obs: Só é permitido ver as informações de seu usuário

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
  "deliveryTime": "2 dias",
  "tags": ["Dsenho", "Ilustração", "Anime"],
  "userId": 2
}
```

`PUT /services/:service:id - FORMATO DA REQUISIÇÃO`

```json
{
  "title": "Eu desenhar você em estilo realista",
  "images": [
    "https://vinteconto.sfo2.cdn.digitaloceanspaces.com/listings/223792/draw4hhrs.jpg",
    "https://vinteconto.sfo2.cdn.digitaloceanspaces.com/listings/223792/drawoc1t3h40min.jpg",
    "https://vinteconto.sfo2.cdn.digitaloceanspaces.com/listings/223792/draw3h20min.jpg",
    "https://vinteconto.sfo2.cdn.digitaloceanspaces.com/listings/223792/084545681e6b6b96e72a9256613a3d3b.jpg"
  ],
  "price": 40,
  "desc": "Vou fazer um desenho digital usando o mouse transformando você em estilo anime ou semi-realista.",
  "deliveryTime": "4 dias",
  "tags": ["Desenho", "Ilustração", "Anime"],
  "userId": 2,
  "id": 4
}
```

`DELETE /services/:service_id`

```
Não é necessário um corpo da requisição.
```

<h2 align ='center'> Vizualizando os serviços contratados/pendentes para o usuário</h2>

para vizualizar os serviços que foram contratados para um especifico prestador de serviço é necessario realizar:

`GET/pendings/ - FORMATO DA RESPOSTA - STATUS 200`

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
