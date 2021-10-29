# hamburgueria_api


INSTRUÇÕES DE ACESSO AOS ENDPOINTS

url base: http://localhost:3001/


1 – USER

POST  /register

- Registro de usuário na API

Formato da requisição:

Body:

{
 "name": "Roberto",
  "email": "email@mail.com",
  "password": "123456"
}

Formato da resposta – status 201

{
  "accessToken":     "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6ImVtYWlsQG1haWwuY29tIiwiaWF0IjoxNjM1NTE1MTgyLCJleHAiOjE2MzU1MTg3ODIsInN1YiI6IjEifQ.ToMYy0SCcROgaxZJKHTo2mlkibgDqILAFY_BUUBEPzA",
  "user": {
    "email": "email@mail.com",
    "name": "Roberto",
    "id": 1
  }
}


Possíveis erros:

1 - "Email and password are required"
   - Tentativa de registro sem informar o e-mail ou a senha.

2 - "Password is too short"
- A senha deve ter 4 caracteres ou mais.

3 - "Email already exists"
- E-mail já cadastrado anteriormente.





POST  /login

- Login do usuário na API

Formato da requisição:

Body:

{
 "email": "email2@mail.com",
 "password": "123456"
}


Formato da resposta – status 200


{
  "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6ImVtYWlsMkBtYWlsLmNvbSIsImlhdCI6MTYzNTUxNjg1NCwiZXhwIjoxNjM1NTIwNDU0LCJzdWIiOiIyIn0.uOq2zaOJThatBS2sfOOLrTw-ciBmDKgaS0Geqsmsqt0",
  "user": {
    "email": "email2@mail.com",
    "name": "Roberto",
    "id": 2
  }
}

Possíveis erros:

1 - "Incorrect password"
   - Senha incorreta.

2 - "Cannot find user"
   - E-mail incorreto ou não cadastrado.

3 - "Email format is invalid"
   - Formatação do endereço de e-mail inválida.


PATCH users/{userId}

- Realiza a atualização dos dados do usuário cadastrado anteriormente

Formato da requisição:

Header:

{
	Authorization: Bearer {token}
}

Body:

{
 "name": "Roberto",
  "email": "email@mail.com",
  "password": "123456"
}

OBS: O formato da requisição pode conter somente o item a ser modificado, como a chave “name” por exemplo.

Formato da resposta – status 200

{
  "email": "email@mail.com",
  "password": "$2a$10$jj95Y1/qpokioNtukLJs4ezNSt4A0Qh7byFf3U278dGx2uwrjOyg.",
  "name": "Roberto",
  "id": 3
}


Possíveis erros:

1 - "Private resource access: entity must have a reference to the owner id"
   - Não foi incluído o ID de usuário no endpoint.

2 - "invalid token"
   - Login do usuário expirado.


GET  users{userId}


- Busca as informações cadastradas do usuário logado e identificado pelo ID.

Formato da requisição:

- Sem corpo


Formato da resposta – status 200

{
  "email": "email3@mail.com",
  "password": "$2a$10$jj95Y1/qpokioNtukLJs4ezNSt4A0Qh7byFf3U278dGx2uwrjOyg.",
  "name": "Roberto",
  "id": 3
}

Possíveis erros:

1 - "Private resource access: entity must have a reference to the owner id"
   - Não foi incluído o ID de usuário no endpoint ou o ID é de outro usuário..

2 - "invalid token"
   - Token inválido ou expirado

3 - "Missing token"
   - Token não informado no Header



2 – PRODUCTS

GET  /products

- Lista todos os produtos registrados

Formato da requisição:

- Sem corpo


Formato da resposta – status 200

[
  {
    "id": 1,
    "name": "Hanburguer",
    "category": "Sanduiches",
    "price": 14,
    "image": "https://i.ibb.co/jDpB9jC/hamburger.png",
    "userId": 1
  },
  {
    "id": 2,
    "name": "X-Burguer",
    "category": "Sanduiches",
    "price": 16…]




POST /products

- Cadastro de novos produtos. Usuário deve estar logado.

Formato da requisição:

Header:
{
	Authorization: Bearer {token}
}


Body:

{
    "id": 9,
    "name": "Hanburguer 2",
    "category": "Sanduiches",
    "price": 14,
    "image": "https://i.ibb.co/jDpB9jC/hamburger.png",
    "userId": 1
}


Formato da resposta – status 201

{
  "id": 9,
  "name": "Hanburguer 2",
  "category": "Sanduiches",
  "price": 14,
  "image": "https://i.ibb.co/jDpB9jC/hamburger.png",
  "userId": 1
}

Possíveis erros:

1 - "Private resource creation: request body must have a reference to the owner id"
   - ID do usuário não informada no Body ou usuário não cadastrado 

2 - "invalid token"
   - Token inválido

3 - "jwt expired"
   - Token expirado

4 – 500 Internal server error
   - Tentativa de cadastrar um outro produto com ID já existente



DELETE products{productId}

- Apaga o produto identificado pelo ID.

Formato da requisição:

Header:
{
	Authorization: Bearer {token}
}

Sem corpo

Formato da resposta – status 200

Sem corpo


Possíveis erros:

1 - "Cannot read property 'userId' of undefined"
   - ID do produto incorreto ou não existente

2 - "invalid token"
   - Token inválido

3 - "jwt expired"
   - Token expirado



PATCH products/{productId}

- Realiza a atualização dos dados do produto cadastrado anteriormente

Formato da requisição:

Header:
{
	Authorization: Bearer {token}
}

Body:

{    
    "name": "Hanburguer 32",
    "category": "Sanduiches",
    "price": 14,
    "image": "https://i.ibb.co/jDpB9jC/hamburger.png",
    "userId": 1
}


Formato da resposta – status 200


{
  "id": 10,
  "name": "Hanburguer 32",
  "category": "Sanduiches",
  "price": 14,
  "image": "https://i.ibb.co/jDpB9jC/hamburger.png",
  "userId": 1
}


Possíveis erros:

1 – 404 não encontrado
- ID não informado no endpoint

2 - "Cannot read property 'userId' of undefined"
- ID informado não existente

3 - "invalid token"
   - Token inválido

4- "jwt expired"
- Token expirado



3 – CART


POST /cart

- Adicionar um produto ao carrinho de compras do usuário logado

Formato da requisição:

Header:
{
	Authorization: Bearer {token}
}

Body:

{    
    "name": "Hanburguer 32",
    "category": "Sanduiches",
    "price": 14,
    "image": "https://i.ibb.co/jDpB9jC/hamburger.png",
    "userId": 1
}


Formato da resposta – status 200

{
  "name": "Hanburguer",
  "category": "Sanduiches",
  "price": 14,
  "image": "https://i.ibb.co/jDpB9jC/hamburger.png",
  "userId": 1,
  "id": 2
}
Possíveis erros:

1 - "Missing token"
- Usuário não está logado.


2 - "invalid token"
   - Token inválido.

3- "jwt expired"
- Token expirado.

4 - "Private resource creation: request body must have a reference to the owner id"
- ID do usuário não informado no Body.


GET  /cart

- Lista os produtos do carrinho de compras do usuário logado

Formato da requisição:

Header:
{
	Authorization: Bearer {token}
}

Body: sem corpo

Formato da resposta – status 200

[
  {
    "name": "Hanburguer 32",
    "category": "Sanduiches",
    "price": 14,
    "image": "https://i.ibb.co/jDpB9jC/hamburger.png",
    "userId": 1,
    "id": 1
  },
  {
    "name": "Hanburguer",
    "category": "Sanduiches"...]


Possíveis erros:

1 - "Missing token"
- Usuário não está logado.


2 - "invalid token"
   - Token inválido.

3- "jwt expired"
- Token expirado.



DELETE cart{Id}

OBS: o Id a ser informado que consta no corpo do objeto pode ser considerado como o cartProductId, pois conforme os produtos são adicionados ao carrinho um novo Id é criado pelo servidor.

Formato da requisição:

Header:
{
	Authorization: Bearer {token}
}

Body: sem corpo

Formato da resposta – status 200

{}


Possíveis erros:

1 - "Missing token"
- Usuário não está logado.


2 - "invalid token"
   - Token inválido.

3- "jwt expired"
- Token expirado.



